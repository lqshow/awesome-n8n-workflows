# Demo & Live API Verification (`b2b-market-intel-mcp-pack`)

Exact `curl` commands executed live on `2026-11-27` against each zero-key public API used by the 5 workflows in this pack, along with verified outputs (personal emails masked where applicable).

---

## 1. UK Gov Contracts Finder OCDS Search (`01_uk_gov_contracts_finder_b2b_tenders.json`)

```bash
curl -sS "https://www.contractsfinder.service.gov.uk/Published/Notices/OCDS/Search?publishedFrom=2026-11-15T00:00:00Z&stages=tender,award&limit=2" \
  | node -e "const d=JSON.parse(require('fs').readFileSync(0,'utf8')); console.log({count:d.releases.length, first:{ocid:d.releases[0].ocid, title:d.releases[0].tender.title, buyer:d.releases[0].parties[0].name}});"
```

Observed output:

```json
{
  "count": 2,
  "first": {
    "ocid": "ocds-b5fd17-09ddfb9e-ef1d-41b6-8a5f-8dce68c29d9e",
    "title": "Fresh Food DPS Contract Award Notices June 2025 - August 2025",
    "buyer": "Supply Chain Coordination Limited"
  }
}
```

---

## 2. ClinicalTrials.gov REST v2 Industry Trials (`02_clinicaltrials_biotech_sponsor_leads.json`)

```bash
curl -sS "https://clinicaltrials.gov/api/v2/studies?query.cond=oncology&filter.overallStatus=RECRUITING&filter.advanced=AREA%5BLeadSponsorClass%5DINDUSTRY&pageSize=2" \
  | node -e "const d=JSON.parse(require('fs').readFileSync(0,'utf8')); console.log(d.studies.map(s=>({nct:s.protocolSection.identificationModule.nctId, sponsor:s.protocolSection.sponsorCollaboratorsModule.leadSponsor.name, phases:s.protocolSection.designModule.phases})));"
```

Observed output:

```json
[
  {
    "nct": "NCT06944444",
    "sponsor": "Shenyang Sunshine Pharmaceutical Co., LTD.",
    "phases": ["PHASE1"]
  },
  {
    "nct": "NCT07284121",
    "sponsor": "Hoffmann-La Roche",
    "phases": ["PHASE1", "PHASE2"]
  }
]
```

---

## 3. WordPress.org Plugins API v1.2 + 1-Star RSS (`03_wordpress_woocommerce_1star_churn_monitor.json`)

```bash
curl -gsS "https://api.wordpress.org/plugins/info/1.2/?action=query_plugins&request%5Bsearch%5D=woocommerce&request%5Bper_page%5D=2" \
  | node -e "const d=JSON.parse(require('fs').readFileSync(0,'utf8')); console.log(d.plugins.map(p=>({slug:p.slug, rating:p.rating, oneStar:p.ratings['1'], installs:p.active_installs})));"

curl -sS -A "Mozilla/5.0" "https://wordpress.org/support/plugin/woocommerce-payments/reviews/feed/?filter=1" \
  | grep -c "<item>"
```

Observed output:

```json
[
  { "slug": "woocommerce", "rating": 90, "oneStar": 410, "installs": 7000000 },
  { "slug": "woocommerce-gateway-stripe", "rating": 62, "oneStar": 94, "installs": 700000 }
]
```

```text
30
```

---

## 4. Google News RSS + `Fbv4je` Canonical URL Resolution (`04_google_news_real_url_rag_decoder.json`)

```bash
python3 - << 'EOF'
import json, re, subprocess

rss = subprocess.check_output(["curl", "-sSL", "-A", "Mozilla/5.0", "https://news.google.com/rss/search?q=AI+agents&hl=en-US&gl=US&ceid=US:en"], text=True)
tok = re.search(r"articles/([A-Za-z0-9_-]+)", rss).group(1)
html = subprocess.check_output(["curl", "-sSL", "-A", "Mozilla/5.0", f"https://news.google.com/articles/{tok}"], text=True)
sg = re.search(r'data-n-a-sg="([^"]+)"', html).group(1)
ts = re.search(r'data-n-a-ts="([^"]+)"', html).group(1)
inner = ["garturlreq", [["X","X",["X","X"],None,None,1,1,"US:en",None,1,None,None,None,None,None,0,1],"X","X",1,[1,1,1],1,1,None,0,0,None,0], tok, int(ts), sg]
freq = json.dumps([[["Fbv4je", json.dumps(inner), None, "generic"]]])
resp = subprocess.check_output(["curl", "-sSL", "-X", "POST", "https://news.google.com/_/DotsSplashUi/data/batchexecute?rpcids=Fbv4je", "-H", "Referer: https://news.google.com/", "--data-urlencode", f"f.req={freq}"], text=True)
hit = re.search(r'\[\s*\\"garturlres\\"\s*,\s*\\"(https?:[^"\\]+)\\"', resp)
print(json.loads(f'"{hit.group(1)}"'))
EOF
```

Observed output:

```text
https://www.nytimes.com/2026/11/26/business/holiday-shopping-ai-agents.html
```

---

## 5. Eclipse Open-VSX Search & Bug Reviews API (`05_openvsx_cursor_extension_bug_spy.json`)

```bash
curl -sS "https://open-vsx.org/api/-/search?query=mcp&size=2&sortBy=downloadCount&sortOrder=desc" \
  | node -e "const d=JSON.parse(require('fs').readFileSync(0,'utf8')); console.log(d.extensions.map(e=>({id:e.namespace+'.'+e.name, downloads:e.downloadCount, rating:e.averageRating, reviews:e.reviewCount})));"

curl -sS "https://open-vsx.org/api/Anthropic/claude-code/reviews" \
  | node -e "const d=JSON.parse(require('fs').readFileSync(0,'utf8')); console.log({total:d.reviews.length, lowStar:d.reviews.filter(r=>r.rating<=3).length});"
```

Observed output:

```json
[
  { "id": "Anthropic.claude-code", "downloads": 69031515, "rating": 3.506172839506173, "reviews": 81 },
  { "id": "saoudrizwan.claude-dev", "downloads": 7543302, "rating": 3.1176470588235294, "reviews": 17 }
]
```

```json
{ "total": 81, "lowStar": 33 }
```
