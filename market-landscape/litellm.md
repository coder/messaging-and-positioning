# Coder and LiteLLM

| Field | Value |
|---|---|
| Date generated | 2026-09-28 |
| Category | Competitive |

*(LiteLLM is developed by BerriAI. The GitHub repository is [BerriAI/litellm](https://github.com/BerriAI/litellm). This comparison is competitive at the AI Gateway layer only. LiteLLM does not compete with the broader Coder platform.)*

## One-Line Positioning

LiteLLM is a standalone LLM gateway that competes with Coder's AI Gateway. It does not compete with the Coder platform, which ties every model request to a developer, a workspace, and an agent session, and governs the environments where that work runs.

## Strategic Themes and Patterns

- **Relationship.** Competitive at the AI Gateway layer, not at the platform level. LiteLLM describes itself as a [self-hosted gateway for platform teams managing LLM access across an organization](https://docs.litellm.ai/docs/), which is the same job Coder's [AI Gateway](https://coder.com/docs/ai-coder/ai-gateway) does for coding agents and IDEs. LiteLLM does not provide development environments, workspace templates, or process-level network enforcement, so it has no equivalent to Coder Workspaces or Agent Firewall. The two can also be stacked. Coder's docs describe pointing AI Gateway's OpenAI base URL [at a LiteLLM deployment](https://coder.com/docs/ai-coder/ai-gateway/setup).
- **Platform context.** A standalone gateway sees API traffic. Coder's AI Gateway runs inside the platform where development happens. Requests are [attributed back to a user](https://coder.com/docs/ai-coder/ai-gateway), spend is attributed [down to the workspace](../products/coder-ai-governance/message-house.md), and activity is organized into [interceptions, threads, and sessions](../products/coder-ai-governance/message-house.md) that line up with Agent Firewall's network decisions. This context comes from the platform, so a standalone gateway can't add it by adding gateway features.
- **Choice, Control, Consistency.** Choosing LiteLLM instead of Coder costs nothing on Choice. LiteLLM is model-agnostic and [MIT-licensed](https://www.litellm.ai/). The tradeoffs are on Control and Consistency. LiteLLM's documented controls apply to traffic that passes through the gateway ([docs](https://docs.litellm.ai/docs/)). It doesn't govern where agents run, what they can reach on the network outside the gateway, or how their environments are provisioned (inferred from the scope of its documentation). Coder covers those through [self-hosted workspaces defined as code](https://coder.com/pricing) and [Agent Firewall](https://coder.com/docs/ai-coder/agent-firewall).
- **Lock-in risk.** LiteLLM itself carries little lock-in risk. It is open source, and any client that works with OpenAI [works with the proxy with no code changes](https://docs.litellm.ai/docs/). The harder-to-reverse decision is architectural. An organization that treats a standalone model gateway as its whole AI governance layer still has to build execution isolation, network policy, and environment standardization separately, and those choices get harder to change once agents are running in production.
- **Build versus buy.** LiteLLM is a building block, not a complete answer to governing coding agents. Teams that use it as their gateway still build the rest themselves: provisioning isolated environments, enforcing egress policy on agent processes, and connecting model activity to developer and workspace identity. That matches [Why Coder](../company/why-coder.md), which says building self-hosted development infrastructure with this depth of governance is realistic for only a small number of organizations.
- **Where LiteLLM is sufficient on its own.** An organization that needs one OpenAI-compatible endpoint, spend tracking, and budgets across many applications, and that isn't asking to govern where coding agents run, may find LiteLLM OSS enough. LiteLLM says OSS already includes [virtual keys, spend tracking, budgets, fallbacks, and request/response logging](https://docs.litellm.ai/docs/enterprise).

## Coder's Strengths Here

- **Gateway activity tied to developer and workspace identity.** Users authenticate to AI Gateway with their [Coder session or API tokens](https://coder.com/docs/ai-coder/ai-gateway), so provider keys [aren't distributed to individual users](https://coder.com/docs/ai-coder/ai-gateway/auth). Every interaction is [attributed back to a user](https://coder.com/docs/ai-coder/ai-gateway), and spend can be attributed [to the workspace](../products/coder-ai-governance/message-house.md).
- **Governs execution, not only model traffic.** Agent Firewall is a [process-level firewall that restricts and audits what AI agents can access](https://coder.com/docs/ai-coder/security) inside Coder workspaces. It enforces [HTTP method, domain, and path rules](https://coder.com/docs/ai-coder/agent-firewall/rules-engine). A standalone gateway doesn't cover this.
- **Model and network activity in one view.** AI Gateway records [the last user prompt, token usage, model reasoning, and every tool invocation](https://coder.com/docs/ai-coder/ai-gateway/monitoring) for each intercepted request. Agent Firewall's network decisions show up in the same session view ([AI Governance message house](../products/coder-ai-governance/message-house.md)).
- **Part of the environment platform.** Platform teams [define environments as code so every developer and agent starts from the same baseline](https://coder.com/pricing), and can preconfigure AI tools inside workspaces to [route through AI Gateway](https://coder.com/docs/ai-coder/ai-gateway/clients).
- **Works with an existing LiteLLM deployment.** AI Gateway's OpenAI-compatible upstream [can point at a LiteLLM deployment](https://coder.com/docs/ai-coder/ai-gateway/setup), so adopting Coder doesn't require removing LiteLLM.

## LiteLLM Overview

- **What it is.** An open-source Python SDK and AI Gateway (proxy server) that gives a [unified interface to 100+ LLMs](https://github.com/BerriAI/litellm). LiteLLM's homepage cites [140+ providers](https://www.litellm.ai/). It also positions itself as a single gateway for [LLMs, A2A agents, and MCP tools](https://docs.litellm.ai/docs/).
- **Architecture.** A [self-hosted OpenAI-compatible gateway](https://docs.litellm.ai/docs/) with a [Rust core and Python SDK](https://github.com/BerriAI/litellm). It runs on the customer's [own Postgres and Redis](https://www.litellm.ai/). It also serves the [Anthropic Messages API format on /v1/messages](https://docs.litellm.ai/docs/tutorials/claude_non_anthropic_models), which lets Claude Code use it.
- **Target customer.** Platform teams managing LLM access across an organization ([docs](https://docs.litellm.ai/docs/)). LiteLLM positions Enterprise for teams with [100+ users or 10+ production AI use cases](https://docs.litellm.ai/docs/enterprise).
- **Deployment model.** Self-hosted. Deployment options include a [Helm chart, Terraform module, and Docker images](https://www.litellm.ai/). LiteLLM states that [data and keys never leave your own infrastructure](https://www.litellm.ai/pricing). Air-gapped deployment is listed on the [Enterprise Standard and SCALE plans](https://www.litellm.ai/pricing).

## Coder Overview for This Comparison

- **AI Gateway.** An intermediary [between users' coding agents or IDEs and providers like OpenAI and Anthropic](https://coder.com/docs/ai-coder/ai-gateway). It supports clients [inside or outside Coder workspaces](https://coder.com/docs/ai-coder/ai-gateway), runs [inside coderd or as a standalone service](https://coder.com/docs/ai-coder/ai-gateway/standalone), and [stops a user's requests once their spend reaches their budget](https://coder.com/docs/ai-coder/ai-gateway/cost-controls).
- **Agent Firewall.** A [process-level firewall](https://coder.com/docs/ai-coder/security) that isolates agent processes using [nsjail or landjail](https://coder.com/docs/reference/cli/agent-firewall).
- **Coder Workspaces.** Self-hosted environments that platform teams [define as code](https://coder.com/pricing), where developers and agents run instead of on laptops ([Coder Message House](../company/message-house.md)).
- **Packaging.** AI Gateway and Agent Firewall make up AI Governance, which is included with a Premium license, not sold as a separate add-on ([AI Governance message house](../products/coder-ai-governance/message-house.md), [Packaging](../company/packaging.md)). [Community deployments cannot access AI Gateway](https://coder.com/docs/ai-coder/ai-gateway/standalone).

## Where LiteLLM Is Strong or Coder Has a Gap

- **Gateway feature depth.** As a standalone gateway, LiteLLM has a broader gateway feature set than Coder's AI Gateway today. The points below are specific.
- **Broader provider and endpoint coverage.** LiteLLM cites [140+ providers](https://www.litellm.ai/) and covers embeddings, image generation, and other endpoints ([docs](https://docs.litellm.ai/docs/)). Coder's AI Gateway supports a narrower set of named providers plus any OpenAI-compatible endpoint ([AI Governance message house](../products/coder-ai-governance/message-house.md)).
- **Routing and load balancing.** LiteLLM offers [load balancing across providers, regions, and keys](https://www.litellm.ai/), [automatic fallbacks](https://docs.litellm.ai/docs/), and [traffic mirroring](https://docs.litellm.ai/docs/simple_proxy). Coder documents [key-pool failover across up to five keys per provider](../products/coder-ai-governance/message-house.md). It doesn't document cross-provider routing.
- **Key and tenant management.** LiteLLM Enterprise lists a [multi-tenant hierarchy of organizations, teams, projects, and keys](https://docs.litellm.ai/docs/enterprise), [automated virtual-key rotation](https://docs.litellm.ai/docs/enterprise), [tag-based budgets, and model-specific budgets per virtual key](https://docs.litellm.ai/docs/enterprise). Coder's public AI Gateway docs don't describe equivalent team-level or per-key controls. Coder's controls are per-user and per-group budgets ([docs](https://coder.com/docs/ai-coder/ai-gateway/cost-controls)).
- **Secret manager integrations.** LiteLLM can read and write secrets using [Azure Key Vault, Google Secret Manager, HashiCorp Vault, CyberArk Conjur, and AWS Secrets Manager](https://docs.litellm.ai/docs/secret). Coder's public AI Gateway docs don't describe native secret manager integrations.
- **Guardrails and payload logging.** LiteLLM includes [custom guardrails and Presidio PII masking](https://docs.litellm.ai/docs/enterprise), with built-in moderation callbacks requiring a license. OSS also includes [request/response logging](https://docs.litellm.ai/docs/enterprise). Coder's AI Gateway records [the last user prompt, reasoning, and tool invocations](https://coder.com/docs/ai-coder/ai-gateway/monitoring), not full request and response payloads. Coder doesn't position AI Governance as content-level prompt filtering ([AI Governance message house](../products/coder-ai-governance/message-house.md)).
- **Not limited to coding tools.** LiteLLM serves any application through its SDK and proxy, and it also offers an [A2A agent gateway](https://docs.litellm.ai/docs/a2a). Coder's AI Gateway is built for [coding agents and IDEs](https://coder.com/docs/ai-coder/ai-gateway).
- **Free open-source tier.** LiteLLM OSS can be self-hosted [with no license fee](https://www.litellm.ai/pricing). Coder's AI Gateway requires a [Premium license](https://coder.com/docs/ai-coder/ai-gateway/standalone).
- **Compliance attestations.** LiteLLM lists [SOC 2 Type 2 and ISO 27001](https://www.litellm.ai/enterprise) on its Enterprise page.

## Known Limitations in LiteLLM's Approach

- **No platform context (as of 2026-09-28).** LiteLLM's documentation covers LLM, MCP, and A2A traffic routed through the gateway ([docs](https://docs.litellm.ai/docs/)). It doesn't describe knowing which workspace or environment a request came from, controlling agent process execution, or controlling network egress that bypasses the gateway. This is inferred from the scope of the docs, not stated by LiteLLM.
- **Several governance controls require Enterprise (as of 2026-09-28).** SSO is [free for up to 5 users](https://docs.litellm.ai/docs/enterprise). Beyond that it requires an enterprise license. [Audit logs](https://docs.litellm.ai/docs/proxy/multiple_admins) of admin and entity changes also require an enterprise license.
- **Global budget enforcement depends on a database (as of 2026-09-28).** LiteLLM's quickstart notes that without a database client, a global [max_budget is not enforced](https://docs.litellm.ai/docs/proxy/docker_quick_start).

## Common Questions

- **Is Coder a LiteLLM replacement?** Only at the gateway layer. Coder's AI Gateway overlaps with LiteLLM's gateway, and LiteLLM has a deeper gateway feature set today (see above). The rest of Coder, including [self-hosted workspaces](https://coder.com/pricing) and [Agent Firewall](https://coder.com/docs/ai-coder/security), has no LiteLLM equivalent.
- **We already run LiteLLM. Do we need to replace it to use Coder?** No. AI Gateway's OpenAI base URL [can point at a LiteLLM deployment](https://coder.com/docs/ai-coder/ai-gateway/setup), so LiteLLM keeps handling upstream routing while AI Gateway adds Coder user attribution and session records ([docs](https://coder.com/docs/ai-coder/ai-gateway)). Coder's docs describe this only for the OpenAI-compatible path.
- **Why pay for AI Gateway when LiteLLM OSS is free?** If all you need is a proxy layer, LiteLLM is often enough. The difference shows up when you need to answer which developers, workspaces, and agent sessions generated a given request or spend. Coder's AI Gateway [attributes every interaction to a user](https://coder.com/docs/ai-coder/ai-gateway) and pairs model activity with Agent Firewall's network activity in the same session ([AI Governance message house](../products/coder-ai-governance/message-house.md)).
- **What does Coder add if LiteLLM already tracks spend and logs requests?** Coder adds control over where the agent runs and what it can reach. Agent Firewall [restricts and audits what AI agents can access](https://coder.com/docs/ai-coder/security) from inside the workspace. Workspaces are [defined as code](https://coder.com/pricing) so every agent starts from the same baseline.
- **Can LiteLLM govern Claude Code?** Yes, for model traffic. LiteLLM documents [calling Claude models through its proxy from Claude Code](https://docs.litellm.ai/docs/tutorials/claude_responses_api), with centralized authentication and cost controls. Coder's AI Gateway also supports Claude Code ([AI Governance message house](../products/coder-ai-governance/message-house.md)).
- **Are both self-hosted?** Yes. LiteLLM is [self-hosted](https://docs.litellm.ai/docs/), and so is Coder, including [air-gapped networks](https://aws.amazon.com/marketplace/pp/prodview-laypqph2nuvaq).
- **Is Coder's AI Gateway free?** No. It requires a [Premium license](https://coder.com/docs/ai-coder/ai-gateway/standalone), and [Community deployments cannot access it](https://coder.com/docs/ai-coder/ai-gateway/standalone).

## When LiteLLM Alone Is Enough

- **Application teams building LLM features.** Teams that need one endpoint across many providers for their own applications, rather than governance for coding agents, are the use case LiteLLM's [SDK and proxy](https://github.com/BerriAI/litellm) are built for.
- **Organizations that only need model access control and spend tracking.** If the requirement is [virtual keys, budgets, and request logging](https://docs.litellm.ai/docs/enterprise), and developers and agents don't need governed execution environments, LiteLLM OSS covers it.
- **Teams that need advanced routing today.** If load balancing strategies, fallback chains, or tag-based controls are the primary requirement, LiteLLM's [routing features](https://www.litellm.ai/) go further than Coder's AI Gateway does today.
- **Teams not yet running coding agents with access to sensitive systems.** Without agents executing code against internal networks, process-level network enforcement and standardized environments matter less.

## Pricing and Packaging

- **LiteLLM.** The open-source gateway is [free to self-host](https://www.litellm.ai/pricing). Enterprise is [sized to annual gateway request capacity, deployment architecture, and support needs, never per token](https://www.litellm.ai/pricing), and requires a sales quote. A [30-day trial](https://www.litellm.ai/pricing) is available, and procurement is available through [AWS and Azure Marketplace](https://docs.litellm.ai/docs/enterprise). Enterprise prices are not public.
- **Coder.** AI Gateway and Agent Firewall require [Premium](https://coder.com/docs/ai-coder/ai-gateway/standalone). AI Premium [removes the concurrent-agent cap](https://coder.com/pricing) for Coder Agents. See [coder.com/pricing](https://coder.com/pricing) for current tiers, and [Packaging](../company/packaging.md) for the narrative behind them.

## Sources

- **[LiteLLM homepage](https://www.litellm.ai/).** Primary. MIT license, provider count, self-hosting and air-gap claims, load balancing, budgets. Accessed 2026-09-28.
- **[LiteLLM pricing](https://www.litellm.ai/pricing).** Primary. OSS free tier, Enterprise pricing basis, trial, air-gapped plans. Accessed 2026-09-28.
- **[LiteLLM Enterprise page](https://www.litellm.ai/enterprise).** Primary. SOC 2 Type 2 and ISO 27001 claims. Accessed 2026-09-28.
- **[LiteLLM docs: Getting Started](https://docs.litellm.ai/docs/).** Primary. Gateway scope, OpenAI compatibility, LLM, MCP, and A2A positioning. Accessed 2026-09-28.
- **[LiteLLM docs: Enterprise](https://docs.litellm.ai/docs/enterprise).** Primary. OSS versus Enterprise features, SSO threshold, guardrails, multi-tenant hierarchy, key rotation, tag-based budgets, secret managers, marketplace procurement. Accessed 2026-09-28.
- **[LiteLLM docs: Secret Managers](https://docs.litellm.ai/docs/secret).** Primary. Supported secret managers. Accessed 2026-09-28.
- **[LiteLLM docs: Audit Logs](https://docs.litellm.ai/docs/proxy/multiple_admins).** Primary. Audit logs require an Enterprise license. Accessed 2026-09-28.
- **[LiteLLM docs: Quickstart](https://docs.litellm.ai/docs/proxy/docker_quick_start).** Primary. Global budget behavior without a database. Accessed 2026-09-28.
- **[LiteLLM docs: AI Gateway (LLM Proxy)](https://docs.litellm.ai/docs/simple_proxy).** Primary. Traffic mirroring and per-key budgets. Accessed 2026-09-28.
- **[LiteLLM docs: A2A Agent Gateway](https://docs.litellm.ai/docs/a2a).** Primary. Agent gateway capability. Accessed 2026-09-28.
- **[LiteLLM docs: Claude Code Quickstart](https://docs.litellm.ai/docs/tutorials/claude_responses_api) and [non-Anthropic models](https://docs.litellm.ai/docs/tutorials/claude_non_anthropic_models).** Primary. Claude Code support and the Anthropic Messages endpoint. Accessed 2026-09-28.
- **[BerriAI/litellm on GitHub](https://github.com/BerriAI/litellm).** Primary. SDK and proxy description, Rust core, 100+ LLMs. Accessed 2026-09-28.
- **[Coder docs: AI Gateway](https://coder.com/docs/ai-coder/ai-gateway).** Primary. Authentication, attribution, deployment options. Accessed 2026-09-28.
- **[Coder docs: AI Gateway Monitoring](https://coder.com/docs/ai-coder/ai-gateway/monitoring).** Primary. What AI Gateway records per request. Accessed 2026-09-28.
- **[Coder docs: AI Gateway Setup](https://coder.com/docs/ai-coder/ai-gateway/setup).** Primary. Pointing the OpenAI base URL at a LiteLLM deployment. Accessed 2026-09-28.
- **[Coder docs: AI Gateway Authentication](https://coder.com/docs/ai-coder/ai-gateway/auth).** Primary. Centralized provider credentials. Accessed 2026-09-28.
- **[Coder docs: AI Gateway Client Configuration](https://coder.com/docs/ai-coder/ai-gateway/clients).** Primary. Preconfiguring tools in workspaces. Accessed 2026-09-28.
- **[Coder docs: Standalone Deployment](https://coder.com/docs/ai-coder/ai-gateway/standalone).** Primary. Premium requirement, Community exclusion, standalone mode. Accessed 2026-09-28.
- **[Coder docs: Cost Control](https://coder.com/docs/ai-coder/ai-gateway/cost-controls).** Primary. Budget enforcement. Accessed 2026-09-28.
- **[Coder docs: Security and Agent Firewall](https://coder.com/docs/ai-coder/security), [Rules Engine](https://coder.com/docs/ai-coder/agent-firewall/rules-engine), [CLI reference](https://coder.com/docs/reference/cli/agent-firewall).** Primary. Agent Firewall behavior and jail types. Accessed 2026-09-28.
- **[Coder pricing](https://coder.com/pricing).** Primary. Environments as code, AI Premium agent cap. Accessed 2026-09-28.
- **[Coder Premium on AWS Marketplace](https://aws.amazon.com/marketplace/pp/prodview-laypqph2nuvaq).** Primary. Self-hosted and air-gapped deployment. Accessed 2026-09-28.
- **[AI Governance message house](../products/coder-ai-governance/message-house.md), [Why Coder](../company/why-coder.md), [Coder Message House](../company/message-house.md), [Packaging](../company/packaging.md).** Primary (this repository). Coder positioning, supported providers and clients, key-pool failover, workspace spend attribution, session structure, AI Governance packaging. Accessed 2026-09-28.
