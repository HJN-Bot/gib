# Process
1) Collect sources (YouTube/Bilibili/公众号/访谈/播客)
2) Normalize metadata (speaker/date/url/topic/quality)
3) Distill into cards (claim/evidence/scenario/mapping/confidence)
4) Agent evaluates fit (per-agent Top5 + non-fit conditions)
5) Publish recommendation packs (short/decision/execution)
6) Writeback to dashboard/feishu/tasks

## Pipeline binding
- n8n: ingestion, queue, retry, weekly refresh
- Define/Dify: synthesis prompts and output formatting
- NotebookLM: retrieval workspace per leader + topic notebooks
- OpenClaw: governance gate + human approval + final dispatch
