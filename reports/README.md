# Lab deliverables — submission checklist

Use this folder when submitting **Lab 20: Multi-Agent Research System**.

## Required files (commit these)

| File | Purpose |
|------|---------|
| [`benchmark_report.md`](benchmark_report.md) | Single vs multi-agent comparison (latency, cost, quality, citations, failure rate) |
| This `README.md` | Checklist for reviewers |

## Required artifacts (add before you push)

| Item | Where | Status |
|------|-------|--------|
| GitHub repo | Your remote | ☐ Push latest code |
| Benchmark report | `reports/benchmark_report.md` | ☑ Generated |
| LangSmith trace | [smith.langchain.com](https://smith.langchain.com) → project `multi-agent-research-lab` | ☐ Screenshot or URL in PR/README |
| Failure mode note | `benchmark_report.md` → Reflection section | ☑ Included |
| Exit ticket (2 questions) | `benchmark_report.md` or PR description | ☐ Copy from report |

## Optional (helpful for demo / peer review)

| Item | Notes |
|------|-------|
| `last_benchmark.json` | **Gitignored** — local cache for Streamlit; regenerate with `python -m multi_agent_research_lab.cli benchmark` |
| Streamlit demo | `streamlit run streamlit_app.py` |
| LangGraph diagram | Overview tab or `MultiAgentWorkflow().get_mermaid_diagram()` |

## Regenerate benchmark

```bash
# Requires OPENAI_API_KEY, optional LANGSMITH_API_KEY + TAVILY_API_KEY in .env
python -m multi_agent_research_lab.cli benchmark \
  --query "Research GraphRAG state-of-the-art and write a 500-word summary"
```

Writes:

- `reports/benchmark_report.md` (tracked in git)
- `reports/last_benchmark.json` (local only, not committed)

## Peer review rubric self-check (10/10)

| Criterion | Evidence in this repo |
|-----------|------------------------|
| Role clarity (2/2) | `agents/` — Supervisor, Researcher, Analyst, Writer |
| State design (2/2) | `core/state.py` — shared handoff |
| Failure guard (2/2) | `max_iterations`, timeout, retry, writer fallback |
| Benchmark (2/2) | LLM judge + 3-query failure rate in `benchmark_report.md` |
| Trace explanation (2/2) | LangSmith + `state.trace` in Streamlit / CLI logs |

## Do not commit

- `.env` (API keys) — already in root `.gitignore`
- `reports/last_benchmark.json` — regenerable runtime artifact

## Suggested PR / submission blurb

```text
Lab 20: Multi-agent research lab with LangGraph supervisor loop, Tavily search,
and LangSmith tracing. Benchmark: baseline 12.5s vs multi-agent 33.3s;
quality 8.0/10 both (LLM judge); multi-agent citation coverage 100%.
Trace: <paste LangSmith run URL or attach screenshot>
```
