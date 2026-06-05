# FastAPI Business Report Server

Companion server for the notebook **`notebooks/5.1-fastapi-business-report.ipynb`**.

It exposes the **research → analysis → reporting** Agents SDK pipeline as an HTTP
endpoint, streaming `phase: commentary` updates followed by the `phase: final_answer`
report, with `prompt_cache_retention: 24h` enabled for cheap repeat runs.

> **Status: placeholder.** This directory currently contains only this README. The
> `app.py` implementation is intentionally left as a build-out step so it can be
> verified against the installed `openai-agents` version (the SDK import surface is
> [unverified] — see the TODO cell in the notebook).

## Planned layout

```
scripts/fastapi_report_server/
├── README.md          # this file
├── app.py             # FastAPI app: POST /report -> streamed pipeline (TODO)
└── requirements.txt   # fastapi, uvicorn, openai, openai-agents (TODO)
```

## Setup (once implemented)

```bash
# from the repo root
python -m venv .venv && source .venv/bin/activate
pip install -U openai openai-agents fastapi uvicorn
export OPENAI_API_KEY=sk-...
```

## Run

```bash
uvicorn scripts.fastapi_report_server.app:app --reload --port 8000
```

## Endpoint (planned)

```
POST /report
{ "question": "Should a mid-size SaaS company expand into the EU market in 2026?" }
```

Response: a streamed body where `commentary` chunks arrive first (live progress),
then the `final_answer` report. Mirror the bucketing logic shown in the notebook's
`run_report()` function.

## TODOs before publishing

- [ ] Implement `app.py` and verify Agents SDK imports against the installed version.
- [ ] Confirm the `prompt_cache_retention` and `phase` parameter names against the live changelog.
- [ ] Add `requirements.txt` pinned to tested versions.
