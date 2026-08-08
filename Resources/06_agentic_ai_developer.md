# GitHub Certified: Agentic AI Developer (GH-600)

<p align="center"><img src="../assets/ai-developer-splash.png" alt="GitHub Certified Agentic AI Developer certification path" width="100%"></p>

Official exam title: **GH-600: Developing in Agentic AI Systems**.

GH-600 focuses on building and operating agentic software-development workflows
with GitHub as the system of record and control plane. This is a systems exam:
an agent is not just a clever prompt, but a loop involving goals, context,
tools, state, evaluation, permissions, and accountable human oversight.

## Start Here

- [Official certification page](https://learn.microsoft.com/en-us/credentials/certifications/agentic-ai-developer/): current exam details, policies, and registration.
- [GH-600 study guide](https://aka.ms/GH600-StudyGuide): skills measured and preparation references.
- [GitHub Learn catalog](https://learn.github.com/certification/AGENTIC): official GitHub learning catalog; sign-in may be required.
- [Foundations of Agentic AI in GitHub](https://learn.microsoft.com/en-us/training/modules/foundations-agentic-ai/): Microsoft Learn introduction to the platform and agent concepts.
- [Designing Agent Architecture and SDLC Integration](https://learn.microsoft.com/en-us/training/modules/design-agent-architecture-integration/): architecture, lifecycle, and integration practice.
- [Tooling, MCP, and Agent Execution Environments](https://learn.microsoft.com/en-us/training/modules/agent-tooling-mcp-execution-environments/): tools, MCP, permissions, and execution environments.
- [GitHub Copilot documentation](https://docs.github.com/en/copilot): current agent, context, customization, and governance concepts.
- [Official practice assessment](https://learn.microsoft.com/en-us/credentials/certifications/agentic-ai-developer/): open the practice assessment from the certification page after studying.

## What to Know

The official GH-600 study guide lists these domains:

1. **Prepare agent architecture and SDLC processes (15-20%):** agent roles, lifecycle integration, task boundaries, context flow, and selecting an appropriate agent pattern.
2. **Implement tool use and environment interaction (20-25%):** tool permissions, repositories, APIs, terminals, workflows, artifacts, sandboxes, and observable actions.
3. **Manage memory, state, and execution (10-15%):** session state, durable memory, checkpoints, context limits, resumability, and controlled execution.
4. **Perform evaluation, error analysis, and tuning (15-20%):** success criteria, test sets, traces, failure categories, metrics, feedback loops, and iteration.
5. **Orchestrate multi-agent coordination (15-20%):** delegation, specialized roles, handoffs, shared context, synchronization, conflicts, and cost or latency trade-offs.
6. **Implement guardrails and accountability (10-15%):** least privilege, approvals, isolation, auditability, policy, human oversight, and rollback or recovery.

Useful companion references include [custom agents](https://docs.github.com/en/copilot/concepts/agents/cloud-agent/about-custom-agents),
[MCP](https://docs.github.com/en/copilot/concepts/context/mcp),
[Copilot Memory](https://docs.github.com/en/copilot/concepts/agents/copilot-memory),
[cloud-agent risks and mitigations](https://docs.github.com/en/copilot/concepts/agents/cloud-agent/risks-and-mitigations),
and [responsible use of agents](https://docs.github.com/en/copilot/responsible-use/agents).

## Hands-On Missions

### Mission 1: Draw the Agent Loop

For a task such as updating a documentation set, diagram the loop: request,
plan, context selection, tool call, observation, state update, validation, and
human approval. Mark every point where the agent can fail or should stop.

### Mission 2: Give It Tools, Then Take Them Away

Define a minimal tool set for an agent that edits a repository. For each tool,
state its input, output, permission boundary, failure mode, and audit evidence.
Then remove one tool and explain how the workflow should degrade gracefully.

### Mission 3: Build an Evaluation Card

Create five representative tasks and score an agent on correctness, safety,
usefulness, trace quality, and recovery from failure. Record one false positive,
one false negative, and one human override. Use those results to propose a tuning
change rather than simply asking for a better prompt.

### Mission 4: Coordinate Without Chaos

Split a documentation task between a researcher, implementer, and reviewer.
Define the handoff contract, shared artifacts, stop conditions, and conflict
resolution rule. Explain when one agent would be better than three.

## Quick Self-Check

- What makes an agentic workflow different from a single model response?
- How do tools, permissions, sandboxes, and approvals constrain action?
- What state should persist, and what context should expire after a task?
- How would you distinguish a planning failure from a tool failure?
- What evidence would let a human audit, reproduce, approve, or roll back an agent's work?

## Keep Current

Agent features, models, policies, and terminology evolve rapidly. Track the
[official GH-600 study guide](https://aka.ms/GH600-StudyGuide) and confirm exam
duration, delivery, language, and policies on the [official certification page](https://learn.microsoft.com/en-us/credentials/certifications/agentic-ai-developer/)
before scheduling or sitting the exam.