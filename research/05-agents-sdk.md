# R5 — Agents SDK Cheatsheet (Primitives + Minimal Snippets)

_Sources: openai-agents-python repo [source: https://github.com/openai/openai-agents-python] and the Agents guide [source: https://developers.openai.com/api/docs/guides/agents]._

> `[unverified]` The snippets below reflect the SDK's documented surface at research time. The repo's import names and constructors evolve — run `pip show openai-agents` and check the quickstart before pinning these in notebooks [source: https://developers.openai.com/api/docs/guides/agents/quickstart].

## When to reach for the SDK
Use the Agents SDK when **your server owns orchestration, tool execution, state, and approvals** — typed Python or TypeScript with direct runtime control [source: https://developers.openai.com/api/docs/guides/agents]. Recommended model: latest is `gpt-5.5` [source: https://developers.openai.com/api/docs/guides/agents].

## Primitives

### Agent
The LLM config: instructions + tools. Plans, calls tools, collaborates, keeps state [source: https://developers.openai.com/api/docs/guides/agents].
```python
from agents import Agent

agent = Agent(
    name="Assistant",
    instructions="Help users with their tasks",
)
```

### Runner
Executes the agent loop; manages streaming, state continuation, result handling [source: https://github.com/openai/openai-agents-python].
```python
from agents import Runner

result = Runner.run_sync(agent, "Your task here")
print(result.final_output)
```

### Tools
Function tools, hosted tools, and MCP servers [source: https://github.com/openai/openai-agents-python].
```python
from agents import Agent, function_tool

@function_tool
def calculate(x: int, y: int) -> int:
    return x + y

agent = Agent(name="Assistant", tools=[calculate])
```
`[unverified]` The repo summary showed a `Tool(...)` wrapper; the idiomatic decorator is `@function_tool`. Confirm against the current README.

### Handoffs
Delegate to specialist agents; you explicitly control which agent handles the reply [source: https://github.com/openai/openai-agents-python] [source: https://developers.openai.com/api/docs/guides/agents].
```python
specialist = Agent(name="Specialist", instructions="Handle refunds")
triage = Agent(name="Triage", handoffs=[specialist])
```

### Guardrails
Configurable input/output validation; can pause or block risky operations / add human review checkpoints [source: https://github.com/openai/openai-agents-python] [source: https://developers.openai.com/api/docs/guides/agents].
```python
from agents import Guardrail

guardrail = Guardrail(name="content_filter", validate_input=True)
agent = Agent(name="Assistant", guardrails=[guardrail])
```

### Sessions
Automatic conversation-history management; resumable context across runs/turns [source: https://github.com/openai/openai-agents-python].
```python
from agents import Session

session = Session()
result = Runner.run_sync(agent, "message", session=session)
```

### Tracing
Built-in tracking of agent runs to view, debug, and optimize workflows; progress from traces to eval loops [source: https://github.com/openai/openai-agents-python] [source: https://developers.openai.com/api/docs/guides/agents].
```python
from agents import trace

with trace("course-demo-workflow"):
    Runner.run_sync(agent, "Trace this run")
```

## Decision (how to teach the SDK in the course)
Teach the primitives in this dependency order — **Agent → Runner → Tools → Sessions → Handoffs → Guardrails → Tracing** — because each builds on the prior. Pin `gpt-5.5` (or `gpt-5.4-mini` for cheaper student runs) as the agent model. Because the SDK import surface is unstable, **verify every snippet against the installed package version in a notebook before publishing** rather than trusting these examples verbatim; mark the `Guardrail`/`Tool` constructor forms as the most likely to have drifted.
