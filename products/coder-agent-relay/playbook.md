# Coder Agent Relay Playbook

> A shared reference for understanding where Coder Agent Relay fits, how it works, and how to support organizations evaluating or adopting it.

For positioning, messaging, and value propositions, see the [Agent Relay message house](./message-house.md). For detailed product questions, see the [Agent Relay for Cursor FAQ](./cursor-faq.md) and the [Agent Relay for Claude FAQ](./claude-code-faq.md).

---

## 1. Quick Reference

| | |
|---|---|
| **The product** | Agent Relay connects cloud agents like Cursor and Claude Code to self-hosted Coder workspaces. |
| **Best fit** | Enterprises that want a supported cloud agent but require execution on infrastructure they control. |
| **Common signal** | "Our developers want Cursor or Claude Code cloud agents, but security won't approve execution in the vendor's cloud." |
| **Key question** | "Is your requirement about where the agent executes, or where the model runs?" |
| **Core value** | Developers keep their agent, and platform and security teams keep control of execution. |
| **Important limitation** | Orchestration and inference stay in the provider's cloud, so it isn't a fit for fully self-hosted or air-gapped requirements. |
| **Status** | Early access (closed preview with design partners). |
| **Journey stage** | Multiply, building on Coder Workspaces and AI Governance. See the [customer journey](../../company/customer-journey.md). |
| **Next step** | Customers connect with their customer success manager (CSM), who aligns with Product Management and the Field CTO on a spot in the closed preview and a pilot scope. |

---

## 2. Overview

Coder Agent Relay is a broker that connects cloud-hosted AI agent sessions, from Cursor Cloud Agents and Claude Code, to ephemeral, self-hosted Coder workspaces on infrastructure the enterprise controls. The provider keeps the developer experience, orchestration, and model inference. The agent's execution, where it reads code, runs commands, and reaches internal systems, happens inside a governed Coder workspace.

Many enterprises can accept SaaS orchestration but not agent execution outside infrastructure they control. Without an approved path, developers adopt cloud agents on their own. Cursor and Anthropic now support self-hosted execution, which makes a governed execution layer possible, and Agent Relay provides that layer using the Coder templates, RBAC, and audit the platform team already manages.

