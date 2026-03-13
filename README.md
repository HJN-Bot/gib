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

## Next
1. Fill 3 leaders as seed set
2. Map per-agent preferences
3. Add weekly refresh workflow
