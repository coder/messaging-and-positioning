# Deploy AI Coding Agents

## Summary

Coder lets developers use the AI coding agents they already prefer, while giving platform and security teams control over where those agents run, what they can access, and how their activity is governed.

## Who This Is For

- **Developers** who want to use AI coding agents like Claude Code, Codex, or custom agents, and want to keep using the models and workflows they already prefer.
- **Platform and security teams** who need centralized visibility and policy control over agent activity instead of it happening ad hoc, unmanaged, on individual laptops.
- **Organizations scaling agent adoption** across a large developer population, who need this to work without standing up a separate platform or rebuilding their existing tech stack.

## The Problem

Developers are already choosing their own AI coding agents, but that activity typically happens outside any centralized visibility: LLM credentials get distributed and managed ad hoc, prompts and tool usage go unlogged, and there's no way to approve or restrict which models and providers are actually being used. Organizations that try to enable agents safely often assume they'll need to rebuild their tech stack or lock developers into a specific vendor's agent and model, which slows adoption and creates the same lock-in risk enterprises are trying to avoid elsewhere in their infrastructure.

## Desired Outcome

Developers keep using the AI agents and models they prefer, Claude Code, Codex, custom agents, or Coder's own native agent, without changing how they work. Admins get centralized authentication for every AI request, an audit trail of prompts, tool calls, and token consumption, and the ability to approve which models and providers are sanctioned for use across the organization. None of this requires standing up new, separate infrastructure.

## How Coder Solves It

### Scale Without Local Risk

Developers and agents run side by side in self-hosted workspaces, deployed from the same pre-configured templates with no drift and no local risk. Teams can build with Claude Code, Codex, or custom agents inside the same developer workspaces they already use, with no separate infrastructure to provision or maintain.

### Observe and Control AI Workflows

AI Gateway centralizes LLM access for policy enforcement, auditability, and troubleshooting. Every AI request is authenticated with an associated user, and Coder captures prompts, model usage, token consumption, and tool invocations, giving admins the audit trail they need for compliance review and the usage data they need to monitor adoption.

### Run Agents Without Lock-In

Organizations can connect supported providers such as Anthropic, OpenAI, Google, and Bedrock, or compatible self-hosted models, and switch configured models without changing platforms. Coder Agents runs its agent loop on the Coder control plane and keeps LLM provider credentials out of workspaces. Source files and credentials needed by workspace tools can still be present there, and prompts and relevant tool results go to the configured inference endpoint ([Coder models](https://coder.com/docs/ai-coder/agents/models), [Coder architecture](https://coder.com/docs/ai-coder/agents/architecture), [template credentials](https://coder.com/docs/ai-coder/agents/platform-controls/template-optimization#external-service-credentials)).

### Choose How Each Agent Runs

Coder supports three ways to run coding agents, and organizations can use all three. Coder Agents runs its loop in the self-hosted Coder control plane and shell/file tools in workspaces, with inference at a configured supported endpoint; keeping inference in-house requires a suitable self-hosted model. Third-party agents such as Claude Code and Codex can run inside workspaces under template network policy, with AI Gateway controls for supported traffic routed through it. Agent Relay connects Claude Code and Cursor cloud sessions to self-hosted workspaces, while the provider retains its cloud orchestration and inference outside AI Gateway's audit path ([Coder architecture](https://coder.com/docs/ai-coder/agents/architecture), [Gateway clients](https://coder.com/docs/ai-coder/ai-gateway/clients), [Agent Relay](https://coder.com/docs/ai-coder/agent-relay)).

Self-hosted Claude Managed Agents, in private beta, overlaps with Coder Agents for coding automation. Anthropic supplies a configurable Claude harness, console, and sandbox deployment tooling; the customer operates that stack. Coder's distinction is supported model-family choice and an integrated development-workspace platform, not the absence of environments in Managed Agents. Teams can retain Coder Workspaces for developers while choosing Managed Agents for separate workloads, but a direct execution-backend integration is not documented as supported. See [Coder and Claude Managed Agents](../market-landscape/claude-managed-agents.md).

## Products Involved

- **Coder Workspaces** — the environment agents execute inside, whether that's a third-party agent running in a workspace or a Coder Agents session. Template-defined network policy controls what every agent in the workspace can reach.
- **Coder Agents** — the native, control-plane agent experience, model-agnostic and requiring no separate deployment.
- **AI Governance (including AI Gateway)** — centralizes model access, authentication, and auditing.
- **Coder Agent Relay** — for organizations that want to keep using a cloud-hosted agent's experience (Cursor, Claude Code) while execution happens inside a self-hosted Coder workspace.

## Proof Points

- A U.S. Defense Intelligence platform gives 2,500+ developers pre-approved, ATO-compliant environments through the U.S. military's first true multi-tenant Coder deployment ([U.S. Defense Intelligence Organization success story](https://coder.com/success-stories/u-s-defense-intelligence-organization)). Coder's [defense sovereignty blog](https://coder.com/blog/ai-agent-security-sovereignty-defense) presents that centralized-approval model as the foundation for governing AI agents in the same kind of environment. The success story itself doesn't describe AI agent usage.
- Industry context: as of Coder's Coder Agents beta announcement, 61% of engineering teams were already running AI coding agents, most still without the infrastructure to scale them safely ([Coder blog: Self-Hosted, AI Model Agnostic Coder Agents](https://coder.com/blog/self-hosted-ai-model-agnostic-coder-agents)). This is an industry-adoption stat Coder has published, not a customer-specific result.

## Known Limitations

Governance depth currently varies by how an agent runs. Third-party agents running inside a Coder workspace are subject to the workspace's template-defined network policy and can be routed through AI Gateway for model-level governance. Coder Agents routes its model traffic through AI Gateway automatically, and its workspaces can be restricted to the control plane and git provider. Network policy is only as strict as the template makes it: if a template doesn't restrict outbound access, its workspaces have full internet access. Cloud-hosted agents connected through Agent Relay keep their orchestration and inference in the provider's cloud, so AI Gateway's model-level auditing doesn't extend to that portion of the activity. See the AI Governance and Agent Relay message houses for the current specifics.

## Related Use Cases

- [Developer Experience](./developer-experience.md)
- [Compute / Resource Optimization](./compute-resource-optimization.md)
- [ML Operations](./ml-operations.md)

## Related Audiences

- [Developer](../audiences/developer.md)
- [Platform Engineer](../audiences/platform-engineer.md)
- [CISO](../audiences/ciso.md)
- [CTO](../audiences/cto.md)
