# R6 — Deprecations & Sunset Dates (Don't Teach Deprecated Features)

_Source: OpenAI API changelog & deprecations page [source: https://developers.openai.com/api/docs/changelog] [source: https://developers.openai.com/api/docs/deprecations]._

## Announcement
All three deprecations were **announced June 3, 2026** — a ~6-month notice window [source: https://developers.openai.com/api/docs/changelog] [source: https://developers.openai.com/api/docs/deprecations].

## Sunset table

| Feature | Announced | Read-only / interim | Final shutdown | Migration path |
|---|---|---|---|---|
| **Agent Builder** (visual workflow tool) | Jun 3, 2026 | — | **Nov 30, 2026** | Migrate to Agents SDK or ChatGPT Workspace Agents [source: https://developers.openai.com/api/docs/deprecations] |
| **Evals platform** | Jun 3, 2026 | Existing evals become **read-only Oct 31, 2026** | **Nov 30, 2026** (dashboard + API inaccessible) | (see deprecations page) [source: https://developers.openai.com/api/docs/deprecations] |
| **Reusable prompt objects** (`v1/prompts`) | Jun 3, 2026 | — | **Nov 30, 2026** | Move prompt content into application code [source: https://developers.openai.com/api/docs/deprecations] |

## Notes
- All three share the **Nov 30, 2026** final shutdown date [source: https://developers.openai.com/api/docs/deprecations].
- The Evals **read-only date of Oct 31, 2026** is the one interim milestone — worth flagging since students mid-course could lose write access a month before full shutdown [source: https://developers.openai.com/api/docs/deprecations].
- `[unverified]` Exact dates were read from the deprecations page via an automated fetch; before locking course copy, re-confirm the Nov 30, 2026 / Oct 31, 2026 dates against the live deprecations page, since OpenAI occasionally extends sunset windows.

## Decision (what the course must change)
**Remove or rewrite any lesson that teaches Agent Builder, the Evals platform UI/API, or reusable prompt objects (`v1/prompts`).** Replace:
- Agent Builder content → **Agents SDK** (see `05-agents-sdk.md`).
- Evals platform content → either the SDK's **tracing → eval loop** workflow or a code-based eval approach, since the hosted Evals platform shuts down Nov 30, 2026.
- Reusable prompt objects → **prompts defined in application code** (string/templated), which is also more portable for students.

Because the course's expected shelf life extends past Nov 30, 2026, teaching any of these three would ship the course already-broken. Prioritize this cleanup.
