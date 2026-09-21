# Agent Relay Message House

## Status Quo

### Without Agent Relay

Developers want the cloud agent experience tools like Cursor Cloud Agents and Claude Code deliver. Enterprises may be comfortable adopting SaaS orchestration, but not agent execution that happens outside infrastructure they control. Security and platform teams need control over where code is accessed, where commands run, and what internal systems agents can reach, and today that's an architectural mismatch, not a product problem with any one tool.

- Developers adopt cloud-hosted agents on their own if the enterprise doesn't provide an approved path, and that's how shadow AI proliferates.
- Enterprises that could otherwise adopt a cloud agent platform hold back specifically because execution happens outside infrastructure they control.
- Security and platform teams are asked to approve tools whose orchestration and execution they can't govern, isolate, or audit.
- A handful of self-hosted machines wired up manually to a cloud agent can work at small scale, but breaks down when hundreds or thousands of agents need governed workspaces at once.

## The 3 Whys

### Why Do Anything?

Developers want the best cloud agents. Platform and security teams need control over where sensitive development work happens. Neither side is wrong, and neither side should have to lose to satisfy the other.

### Why Now?

Agent adoption is moving fast. Enterprises need an approved path to the cloud agents developers already want before unmanaged usage becomes the default. Shadow AI isn't a hypothetical risk; it's already how these tools get adopted in the absence of a sanctioned path.

### Why Agent Relay?

Agent Relay creates that approved path without changing the agent experience developers already want. It connects cloud-hosted agent sessions, from Cursor Cloud Agents or Claude Code, to self-hosted Coder Workspaces on infrastructure the enterprise controls. The agent's orchestration and model inference stay with the provider; execution, where the agent accesses code, runs commands, and reaches internal systems, happens inside a governed Coder workspace. Agent Relay itself is the means, not the end: the value customers are buying is the Coder infrastructure underneath, self-hosting, neutrality, standardization, connectivity, and governance, that already works for human developers and now extends to agents.

## Messaging Statement

### Short

Agent Relay connects cloud-hosted AI agents, like Cursor Cloud Agents and Claude Code, to secure, self-hosted Coder Workspaces on infrastructure the enterprise controls. Developers keep the cloud agent experience they want; platform and security teams get the execution control, isolation, and auditability they require. Neither side has to compromise.

### Medium

Enterprises face a choice that shouldn't have to be a trade-off: give developers the cloud AI agents they want, or maintain control over where that agent's work actually happens. Agent Relay resolves that tension. It's a broker that connects cloud-hosted agent sessions from providers like Cursor and Claude Code to ephemeral, self-hosted Coder Workspaces, provisioned, governed, and torn down automatically as sessions start and end.

Orchestration and model inference stay with the agent provider; execution happens inside infrastructure the enterprise already trusts, with the same governance, identity, and network controls Coder already provides for human developers. The result is an approved path to the agents developers already want, on infrastructure security and platform teams can actually control.

## Taglines

- Cloud-hosted agents. Self-hosted execution.
- The approved path to the cloud agents developers already want
- Your infrastructure, their agent
- Best-of-breed agent experience, on infrastructure you control
- Give developers the agents they want, before they find their own

## Use Cases

### Use Case 1: Cloud Agent Adoption Without Losing Execution Control

**Desired Outcome:** Give developers access to cloud-hosted agents like Cursor Cloud Agents and Claude Code without agent execution happening outside infrastructure the enterprise controls.

**Challenges:** Cloud agent platforms orchestrate and execute in the provider's cloud. Enterprises with strict requirements around source code, execution, or private system access can't accept that model, even if they're otherwise comfortable with SaaS.

**Coder's Solution:** Agent Relay connects the provider's cloud-hosted session to an ephemeral, self-hosted Coder workspace. Orchestration and inference stay with the provider; execution runs inside infrastructure the enterprise controls, with normal Coder governance applied to it.

### Use Case 2: Extending Existing Coder Infrastructure to Cloud-Hosted Agents

**Desired Outcome:** Platform teams that already run Coder for human developers extend the same governed infrastructure to cloud-hosted agents, without standing up a new platform.

**Challenges:** A few self-hosted machines wired up manually to a cloud agent can work at small scale, but breaks down once hundreds or thousands of agent sessions need governed workspaces concurrently. Existing infrastructure isn't designed to provision, isolate, and tear down environments at that pace.

