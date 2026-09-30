# Coder Agents Message House

Coder Agents is mostly part of the Multiply stage of the [customer journey](../../company/customer-journey.md), with a partial role in Modernize, building on the Migrate and Modernize foundation established by Coder Workspaces and AI Governance.

## Status Quo

### Without Coder

Enterprises face an AI coding paradox: most engineering leaders want to employ AI coding agents to multiply developer productivity, but only if the infrastructure can ensure it's done safely and at scale.

| Dimension | Reality |
| :---- | :---- |
| Shadow AI sprawl | Developers adopt Claude Code, Cursor, Windsurf, and a half-dozen other AI tools individually, each tunneling code, context, and credentials to different third-party clouds. Security has zero visibility. |
| No secure environment | AI agents run on developer laptops with ambient credentials, full network access, and no sandboxing. A prompt-injection or hallucinated `rm -rf` runs with the developer's full permissions. |
| Idle-human bottleneck | Agents running inside a developer's IDE lock up their machine. Background tasks that could run autonomously, test generation, refactoring, migrations, still require a human watching a spinner. |
| Governance is nonexistent | CISOs cannot answer: "Which AI models touch our code? What data leaves our perimeter? What did an agent actually do?" No audit trail, no policy enforcement, no kill switch. |
| Compliance blockers | Regulated industries (FinServ, Gov, Healthcare) cannot adopt AI agents because no vendor can prove data residency, audit trails, or access controls. Adoption stalls entirely. |
| Cost blindness | Token spend and agent compute are invisible and unattributable. Nobody knows which team, project, or agent is burning through budgets. ROI conversations are faith-based. |
| Tool fragmentation | Every team picks a different AI agent, configures it differently, and connects to different models. Platform engineering has no unified control plane. Best practices don't propagate; mistakes repeat. |

Organizations either avoid AI coding agents entirely (competitive disadvantage) or, more likely, allow ungoverned usage that creates security, compliance, and cost exposure. Neither path is acceptable.

## The 3 Whys

### Why do anything?

Coding agents are the largest productivity lever in software development, but consequently also the largest new attack surface since cloud migration. Agents can now autonomously write, test, debug, and commit code across multi-file repositories. Organizations that fail to operationalize them will lose developer velocity and top talent to competitors that do. But unmanaged adoption introduces data-leakage, compliance, IP, and supply-chain risks that can be existential. Doing nothing is not standing still. It is actively accumulating risk.

### Why now?

Several forces are converging:

- Frontier models have crossed the capability threshold. Claude, Codex, Gemini, and open-weight models like Llama and DeepSeek can all perform complex, multi-file, multi-step coding tasks autonomously. The agent layer on top of these models is rapidly commoditizing. The performance gap between well-implemented agents is narrowing to single-digit percentages on standard benchmarks. The differentiation has shifted from "which agent is smartest" to "which agent can I actually deploy in my environment."
- The headless agent paradigm is here. Agents that operate in the background, executing multi-step tasks without human supervision, are being adopted now. This changes the unit economics of software development, but only if you have infrastructure to run them.
- Developer expectations have shifted. Top-tier engineers now expect AI-augmented workflows as table stakes. Recruiting and retention depend on it.
- Competitors are already deploying. Early adopters report massive reductions in time-to-merge for routine tasks. Every quarter you wait is a quarter they compound that advantage.

### Why Coder Agents?

Because the hard problem was never the agent, it was the infrastructure.

Every AI coding agent needs the same things: a safe execution environment, access to the codebase, the ability to run commands, and a connection to a frontier model. The agent logic is important, and Coder Agents is performant and competitive at this layer. But this is table stakes. Every serious vendor ships a capable agent.

What enterprises actually need is the infrastructure to run that agent self-hosted, air-gapped, governed, auditable, model-flexible, and on infrastructure they already control.

Coder Agents delivers this because it natively runs on the same Coder infrastructure already designed to provision, isolate, and manage development environments at scale:

