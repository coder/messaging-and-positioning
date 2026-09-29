# Coder Agent Relay

> A shared reference for understanding where Coder Agent Relay fits, how it works, and how to support organizations evaluating or adopting it.

This playbook builds on the [Agent Relay message house](./message-house.md), the [Agent Relay for Cursor FAQ](./cursor-faq.md), and the [Agent Relay for Claude FAQ](./claude-code-faq.md). When they conflict, the message house governs positioning and the FAQs govern provider-specific technical detail. Items marked `TBD` are open questions for Product Marketing. For preview access, see [Contacts](#contacts).

---

## 1. Product Overview

### What is Coder Agent Relay?

Coder Agent Relay is a broker that connects cloud-hosted AI agent sessions, from Cursor Cloud Agents and Claude Code, to ephemeral, self-hosted Coder workspaces on infrastructure the enterprise controls. The provider keeps orchestration and model inference; the agent's execution, where it reads code, runs commands, and reaches internal systems, happens inside a governed Coder workspace.

### What problem does it address?

Developers want the cloud agent experience that tools like Cursor and Claude Code deliver. Many enterprises can accept SaaS orchestration but not agent execution outside infrastructure they control, because agents need access to source code, dependencies, credentials, and internal services to do useful work. That's an architectural mismatch, not a product problem with any one tool, and without an approved path developers adopt cloud agents on their own.

### Why does this matter now?

Agent adoption is moving fast, and shadow AI is already how these tools get adopted in the absence of a sanctioned path. Cloud agent providers have started to support self-hosted execution (Cursor self-hosted machines and Team Pools, Claude Code self-hosted environments), which makes a governed, platform-level execution layer possible. Enterprises need that approved path before unmanaged usage becomes the default.

### Core value proposition

> Give developers the cloud agents they want, with execution on infrastructure platform and security teams control.

### Short description

Agent Relay connects cloud-hosted AI agents, like Cursor Cloud Agents and Claude Code, to secure, self-hosted Coder workspaces on infrastructure the enterprise controls. Developers keep the cloud agent experience they want; platform and security teams get the execution control, isolation, and auditability they require.

---

## 2. Best-Fit Organizations

### Organizations that may benefit most

- Want, or already use, a supported cloud agent (Cursor Cloud Agents or Claude Code)
- Operate primarily on self-hosted infrastructure, or already run Coder
- Have strict requirements around where source code is accessed and where commands execute
- Need agents to reach private tools, dependencies, or internal systems
- Involve platform, security, or compliance teams in AI adoption decisions
- Want to expand agent usage beyond individual developers to the broader organization

### Common environments

- Financial services
- Healthcare and insurance
- Large enterprises with strict security, compliance, or data sovereignty requirements
- Existing Coder customers that already standardize development environments with Terraform templates

### Signs the need may be emerging

- Developers are asking for Cursor Cloud Agents or Claude Code cloud sessions, and security hasn't approved them
- Security review blocks a cloud agent specifically because execution happens in the vendor's cloud
- A team has wired up a few self-hosted machines to a cloud agent manually and is asking how to scale it
- Unapproved cloud agent usage is showing up with unmanaged credentials and no audit trail

### Situations where another approach may be more appropriate

- **Everything, including inference, must stay inside the perimeter.** Common in government and defense. Orchestration and inference stay in the provider's cloud, so Agent Relay isn't a fit today. Consider [Coder Agents](../coder-agents/message-house.md), or an agent running inside a workspace against a customer-controlled inference endpoint.
- **Highly regulated financial services where the requirement covers the whole stack.** Agent Relay addresses the execution-control piece of third-party risk, not the entire compliance picture.
- **Fully comfortable with vendor-hosted execution.** If the provider's hosted agents meet the organization's requirements, Agent Relay is unlikely to be the deciding factor.
- **The desired provider isn't supported.** Cursor and Claude Code are the supported providers today. Codex cloud and Devin Outposts are not.

---

## 3. Audiences and Stakeholders

See the role pages under [`audiences/`](../../audiences/) for full context on each role. For the cross-role buyer motivations behind these roles, see [Buyer Personas](../../audiences/personas/overview.md) and the [message house](./message-house.md#buyer-personas).

### CISO and security leaders

**Primary goals**

- Control where agent execution happens and what it can reach
- Keep agent activity auditable and inside existing controls
- Enable AI adoption without unnecessary risk

**Common concerns**

- Developers adopting cloud agents security hasn't approved
- Unmanaged, unauditable agent activity across the organization
- What data flows to the agent provider for inference

**Relevant value**

Execution runs inside infrastructure the organization already governs, with the same identity, network, and audit controls, including Agent Firewall. Each run is tied to the agent session and user it served. This lets the organization say yes to agent adoption instead of blocking it or accepting the risk of unmanaged usage.

**Useful framing**

> An approved path to the agents developers want, on infrastructure you already govern.

---

### Platform engineers

**Primary goals**

- Provide self-service, standardized environments for developers and agents
- Reduce operational toil through templates and automation
- Avoid standing up a new platform or a new security review

**Common concerns**

- A few manually wired self-hosted machines won't hold up as agent usage scales
- Owning worker images, isolation, scaling, and cleanup for agent environments
- Session startup time

**Relevant value**

Agent Relay extends infrastructure existing Coder customers already operate, organizations, templates, RBAC, and audit logging, to cloud-hosted agents. Coder provisions one ephemeral workspace per session and scales to zero when idle. Startup time depends on template complexity; templates can be simplified to start in seconds, and prebuilt workspaces can warm environments for faster starts.

**Useful framing**

> Extend the Coder platform you already run to cloud agents, without a new platform.

---

### Developers

**Primary goals**

- Use the Cursor or Claude Code experience they already prefer
- Give agents access to the code, tools, and services real work requires

**Common concerns**

- Security or platform concerns blocking the tools they want
- Changes that make the agent experience slower or worse

**Relevant value**

Developers keep using Cursor or Claude Code exactly as they would otherwise. The difference is invisible to them, since execution happens inside a Coder workspace behind the scenes, with access to the internal resources the template provides.

**Useful framing**

> Keep your agent. It just runs where your code already lives.

---

### CTO and CIO

**Primary goals**

- Accelerate software delivery and engineering productivity with AI
- Adopt new technology without compromising security, reliability, or cost control

**Common concerns**

- Shadow AI and fragmented, unmanaged tooling
- Locking the organization into a single agent vendor

**Relevant value**

Agent Relay gives the organization a sanctioned path to the cloud agents developers want, on one governed platform that also runs Coder Agents and other agents side by side. Engineering gets the tools; security and platform teams keep control.

**Useful framing**

> Adopt the best cloud agents without giving up control of where they run.

---

## 4. Core Product Story

### The problem

Developers want the best cloud agents. Platform and security teams need control over where sensitive development work happens. Neither side is wrong, and neither side should have to lose to satisfy the other.

### The approach

Split the agent stack at the execution boundary. The provider keeps the developer experience, orchestration, and inference. Coder provides the execution environment: an ephemeral, governed workspace per session, provisioned from a platform-managed template. Agent Relay connects the two and manages the workspace lifecycle.

### The value

Agent Relay is the means, not the end. The value customers are buying is the Coder infrastructure underneath: self-hosting, neutrality, standardization, connectivity, and governance that already work for human developers and now extend to cloud agents.

### Key capabilities

- Provider pools mapped to a Coder organization and Terraform-based workspace template
- One ephemeral workspace per agent session, created on demand and deleted when the session ends
- Designed for high concurrency (hundreds or thousands of sessions), scaling to zero when idle
- Existing Coder governance (RBAC, Agent Firewall, secrets management, audit) applies to agent workspaces
- Audit records that correlate each run to the agent session and user
- Out of the agent's communication path once the session and workspace are connected

### Business or operational outcomes

- Sanctioned cloud agent adoption instead of shadow AI
- No new platform or separate security model for existing Coder customers
- Agent scale driven by platform automation rather than manual provisioning
- One governed platform for Cursor, Claude Code, Coder Agents, and other agents

---

## 5. How It Works

### Architecture summary

Anthropic or Cursor orchestrates and performs inference, Coder provides the self-hosted execution environment, and Agent Relay connects the two. Agent Relay watches for pending sessions from a supported provider, provisions a Coder workspace from a mapped template, and lets the provider's worker inside that workspace connect directly to the cloud session.

### Components and responsibilities

| Component | Responsibility |
|---|---|
| Provider (Cursor or Anthropic) | Developer client, cloud session orchestration, agent loop, model inference, and the worker or runner software |
| Agent Relay | Watches provider pools, claims eligible sessions, resolves the session owner, triggers workspace creation, and reaps completed workspaces |
| Coder control plane | Provisions and deletes workspaces from Terraform templates, and enforces RBAC and audit |
| Coder workspace | Execution environment with the code, tools, dependencies, network access, and credentials the customer provides |
| Provider worker or runner | Runs inside the workspace, connects directly to the cloud session, and executes the agent's tool calls |

### Typical workflow

1. **Start**  
   A developer starts a cloud agent session in Cursor or Claude Code and selects the pool or environment mapped to Coder.

2. **Relay**  
   Agent Relay detects the pending session, validates it, and claims it. For Claude Code, it matches the Anthropic-attested account email to an active member of the mapped Coder organization.

3. **Provision**  
   The Coder control plane creates an ephemeral workspace from the mapped template for that user.

4. **Execute and tear down**  
   The worker or runner connects directly to the cloud session and executes tool calls. When it exits (for Cursor, after a configurable idle period), Agent Relay's reaper deletes the workspace.

### Deployment model

The Coder control plane, Agent Relay, and workspaces run on customer-controlled infrastructure and are operated by the customer. Agent Relay ships as a public container image (`ghcr.io/coder/agent-relay`) and Helm chart (`oci://ghcr.io/coder/chart/coder-agent-relay`). The provider's orchestration and inference run in the provider's cloud.

### Data and trust boundaries

Repositories, build caches, credentials, internal services, and development tooling stay in the customer's Coder deployment. Some content must cross the boundary: the worker or runner sends conversation content, including tool results that can contain code, to the provider for inference. Cursor documents that file contents, terminal output, diffs, screenshots, local MCP results, and routing metadata are sent to Cursor. Evaluate specific data flows against each provider's architecture and security documentation rather than assuming all data stays inside. Coder doesn't proxy or observe model inference, and Coder AI Gateway isn't in the inference path.

---

## 6. Product Boundaries and Limitations

### What the product does

- Connects supported cloud agent sessions to self-hosted Coder workspaces
- Manages the lifecycle of one ephemeral workspace per session
- Applies existing Coder templates, RBAC, Agent Firewall, and audit to agent execution
- Correlates each run to the agent session and user

### What the product does not do

- Self-host the provider's control plane, orchestration, or agent loop
- Perform, proxy, or observe model inference, or report model selection or token usage
- Keep all data inside the customer's environment
- Support providers other than Cursor and Claude Code today
- Replace Coder Agents or a full regulatory compliance program

### Important distinctions

- **Self-hosted execution, not a self-hosted agent.** Only the execution environment is self-hosted.
- **Broker, not proxy.** Agent Relay brokers the session-to-workspace association, then steps out of the agent's communication path.
- **Platform, not runner.** A runner provides compute; Coder provides complete, governed development environments.

### Recommended terminology

**Preferred**

- "Cloud-hosted agents, self-hosted execution"
- "Execution runs on infrastructure you control"
- "An approved path to the cloud agents developers already want"

**Avoid**

- "Self-hosted Cursor" or "self-hosted Claude Code"
- "Your data never leaves your network"
- "Air-gapped cloud agents"
- "Agent Relay proxies or governs inference"

**Why**

Orchestration and inference stay with the provider, and some content crosses the customer boundary for inference. Overstating the boundary creates security review surprises and erodes trust.

---

## 7. Questions to Understand the Environment

### Current environment

- Which cloud agents are developers using or asking for today?
- Is the organization already running Coder? For which teams and templates?
- Has anyone connected a cloud agent to self-hosted machines already?

### Technical requirements

- Which Cursor or Anthropic plan does the organization have? (Cursor Enterprise, or Anthropic Team or Enterprise, is required.)
- What internal repositories, dependencies, and services do agents need to reach?
- Can existing workspace templates be adapted to install the Cursor worker or Anthropic runner?

### Security and governance

- Is the requirement execution control, or does it extend to inference and orchestration?
- Which data flows to the provider are acceptable, and has security reviewed the provider's documentation?
- What network policy, secrets, and audit requirements apply to agent workloads?

### Scale and operations

- How many concurrent agent sessions do you expect at launch and at scale?
- Who owns templates, capacity, and workspace lifecycle policy?
- How sensitive are users to session startup latency?

### Organizational considerations

- Who approves AI tools: platform, security, compliance, or a central AI group?
- Is there a mandate to reduce shadow AI or provide an approved path?
- Which regulatory frameworks (for example DORA or FCA/PRA operational resilience) are in scope?

---

## 8. Fit Indicators

### Strong indicators

- Wants Cursor Cloud Agents or Claude Code but security won't approve vendor-hosted execution
- Existing Coder customer with growing agent demand
- Agents need access to private repositories, tools, or internal systems

### Emerging indicators

- Shadow cloud agent usage is appearing
- A small DIY self-hosted worker setup that needs to scale

### Potential mismatch

- Requires inference and orchestration inside the perimeter, or fully air-gapped operation
- Fully comfortable with provider-hosted execution
- Wants an unsupported provider, such as Codex cloud or Devin Outposts

### Questions that help clarify fit

- "Is your concern where the agent runs, or where the model runs?"
- "What would security need to see to approve a cloud agent?"

---

## 9. Alternative Approaches

### DIY self-hosted workers

**How it works**

The organization uses the provider's self-hosted option (Cursor self-hosted machines or Team Pools, Anthropic self-hosted environments) and builds the worker image, infrastructure, secrets, scaling, and orchestration itself.

**Where it can work well**

- Small teams or a handful of machines
- Organizations with platform capacity to build and maintain the stack

**Considerations**

- The customer owns image builds, updates, scaling policy, isolation, and cleanup
- Cursor's My Machines isn't an org-wide fleet system; each worker belongs to one user
- Breaks down when hundreds or thousands of sessions need governed workspaces at once

**How Coder Agent Relay differs**

The execution environment is provisioned, isolated, governed, and torn down as part of a platform, using templates, RBAC, Agent Firewall, and audit the platform team already manages. Agent Relay is designed for high-concurrency bursts. That scale hasn't been publicly benchmarked yet, and in practice it may also depend on the provider's orchestration capacity.

---

### Provider-hosted execution

**How it works**

The agent runs in the provider's managed cloud environment.

**Where it can work well**

- Organizations with no meaningful execution or infrastructure constraints
- Cursor states its hosted agents are sufficient for over 80% of its customers

**Considerations**

- Execution happens outside infrastructure the enterprise controls
- Limited access to private networks and internal systems

**How Coder Agent Relay differs**

Keeps the same developer experience while moving execution onto customer-controlled infrastructure.

---

### Sandbox platforms (for example Daytona or E2B)

**How it works**

A third-party sandbox platform runs the worker, often with a customer-run orchestrator.

**Where it can work well**

- Programmatic code execution inside AI products

**Considerations**

- The control plane may remain with the vendor
- Sandboxes aren't the same environments human developers use

**How Coder Agent Relay differs**

Provisions from a platform-managed template per session on fully self-hosted infrastructure, logs which session and user it served, and uses the same environments as human developers. See [Daytona](../../market-landscape/daytona.md) and [E2B](../../market-landscape/e2b.md).

---

### Accepting shadow AI

**How it works**

No sanctioned path; developers use the agents they want.

**Considerations**

- Moves the cost into security risk, fragmented infrastructure, and loss of control

**How Coder Agent Relay differs**

Adoption happens inside an approved path the platform team provisions and governs.

---

## 10. Related Products

### Coder Agents vs. Coder Agent Relay

| Dimension | Coder Agent Relay | Coder Agents |
|---|---|---|
| Agent experience | Provider's client (Cursor, Claude Code) | Coder's native agent experience |
| Orchestration | Provider's cloud | Self-hosted Coder control plane |
| Inference | Provider's cloud | Customer-configured LLM provider |
| Execution | Self-hosted Coder workspace | Self-hosted Coder workspace |
| Air-gapped fit | No | Yes |

### When each may be appropriate

**Coder Agent Relay**

- Developers want a specific cloud agent's experience
- Execution control is required, but cloud orchestration and inference are acceptable

**Coder Agents**

- Orchestration and inference must stay inside the perimeter
- The organization wants a model- and provider-agnostic native agent

### How they can work together

Customers can run Cursor, Claude Code, Coder Agents, and other agents at the same time on the same governed workspaces. AI Governance (AI Gateway and Agent Firewall) applies to agents in Coder, with the caveat that AI Gateway isn't in the inference path for Agent Relay sessions. See the [Coder Agents message house](../coder-agents/message-house.md) and [AI Governance message house](../coder-ai-governance/message-house.md).

---

## 11. Common Questions

### "Is Cursor or Claude Code fully self-hosted with this?"

**Context**

Buyers often hear "self-hosted" and assume the whole stack moves in-house.

**Response**

No. The execution environment is self-hosted. Orchestration and inference remain in the provider's cloud.

**Useful follow-up**

> Is your requirement about where the agent executes, or where the model runs?

---

### "Does any code leave our network?"

**Context**

Security teams want to know the real data boundary.

**Response**

Tool calls execute inside the self-hosted workspace, but conversation content, including tool results that can contain code, goes to the provider for inference. Evaluate specific flows against the provider's documentation.

**Useful follow-up**

> Has your security team reviewed the provider's self-hosted execution documentation?

---

### "The provider already supports self-hosted workers. Why add Coder?"

**Context**

The buyer is weighing a DIY build.

**Response**

The provider's self-hosted option leaves the worker image, infrastructure, secrets, scaling, and validation to the customer. Coder provides that as a platform, with templates, ephemeral per-session workspaces, RBAC, Agent Firewall, and audit.

**Useful follow-up**

> How many concurrent agent sessions do you expect, and who will operate the workers?

---

### "Does Coder AI Gateway govern inference for these sessions?"

**Context**

Existing AI Governance customers expect Gateway coverage everywhere.

**Response**

No. Coder doesn't proxy or observe inference for Agent Relay sessions and has no access to model selection or token usage.

**Useful follow-up**

> Is centralized inference governance a requirement for this use case?

---

### "Is this available now?"

**Context**

Timing and access.

**Response**

Agent Relay is in early access, in closed preview with design partners. Space is limited; interested customers should connect with Nicky Pike and Atif (see [Contacts](#contacts)).

**Useful follow-up**

> Which provider and plan are you on, and what timeline are you working toward?

---

### "How long does a session take to start?"

**Context**

Developers are used to provider-hosted agents starting quickly, and platform teams worry ephemeral workspaces add delay.

**Response**

It depends on the complexity of the workspace template. Templates can be simplified to start in seconds, and prebuilt workspaces can warm environments for faster starts.

**Useful follow-up**

> What does your current workspace template install at startup, and which parts do agents actually need?

---

### "How many concurrent sessions can it handle?"

**Context**

Platform teams planning broad rollout want to know the ceiling.

**Response**

Agent Relay is designed to support bursts of hundreds or thousands of concurrent sessions, and Coder can support that scale. It hasn't been publicly benchmarked at that level yet, and in practice concurrency may also depend on the provider's orchestration capacity.

**Useful follow-up**

> What concurrency do you expect at launch, and how quickly do you expect it to grow?

---

### "Do you support Codex, Devin, or other providers?"

**Context**

The buyer's preferred agent may not be supported.

**Response**

Not today. Cursor and Claude Code are supported. The architecture is designed to support additional providers as they enable self-hosted execution, but we don't comment on unannounced partnerships or timing.

**Useful follow-up**

> Would Coder Agents, or running that agent's CLI inside a workspace, meet the need in the meantime?

---

## 12. Evaluation Journey

### Initial exploration

Typical goals:

- Understand the architecture split and the data boundary
- Confirm the provider and plan are supported

Helpful resources:

- [Agent Relay docs](https://coder.com/docs/ai-coder/agent-relay)
- [Agent Relay for Cursor FAQ](./cursor-faq.md) and [Agent Relay for Claude FAQ](./claude-code-faq.md)

### Technical evaluation

Typical goals:

- Adapt a workspace template to install the provider's worker or runner
- Validate session routing, provisioning, and teardown

Participants commonly involved:

- Platform engineering (template and Coder owners)
- Developers who use the cloud agent

### Security and architecture review

Areas commonly evaluated:

- Data flows to the provider for inference
- Network policy and Agent Firewall configuration for agent workspaces
- Identity mapping, RBAC, and audit records per session

### Pilot or proof of value

Recommended characteristics:

- One provider, one Coder organization, one template
- A realistic task that needs internal resources
- A defined group of developers

### Production planning

Topics to address:

- Capacity for concurrent sessions, and startup time targets (simplify templates or use prebuilt workspaces)
- Template ownership and update process
- Rollout to additional teams and providers

---

## 13. Pilot / Proof-of-Value Guidance

### A well-defined evaluation includes

- A realistic use case where agents need private repositories or internal services
- Named stakeholders from platform, security, and the developer group
- A licensed Coder Premium deployment and a supported provider plan
- Agreed success criteria
- An agreed timeline

### Suggested success criteria

- Developers complete real tasks in their normal Cursor or Claude Code workflow
- Each session gets its own workspace, and workspaces are deleted when sessions end
- Agent Firewall and RBAC policies apply to agent workspaces as expected
- Audit records tie each run to the session and user
- Security signs off on the documented data flows

### Questions to answer before beginning

- Which provider, plan, and pool or environment will be used?
- Which template and Coder organization will sessions map to?
- What internal resources should agents reach, and which must they not?

---

## 14. Demo Guidance

### What the demo should communicate

The developer's experience doesn't change, but the agent's work runs in a governed Coder workspace on the customer's infrastructure, and that workspace appears and disappears with the session.

### Recommended flow

1. Start a session in Cursor or Claude Code, selecting the Coder-mapped pool or environment.
2. Show the ephemeral workspace appear in Coder for that user, built from the mapped template.
3. Show the agent using internal resources, and Agent Firewall blocking a disallowed destination.
4. End the session and show the workspace deleted and the audit record tied to the session and user.

### Key points to reinforce

- Same agent experience for developers
- Execution on infrastructure the customer controls
- Existing Coder governance applies automatically

### Areas to avoid over-emphasizing

- Data sovereignty claims beyond execution
- Complex template startup times; if the demo template is heavy, simplify it or use prebuilt workspaces first
- Unbenchmarked concurrency numbers

### Audience-specific variations

**Technical audience**

Template configuration, pool mapping, lifecycle, scale-to-zero, and prebuilt workspaces for faster starts.

**Security audience**

Data boundary, Agent Firewall, RBAC, and per-session audit records.

**Executive audience**

Approved path versus shadow AI, and no new platform for existing Coder customers.

---

## 15. Evidence and Validation

### Customer evidence

- None published yet. When added, refer to customers by anonymized type (for example, "a large financial institution") unless they have publicly agreed to be named.

### Product evidence

- Agent Relay supports Cursor (first supported provider) and Claude Code, and is in early access ([Agent Relay docs](https://coder.com/docs/ai-coder/agent-relay)).
- None published yet for usage, scale, or startup time.

### Market evidence

- Cursor lists Coder as a self-hosted machines integration partner ([Cursor docs](https://cursor.com/docs/cloud-agent/self-hosted/integrations)).
- Coder and Anthropic announced Claude Code support in Agent Relay on September 15, 2026 ([Coder announcement](https://coder.com/blog/agent-relay-claude-code-agentic-development)).
- Cursor states self-hosting is usually driven by compliance or security policy ([Cursor docs](https://cursor.com/docs/cloud-agent/choose-runtime)).

---

## 16. Commercial Model

### Packaging

Agent Relay is a capability within existing Coder tiers rather than a separate SKU, and it requires Coder Premium. As of this writing, it doesn't introduce its own billing. See [Packaging](../../company/packaging.md).

### Prerequisites

- A licensed Coder Premium deployment
- For Cursor: a Cursor Enterprise plan
- For Claude Code: an Anthropic Team or Enterprise plan (Anthropic self-hosted environments are in public beta on these plans)

### Pricing metric

No separate pricing metric. Agent Relay is included with Coder Premium.

### Evaluation / trial model

Agent Relay is in early access, in closed preview with design partners, and space is limited. Interested customers should connect with Nicky Pike and Atif (see [Contacts](#contacts)).

### Example deployment profiles

#### Existing Coder customer adding cloud agents

- Organization: Regulated enterprise already running Coder Premium for developers
- Usage pattern: Developers request Cursor Cloud Agents or Claude Code; platform team maps a pool to an existing template
- Relevant package: Coder Premium plus the provider's enterprise plan

#### Cloud-agent-led opportunity

- Organization: Enterprise standardizing on Cursor or Claude Code, blocked by execution requirements
- Usage pattern: Adopts Coder to provide governed execution for cloud agent sessions
- Relevant package: Coder Premium plus the provider's enterprise plan

---

## 17. Partner and Ecosystem Context

### Relevant partners

- Cursor
- Anthropic (Claude Code)

### Division of responsibilities

| Organization | Responsibility |
|---|---|
| Coder | Agent Relay, control plane, workspace provisioning and lifecycle, networking, governance, and audit |
| Cursor or Anthropic | Developer experience, cloud orchestration, agent loop, inference, worker or runner software, and billing for the agent |
| Customer | Infrastructure and compute, workspace templates, network and security policy, and the pool or environment configuration |

### When partner involvement may help

- Security review of the provider's data flows
- Provider plan, pool, or environment setup

### Shared positioning

> The provider delivers the agent experience developers want; Coder governs where that agent executes. Neither side has to change what it does well.

---

## 18. When to Involve a Specialist

Additional technical, product, security, or commercial expertise may be useful when:

- The customer requires inference or orchestration inside the perimeter
- Security needs detailed data-flow answers for a specific provider
- Expected concurrency is in the hundreds or thousands of sessions
- The customer asks about an unsupported provider or roadmap timing
- Pricing, packaging, or regulatory positioning (for example DORA) comes up

### Contacts

| Topic | Contact / Team |
|---|---|
| Preview access | Nicky Pike and Atif |
| Messaging and positioning | Matt Vollmer, Product Marketing |
| Everything else | Your [Coder account team](https://coder.com/contact) or [sales@coder.com](mailto:sales@coder.com) |

---

## 19. Supporting Resources

### Product

- [Agent Relay docs](https://coder.com/docs/ai-coder/agent-relay)
- [Agent Relay for Cursor](https://coder.com/docs/ai-coder/agent-relay/cursor) and [Agent Relay for Claude Code](https://coder.com/docs/ai-coder/agent-relay/claude-code)
- [Agent Relay message house](./message-house.md)
- [Agent Relay for Cursor FAQ](./cursor-faq.md) and [Agent Relay for Claude FAQ](./claude-code-faq.md)
- [Coder + Anthropic](https://coder.com/anthropic)

### Evaluation

- Preview access and pilot scoping: see [Contacts](#contacts)

### Market context

- [Introducing Agent Relay](https://coder.com/blog/introducing-agent-relay-cloud-hosted-agents-self-hosted-execution)
- [Coder Brings Claude Code to Agent Relay](https://coder.com/blog/agent-relay-claude-code-agentic-development)
- Market landscape: [Cursor](../../market-landscape/cursor.md), [Claude Code](../../market-landscape/claude-code.md), [Daytona](../../market-landscape/daytona.md), [E2B](../../market-landscape/e2b.md)

---

## 20. Quick Reference

### The product

> Agent Relay connects cloud agents like Cursor and Claude Code to self-hosted Coder workspaces.

### Best fit

> Enterprises that want a supported cloud agent but require execution on infrastructure they control.

### Common signal

> "Our developers want Cursor or Claude Code cloud agents, but security won't approve execution in the vendor's cloud."

### Key question

> "Is your requirement about where the agent executes, or where the model runs?"

### Core value

> Developers keep their agent; platform and security teams keep control of execution.

### Important limitation

> Orchestration and inference stay in the provider's cloud, so it isn't a fit for fully self-hosted or air-gapped requirements.

### Next step

> Connect with Nicky Pike and Atif to request a spot in the closed preview and scope a pilot.

---

## Document Maintenance

**Owner:** Matt Vollmer, Product Marketing  
**Last updated:** 2026-09-29  
**Product status:** Early access (closed preview with design partners)  
**Version:** 0.1

### Update this guide when

- Product architecture changes
- Packaging or pricing changes
- New integrations are supported
- New customer patterns emerge
- Important questions recur
- Product boundaries change
- New public evidence becomes available