**Coder's Solution:** Agent Relay maps agent pools to existing Coder organizations and Terraform-based workspace templates. Coder handles provisioning and deprovisioning automatically as sessions start and end, scaling to zero when idle, using the same templates, RBAC, and audit infrastructure the platform team already manages.

### Use Case 3: Providing an Approved Path Before Shadow AI Takes Hold

**Desired Outcome:** Give developers a sanctioned way to use the cloud agents they want, before they adopt them unmanaged.

**Challenges:** Developers will use the tools they want with or without approval. Without a sanctioned path, that usage happens outside any platform team's visibility, with unmanaged credentials and no audit trail.

**Coder's Solution:** Agent Relay gives developers the cloud agent experience they're already asking for, routed through infrastructure the platform team provisions and governs, so adoption happens inside an approved path instead of the shadows.

## Value Props / Differentiators

- **Best-of-breed agent experience, self-hosted execution**: Developers keep the Cursor or Claude Code experience they already want. The enterprise keeps control over where that agent's work actually happens.
- **Solves the scale problem DIY can't**: Wiring up a few self-hosted machines to a cloud agent works at small scale. Agent Relay is built for bursts of hundreds or thousands of agent sessions competing for governed workspaces at once.
- **Zero-incremental-platform for existing Coder customers**: Organizations already running Coder extend to cloud-hosted agents using the templates, RBAC, and audit infrastructure they already manage, no new platform or security review required.
- **Provider-agnostic by design**: Cursor and Claude Code are supported today; the underlying architecture is built to support additional cloud-hosted agent providers as they enable self-hosted execution.
- **Out of the data path once connected**: Agent Relay brokers the initial session-to-workspace connection, then steps back to managing the workspace's lifecycle. It isn't a proxy sitting between the agent and its work.

## Supporting Features

### Division of Labor

Cloud agent providers (Cursor, Claude Code) continue to deliver the agent experience, cloud-hosted orchestration, model inference, and developer workflow. Coder provides the self-hosted execution layer: customer-controlled workspaces, compute and environment lifecycle, and the networking, access, policy, and governance controls the enterprise already trusts.

### How It Works

1. **Start**: A developer delegates a task to a cloud agent session through the provider's normal interface.
2. **Relay**: Agent Relay detects the new session waiting for execution capacity.
3. **Provision**: Coder creates an ephemeral workspace on the enterprise's infrastructure from a mapped organization and template.
4. **Execute**: The agent's worker connects directly to that workspace and performs its work there. Agent Relay steps out of the data path at this point and manages the workspace's lifecycle rather than sitting between the agent and its execution.

### Lifecycle and Scale

Workspaces are ephemeral: one per agent session, created when the session starts and deleted once the agent's work is done. The architecture scales to zero when no sessions are active, so idle capacity isn't held open, and scales up automatically as concurrent sessions grow.

### Governance

Workspace-level controls, network policy via Agent Firewall, secrets management, and RBAC, apply to the execution environment the same way they would for any other Coder workspace.

## Known Limitations

- **Not fully self-hosted or air-gapped today**: Orchestration and model inference remain in the agent provider's cloud. Agent Relay governs execution, not the entire stack. Organizations that require everything, including inference, inside their perimeter (common in government and defense) are not a fit for this architecture today.
- **Addresses execution control, not a full regulatory review**: Frameworks like the EU's DORA or the UK's FCA/PRA operational resilience regime introduce third-party risk, concentration risk, and resilience requirements that go beyond where execution happens. Agent Relay solves the execution-control piece of that equation, not the entire compliance picture.
- **Early access**: Agent Relay is in preview with select regulated enterprise customers, currently supporting Cursor and Claude Code as cloud agent providers.

## Competitive Position

**Agent Relay vs. DIY self-hosted machines:** An enterprise can wire up a few self-hosted machines to a cloud agent's self-hosted execution option without Coder. The value of Agent Relay isn't that the machine is customer-owned; it's that the execution environment is provisioned, isolated, governed, and torn down as part of a platform. That distinction doesn't matter at small scale. It matters enormously when hundreds or thousands of agents need governed workspaces concurrently, which is a problem DIY infrastructure isn't built to solve.