- **Self-hosted on your infrastructure** - cloud VPC, on-prem data center, or air-gapped enclave. Source code never leaves your perimeter.
- **LLM-agnostic** - connect any model: Anthropic Claude, OpenAI GPT, Google Gemini, or self-hosted open-weight models via Ollama, vLLM, or any OpenAI-compatible API. Switch models without changing tools.
- **Terraform-provisioned workspaces** - every agent session runs in a reproducible, IaC workspace.
- **Headless execution** - agents run autonomously in the background, report status to the dashboard, and integrate into CI/CD and review workflows.
- **AI governance** - AI Gateway for prompt auditing and user-level attribution, zero API keys in workspaces, template-level network policies, SSO/OIDC, centralized model and tool configuration enforced server-side.
- **Full observability** - track how developers are using agents and what agents are doing across your environment. Every prompt, action, and outcome is attributable, giving platform and security teams visibility into usage, behavior, and impact.
- **Centralized agent distribution** - deploy coding agents once and make them available consistently across your developer population. No per-user setup, no configuration drift.

## Messaging Statement

### Short (50 words)

Coder Agents runs AI coding agents entirely on infrastructure you govern, the orchestration, the execution, and the environments. It is LLM-agnostic and air-gap capable. Agents can be invoked by developers through chat or triggered headlessly via API, and each task runs in a securely provisioned, isolated environment.

### Medium (150 words)

Coder Agents is the self-hosted way to run coding agents natively on infrastructure you control. It is LLM-agnostic, supporting Anthropic Claude, OpenAI GPT, Google Gemini, and self-hosted models.

Instead of sending source code to a third-party cloud service, Coder Agents runs entirely within your VPC, on-prem infrastructure, or air-gapped environment. Developers describe the work they want done, and Coder Agents provisions isolated environments where agents can execute tasks, run tests, and modify code.

For platform teams, Coder Agents provides a consistent way to deploy and govern coding agents across the organization. Agents run within standardized, policy-controlled environments defined by infrastructure templates, with role-based access control, audit logs, and network policies applied by default. This allows teams to distribute agents to developers with the same level of control, visibility, and repeatability as any other critical system.

## Taglines

- AI coding agents on your infrastructure
- Run AI coding agents inside your perimeter
- Your infrastructure. Your agent.
- The self-hosted alternative to Cursor Agents

## Problem Areas

### Use Case 1: Data Residency and Sovereign AI

**Desired Outcome:** Engineering teams at regulated enterprises adopt AI coding agents at scale, without routing proprietary source code through third-party cloud infrastructure, violating data residency requirements, or failing compliance audits.

**Pain Points:** Cloud-only agents require code to leave the perimeter, legal/compliance blocks adoption. Shadow IT usage is already happening with no audit trail. DIY approaches lack governance and maturity. Security review cycles for new AI tooling take 6-12 months.

**Coder's Solution:** Coder Agents runs self-hosted inside the enterprise's VPC, on-prem data center, or air-gapped enclave. Every session runs in a Terraform-provisioned workspace with a full network solution. Connect any approved model, including self-hosted open-weight models for fully on-premises inference.

### Use Case 2: Avoiding Vendor Lock-In to a Single Proprietary AI Provider

**Desired Outcome:** Enterprises adopt an AI coding agent without being locked into a single model provider's pricing, capabilities, roadmap, or contractual terms.

**Pain Points:** Claude Code = Anthropic only. Codex = OpenAI only. Frontier model leadership rotates every few weeks. Lock-in eliminates negotiating power. Some orgs need self-hosted open-weight models for cost or sovereignty.

**Coder's Solution:** Coder Agents is LLM-agnostic. Connects to Anthropic Claude, OpenAI GPT, Google Gemini, or OpenAI-compatible self-hosted models. Switching models is a configuration change, not a platform migration. Run different models for different teams, use cases, or cost tiers.

### Use Case 3: Scaling AI Agents on Existing Coder Infrastructure

**Desired Outcome:** Platform teams already running Coder workspaces extend their existing infrastructure to support autonomous AI coding agents, no new platform, no new security review, no new vendor assessment.

