# R1 — GPT-5.5 Model Line (Current Variants)

_Last researched: 2026-06-05. Prices are per 1M tokens, standard tier._

## Summary Table

| Model | Input | Output | Cached input | Context window | Max output | Recommended use |
|---|---|---|---|---|---|---|
| `gpt-5.5` | $5.00 | $30.00 | $0.50 | 1,050,000 | 128,000 | Frontier coding + professional work [source: https://developers.openai.com/api/docs/models/gpt-5.5] |
| `gpt-5.5-pro` | $30.00 | $180.00 | — | 1,050,000 | 128,000 | Hardest problems needing extended reasoning [source: https://developers.openai.com/api/docs/models/gpt-5.5-pro] |
| `gpt-5.5-instant` | $5.00 | $30.00 | — | ~1M (400K input listed) | 128,000 | Fast, concise everyday tasks; ChatGPT default [source: https://www.mindstudio.ai/blog/what-is-gpt-5-5-instant] [source: https://llm-stats.com/models/gpt-5.5-instant] |
| `gpt-5.4-mini` | $0.75 | $4.50 | — | 400,000 | 128,000 | Strong small model: coding, computer use, subagents [source: https://developers.openai.com/api/docs/models] |
| `gpt-5.4-nano` | $0.20 | $1.25 | — | 400,000 | 128,000 | Speed/cost-critical: classification, extraction, ranking, sub-agents [source: https://developers.openai.com/api/docs/models/gpt-5.4-nano] |
| `gpt-5.3-codex` | $1.75 | $14.00 | — | 400,000 | 128,000 | Agentic coding in Codex or similar environments [source: https://developers.openai.com/api/docs/models/gpt-5.3-codex] |

## Per-model notes

### `gpt-5.5`
OpenAI positions it as "a new class of intelligence for coding and professional work" — the current frontier model for complex professional tasks. Default `reasoning_effort` is `medium`; supports `none`, `low`, `medium`, `high`, `xhigh` [source: https://developers.openai.com/api/docs/models/gpt-5.5]. Long-context surcharge: prompts >272K input tokens are billed at 2x input and 1.5x output for the full session (standard, batch, and flex tiers) [source: https://openrouter.ai/openai/gpt-5.5].

### `gpt-5.5-pro`
"Uses more compute to think harder and provide consistently better answers." Requests can take several minutes; OpenAI recommends background mode to avoid timeouts. Best when accuracy matters more than latency [source: https://developers.openai.com/api/docs/models/gpt-5.5-pro].

### `gpt-5.5-instant`
This is primarily the **ChatGPT default model**, trained for faster time-to-first-token and more concise output (released ~May 5, 2026). `[unverified]` Dedicated API access via `gpt-5.5-instant` was still listed as "API access coming soon / available through our gateway shortly" at research time — confirm availability before teaching it as an API model name [source: https://llm-stats.com/models/gpt-5.5-instant] [source: https://www.mindstudio.ai/blog/what-is-gpt-5-5-instant]. For deep research synthesis or high-stakes medical/legal/financial work, the full `gpt-5.5` is preferred over instant [source: https://www.mindstudio.ai/blog/what-is-gpt-5-5-instant].

### `gpt-5.4-mini`
"Our strongest mini model yet for coding, computer use, and subagents" — the value tier for high-volume agentic workloads [source: https://developers.openai.com/api/docs/models].

### `gpt-5.4-nano`
Cheapest in the line. API-only. Excels at "tasks where speed and cost matter most like classification, data extraction, ranking, and sub-agents" [source: https://developers.openai.com/api/docs/models/gpt-5.4-nano].

### `gpt-5.3-codex`
"Optimized for agentic coding tasks in Codex or similar environments"; reasons across extended codebases. Supports `low`, `medium`, `high`, `xhigh` reasoning effort [source: https://developers.openai.com/api/docs/models/gpt-5.3-codex].

## Cross-tier pricing mechanics (applies to all variants)
- Batch and Flex: half the standard rate.
- Priority processing: 2.5x the standard rate [source: https://openai.com/index/introducing-gpt-5-5/ (via search summary)] `[unverified — index page returned 403; confirm against live pricing page]`.

## Decision (which model to teach as the default for the course)
**Teach `gpt-5.5` as the default workhorse**, with `gpt-5.4-mini` as the cost-optimized alternative for high-volume student exercises and `gpt-5.4-nano` for classification/extraction demos. Reserve `gpt-5.5-pro` for one "hard reasoning" demo only (its 6x input / 6x output premium over `gpt-5.5` makes it a poor default for a teaching repo that runs many calls). Treat `gpt-5.5-instant` as a **ChatGPT product concept**, not a guaranteed API model name, until API availability is confirmed [unverified].
