# Learn AI Infrastructure

I checked these against search results. Links marked ✓ appeared in those results; the rest I’m recalling from memory, so open them to confirm they still exist.

## 1. The core agent loop

- ✓ [anthropics/claude-cookbooks](https://github.com/anthropics/claude-cookbooks): The `patterns/agents` folder has notebooks for prompt chaining, parallelization, routing, orchestrator-subagents, and evaluator-optimizer. These are minimal implementations, ideal for building your own 150-line loop.
- ✓ [anthropics/claude-agent-sdk-demos](https://github.com/anthropics/claude-agent-sdk-demos): Working demos built on the Agent SDK.
- ✓ [openai/openai-agents-python](https://github.com/openai/openai-agents-python): A second SDK to compare against.
- ✓ [SWE-agent/mini-swe-agent](https://github.com/SWE-agent/mini-swe-agent): A roughly 100-line descendant of SWE-agent, making it easy to read end to end.

## 2. Real agents to study

### Coding agents

- [All-Hands-AI/OpenHands](https://github.com/All-Hands-AI/OpenHands): The fuller, production-oriented option, with Docker sandboxing, browser access, Bash, and an editor. The organization may have been renamed to match [openhands.dev](https://openhands.dev).
- [SWE-agent/SWE-agent](https://github.com/SWE-agent/SWE-agent): The minimal research reference for agent-computer interfaces.

### Multi-agent and research patterns

- The `orchestrator_workers` notebook in the Claude cookbook above.
- The sub-agent examples under `claude_agent_sdk/`.

## 3. Production infrastructure

### Sandboxing

- ✓ [kubernetes-sigs/agent-sandbox](https://github.com/kubernetes-sigs/agent-sandbox): The Kubernetes-native project for isolated agent workloads. Third-party projects such as k8e advertise compatibility with it.
- [firecracker-microvm/firecracker](https://github.com/firecracker-microvm/firecracker): MicroVM-based sandboxing.
- [google/gvisor](https://github.com/google/gvisor): Userspace kernel and container isolation.
- [kata-containers/kata-containers](https://github.com/kata-containers/kata-containers): VM-backed container isolation.
- [e2b-dev/E2B](https://github.com/e2b-dev/E2B): A hosted-sandbox reference and API that many self-hosted sandboxes imitate. Its SDK is useful for understanding sandbox interfaces.
- ✓ [StacyOS/stacyvm](https://github.com/StacyOS/stacyvm) and ✓ [xiaods/k8e](https://github.com/xiaods/k8e): Newer, smaller projects. StacyVM lets you swap Docker, gVisor, or Firecracker backends with one configuration line. Use them as architecture references, but vet them carefully before using them in production.

### Durable execution

- ✓ [temporalio/samples-python](https://github.com/temporalio/samples-python): The `openai_agents` directory contains agent patterns, handoffs, and a multi-agent financial research example running on Temporal.
- ✓ [temporalio/samples-typescript](https://github.com/temporalio/samples-typescript): The AI SDK samples add durable execution to Vercel AI SDK agents.
- ✓ [temporal-community/daily-news-briefing-agent-demo](https://github.com/temporal-community/daily-news-briefing-agent-demo): Runs the same agent workflow in plain Python and on Temporal side by side, making crash recovery easy to observe. This is the best single repository for learning why durability matters.

### Observability

- [langfuse/langfuse](https://github.com/langfuse/langfuse): Open-source and self-hostable. It accepts OpenTelemetry traces through an OTLP endpoint.
- ✓ [traceloop/openllmetry](https://github.com/traceloop/openllmetry): OpenTelemetry-based instrumentation that works with backend systems including Datadog, Grafana, and Jaeger. A good fit for an existing OTel stack.

## 4. Evals

- ✓ [UKGovernmentBEIS/inspect_ai](https://github.com/UKGovernmentBEIS/inspect_ai)
- ✓ [UKGovernmentBEIS/inspect_evals](https://github.com/UKGovernmentBEIS/inspect_evals): Community evaluations for the Inspect AI framework, including agent tasks. The SWE-bench task lets you plug in your own agent and compare it against baselines.
- ✓ [princeton-pli/hal-harness](https://github.com/princeton-pli/hal-harness): A reproducible agent-evaluation harness across benchmarks such as SWE-bench Verified, GAIA, and tau-bench. It does not constrain your agent framework. The result found may be a fork, so check for the Princeton original.
- [SWE-bench/SWE-bench](https://github.com/SWE-bench/SWE-bench): The benchmark itself.
- [sierra-research/tau-bench](https://github.com/sierra-research/tau-bench): The benchmark itself.

## 5. Ecosystem

- ✓ [modelcontextprotocol/python-sdk](https://github.com/modelcontextprotocol/python-sdk): The official Python SDK for MCP servers and clients.
- [modelcontextprotocol/typescript-sdk](https://github.com/modelcontextprotocol/typescript-sdk): The official TypeScript SDK.
- ✓ [modelcontextprotocol/servers](https://github.com/modelcontextprotocol/servers): Reference server implementations for filesystem, Git, PostgreSQL, and more. Study these for tool-design conventions, then write your own.
- Frameworks to compare after building your own loop:
  - [langchain-ai/langgraph](https://github.com/langchain-ai/langgraph)
  - [OpenAI Agents SDK](https://github.com/openai/openai-agents-python)

## 6. Study order

1. Study the Claude Cookbook `patterns/agents` examples and mini-SWE-agent, then build your own loop.
2. Run the Temporal news-briefing demo. Crash a worker and watch it resume.
3. Study agent-sandbox alongside Firecracker or gVisor documentation, then run model-generated code in isolation.
4. Add Langfuse or OpenLLMetry and trace your loop.
5. Explore `inspect_evals`, write 10 tasks for your agent, and gate changes on the pass rate.
