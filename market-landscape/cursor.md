# Coder and Cursor

| Field | Value |
|---|---|
| Date generated | 2026-09-28 |
| Last reviewed | 2026-09-28 |
| Category | Complementary |

*Cursor is made by Anysphere, Inc. As of August 2026, Anysphere is reported to be a wholly owned subsidiary of SpaceX, being integrated into the SpaceXAI team ([Techzine](https://www.techzine.eu/news/devops/143619/spacex-completes-acquisition-of-cursor/), [Wikipedia](https://en.wikipedia.org/wiki/Cursor_(company))). The product name is unchanged.*

## One-Line Positioning

Cursor provides the AI coding experience, agent orchestration, and inference, and Coder provides the self-hosted, governed workspaces where Cursor's IDE, CLI, and Cloud Agents do their work.

## Strategic Themes and Patterns

- **Relationship.** Complementary. Cursor connects to Coder workspaces as an IDE through the Coder extension ([Coder docs](https://coder.com/docs/user-guides/workspace-access/cursor)), runs inside workspaces as a CLI agent through a registry module ([Coder Registry](https://registry.coder.com/modules/coder-labs/cursor-cli)), and executes Cursor Cloud Agent tool calls in Coder workspaces through Agent Relay ([Coder docs](https://coder.com/docs/ai-coder/agent-relay/cursor)). Cursor's own docs list Coder as a Self-Hosted Machines integration partner ([Cursor docs](https://cursor.com/docs/cloud-agent/self-hosted/integrations)).
- **Where the products touch.** Cursor also sells Cursor-hosted Cloud Agents that run each agent in an isolated cloud VM ([Cursor docs](https://cursor.com/docs/cloud-agent/choose-runtime)). That managed execution environment is the one area adjacent to Coder. Cursor itself offers self-hosted execution as an alternative for customers whose constraints the managed cloud can't meet ([Cursor docs](https://cursor.com/docs/cloud-agent/self-hosted)), and Coder is one way to provide it.
- **Choice, Control, Consistency.** Doesn't apply as a tradeoff, since customers don't choose between the two. Coder adds Control and Consistency under Cursor and preserves Choice by letting the same workspaces run Cursor, Coder Agents, and other agents side by side ([Agent Relay for Cursor FAQ](../products/coder-agent-relay/cursor-faq.md)).
- **How they work together.**
  - **IDE.** Developers run Cursor locally and connect to a Coder workspace over the Coder extension. Admins can add a Cursor module to templates ([Coder docs](https://coder.com/docs/user-guides/workspace-access/cursor)) and define MCP servers for Cursor in Terraform template code ([Coder blog](https://coder.com/blog/ship-fast-and-consistent-mcp-tooling-for-cursor)).
  - **CLI agent.** The Cursor CLI module installs the Cursor CLI in a workspace and writes its MCP and rules configuration ([Coder Registry](https://registry.coder.com/modules/coder-labs/cursor-cli)).
  - **Cloud Agents.** A developer picks a Cursor worker pool mapped to a Coder organization and template. Agent Relay claims the request, Coder provisions an ephemeral workspace, and a Cursor worker in that workspace executes the agent's tool calls. Agent Relay tears the workspace down when the session ends ([Coder docs](https://coder.com/docs/ai-coder/agent-relay/cursor)).
  - **Division of labor.** Cursor keeps the client, agent loop, orchestration, and inference. Coder provides the execution environment, networking, identity, policy, and audit around it. Coder doesn't proxy or observe Cursor's model inference ([Coder docs](https://coder.com/docs/ai-coder/agent-relay/cursor)).

## Coder's Strengths Here

- **Governed fleet, not individual machines.** Cursor's My Machines is not an org-wide fleet system, and each worker belongs to one user who owns its cleanup ([Cursor docs](https://cursor.com/docs/cloud-agent/choose-runtime)). Cursor's Team Pools leave the worker image, infrastructure, secrets, scaling policy, and production validation to the customer ([Cursor docs](https://cursor.com/docs/cloud-agent/self-hosted/integrations)). Coder supplies that layer with Terraform templates and per-session ephemeral workspaces ([Coder docs](https://coder.com/docs/ai-coder/agent-relay/cursor)).
- **Existing controls apply automatically.** Because Cursor agent work runs in a Coder workspace, Agent Firewall, RBAC, and audit logging apply without a separate security model ([Coder blog](https://coder.com/blog/introducing-agent-relay-cloud-hosted-agents-self-hosted-execution)).
- **Session-to-user traceability.** Coder logs correlate the Cursor session and user to the workspace where the agent executed ([Coder docs](https://coder.com/docs/ai-coder/agent-relay/cursor)).
- **Customer-operated infrastructure.** Coder runs on infrastructure the customer controls, and all Coder features are supported in air-gapped or offline deployments ([Coder docs](https://coder.com/docs/install/airgap)). Cursor says it doesn't offer on-premises deployment ([Cursor Enterprise](https://cursor.com/enterprise)).
- **One platform for many agents.** The same Coder workspaces run Cursor, Coder Agents, and other agent harnesses, so standardizing on Coder doesn't require standardizing on one agent ([Agent Relay for Cursor FAQ](../products/coder-agent-relay/cursor-faq.md), [coder/coder](https://github.com/coder/coder)).

## Cursor Overview

- **What it is.** An AI coding agent and development environment for understanding codebases, building features, fixing bugs, and reviewing changes ([Cursor docs](https://docs.cursor.com/welcome)). Surfaces include the desktop app, web, mobile, CLI, and Cloud Agents ([Cursor docs](https://cursor.com/docs/cloud-agent/self-hosted), [Wikipedia](https://en.wikipedia.org/wiki/Cursor_(company))).
- **Architecture.** Cursor sends prompts and code context to model providers such as OpenAI, Anthropic, and Google, and to its own inference providers for Cursor models like Composer ([Cursor docs](https://cursor.com/docs/enterprise/privacy-and-data-governance)). Cloud Agents run in Cursor-hosted isolated VMs by default. With Self-Hosted Machines, Cursor still runs the agent loop, inference, and planning, and a worker on customer hardware runs file edits, terminal commands, computer-use tools, and local MCP servers ([Cursor docs](https://cursor.com/docs/cloud-agent/self-hosted)). Workers connect outbound over HTTPS with no inbound ports ([Cursor docs](https://cursor.com/docs/cloud-agent/self-hosted/pool)).
- **Target customer.** Individual developers through large enterprises. Cursor recommends Enterprise for organizations that need pooled usage, invoicing, SCIM, or advanced security controls ([Cursor docs](https://cursor.com/docs/account/teams/pricing)).
- **Deployment model.** SaaS on AWS infrastructure. Cursor doesn't offer on-premises deployment ([Cursor Enterprise](https://cursor.com/enterprise)). Self-Hosted Machines moves tool execution, not the agent loop, onto customer machines ([Cursor docs](https://cursor.com/docs/cloud-agent/self-hosted/pool)).
- **Enterprise controls.** SSO, SCIM, RBAC, MDM policies, Privacy Mode, data residency, and private connectivity over AWS PrivateLink or Cloudflare Tunnel ([Cursor docs](https://cursor.com/docs/enterprise)). Enterprise adds audit logs, an AI code tracking API, model restrictions, and customer-managed encryption keys for Cloud Agent data ([Cursor docs](https://cursor.com/help/security-and-privacy/privacy)). Cursor reports SOC 2 Type II, ISO/IEC 27001:2022, ISO/IEC 42001:2023, and AIUC-1 ([Cursor Security](https://cursor.com/security)).

## Coder Overview for This Comparison

- **Coder Workspaces.** Self-hosted development environments defined in Terraform on VMs, Kubernetes pods, or containers, connected over a WireGuard tunnel ([coder/coder](https://github.com/coder/coder)). Cursor connects to them through the Coder extension and template modules ([Coder docs](https://coder.com/docs/user-guides/workspace-access/cursor)).
- **Agent Relay.** Connects cloud-hosted agent sessions to self-hosted Coder workspaces. It changes where tool calls execute, not where orchestration or inference run. Cursor is the first supported provider ([Coder docs](https://coder.com/docs/ai-coder/agent-relay)). Coder has also announced a Claude Code integration ([Coder blog](https://coder.com/blog/introducing-agent-relay-cloud-hosted-agents-self-hosted-execution)). See the [Agent Relay message house](../products/coder-agent-relay/message-house.md) and [Agent Relay for Cursor FAQ](../products/coder-agent-relay/cursor-faq.md).
- **AI Governance.** AI Gateway for auditing AI sessions, central MCP management, and policy enforcement, plus Agent Firewall for process-level domain restrictions ([Coder docs](https://coder.com/docs/ai-coder/ai-governance)).
- **Coder Agents.** Coder's native agent, whose loop runs in the Coder control plane on customer infrastructure ([coder/coder](https://github.com/coder/coder)). This is the option for organizations that need orchestration inside their perimeter too.

## Known Limitations in Cursor's Approach

- **Agent loop and inference stay in Cursor's cloud (as of 2026-09-28).** Self-hosted pools don't move the agent loop out of Cursor's cloud ([Cursor docs](https://cursor.com/docs/cloud-agent/self-hosted/pool)). Coder doesn't change this, so Cursor with Agent Relay isn't a fit for organizations that require inference inside their perimeter ([Agent Relay message house](../products/coder-agent-relay/message-house.md)).
- **Some content leaves the customer network during self-hosted runs (as of 2026-09-28).** The worker sends Cursor file contents, terminal output, diffs, screenshots, local MCP results, and routing metadata, and uploads artifacts to Cursor-managed storage. The full checkout, build cache, and machine-local credentials stay on the machine ([Cursor docs](https://cursor.com/docs/cloud-agent/self-hosted)). Cursor's March 2026 launch post describes code and tool execution as staying entirely in the customer network ([Cursor blog](https://cursor.com/blog/self-hosted-cloud-agents)). The current docs are more specific, and this file follows the docs.
- **No on-premises deployment of Cursor itself (as of 2026-09-28).** Cursor states it doesn't offer on-premises deployment ([Cursor Enterprise](https://cursor.com/enterprise)).
- **Self-hosted Team Pools are Enterprise-only (as of 2026-09-28).** Team Pools are for Enterprise teams ([Cursor docs](https://cursor.com/docs/cloud-agent/self-hosted/pool)), so Agent Relay for Cursor assumes a Cursor Enterprise plan. This is inferred from Cursor's docs, not stated in Coder's.

## Common Questions

- **Does Coder replace Cursor?** No. Cursor provides the developer experience, orchestration, and inference, and Coder provides the workspaces where Cursor agents execute ([Agent Relay for Cursor FAQ](../products/coder-agent-relay/cursor-faq.md), [Coder docs](https://coder.com/docs/ai-coder/agent-relay/cursor)).
- **Can developers use the Cursor IDE with Coder today?** Yes. Cursor connects to Coder workspaces through the Coder extension, and admins can add a Cursor module to templates ([Coder docs](https://coder.com/docs/user-guides/workspace-access/cursor)).
- **Is Agent Relay for Cursor generally available?** No. It's in early access and closed preview with select customers ([Coder docs](https://coder.com/docs/ai-coder/agent-relay/cursor)).
- **Does Cursor become fully self-hosted with Coder?** No. The execution environment is self-hosted, while Cursor's orchestration and inference remain cloud-hosted ([Coder docs](https://coder.com/docs/ai-coder/agent-relay/cursor)).
- **Does Coder AI Gateway sit in Cursor's inference path?** No. Coder doesn't proxy or observe Cursor's model inference in the Agent Relay integration ([Coder docs](https://coder.com/docs/ai-coder/agent-relay/cursor)).
- **Cursor already supports self-hosted workers. Why add Coder?** Cursor's reference architectures leave the worker image, infrastructure, secrets, scaling, and validation to the customer ([Cursor docs](https://cursor.com/docs/cloud-agent/self-hosted/integrations)). Coder provides that as a platform with templates, ephemeral per-session workspaces, RBAC, Agent Firewall, and audit logging ([Coder blog](https://coder.com/blog/introducing-agent-relay-cloud-hosted-agents-self-hosted-execution)).
- **Do we need Coder if Cursor-hosted Cloud Agents meet our requirements?** Probably not for execution alone. Cursor states its hosted agents are sufficient for over 80% of its customers and that self-hosting is usually driven by compliance or security policy ([Cursor docs](https://cursor.com/docs/cloud-agent/choose-runtime)). Coder is relevant when execution must happen on infrastructure the organization controls, or when the organization wants one governed platform for Cursor and other agents.
- **Can we run Cursor, Coder Agents, and other agents at the same time?** Yes. Coder is agent-agnostic and supports multiple agent experiences on the same workspaces ([Agent Relay for Cursor FAQ](../products/coder-agent-relay/cursor-faq.md)).

## Pricing and Packaging

- **Cursor.** Individual plans range from free (Hobby) to Pro, Pro+, and Ultra ([Cursor pricing](https://cursor.com/pricing)). Teams seats are $40 per user per month (Standard) or $120 per user per month (Premium, 5x usage), and Enterprise is custom ([Cursor docs](https://cursor.com/docs/account/teams/pricing)). Third-party model requests on Teams and Enterprise add a Cursor Token Rate of $0.25 per million tokens on top of model API pricing ([Cursor docs](https://cursor.com/docs/models-and-pricing)). Cursor changed its pricing several times in 2026, so check the live page.
- **Coder.** Coder offers a free Community edition and a quote-based Premium edition ([coder.com/pricing](https://coder.com/pricing)). The pricing page also references an AI Premium tier that removes the five-concurrent-agent cap on Coder Agents ([coder.com/pricing](https://coder.com/pricing)). AI Governance (AI Gateway and Agent Firewall) is included with a Premium license, not sold as a separate add-on ([AI Governance message house](../products/coder-ai-governance/message-house.md), [Packaging](../company/packaging.md)).
- **Agent Relay.** No public pricing. Access is through the Coder account team during preview ([Coder docs](https://coder.com/docs/ai-coder/agent-relay/cursor)).
- **Combined cost.** A customer using Cursor Cloud Agents on Coder pays for a Cursor plan, including model usage, and a Coder license, plus the compute that runs Coder workspaces. This is inferred from the architecture, not a published bundle.

## Sources

- **[Cursor Docs: Self-Hosted Machines](https://cursor.com/docs/cloud-agent/self-hosted).** Primary. Execution split, data sent to Cursor, when to self-host. Accessed 2026-09-28.
- **[Cursor Docs: Self-Hosted Agents (Team Pools)](https://cursor.com/docs/cloud-agent/self-hosted/pool).** Primary. Pools are Enterprise-only, agent loop stays in Cursor's cloud, outbound-only workers. Accessed 2026-09-28.
- **[Cursor Docs: Integrations](https://cursor.com/docs/cloud-agent/self-hosted/integrations).** Primary. Coder listed as a partner, customer owns worker infrastructure. Accessed 2026-09-28.
- **[Cursor Docs: Choose where Cloud Agents run](https://cursor.com/docs/cloud-agent/choose-runtime).** Primary. Hosted VMs, My Machines limits, 80% sufficiency statement. Accessed 2026-09-28.
- **[Cursor Blog: Run cloud agents in your own infrastructure](https://cursor.com/blog/self-hosted-cloud-agents).** Primary. March 2026 launch of self-hosted cloud agents. Accessed 2026-09-28.
- **[Cursor Docs: Welcome](https://docs.cursor.com/welcome).** Primary. Product description. Accessed 2026-09-28.
- **[Cursor Docs: Enterprise](https://cursor.com/docs/enterprise).** Primary. Enterprise controls. Accessed 2026-09-28.
- **[Cursor Docs: Privacy and Data Governance](https://cursor.com/docs/enterprise/privacy-and-data-governance).** Primary. Data flows to model providers. Accessed 2026-09-28.
- **[Cursor Help: Privacy and data](https://cursor.com/help/security-and-privacy/privacy).** Primary. Enterprise-only controls, CMEK. Accessed 2026-09-28.
- **[Cursor Security](https://cursor.com/security).** Primary. Certifications. Accessed 2026-09-28.
- **[Cursor Enterprise](https://cursor.com/enterprise).** Primary. AWS hosting, no on-premises deployment. Accessed 2026-09-28.
- **[Cursor Pricing](https://cursor.com/pricing), [Team Pricing](https://cursor.com/docs/account/teams/pricing), [Models and Pricing](https://cursor.com/docs/models-and-pricing).** Primary. Plans, seat prices, Cursor Token Rate. Accessed 2026-09-28.
- **[Techzine: SpaceX completes acquisition of Cursor](https://www.techzine.eu/news/devops/143619/spacex-completes-acquisition-of-cursor/).** Secondary. Acquisition completion, August 2026. Accessed 2026-09-28.
- **[Wikipedia: Cursor (company)](https://en.wikipedia.org/wiki/Cursor_(company)).** Secondary. Subsidiary status, product surfaces. Accessed 2026-09-28.
- **[Coder Docs: Agent Relay](https://coder.com/docs/ai-coder/agent-relay) and [Agent Relay for Cursor](https://coder.com/docs/ai-coder/agent-relay/cursor).** Primary. Architecture, preview status, inference not proxied. Accessed 2026-09-28.
- **[Coder Blog: Introducing Agent Relay](https://coder.com/blog/introducing-agent-relay-cloud-hosted-agents-self-hosted-execution).** Primary. Governance applied automatically, Claude Code integration. Accessed 2026-09-28.
- **[Coder Docs: Cursor workspace access](https://coder.com/docs/user-guides/workspace-access/cursor).** Primary. IDE connection. Accessed 2026-09-28.
- **[Coder Registry: Cursor CLI module](https://registry.coder.com/modules/coder-labs/cursor-cli).** Primary. CLI in workspaces. Accessed 2026-09-28.
- **[Coder Blog: MCP tooling for Cursor](https://coder.com/blog/ship-fast-and-consistent-mcp-tooling-for-cursor).** Primary. MCP config in templates. Accessed 2026-09-28.
- **[Coder Docs: Air-gapped deployments](https://coder.com/docs/install/airgap).** Primary. Air-gapped support. Accessed 2026-09-28.
- **[Coder Docs: AI Governance](https://coder.com/docs/ai-coder/ai-governance) and [AI Governance Cost Control](https://coder.com/docs/ai-coder/ai-gateway/cost-controls).** Primary. AI Governance features. Accessed 2026-09-28.
- **[coder.com/pricing](https://coder.com/pricing).** Primary. Editions and AI Premium. Accessed 2026-09-28.
- **[coder/coder README](https://github.com/coder/coder).** Primary. Platform architecture, Coder Agents. Accessed 2026-09-28.
- **Repository files: [Agent Relay for Cursor FAQ](../products/coder-agent-relay/cursor-faq.md), [Agent Relay message house](../products/coder-agent-relay/message-house.md), [Why Coder](../company/why-coder.md), [Message house](../company/message-house.md), [AI Governance message house](../products/coder-ai-governance/message-house.md), [Packaging](../company/packaging.md).** Primary. Coder positioning. Accessed 2026-09-28.
