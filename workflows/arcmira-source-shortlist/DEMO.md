# CLI demonstration

[Arcmira](https://arcmira.com) · [API docs](https://arcmira.com/docs) · [Setup](README.md)

On October 8, 2026 at 17:09 UTC, this workflow ran in n8n 2.41.3 against Arcmira using an isolated Free account. It searched `creativity` between August 1 and September 1, 2026, with `limit=3`.

## Run through the CLI

Use a separate temporary `N8N_USER_FOLDER` and database, import the workflow, and bind your own HTTP Bearer Auth credential as described in the setup guide. Then execute the imported workflow:

```sh
N8N_LOG_LEVEL=info n8n execute --id="<imported-workflow-id>" --rawOutput
```

Replace the ID placeholder with the actual imported workflow ID. Keep credential files and raw execution output private. The raw output includes transcript passages; this demonstration publishes only source identifiers and coverage facts.

## Observed results

All four nodes executed once: **Manual trigger**, **Search input**, **Search Arcmira**, and **Build source shortlist**. The search node made one request. It returned three passages and preserved the requested date window.

| Video ID | Passage start, seconds | Source links |
|---|---:|---|
| `t5KsyuXAtK4` | 566 | [YouTube](https://www.youtube.com/watch?v=t5KsyuXAtK4&t=566s) · [Arcmira](https://arcmira.com/watch?v=t5KsyuXAtK4&t=566) |
| `t5KsyuXAtK4` | 526 | [YouTube](https://www.youtube.com/watch?v=t5KsyuXAtK4&t=526s) · [Arcmira](https://arcmira.com/watch?v=t5KsyuXAtK4&t=526) |
| `gWgM6SGFGcM` | 833 | [YouTube](https://www.youtube.com/watch?v=gWgM6SGFGcM&t=833s) · [Arcmira](https://arcmira.com/watch?v=gWgM6SGFGcM&t=833) |

The response reported `partial=false`, zero failed batches and `search_index.state=live`. All three passages were labeled `third_party_quick`. Plan-credit, available-credit, on-demand and monetary usage were unchanged; on-demand was disabled before and after.

An earlier CLI attempt exited 0 but hid its JSON result because the log level was `error`. Those results were not validated. Correcting the log level produced the evidence above; account-usage observations stayed unchanged across both attempts.

## Scope

This is a real CLI execution, not an editor screenshot or browser test. Only a temporary workflow ID and credential reference were added for execution. Distributed nodes, code and wiring are unchanged, and temporary credentials/database were removed.

The [machine-readable receipt](demo-verification.json) records the workflow hash, node counts and public source links. No transcript text, API key, private account identifier or raw execution log is included. Results may change; source playback, speaker identity, edit boundaries and reuse rights remain unverified.

Copyright 2026 Arcmira. This demonstration and workflow retain [Apache-2.0](LICENSE).