**Pain Points:** Adopting a new agent platform means a new vendor, new SOC2 assessment, new SSO integration, new cost monitoring, 6+ months of procurement. Developers want agents now. The gap creates shadow IT.

**Coder's Solution:** Coder Agents runs inside Coder workspaces, same Terraform templates, same RBAC, same audit logs, same dashboard. Platform teams enable agents by extending workspace templates they already manage. Agents enjoy the full benefits of the same Coder deployment platform teams already manage.

### Use Case 4: Headless Agent Orchestration from External Workflows

**Desired Outcome:** Production errors trigger an end-to-end remediation loop, investigation, fix, multi-dimensional code review, and merge with minimal human involvement, all running on internal infrastructure.

**Pain Points:** Incident response is manual, slow, and expensive after hours. Engineers context-switch from feature work to triage. Existing CI/CD pipelines can detect failures but can't reason about fixes. Cloud-hosted agents can't be triggered programmatically from internal CI or operate inside network-restricted environments.

**Coder's Solution:** A CI webhook triggers Coder Agents via the Coder Agents API. An agent provisions a workspace, analyzes the failure, correlates it with recent commits, identifies the root cause, and opens a pull request with a fix. Review agents evaluate the change in parallel, and once approved, the agent updates the PR and merges it, all running self-hosted within your infrastructure.

### Use Case 5: AI Adoption Observability for Platform Teams

**Desired Outcome:** Platform engineering has full visibility into how AI coding agents are used across the organization, adoption rates, model effectiveness, cost per outcome, and merge rates to justify investment and optimize spend.

**Pain Points:** AI tooling budgets are approved on faith, not data. No way to measure which models perform best for which workloads. No attribution between agent activity and engineering outcomes (PRs merged, CI pass rate, time-to-merge). Shadow AI usage makes ROI measurement impossible.

**Coder's Solution:** Coder's AI Gateway records every interaction in the agent workflow, including prompts, token usage, model selection, and tool invocations, with each action attributed to an individual user. This data is available through AI Gateway's API, allowing platform teams to export it into tools like Grafana to analyze agent activity and track costs.

## Value Props / Differentiators

| Value Prop | Why It Matters |
| :---- | :---- |
| Self-Hosted | Agent orchestration, tool execution, and source code stay inside your perimeter. With self-hosted models, inference stays in-perimeter too, enabling fully air-gapped operation. |
| LLM-Agnostic | Works with any frontier model. Switch providers without switching agents. No vendor lock-in. |
| Terraform-Provisioned Agent Workspaces | Every session runs in reproducible, IaC-defined workspaces. Same templates, same lifecycle as human dev environments. |
| Headless Autonomous Execution | Agents run background tasks with no IDE tethered. Dashboard visibility, CI/CD integration, human-in-the-loop review. |
| Zero-Incremental-Platform for Coder Customers | Existing Coder users adopt Coder Agents with no new platform, no new security review. Days to production, not months. |
| First-Class User Experience | A polished, intuitive experience with the right ergonomics is table stakes for adoption. |
| Centralized Agent Distribution | Platform teams deploy coding agents once and make them available across the organization. No fragmented configurations, and no shadow AI usage. |

## Supporting Features

### Architecture

- **Control-plane agent loop** - the agent runs inside the Coder control plane, not in the workspace. No sidecar, no new network paths, no separate service to deploy.
- **Same Tailnet connection** - the agent reaches workspaces over the same tunnel used by web terminals, VS Code Remote, and SSH. No additional ports or services required.
- **No inbound ports** - the workspace daemon dials out to the control plane, never the reverse. All inbound traffic to the workspace can be blocked.
- **Lazy workspace connection** - workspace connections are established only when tool execution is needed. Chats that don't require workspace access (planning, architecture, Q&A) start instantly with no provisioning delay.
- **Automatic workspace provisioning** - the agent reads template descriptions and parameters, selects the appropriate template, and provisions a workspace without developer input.

### Agent Capabilities