See the message house for the full [status quo and 3 Whys](./message-house.md#the-3-whys).

---

## 3. How It Works

### Architecture summary

The provider orchestrates and performs inference, Coder provides the self-hosted execution environment, and Agent Relay connects the two. Agent Relay watches for pending sessions, provisions a Coder workspace from a mapped template, and lets the provider's worker inside that workspace connect directly to the cloud session. Once connected, Agent Relay stays out of the agent's communication path and only manages the workspace lifecycle.

### Components and responsibilities

| Component | Responsibility |
|---|---|
| Provider (Cursor or Anthropic) | Developer client, cloud session orchestration, agent loop, model inference, worker or runner software, and billing for the agent |
| Agent Relay | Watches provider pools, claims eligible sessions, resolves the session owner, triggers workspace creation, and reaps completed workspaces |
| Coder control plane | Provisions and deletes workspaces from Terraform templates, and enforces RBAC and audit |
| Coder workspace | Execution environment with the code, tools, dependencies, network access, and credentials the customer provides, governed by Agent Firewall |
| Customer | Infrastructure and compute, workspace templates, network and security policy, and the provider pool or environment configuration |

### Typical workflow

1. **Start.** A developer starts a cloud agent session in Cursor or Claude Code and selects the Cursor Team Pool or Claude Code environment mapped to Coder.
2. **Relay.** Agent Relay detects the pending session, validates it, and claims it.
3. **Provision.** The Coder control plane creates an ephemeral workspace from the mapped template for that user.
4. **Execute and tear down.** The worker or runner connects directly to the cloud session and executes tool calls. When it exits, Agent Relay deletes the workspace.

For provider-specific details, such as identity matching and idle timeouts, see the [Cursor FAQ](./cursor-faq.md#technical-architecture) and [Claude FAQ](./claude-code-faq.md#technical-architecture).

### Deployment model

The Coder control plane, Agent Relay, and workspaces run on customer-controlled infrastructure and are operated by the customer. Agent Relay ships as a public container image (`ghcr.io/coder/agent-relay`) and Helm chart (`oci://ghcr.io/coder/chart/coder-agent-relay`).

### Data and trust boundaries

Repositories, build caches, credentials, internal services, and development tooling stay in the customer's Coder deployment. Some content must cross the boundary. The worker or runner sends conversation content, including tool results that can contain code, to the provider for inference. Coder doesn't proxy or observe model inference, and Coder AI Gateway isn't in the inference path. Evaluate specific data flows against each provider's documentation, such as [Cursor's Self-Hosted Machines docs](https://cursor.com/docs/cloud-agent/self-hosted) and [Anthropic's self-hosted environments docs](https://code.claude.com/docs/en/self-hosted-environments).

---

## 4. Boundaries and Terminology

### What the product does not do

- Self-host the provider's control plane, orchestration, or agent loop
- Perform, proxy, or observe model inference, or report model selection or token usage
- Keep all data inside the customer's environment
- Support providers other than Cursor and Claude Code today
- Replace Coder Agents or a full regulatory compliance program

See the message house's [Known Limitations](./message-house.md#known-limitations) and the FAQs' "Frequently Misunderstood Concepts" sections for more.

### Recommended terminology

| Preferred | Avoid | Why |
|---|---|---|
| "Cloud-hosted agents, self-hosted execution" | "Self-hosted Cursor" or "self-hosted Claude Code" | Only the execution environment is self-hosted. |
| "Execution runs on infrastructure you control" | "Your data never leaves your network" | Conversation content goes to the provider for inference. |
| "An approved path to the cloud agents developers already want" | "Air-gapped cloud agents" | Orchestration and inference require the provider's cloud. |
| "Agent Relay brokers the connection" | "Agent Relay proxies or governs inference" | Agent Relay steps out of the communication path once connected. |

---

## 5. Fit

See the message house's [Target Market / ICP](./message-house.md#target-market--icp) for the full ideal customer profile.

### Use cases

Agent Relay's primary use cases are cloud agent adoption without losing execution control, extending existing Coder infrastructure to cloud agents, and providing an approved path before shadow AI takes hold. See the message house's [Use Cases](./message-house.md#use-cases) and [Deploy AI Coding Agents](../../use-cases/deploy-ai-coding-agents.md).

### Good-fit signals

- Developers want Cursor Cloud Agents or Claude Code, and security won't approve vendor-hosted execution
- An existing Coder customer with growing agent demand
- Agents need access to private repositories, tools, or internal systems
- Shadow cloud agent usage is appearing, with unmanaged credentials and no audit trail
- A team has wired a few self-hosted machines to a cloud agent and needs to scale it

### Poor fit or another approach

- **Everything, including inference, must stay inside the perimeter.** Common in government and defense. Consider [Coder Agents](../coder-agents/message-house.md).
- **The requirement covers the whole stack in highly regulated financial services.** Agent Relay addresses execution control, not the entire third-party risk picture.
- **Provider-hosted execution already meets requirements.** Agent Relay is unlikely to be the deciding factor.
- **The desired provider isn't supported.** Codex cloud and Devin Outposts aren't supported today.

### Discovery questions

- **Current tools.** Which cloud agents are developers using or asking for, and is the organization already running Coder?
- **Provider plan.** Does the organization have Cursor Enterprise, or Anthropic Team or Enterprise?
- **Security boundary.** Is the requirement execution control, or does it extend to inference and orchestration?
- **Internal access.** Which repositories, dependencies, and services do agents need to reach?
- **Scale.** How many concurrent agent sessions do you expect at launch and at scale?
- **Ownership.** Who owns templates, capacity, and AI tool approval?
- **Regulation.** Which frameworks, such as DORA or FCA/PRA operational resilience, are in scope?

---

## 6. Audiences

See the message house's [Buyer Personas](./message-house.md#buyer-personas) for how each persona applies to Agent Relay.

| Role | Cares most about | Useful framing |
|---|---|---|
| [CISO and security leaders](../../audiences/ciso.md) | Controlling where agents execute, what they reach, and what data flows to the provider | "An approved path to the agents developers want, on infrastructure you already govern." |
| [Platform engineers](../../audiences/platform-engineer.md) | Extending existing templates and RBAC to agents without owning worker fleets, plus startup time | "Extend the Coder platform you already run to cloud agents, without a new platform." |
| [Developers](../../audiences/developer.md) | Keeping the Cursor or Claude Code experience while agents reach internal resources | "Keep your agent. It just runs where your code already lives." |
| [CTO](../../audiences/cto.md) and [CIO](../../audiences/cio.md) | Sanctioned AI adoption without shadow AI or single-vendor lock-in | "Adopt the best cloud agents without giving up control of where they run." |

---

## 7. Alternatives and Related Products

See the message house's [Competitive Position](./message-house.md#competitive-position) for the full narrative.

- **DIY self-hosted workers.** Cursor Team Pools and Anthropic self-hosted environments leave the worker image, infrastructure, scaling, and cleanup to the customer. Agent Relay provides that as a governed platform. See [Coder and Cursor](../../market-landscape/cursor.md) and [Coder and Claude Code](../../market-landscape/claude-code.md).
- **Provider-hosted execution.** Cursor states its hosted agents are sufficient for over 80% of its customers ([Cursor docs](https://cursor.com/docs/cloud-agent/choose-runtime)). Agent Relay matters when execution must run on infrastructure the organization controls.
- **Sandbox platforms.** Services like Daytona and E2B can run provider workers, but the control plane may stay with the vendor and the environments differ from the ones developers use. See [Coder and Daytona](../../market-landscape/daytona.md) and [Coder and E2B](../../market-landscape/e2b.md).
- **Coder Agents.** Coder's native agent runs orchestration in the self-hosted Coder control plane and suits organizations that need inference inside the perimeter. Customers can use both. See the FAQ answer on [Agent Relay versus Coder Agents](./cursor-faq.md#product--roadmap) and the [Coder Agents message house](../coder-agents/message-house.md).

---

## 8. Common Questions

For architecture, data, positioning, and roadmap questions, see the [Cursor FAQ](./cursor-faq.md) and [Claude FAQ](./claude-code-faq.md). The questions below aren't covered there.

### "How do we get access?"

Agent Relay is in early access, in closed preview with design partners. Space is limited, so interested customers should connect with their CSM, who then aligns with Product Management and the Field CTO (see [Contacts](#contacts)). It requires Coder Premium and a supported provider plan.

> Useful follow-up: "Which provider are you using, and what version of Coder are you running?"

### "How long does a session take to start?"

It depends on the complexity of the workspace template. Templates can be simplified to start in seconds, and prebuilt workspaces can warm environments for faster starts.

> Useful follow-up: "What does your current template install at startup, and which parts do agents actually need?"

### "How many concurrent sessions can it handle?"

Agent Relay is designed to support bursts of hundreds or thousands of concurrent sessions, and Coder can support that scale. It hasn't been publicly benchmarked at that level yet, and in practice concurrency may also depend on the provider's orchestration capacity.

> Useful follow-up: "What concurrency do you expect at launch, and how quickly do you expect it to grow?"

### "Do you support Codex, Devin, or other providers?"

Not today. Cursor and Claude Code are supported. The architecture is designed to support additional providers as they enable self-hosted execution, but we don't comment on unannounced partnerships or timing.

> Useful follow-up: "Would Coder Agents, or running that agent's CLI inside a workspace, meet the need in the meantime?"

---

## 9. Evaluation and Demo

### Evaluation stages

| Stage | Goals | Typically involved |
|---|---|---|
| Initial exploration | Understand the architecture split and data boundary, and confirm the provider and plan are supported | Platform and security leads |
| Technical evaluation | Adapt a template to install the provider's worker or runner, and validate routing, provisioning, and teardown | Platform engineers, developers |
| Security and architecture review | Data flows to the provider, Agent Firewall and network policy, identity mapping, RBAC, and per-session audit | Security, compliance |
| Production planning | Concurrency, startup time targets, template ownership, and rollout to more teams | Platform engineering, engineering leadership |

### Pilot setup

- One provider, one Coder organization, and one template
- A realistic task where agents need private repositories or internal services
- Named stakeholders from platform, security, and the developer group
- A licensed Coder Premium deployment and a supported provider plan
- Agreed success criteria and timeline

### Success criteria

- Developers complete real tasks in their normal Cursor or Claude Code workflow
- Each session gets its own workspace, and workspaces are deleted when sessions end
- Agent Firewall and RBAC policies apply to agent workspaces as expected
- Audit records tie each run to the session and user
- Security signs off on the documented data flows

### Demo flow

1. Start a session in Cursor or Claude Code, selecting the Coder-mapped pool or environment.
2. Show the ephemeral workspace appear in Coder for that user, built from the mapped template.
3. Show the agent using internal resources, and Agent Firewall blocking a disallowed destination.
4. End the session and show the workspace deleted and the audit record tied to the session and user.

Tailor emphasis to the audiences in [section 6](#6-audiences). Avoid over-emphasizing data sovereignty beyond execution or unbenchmarked concurrency, and use a simple template or prebuilt workspaces so startup stays fast.

---

## 10. Commercial, Partners, and Contacts

### Packaging and prerequisites

- A licensed Coder Premium deployment, with no separate Agent Relay SKU or billing
- A Cursor Enterprise plan, for Cursor
- An Anthropic Team or Enterprise plan, for Claude Code (Anthropic self-hosted environments are in public beta on these plans)

See [Packaging](../../company/packaging.md) for how Agent Relay fits Coder's tiers.

### Evaluation access

Agent Relay is in early access, in closed preview with design partners, and space is limited. Interested customers connect with their CSM, who aligns with Product Management and the Field CTO.

### Partners

Cursor and Anthropic deliver the agent experience developers want, and Coder governs where that agent executes. See the message house's [Partner Narrative](./message-house.md#partner-narrative).

### Contacts

| Topic | Contact / Team |
|---|---|
| Preview access | The customer's CSM, who aligns with Product Management and the Field CTO |
| Messaging and positioning | Matt Vollmer, Product Marketing |
| Everything else | Your [Coder account team](https://coder.com/contact) or [sales@coder.com](mailto:sales@coder.com) |

---

## 11. Resources

- [Agent Relay docs](https://coder.com/docs/ai-coder/agent-relay), including [Agent Relay for Cursor](https://coder.com/docs/ai-coder/agent-relay/cursor) and [Agent Relay for Claude Code](https://coder.com/docs/ai-coder/agent-relay/claude-code)
- [Agent Relay message house](./message-house.md), [Cursor FAQ](./cursor-faq.md), and [Claude FAQ](./claude-code-faq.md)
- [Introducing Agent Relay](https://coder.com/blog/introducing-agent-relay-cloud-hosted-agents-self-hosted-execution) and [Coder Brings Claude Code to Agent Relay](https://coder.com/blog/agent-relay-claude-code-agentic-development), announced September 15, 2026
- [Coder + Anthropic](https://coder.com/anthropic)
- [Cursor's Self-Hosted Machines integrations](https://cursor.com/docs/cloud-agent/self-hosted/integrations), which list Coder as a partner
- Market landscape pages for [Cursor](../../market-landscape/cursor.md), [Claude Code](../../market-landscape/claude-code.md), [Daytona](../../market-landscape/daytona.md), and [E2B](../../market-landscape/e2b.md)

No public customer evidence is available yet. When added, refer to customers by anonymized type unless they have publicly agreed to be named.

---

## Document Maintenance

**Owner:** Matt Vollmer, Product Marketing  
**Last updated:** 2026-09-29  
**Version:** 0.2

Update this playbook when the product's architecture, packaging, supported integrations, boundaries, or public evidence change, or when new questions recur.
