# GIB (Guru Intelligence Base)

Agent-facing leader knowledge base for scenario mapping.

## Structure
- `sources/` raw source index (YouTube/articles/books)
- `cards/` distilled insight cards (fast retrieval)
- `templates/` output templates (short/decision/execution)
- `docs/` process & governance

## Card schema (v1)
- leader
- claim
- evidence
- applicable_scenarios
- non_applicable_scenarios
- mapping_to_jianan
- confidence
- source_url

## Seed Leaders (2026-03-13 update)
- International: to be proposed by 4 agents
- China speech/debate masters (new):
  - 詹青云（论证结构、语言力度、价值澄清）
  - 陈铭（表达节奏、现场说服、辩题拆解）

## Orchestration (Define + n8n + NotebookLM)
- Define/Dify: prompt workflow + judgment templates
- n8n: source ingestion, retries, scheduling, writeback
- NotebookLM: long-context retrieval workspace per leader/topic
- OpenClaw agents: scenario mapping to Jianan + actionable recommendations

## Next
1. Fill first CN seed set (詹青云 / 陈铭) with 20+ source items
2. Map per-agent leader preferences (Andrew/Rex/Lulu/Alex)
3. Add weekly refresh workflow (n8n cron + writeback)
4. Sync to Feishu collaboration page + Dashboard project summary