- **Sub-agent delegation** - the root agent spawns child agents to work on independent tasks in parallel, each with its own context window to avoid quality degradation from context growth.
- **Context compaction** - as conversations grow, the agent automatically summarizes older context to stay within the model's context window. Earlier messages remain in the database for user review.
- **Message queuing** - users can send follow-up messages while the agent is working. Messages are queued and delivered when the agent completes its current turn.
- **Chat persistence** - all chat state is stored in the control plane database, not the workspace. History survives workspace stops, rebuilds, and deletions. Agents can resume work by targeting a new workspace.
- **Projects** - users can group multiple related chats into a project. Memory shared within a project is available to other agents working in that same project, so context carries across chats instead of staying siloed in a single conversation.
- **Built-in tool set** - file read/write, atomic multi-file search-and-replace edits, shell execution (foreground and background), process management (list, output, signal), template browsing, and workspace creation.

### Security

- **Zero API keys in workspaces** - LLM provider credentials exist only in the control plane. Nothing for a developer, compromised dependency, or rogue process to exfiltrate.
- **Full workspace network isolation** - workspaces need outbound access only to the control plane and your git provider. Everything else can be blocked. Agent workspaces need no outbound access to LLM providers.
- **User identity on every action** - every agent action (PRs, commits, commands) is tied to the user who submitted the prompt. No shared bot account or anonymous identity.
- **No agent software in workspaces** - no Claude Code, Codex, or agent harness installed. Eliminates supply chain risk and per-workspace agent maintenance. A workspace created by the agent looks identical to one a developer created manually.

### Platform Controls

- **Centralized provider and model configuration** - admins configure LLM providers, API keys, base URLs (for enterprise proxies or self-hosted models), and per-model parameters (context limits, thinking budgets, reasoning effort) from the dashboard. Developers can select from enabled models; they cannot add providers or supply their own keys unless the admin allows it.
- **Admin-controlled system prompt** - admins set an organization-wide system prompt (coding standards, commit formats, preferred libraries). Enforced server-side, developers do not see or interact with it.
- **Template routing** - platform teams guide agent template selection by writing clear template descriptions. Developers don't need to understand template selection.
- **Enforcement, not defaults** - all agent configuration is admin-level policy enforced server-side, not user preferences developers can override. When an admin removes a model or modifies the system prompt, the change applies to all sessions immediately.

### Model Provider Support

Anthropic, OpenAI, Google, Azure OpenAI, AWS Bedrock, OpenRouter, Vercel AI Gateway, and any OpenAI-compatible endpoint, including enterprise LLM proxies, self-hosted model endpoints, and internal gateways via custom base URLs. Multiple providers can be configured simultaneously.

## Market Landscape

**Core Thesis:** We've already solved the hard part, native AI development, self-hosted infrastructure, enterprise governance, workspace orchestration at scale. AI providers are trying to work backward from AI into infrastructure. We're working forward from infrastructure into AI. The hard part is behind us; the UI/UX layer is what remains.

**Why This Asymmetry Exists:** Running a self-hosted control plane, Terraform-provisioned workspaces, secure tunnel connectivity, air-gapped deployments, and enterprise identity integration are hard distributed systems problems. Coder has invested years of engineering effort solving them for human developer workspaces, and that same infrastructure extends naturally to AI agents. AI providers building agent-first products are solving these problems for the first time, on a much shorter timeline.

**By Player:**

