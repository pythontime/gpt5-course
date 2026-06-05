# R3 — Responses API Surface (Current Capabilities Students Will Encounter)

_Primary sources: Responses API changelog and conversation-state guide._

## Conversation state & persistence
- **`client.conversations.create()`** — creates a persistent, durable conversation object with its own ID. Stores items (messages, tool calls, tool outputs) as a long-running object; pass the conversation ID on later calls so context is shared automatically without manually rebuilding history [source: https://developers.openai.com/api/docs/guides/conversation-state].
- **`store: true`** — saves responses for 30 days by default (visible in dashboard logs). `store: false` disables retention. Responses **attached to a conversation persist indefinitely** (no 30-day TTL). Billing note: even with `previous_response_id`, all prior input tokens in the chain are re-billed as input tokens [source: https://developers.openai.com/api/docs/guides/conversation-state].
- **`previous_response_id`** — chains turns by referencing a prior response ID; the model auto-pulls needed context. In WebSocket mode it uses a connection-local cache for low-latency continuation [source: https://developers.openai.com/api/docs/guides/conversation-state].
- **`/responses/compact`** — standalone endpoint for "shrinking the context you send with each turn." Also exposed inline via `context_management` and `compact_threshold` parameters for server-side compaction [source: https://developers.openai.com/api/docs/guides/conversation-state] [source: https://developers.openai.com/api/docs/changelog].

## Response shaping
- **`phase` parameter** — labels assistant messages as either `commentary` or `final_answer`, separating in-progress narration from the deliverable [source: https://developers.openai.com/api/docs/changelog].
- **Moderation scores** — responses now include moderation scores for both the model input and the generated output [source: https://developers.openai.com/api/docs/changelog].

## Transport
- **WebSocket mode** — streaming transport for low-latency, connection-local continuation of responses [source: https://developers.openai.com/api/docs/changelog] [source: https://developers.openai.com/api/docs/guides/conversation-state].

## Tools & execution
- **Hosted shell tool** — container-based command execution provided by OpenAI [source: https://developers.openai.com/api/docs/changelog].
- **Skills** — supported for both local and hosted container execution [source: https://developers.openai.com/api/docs/changelog].
- **Connectors** — OpenAI-maintained MCP wrappers for third-party services (e.g., Google apps, Dropbox) [source: https://developers.openai.com/api/docs/changelog].
- **Image/file as tool outputs** — tool outputs can now return images and files as results, not just text [source: https://developers.openai.com/api/docs/changelog].

## Caching
- **`store: true` extended prompt-cache retention** — up to 24 hours of extended prompt cache retention is associated with the store flag [source: https://developers.openai.com/api/docs/changelog].

## Teaching note
The Responses API is now the primary surface (Chat Completions still exists for `gpt-5.5` but the conversation-state, compaction, phase, connectors, and hosted-tool features above are Responses-API-first). `[unverified]` Confirm each feature's exact parameter name against the live changelog at build time — the changelog is updated frequently and some of the above (e.g., `compact_threshold` vs `context_management`) may be renamed [source: https://developers.openai.com/api/docs/changelog].