**Agent Relay vs. accepting shadow AI:** The alternative to an approved path isn't "no AI usage." Developers will use the agents they want regardless. Shadow AI isn't a cheaper alternative to Agent Relay; it just moves the cost into security risk, fragmented infrastructure, and loss of control.

## Target Market / ICP

**Best-fit customers:**

- Want or already use a supported cloud agent (Cursor, Claude Code)
- Operate primarily on self-hosted infrastructure
- Have strict requirements around source code or execution
- Need agents to access private tools, dependencies, or internal systems
- Involve platform, security, or compliance teams in AI adoption decisions
- Want to expand agent usage beyond individual developers to the broader organization

**Often found in:** Financial services, healthcare, and insurance.

**Qualification note:** For existing Coder customers, self-hosting is already the default; the signal to look for is agent adoption. For cloud-agent-led opportunities, self-hosting requirements are a signal to uncover early. If a prospect is fully comfortable with cloud-hosted execution and has no meaningful security or infrastructure constraints, Agent Relay isn't likely to be the deciding factor.

**Where it's a weaker fit:**

- **Fully self-hosted or air-gapped requirements**, common in government and defense, since orchestration and inference still happen in the provider's cloud today.
- **Highly regulated financial services** where the requirement extends beyond execution to the entire stack, including inference; regulation here is a spectrum, and Agent Relay addresses part of the third-party risk equation, not all of it.

## Buyer Personas

### Economic Buyer (CISO, CTO, etc.)

**Common pain points:** Developers want cloud agents the security team hasn't approved. No way to control where agent execution happens or what it can access. Risk of unmanaged, unauditable agent activity across the organization.

Agent Relay gives economic buyers an approved path to the cloud agents developers already want, without giving up control over where that work happens. Execution runs inside infrastructure the organization already governs, with the same identity, network, and audit controls applied to it. This lets the organization say yes to agent adoption instead of either blocking it or accepting the risk of unmanaged usage.

### Platform Engineering Leaders (VP / Dir of Platform Engineering)

**Common pain points:** Pressure to give developers the AI tools they're asking for. No standardized way to provision execution environments for cloud-hosted agents. Concern that a few manually wired self-hosted machines won't hold up as agent usage scales.

Agent Relay lets platform teams extend infrastructure they already operate, Coder organizations, templates, RBAC, and audit logging, to cloud-hosted agents, without standing up a new platform. It's built to handle bursts of concurrent agent sessions that ad hoc, manually provisioned machines can't.

### Developers

**Common pain points:** Wanting to use Cursor or Claude Code, but being blocked by security or platform team concerns. Having to choose between the agent experience they want and the infrastructure their organization will approve.

Agent Relay doesn't change the agent experience developers already want. They keep using Cursor or Claude Code exactly as they would otherwise; the difference is invisible to them, since the agent's execution happens inside a Coder workspace behind the scenes.

## Vertical Messaging

### Financial Services

Agent Relay gives financial services organizations a way to adopt cloud agents like Cursor Cloud Agents while keeping execution inside infrastructure they control. This addresses the execution-control piece of frameworks like the EU's DORA or the UK's FCA/PRA operational resilience regime, though organizations should evaluate it as one part of a broader third-party risk and resilience program, not a complete regulatory solution on its own.

### Healthcare and Insurance

Agent Relay lets healthcare and insurance organizations give developers access to cloud agents without agent execution reaching systems or data outside infrastructure they control, supporting the access controls and auditability these industries typically require for any system touching sensitive data.

## Partner Narrative

### Cursor

Cursor delivers the cloud agent experience and orchestration developers already want; Coder governs where that agent executes. Neither side has to change what it does well. Customers get the best-of-breed agent experience they're asking for, running on infrastructure their platform and security teams can actually approve. Cursor's integration with Coder is designed to unlock enterprise accounts that an execution-in-the-cloud-only model couldn't reach on its own, particularly in financial services and other regulated industries.

### Anthropic (Claude Code)

The same model applies to Claude Code: orchestration and inference stay with Anthropic's cloud, while Agent Relay connects Claude Code's cloud sessions to self-hosted Coder workspaces for execution. This gives Anthropic a path into enterprises that need execution control they can't get from a cloud-only deployment, while giving Coder customers another supported cloud agent option on the same governed infrastructure they already operate.