- **Cursor** - Cursor offers a hybrid self-hosted option: agent orchestration and model inference run in Cursor's cloud, while execution connects out to a self-hosted environment, such as a Coder workspace. That hybrid model is a fit for organizations willing to keep orchestration and inference off-premises, and Coder Agent Relay helps those customers connect Cursor's cloud-based orchestration to a self-hosted execution environment. It is not acceptable to highly regulated enterprises and government agencies that require everything, orchestration, inference, and execution, to run fully self-hosted and air-gapped. For those organizations, Coder Agents is the fully self-hosted, air-gapped solution; Cursor's hybrid model is not viable.
- **Claude Code (Anthropic) / OpenAI Codex** - Terminal-native agents that have some capability to run outside the terminal, but largely in cloud-based deployment models with limited governance and no easy path to fully air-gapped, self-hosted operation at scale. As the performance gap between agents narrows, the agent layer itself becomes less of a differentiator: developers use Claude Code to get access to Claude, and Codex to get access to GPT. The agent is largely the vehicle to reach the frontier model. Coder Agents offers that same model access, Anthropic, OpenAI, Google, AWS Bedrock, and self-hosted open-weight models agnostically, out of the box, on infrastructure the enterprise already controls.
- **Devin (Cognition)** - Primarily a cloud-only SaaS, though Cognition also offers a VPC deployment option that is more palatable than pure cloud-only for some buyers. Cognition lists on-prem and air-gapped operation for Devin's CLI and desktop editor, and its federal FAQ describes those versions as still being finalized, but Devin's reasoning layer, the "brain" that plans and drives the agent, always runs in Cognition's cloud, including in the VPC option, with no documented air-gapped path for that cloud-hosted agent. It also does not integrate with existing enterprise identity or infrastructure in the way regulated enterprises and government agencies require for the full agent loop. It demonstrates well, but enterprises that need the agent's orchestration and reasoning, not just its CLI or editor, to run air-gapped cannot adopt it for that use case.
- **Agentic IDEs (Windsurf, Zed, Kiro, etc.)** - Not competitors. These are text editors with agentic extensions, a different class of tool. Coder Agents is not looking to displace the IDE. Developers still connect to workspaces via VS Code, Cursor, JetBrains, or any other editor to review, refine, and complete work the agent produces. Agentic IDEs complement Coder Agents the same way traditional IDEs do; they are the place developers go after the agent has done its work, not an alternative to it.

## Target Market / ICP

**Primary Market:** Two motions, one ICP.

- **Existing Coder Customers** - Organizations already running Coder for their human developers. They've already procured the platform, integrated identity, built templates, and trained teams. Coder Agents is a new solution on infrastructure they already own, not a new tool to evaluate, procure, and secure. These customers are advancing along the AI fluency maturity curve and need a way to distribute coding agents quickly without introducing another class of tooling or going through another procurement cycle.
- **Organizations that have not yet adopted Coder** - A much larger market with the same profile: regulated, governance-sensitive, and requiring self-hosted infrastructure, but not yet using Coder for human developer workspaces. For these organizations, Coder Agents often becomes the reason they first evaluate Coder. The need that brings them to the table is straightforward: give developers native AI coding agents without sending source code to a third party. Coder's workspace infrastructure is what makes that possible, even though it may not be the initial motivation for evaluating the platform.

The logic that drives a traditional Coder Workspace-first purchase is the same logic that drives a Coder Agents purchase. If an organization needs centralization and governance over development environments for human developers, they need centralization and governance over development environments for AI agents, for the same reasons. The infrastructure and architecture are the same. The end user changes from a human to an agent. Everything else, identity, network policies, audit requirements, compliance posture, stays the same.

The same need extends beyond professional developers. Organizations that want a governed, standardized way to distribute agents to engineering-adjacent knowledge workers or citizen developers are also a strong fit.

## Buyer Personas

See [Buyer Personas](../../audiences/personas/overview.md) for the canonical definition of each persona. The application to Coder Agents is below.

### Protectionist

Protectionists face competitive pressure to adopt AI coding agents quickly, but uncontrolled usage introduces existential risk: source code leaving the perimeter, no audit trail, and compliance exposure that can jeopardize deals or trigger regulatory action. Coder Agents removes that tradeoff. Developers get native AI coding agents on infrastructure the organization already controls, with full auditability, so the business can move faster without taking on unmanaged risk.

### Opportunist

Opportunists want AI coding agents to be a productivity multiplier, not a cost center or a shadow IT liability. Coder Agents is a zero-incremental-platform for existing Coder customers: no new security review, no fragmented per-developer tooling, and no vendor lock-in from switching models. Headless, background agent execution lets an organization throw compute at problems, running parallel sub-agents and CI-triggered workflows, so throughput scales with infrastructure rather than headcount.

### Caring Provider

