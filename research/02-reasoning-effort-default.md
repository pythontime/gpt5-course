# R2 — `reasoning_effort` Default: Did it flip to `none`, and is that inherited by GPT-5.5?

## Headline finding (important correction to the briefing's assumption)

The briefing asked us to "confirm whether `reasoning_effort` default flipped to `none` in GPT-5.2 and whether that default is inherited by GPT-5.5." The research shows a **two-part answer that does not match a simple "inherited" model**:

1. **The `none` default applies to GPT-5.1 and GPT-5.2 — NOT GPT-5.5.**
   > "default reasoning level for GPT-5 is medium, and for GPT-5.1 and GPT-5.2 is none." [source: https://developers.openai.com/cookbook/examples/gpt-5/gpt-5-2_prompting_guide]

2. **GPT-5.5 does NOT inherit `none`. It defaults to `medium`.**
   GPT-5.5's `reasoning_effort` "defaults to `medium`," supporting `none`, `low`, `medium`, `high`, `xhigh` [source: https://developers.openai.com/api/docs/models/gpt-5.5] [source: https://developers.openai.com/api/docs/guides/latest-model].

So the default did **not** simply propagate forward. The trajectory is:

| Model | Default `reasoning_effort` | Supported values |
|---|---|---|
| GPT-5 (and earlier) | `medium` | minimal, low, medium, high [source: https://developers.openai.com/cookbook/examples/gpt-5/gpt-5-2_prompting_guide] |
| GPT-5.1 | `none` | none, low, medium, high [source: https://x.com/kevinwhinnery/status/1989338879065751863] |
| GPT-5.2 | `none` | none, low, medium, high [source: https://developers.openai.com/cookbook/examples/gpt-5/gpt-5-2_prompting_guide] |
| **GPT-5.5** | **`medium`** | none, low, medium, high, xhigh [source: https://developers.openai.com/api/docs/models/gpt-5.5] |

`[unverified]` The precise GPT-5.1 default of `none` comes from a developer (Kevin Whinnery) post, corroborated by the 5.2 guide's "GPT-5.1 and GPT-5.2 is none" statement; treat the exact GPT-5.1 value as strongly indicated but confirm on the GPT-5.1 model page before teaching it verbatim.

## Why GPT-5.5 reverted to `medium`
GPT-5.5 is characterized as a release that "shifts defaults rather than features." `medium` is now "the recommended balanced starting point," and `none` is reserved strictly for latency-critical tasks (voice turns, fast retrieval, classification) [source: https://developers.openai.com/api/docs/guides/latest-model]. Notably, "higher effort ≠ automatic improvement" — with weak stopping criteria or open-ended tool access, higher effort can cause overthinking [source: https://developers.openai.com/api/docs/guides/latest-model].

## Migration mapping

### From GPT-5 (`medium` default) → GPT-5.5
| Coming from GPT-5 setting | Set explicitly on GPT-5.5 | Rationale |
|---|---|---|
| (relied on default `medium`) | `medium` (or omit) | Same effective default — behavior preserved [source: https://developers.openai.com/api/docs/models/gpt-5.5] |
| `minimal` | `none` | `minimal` was retired; map to `none` [source: https://developers.openai.com/cookbook/examples/gpt-5/gpt-5-2_prompting_guide] |
| `low` / `high` | keep same value | Preserve latency/quality profile [source: https://developers.openai.com/cookbook/examples/gpt-5/gpt-5-2_prompting_guide] |
| (wants max reasoning) | `xhigh` | New top tier in 5.5 for hardest async tasks [source: https://developers.openai.com/api/docs/models/gpt-5.5] |

### From GPT-5.2 (`none` default) → GPT-5.5 — the trap to warn students about
If a student moves 5.2 code to 5.5 **without pinning** `reasoning_effort`, the default silently jumps from `none` to `medium`, increasing latency, token cost, and verbosity. The 5.2 guide explicitly warns to pin effort during migration to "avoid provider-default 'thinking' traps that skew cost/verbosity/structure" [source: https://developers.openai.com/cookbook/examples/gpt-5/gpt-5-2_prompting_guide].

| Coming from GPT-5.2 (default `none`) | Set explicitly on GPT-5.5 | Why |
|---|---|---|
| relied on default `none` | `none` (explicit) | Otherwise you silently get `medium` |
| explicit `none/low/medium/high` | keep same value | Preserve consistent profile [source: https://developers.openai.com/cookbook/examples/gpt-5/gpt-5-2_prompting_guide] |

## Decision (what the course should teach)
**Always set `reasoning_effort` explicitly** in course code rather than relying on defaults — defaults moved twice across the 5.x line (`medium` → `none` → `medium`) and will confuse students. Teach the explicit `none` value for latency-sensitive demos and explicit `medium` for general reasoning. Add a callout box: "Defaults changed across versions; pin `reasoning_effort` so your cost and latency are predictable." Do **not** teach "5.2's `none` default is inherited by 5.5" — it is not [source: https://developers.openai.com/api/docs/models/gpt-5.5].
