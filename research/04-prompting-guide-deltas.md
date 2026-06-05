# R4 — Prompting Guide Deltas: GPT-5.2 Guide vs Original GPT-5 Guide

_Sources: GPT-5.2 prompting guide [source: https://developers.openai.com/cookbook/examples/gpt-5/gpt-5-2_prompting_guide] and original GPT-5 prompting guide [source: https://developers.openai.com/cookbook/examples/gpt-5/gpt-5_prompting_guide]._

## What was in the ORIGINAL GPT-5 guide
Confirmed sections [source: https://developers.openai.com/cookbook/examples/gpt-5/gpt-5_prompting_guide]:
- Agentic workflow predictability (incl. **controlling agentic eagerness**)
- **Tool preambles**
- **Reasoning effort**
- Reusing reasoning context with the Responses API
- Maximizing coding performance (frontend + codebase)
- Optimizing intelligence & instruction-following (steering, the **`verbosity` API parameter**, instruction following, minimal reasoning, markdown formatting, metaprompting)

Explicitly **absent** from the original guide: `output_verbosity_spec`, scope discipline, long-context re-grounding, uncertainty self-checks [source: https://developers.openai.com/cookbook/examples/gpt-5/gpt-5_prompting_guide].

## The four new/expanded sections in the GPT-5.2 guide

### 1. `output_verbosity_spec` (NEW — structured verbosity control)
| Original GPT-5 | GPT-5.2 |
|---|---|
| A single `verbosity` API parameter (low/medium/high) to steer output length [source: https://developers.openai.com/cookbook/examples/gpt-5/gpt-5_prompting_guide] | A **prompt-level spec**: "Default: 3–6 sentences or ≤5 bullets for typical answers," break into "digestible chunks," avoid "long narrative paragraphs" [source: https://developers.openai.com/cookbook/examples/gpt-5/gpt-5-2_prompting_guide] |

Delta: moves from a coarse API knob to an explicit, in-prompt verbosity contract.

### 2. Scope discipline (NEW)
| Original GPT-5 | GPT-5.2 |
|---|---|
| Covered via "agentic eagerness" — tune proactivity, mostly through `reasoning_effort` [source: https://developers.openai.com/cookbook/examples/gpt-5/gpt-5_prompting_guide] | Dedicated block: "Implement EXACTLY and ONLY what the user requests. No extra features, no added components, no UX embellishments." [source: https://developers.openai.com/cookbook/examples/gpt-5/gpt-5-2_prompting_guide] |

Delta: directly counters GPT-5.2's tendency to produce more code than the minimal spec.

### 3. Long-context re-grounding (NEW)
| Original GPT-5 | GPT-5.2 |
|---|---|
| No equivalent section [source: https://developers.openai.com/cookbook/examples/gpt-5/gpt-5_prompting_guide] | For inputs >~10k tokens: "produce a short internal outline" and "re-state the user's constraints explicitly before answering," anchoring claims to specific sections [source: https://developers.openai.com/cookbook/examples/gpt-5/gpt-5-2_prompting_guide] |

### 4. Uncertainty self-checks (NEW)
| Original GPT-5 | GPT-5.2 |
|---|---|
| No equivalent section [source: https://developers.openai.com/cookbook/examples/gpt-5/gpt-5_prompting_guide] | High-risk domains: prompt the model to flag "unstated assumptions," "specific numbers or claims not grounded," and "overly strong language" before finalizing [source: https://developers.openai.com/cookbook/examples/gpt-5/gpt-5-2_prompting_guide] |

## Continuity (carried over, evolved)
- **Tool preambles** persist but verbosity is clamped: "brief updates (1–2 sentences) only when starting new major phases of work or discovering something that changes the plan" vs the original's tunable-across-four-axes framing [source: https://developers.openai.com/cookbook/examples/gpt-5/gpt-5-2_prompting_guide] [source: https://developers.openai.com/cookbook/examples/gpt-5/gpt-5_prompting_guide].
- **Reasoning effort** persists but with the changed default (see `02-reasoning-effort-default.md`).

## Decision (what to add to the course's prompting module)
Add four new mini-lessons keyed to the 5.2 additions — (1) an explicit `output_verbosity_spec` template, (2) a "scope discipline" guardrail snippet, (3) a long-context re-grounding preamble, (4) an uncertainty self-check checklist — and frame them as the deltas since the original GPT-5 guide. These are the highest-leverage updates because they address concrete regressions (over-coding, verbosity, ungrounded claims) that students hit in practice.
