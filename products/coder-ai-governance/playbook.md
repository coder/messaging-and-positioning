# Coder AI Governance Playbook

> A shared reference for understanding where AI Governance fits, how it works, and how to support organizations evaluating or adopting it.

For positioning, messaging, and value propositions, see the [AI Governance message house](./message-house.md). AI Governance doesn't have an FAQ yet, so common questions are collected in [section 8](#8-common-questions).

---

## 1. Quick Reference

| | |
|---|---|
| **The product** | AI Governance is Coder's governance layer for AI coding tools and agents. AI Gateway centralizes model access, audit, and spend controls, and Agent Firewall restricts what agent processes can reach from inside a workspace. |
| **Best fit** | Enterprises whose developers already use AI coding agents and that need audit, approved models, and spend limits without banning the tools. |
| **Common signal** | "Developers are using Claude Code and Codex with their own API keys, and we can't see what the agents are doing." |
| **Key question** | "If an agent did something it shouldn't, could you reconstruct who prompted it, what it ran, and what it reached?" |
| **Core value** | Developers keep the agents and models they prefer. Platform and security teams get one place to approve models, attribute every request to a user, cap spend, and limit what agents can reach. |
| **Important limitation** | AI Gateway governs only the clients routed through it, and some popular tools, including Cursor, aren't supported clients today. It records, attributes, and limits AI usage, but doesn't inspect or block prompt content. |
| **Status** | Generally available since Coder v2.30 (February 2026). |
| **Journey stage** | Modernize. See the [customer journey](../../company/customer-journey.md). |
| **Next step** | Start a self-serve [Premium trial](https://coder.com/trial), [set up AI Gateway](https://coder.com/docs/ai-coder/ai-gateway/setup), and route one agent, such as Claude Code, through it. |

---

## 2. Overview

AI Governance is included in Coder Premium and is made up of two products. [AI Gateway](https://coder.com/docs/ai-coder/ai-gateway) sits between AI coding tools and model providers. It authenticates users with their Coder identity, holds provider keys centrally, records prompts, tool calls, and token usage, and enforces spend budgets. [Agent Firewall](https://coder.com/docs/ai-coder/agent-firewall) wraps agent processes inside a workspace and limits them to an allowlist of domains, HTTP methods, and paths, logging every decision.

Most enterprises already have developers using AI agents, often on laptops, with personal API keys and no central record of what those agents did. Blocking the tools slows teams down and pushes usage into the shadows. AI Governance lets organizations allow the tools while governing model access and the environment the tools run in.

The difference from a standalone AI gateway is context. Because AI Gateway is part of the platform where development happens, every request is tied to a user, a workspace, and a session, and Coder also governs where agents run. See the message house's [3 Whys](./message-house.md#the-3-whys) and [Competitive Position](./message-house.md#competitive-position).

---

## 3. How It Works

### Architecture summary

AI clients point their model base URL at Coder and authenticate with a Coder session or API token. AI Gateway forwards each request to the configured provider using centrally managed keys, or the user's own key if bring-your-own-key (BYOK) is allowed, and records the request. For clients that can't change their base URL but respect proxy settings, [AI Gateway Proxy](https://coder.com/docs/ai-coder/ai-gateway/ai-gateway-proxy) intercepts traffic to enabled providers and forwards it to AI Gateway. Inside a workspace, Agent Firewall runs the agent process in a jail that sends its network traffic through a policy proxy, allowing only what the allowlist permits.

### Components and responsibilities

| Component | Responsibility |
|---|---|
| AI Gateway | Authenticates users, holds provider keys, records prompts, reasoning, tool calls, and token usage, and enforces per-user and per-group budgets |
| AI Gateway Proxy | Brings clients that can't override their base URL, such as GitHub Copilot, under AI Gateway |
| Agent Firewall | Restricts agent processes in a workspace to allowlisted domains, methods, and paths, and logs each allow or deny decision to the control plane |
| Coder Agents MCP management | Defines approved MCP servers and tools, with group and user access controls |
| Coder Workspaces | The self-hosted environment where developers and agents run, with network policy defined in the template |
| Platform team | Configures providers, budgets, retention, templates, allowlists, and workspace network policy |

### Typical workflow

**Platform team**

1. **Connect providers.** Enable AI Gateway, add provider keys centrally in **AI settings > Providers**, and decide whether to allow BYOK.
2. **Preconfigure tools.** Inject the AI Gateway base URL and the user's session token into workspace templates, so tools such as Claude Code route through AI Gateway with no setup by developers.
3. **Set limits.** Set group budgets, adjust data retention, and add Agent Firewall with a tightened allowlist to agent templates.
4. **Observe.** Review usage and spend, and send metrics to existing monitoring.

**Developer**

1. **Work as usual.** Use Claude Code, Codex, or another supported tool, with no provider API key to manage.
2. **Stay within budget.** Get notified at 85% and 100% of budget.

**Security team**

1. **Investigate.** Open a session to see the prompt, the model's reasoning, each tool call, and the related Agent Firewall decisions, attributed to a user.
2. **Report.** Use spend reports and metrics for audit and chargeback.

### Deployment model

AI Governance runs in the customer's self-hosted Coder deployment, in a cloud VPC, on-premises, or air-gapped with a self-hosted model endpoint. AI Gateway runs inside the Coder control plane by default, or as a [standalone service](https://coder.com/docs/ai-coder/ai-gateway/standalone) that scales separately. It supports clients [inside or outside workspaces](https://coder.com/docs/ai-coder/ai-gateway/clients#external-and-desktop-clients). Agent Firewall applies inside workspaces.

### Data and trust boundaries

Prompts and code context go to whichever provider the platform team configures. AI Gateway [stores](https://coder.com/docs/ai-coder/ai-gateway/audit#what-we-store) the last user prompt, token usage, tool call requests, and model reasoning inside the customer's Coder deployment. It discards model-generated text and doesn't store tool results. Data is kept for 60 days by default, and [retention is configurable](https://coder.com/docs/ai-coder/ai-gateway/setup#data-retention). Agent Firewall decisions are emitted as structured logs from the Coder server.

---

## 4. Boundaries and Terminology

See the message house's [Governance Scope](./message-house.md#governance-scope) for more.

### What the product does not do

- Govern AI clients that aren't routed through it. Cursor, Devin Desktop (formerly Windsurf), Kiro, Amp, Gemini CLI, and Antigravity can't be routed through AI Gateway today. For Cursor, fixing its open custom-endpoint bug wouldn't close the gap on its own: Cursor routes custom-endpoint traffic through its own servers, and Tab completion and Cursor's own models never use a custom endpoint. See the [compatibility table](https://coder.com/docs/ai-coder/ai-gateway/clients#compatibility).
- Inspect, redact, or block prompt content, as a DLP or guardrails product does. A policy engine is under active investigation.
- Store full model responses or tool results.
- Tell with certainty whether a request came from a human or an agent.
- Restrict agents that aren't launched through Agent Firewall. It applies to the processes it's configured to run.
- Integrate natively with specific SIEM platforms. Prometheus, OpenTelemetry, and structured logs are the supported path today.
- Replace a corporate secure web gateway, EDR, or DLP stack. AI Governance is one layer of a broader security posture.

### Recommended terminology

| Preferred | Avoid | Why |
|---|---|---|
| "AI Governance, included in Premium" | "The AI Governance add-on" | It's part of Premium, not a separate purchase. |
| "AI Gateway" and "Agent Firewall" | "AI Bridge" and "Agent Boundaries" | Those are the former names. |
| "Records prompts, tool calls, and token usage" | "Records everything the agent does" | Model output and tool results aren't stored. |
| "Limits what agents launched through Agent Firewall can reach" | "Controls all egress" | Coverage depends on which processes are wrapped and on the allowlist. |
| "Supported AI clients" | "Any AI tool" | Some clients can't be routed through AI Gateway. |

---

## 5. Fit

See the message house's [Target Market / ICP](./message-house.md#target-market--icp) for the full ideal customer profile.

### Use cases

AI Governance's primary use cases are secure execution for AI agents, audit and forensics, usage and cost control, protecting sensitive code and data, standardizing AI tooling, and managing agent workloads. See the message house's [Use Cases](./message-house.md#use-cases) and [Secure Development Environments](../../use-cases/secure-development-environments.md).

### Good-fit signals

- Developers use Claude Code, Codex, GitHub Copilot, or similar tools with personal API keys
- Security wants an audit trail of prompts and tool calls tied to named users
- Finance or engineering leadership asks who is spending what on AI
- Agents are moving from experiments to headless or production workflows
- The organization already runs Coder Workspaces, or is moving development off laptops
- Regulated industries that need audit data to stay on infrastructure they control
- The organization wants to approve, switch, or mix model providers, including self-hosted models

### Poor fit or another approach

- **The main AI tool can't be routed through AI Gateway.** If most usage is in Cursor, for example, model-level governance won't cover it. Cursor cloud agents can still run in governed workspaces through [Agent Relay](../coder-agent-relay/playbook.md).
- **The immediate need is prompt content inspection or DLP.** Pair Coder with a DLP tool for now. A policy engine is under active investigation.
- **The need is one model endpoint for many non-development applications.** A general-purpose gateway may be enough. See [Coder and LiteLLM](../../market-landscape/litellm.md).
- **The organization isn't using AI coding tools yet.** Start with Coder Workspaces and the Migrate stage.

### Discovery questions

- **Tools.** Which AI tools and agents do developers use today, and where do they run?
- **Keys.** How are model API keys issued, and could you revoke them all today?
- **Existing gateway.** Do you already run an AI gateway or proxy, and what does it cover?
- **Audit.** What would you need to reconstruct an agent incident, and how long must records be kept?
- **Monitoring.** Where should AI usage data go: Prometheus, OpenTelemetry, a log pipeline, or a SIEM?
- **Spend.** Who owns AI spend, and do you need limits by team or user?
- **Network.** What can workspaces and agents reach today, and who decides?
- **Privacy.** Will prompt logging need review by a works council or privacy team?

---

## 6. Audiences

See the message house's [Buyer Personas](./message-house.md#buyer-personas) for how each persona applies to AI Governance.

| Role | Cares most about | Useful framing |
|---|---|---|
| [CISO and security leaders](../../audiences/ciso.md) | Audit, attribution, and limiting what agents can reach | "Every prompt and tool call tied to a named user, and agents that can only reach what you allow." |
| [Platform engineers](../../audiences/platform-engineer.md) | Providing AI tools without distributing keys or configuring each tool by hand | "Configure providers once, and every template routes AI through the gateway." |
| [Developers](../../audiences/developer.md) | Keeping their preferred tools without managing keys | "Use the agents you like, with nothing to set up." |
| [CTO](../../audiences/cto.md) and [CIO](../../audiences/cio.md) | Scaling AI adoption with visibility into usage and spend | "Allow AI tools instead of banning them, and see what they cost and who uses them." |

---

## 7. Alternatives and Related Products

See the message house's [Competitive Position](./message-house.md#competitive-position) for the full narrative.

- **Standalone AI gateways, such as LiteLLM, Kong, Portkey, and Tetrate.** They govern model traffic routed through them. Coder governs model access and where agents run, and AI Gateway can route through an existing gateway. See [Coder and LiteLLM](../../market-landscape/litellm.md).
- **Corporate proxies and secure web gateways.** They see network traffic, but not the Coder user, workspace, or agent session behind it. They complement AI Governance.
- **Agent sandboxes.** Isolation alone doesn't provide model access control, attribution, or organization-wide policy. See [Coder and NVIDIA OpenShell](../../market-landscape/nvidia-openshell.md).
- **Admin controls built into AI tools.** Each covers its own tool. AI Gateway gives one audit trail and one set of budgets across supported tools.
- **Building in-house.** Teams would need a gateway, identity integration, environment isolation, and network policy. See [Why Coder](../../company/why-coder.md).
- **Coder Agents and Agent Relay.** Coder Agents routes all model traffic through AI Gateway automatically. Agent Relay runs Cursor and Claude Code cloud agents in governed workspaces. See the [Coder Agents playbook](../coder-agents/playbook.md) and [Agent Relay playbook](../coder-agent-relay/playbook.md).

---

## 8. Common Questions

### "We already have an AI gateway. Why do we need this?"

A gateway governs the model call: approved models, logs, and spend for traffic routed through it. It doesn't govern what an agent does with the response, such as the commands it runs, the code and credentials it can read, or the network calls it makes outside the gateway. Coder governs the environment where agents run, and AI Gateway ties each request to a user, workspace, and session. Customers don't have to remove their gateway: AI Gateway can route through an existing OpenAI-compatible gateway such as LiteLLM.

> Useful follow-up: "What can your agents reach today that doesn't go through the gateway?"

### "Logging isn't enough. Can we block risky prompts or actions?"

AI Governance enforces limits in several places today: approved providers, with BYOK optionally disabled; per-user and per-group budgets enforced before requests reach the provider; approved MCP servers and tools for Coder Agents; Agent Firewall allowlists; and workspace network policy. It doesn't inspect or block prompt content. A policy engine is under active investigation. Customers who want to help shape it should raise it with their customer success team, who will work with the product manager on next steps.

> Useful follow-up: "Which specific actions or content would you need to block?"

### "Does it cover AI tools outside Coder workspaces?"

Yes, for supported clients. Tools on laptops or desktops can use AI Gateway with a Coder API token, through a base URL or AI Gateway Proxy. Workspace controls and Agent Firewall apply only inside workspaces.

> Useful follow-up: "How much AI usage happens outside development environments today?"

### "Does it work with Cursor and GitHub Copilot?"

GitHub Copilot works through AI Gateway Proxy. Cursor isn't a supported AI Gateway client today. Its custom-endpoint mode sends request formats AI Gateway doesn't accept (an open Cursor bug), routes traffic through Cursor's servers, and doesn't cover Tab completion. Cursor cloud agents can run in governed Coder workspaces through Agent Relay, where workspace controls apply. See the [compatibility table](https://coder.com/docs/ai-coder/ai-gateway/clients#compatibility).

> Useful follow-up: "Which tools account for most of your AI usage?"

### "Can we send this data to our SIEM?"

Metrics and traces export to Prometheus, Grafana, and OpenTelemetry, and structured records can feed existing log pipelines. Native integrations with specific SIEM platforms are on the roadmap.

> Useful follow-up: "Which SIEM do you use, and which events matter most?"

### "Isn't logging prompts a form of employee monitoring?"

AI Gateway stores the last user prompt, tool call requests, token usage, and model reasoning, not model output. The data stays in the customer's deployment, and retention is configurable. Organizations with works councils or strict privacy rules should involve them early and settle retention and access as part of the rollout.

> Useful follow-up: "Who needs to approve AI usage logging in your organization?"

### "Our corporate proxy already controls egress. Why add Agent Firewall?"

A corporate proxy sees traffic, but not which Coder user, workspace, or agent session produced it. Agent Firewall applies per-agent allowlists inside the workspace and correlates each decision with the AI Gateway session. The two work together.

> Useful follow-up: "Do you need different rules for agents than for developers?"

### "We're not running agents in production yet."

Developers usually already use AI tools, often with personal keys. Starting with AI Gateway gives visibility and spend control now, and puts guardrails in place before agents reach production. It's already included in Premium.

> Useful follow-up: "Which AI tools are developers using today, and how did they get access?"

### "Can we build this ourselves?"

A gateway is the easy part. Teams would also need identity integration, attribution to workspaces and sessions, isolated environments, and network policy, and then maintain them. See [Why Coder](../../company/why-coder.md).

> Useful follow-up: "Who would own and maintain it?"

### "Do we need to buy AI Governance separately?"

No. AI Governance is included in Premium. Community deployments can't use it. See [Packaging](../../company/packaging.md).

---

## 9. Evaluation and Demo

### Evaluation stages

| Stage | Goals | Typically involved |
|---|---|---|
| Initial exploration | Map current AI tools, key management, and gaps in audit and spend visibility | Platform and security leads |
| Technical evaluation | Enable AI Gateway, route supported tools through it, and set budgets | Platform engineers, developers |
| Security and architecture review | Stored data and retention, Agent Firewall allowlists, workspace network policy, and monitoring integration | Security, compliance, privacy |
| Production planning | Provider strategy, BYOK policy, budgets by group, template rollout, and coexistence with any existing gateway | Platform engineering, engineering leadership |

### Pilot setup

- A Coder deployment on v2.30 or later, with a Premium or trial license
- AI Gateway enabled with at least one provider key
- Workspace templates that inject the AI Gateway base URL and session token
- A pilot group using a supported tool, such as Claude Code or Codex
- Agent Firewall on at least one agent template, with an allowlist tightened for the pilot
- Group budgets for the pilot group
- Named stakeholders from platform, security, and the developer group, with agreed success criteria and timeline

### Success criteria

- All pilot AI traffic is attributed to named users in AI Gateway
- No provider keys are distributed to developers, unless BYOK is intentionally allowed
- Budgets are enforced and notifications reach users
- Security can reconstruct a session from prompt to tool calls to network decisions
- A blocked request appears in Agent Firewall's audit log
- Metrics reach the customer's monitoring stack

### Demo flow

1. Open **AI settings > Providers** to show that admins connect providers such as OpenAI, Anthropic, and Amazon Bedrock in one place, with keys held centrally.
2. Click through to **AI settings > Models** to show the range of models the organization can offer.
3. Show a template that injects the AI Gateway base URL and session token, so the developer never handles a provider key.
4. Start a workspace from that template and run a Claude Code task.
5. Open the session in AI Gateway, with the prompt, reasoning, tool calls, and token usage attributed to the user.
6. Have the agent try to reach a domain that isn't on the allowlist, and show the denied request alongside the session.
7. Show group budgets and the spend report.
8. Show metrics in Prometheus or Grafana.

Tailor emphasis to the audiences in [section 6](#6-audiences).

---

## 10. Commercial, Partners, and Contacts

### Packaging and prerequisites

- AI Governance, including AI Gateway, AI Gateway Proxy, and Agent Firewall, is included in Premium
- Community deployments can't use AI Governance
- Coder Agents routes all model traffic through AI Gateway automatically
- Coder v2.30 or later. Agent Firewall audit logs require Agent Firewall v0.5.2 or later
- Credentials for at least one supported provider, or a self-hosted OpenAI-compatible endpoint
- AI Gateway Proxy requires a CA certificate that clients trust

See [Packaging](../../company/packaging.md) and [coder.com/pricing](https://coder.com/pricing) for current tiers and prices.

### Evaluation access

Self-serve. The [Premium trial](https://coder.com/trial) includes AI Governance. For larger evaluations, work with the Coder account team.

### Partners

AI Governance complements cloud and model providers such as AWS and Amazon Bedrock. See the message house's [Partner Narrative](./message-house.md#partner-narrative).

### Contacts

| Topic | Contact / Team |
|---|---|
| Messaging and positioning | Matt Vollmer, Product Marketing |
| Product direction and roadmap | AI Governance product manager |
| Technical evaluations | AI Governance solutions engineering owner |
| Customer support | Coder Support |
| Everything else | Your [Coder account team](https://coder.com/contact) or [sales@coder.com](mailto:sales@coder.com) |

---

## 11. Resources

- [AI Governance docs](https://coder.com/docs/ai-coder/ai-governance), including [AI Gateway](https://coder.com/docs/ai-coder/ai-gateway), [AI Gateway Proxy](https://coder.com/docs/ai-coder/ai-gateway/ai-gateway-proxy), [client compatibility](https://coder.com/docs/ai-coder/ai-gateway/clients), [auditing](https://coder.com/docs/ai-coder/ai-gateway/audit), [cost controls](https://coder.com/docs/ai-coder/ai-gateway/cost-controls), and [Agent Firewall](https://coder.com/docs/ai-coder/agent-firewall)
- [AI Governance message house](./message-house.md)
- [Secure Development Environments](../../use-cases/secure-development-environments.md) and [Deploy AI Coding Agents](../../use-cases/deploy-ai-coding-agents.md)
- Market landscape pages for [LiteLLM](../../market-landscape/litellm.md), [NVIDIA OpenShell](../../market-landscape/nvidia-openshell.md), [Cursor](../../market-landscape/cursor.md), and [Claude Code](../../market-landscape/claude-code.md)