Developers are adopting AI coding agents whether platform teams distribute them or not, and Caring Providers, whether platform engineers responsible for their developer population or developers themselves, want that adoption to happen with a great experience rather than as fragmented shadow IT. Coder Agents gives platform teams a single place to distribute a native coding agent to their developer population, with centralized oversight and observability built in, while remaining a first-class developer experience rather than a locked-down portal developers route around. For an individual developer, the agent provisions a workspace, writes the code, runs the tests, and opens the PR in the background, unsupervised and safely sandboxed. Developers can check progress from their phone, review the diff on their laptop when ready, and pick up in their editor to refine the result. It works with the models developers would choose anyway, including Claude, GPT, and Gemini, without needing to manage API keys, configure an agent, or request access from IT.

## Vertical Messaging

### Government

- Runs fully air-gapped with no external network dependencies. The agent loop, model inference (via self-hosted open-weight models), and workspace execution all operate within your security boundary.
- Deployable in classified environments across impact levels.
- No SaaS component, no telemetry, no external call-home. The entire stack runs on infrastructure your agency owns and your team operates.
- Meets the bar for ATO conversations today, self-hosted, auditable, identity-attributed, and running on compute you already accredit.

### Regulated Industries

- Source code and agent execution are co-located in the same geography on infrastructure you control. Data sovereignty is an architectural guarantee, not a vendor promise.
- LLM credentials never enter the workspace. Workspaces can be network-restricted to only your git provider and control plane, eliminating data exfiltration vectors.
- Every agent action is attributed to a named user with a full audit trail. No shared bot accounts, no anonymous execution, no gaps in your compliance record.
- Connect to model providers hosted in your region, or run self-hosted open-weight models on-premises. Your data residency posture extends to your AI tooling, not around it.

### Tech Innovators

- Ship agents to every developer in days, not quarters. No per-developer configuration, no API key distribution, no agent software to install. The platform team enables it, developers start using it.
- Fire off background tasks and move on. Agents provision their own workspaces, write code, run tests, and open PRs unsupervised. Developers review results when they're ready, from their laptop, phone, or editor.
- First-class developer experience is the priority, not a tradeoff for governance. Developers get the models they want, the speed they expect, and a UI they don't route around.
- Parallel sub-agents let you throw compute at problems, 10 agents reviewing a PR, 300 agents migrating a codebase, continuous background agents triggered from CI. Move at the speed of your infrastructure, not your headcount.

## Partner Narrative

**Core Framing:** Coder Agents is a consumption multiplier for our partners, not a competitor to any of them. Every agent task provisions a workspace, that's compute. Every prompt hits a model, that's inference. The more agents our customers run, the more resources they consume on partner infrastructure.

### AWS

- Every Coder Agents workspace is an EC2 instance, an EKS pod, or an ECS task running in the customer's AWS account. More agents means more compute consumption. A single migration use case spinning up 300 parallel agents is 300 concurrent workspaces on AWS infrastructure.
- Customers using Bedrock for model inference get the same benefit. Coder Agents natively supports AWS Bedrock as a provider. Every prompt, every sub-agent, every context compaction cycle is Bedrock inference the customer is paying AWS for.
- Coder doesn't host anything. We don't compete for the infrastructure dollar. We're the reason the infrastructure dollar gets spent, another line item that drives consumption toward a customer's AWS commitment.

### Model Providers

Model providers benefit directly from Coder Agents' growth. Their models power every agent interaction: when a customer configures Claude via the Anthropic API, GPT via OpenAI, or Gemini via Google, every agent interaction is inference revenue for the provider.

Coder Agents also makes these models accessible in environments they otherwise couldn't reach. A bank running air-gapped infrastructure can't use Claude Code, but it can use Claude models through Coder Agents via Bedrock or a self-hosted proxy, expanding the addressable market for model providers into regulated enterprise.

### Cloud Providers (Azure, GCP)

Same dynamic as AWS. Azure customers run Coder Agents workspaces on Azure VMs or AKS, and access models via Azure OpenAI. GCP customers run workspaces on GCE or GKE and access models via Vertex AI. Coder is cloud-agnostic; wherever the customer runs, Coder Agents drives consumption on that cloud.
