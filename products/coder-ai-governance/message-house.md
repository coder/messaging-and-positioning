# AI Governance Message House

AI Governance is the Modernize stage of the [customer journey](../../company/customer-journey.md), typically adopted alongside Coder Workspaces. See [The AI Operating Layer](../../company/ai-operating-layer.md) for the underlying argument this product is built on.

## Status Quo

### Without AI Governance

Currently teams across industries are in an "experimentation" phase where builders are using every "it" AI tool, but lack visibility into what is actually working, what is failing, and what should be scaled. Teams are adding AI to development in ad hoc ways. Developers commonly use tools like GitHub Copilot, Cursor, Claude Code extensions, and JetBrains AI Assistant, alongside general tools like ChatGPT and custom agents across laptops, VMs, and cloud services. These workflows sit outside standard or centralized development environments, with inconsistent setups and loosely controlled access to models, prompts, and data. As AI usage scales, this creates gaps in governance, security, and cost control.

The challenges multiply, as AI agents for long-running or automated tasks gain access to sensitive data, ingest untrusted inputs, and communicate externally (lethal trifecta), increasing the risk of data exfiltration, prompt injection, and automated misuse.

- Teams lack visibility into what agents are executing or accessing, with no centralized record of prompts, responses, or tool usage to evaluate effectiveness, risk, or cost.
- Organizations cannot attribute token usage by team, project, or workflow, or determine which AI usage is effective versus wasteful.
- Developers widely use AI assistants and agents outside approved tooling, creating shadow AI and uncontrolled model access.
- Organizations assume models will police themselves, leaving gaps in infrastructure, access control, and monitoring.
- Developers embed LLM credentials across laptops, scripts, and repositories with no centralized revocation.
- Many organizations are hesitant to push autonomous agents into production because security best practices and infrastructure guardrails are not yet in place.

## The 3 Whys

### Why Do Anything?

AI is already embedded in modern software development, but it is being adopted in fragmented and uncontrolled ways. Developers are using AI tools and agents across laptops, IDEs, and cloud services without centralized oversight, creating shadow AI, unmanaged credentials, and little visibility into how sensitive code and data are accessed. At the same time, AI agents are no longer passive assistants. They can execute commands, access systems, and communicate externally, introducing new risks that traditional security models were not designed to handle. Without governance and best practices in place, organizations cannot effectively control risk, ensure accountability, or standardize AI usage across teams.

### Why Now?

The need for AI governance is especially urgent now as enterprises move rapidly from experimentation to production AI workflows. Organizations face a critical tradeoff: blocking AI slows innovation, while enabling it without controls introduces significant security, compliance, and cost risks. The rise of autonomous agents, increased exposure of internal systems, and growing pressure on platform teams to enable AI safely at scale make governance foundational and not optional. AI is already present in development workflows, and the real question is whether it operates in the shadows or within governed infrastructure.

### Why Coder?

Coder provides the governed AI infrastructure layer that enables organizations to move from experimentation to auditable AI development. AI Governance, included in Coder Premium and made up of AI Gateway and Agent Firewall, centralizes model access, credential management, and network policy enforcement for AI activity running inside Coder Workspaces. Coverage differs by component: AI Gateway's model-level governance applies to Coder Agents and to supported third-party clients such as Claude Code and Codex, while Agent Firewall's network policy applies to the agent processes it wraps inside a workspace. Coder reduces blast radius, delivers full observability into AI activity, and gives organizations the foundation to scale AI adoption while maintaining visibility, control, and compliance.

## What's Included

AI Governance is Coder's name for the capability set included in Coder Premium, made up of two products:

- **AI Gateway** (formerly named AI Bridge): the LLM gateway that centralizes model access, authentication, auditing, and cost controls.
- **Agent Firewall** (formerly named Agent Boundaries): the process-level network firewall that restricts and audits what agent processes can reach from inside a workspace.

Both have been generally available since Coder v2.30 (February 2026) and require a Premium license; Community deployments cannot access them. Coder Agents and Coder Agent Relay are separate, complementary Coder capabilities, not part of the AI Governance license itself, though they integrate with it directly: Coder Agents routes all of its model traffic through AI Gateway automatically, so AI Gateway's audit trail and budgets apply to it out of the box.

## Messaging Statement

### Short (~50 words)

For platform and security leaders enabling AI development, uncontrolled agent usage, shadow AI, and lack of visibility create serious risk. Coder Workspaces already lets teams run AI agents in self-hosted, isolated environments. Coder AI Governance is what makes doing that safe at enterprise scale: centralized model access, policy enforcement, and full auditability over every agent action. Unlike tools that only govern model access, Coder governs the infrastructure layer where agents run, delivering the control, visibility, and protection enterprises need for safe, scalable AI adoption.

### Medium (~100 words)

For platform engineering and security teams tasked with enabling AI adoption, the rise of autonomous agents introduces risks like shadow AI, API key sprawl, and lack of visibility into how code and data are accessed. Existing tools fail to control where agents run or how they behave. Agents already run in isolated, ephemeral Coder Workspaces, but running them there isn't the same as governing them. Coder AI Governance adds that layer: AI Gateway centralizes and audits every model interaction, and Agent Firewall enforces network policy on agent processes, together providing policy enforcement, usage attribution, and complete observability across prompts, tools, and agent actions.

Unlike solutions focused only on model gateways or IDEs, Coder delivers infrastructure-level governance controlling execution and network access on top of the workspace infrastructure agents already run in. The result is a secure, standardized foundation that allows teams to scale AI development confidently without sacrificing control or compliance.

### Long (~250 words)

For enterprise platform engineering and security leaders responsible for enabling AI-driven development, the rapid adoption of AI agents introduces new and urgent risks. Developers are increasingly using AI tools and autonomous agents across laptops, scripts, and cloud services, creating shadow AI, fragmented tooling, API key sprawl, and little to no visibility into how sensitive code and data are accessed or exposed. Traditional security controls are not designed for agents that can execute commands, ingest untrusted inputs, and communicate externally at scale.

Coder Workspaces already gives organizations a way to run AI agents inside isolated, ephemeral, self-hosted environments instead of on unmanaged laptops. But running an agent inside a workspace isn't the same as governing it: without additional controls, that agent can still make unrestricted network calls, use unmanaged provider credentials, and leave no audit trail. Coder AI Governance closes that gap. AI Gateway centralizes every interaction with language models, eliminating API key sprawl and providing a secure gateway for authentication, policy enforcement, budget enforcement, and detailed auditing, whether it runs embedded in the control plane or as an independently scalable standalone service. Organizations gain full visibility into prompts, tool usage, token consumption, and agent actions, with user attribution for auditability and compliance. Agent Firewall complements this by enforcing default-deny, domain-level network policy on agent processes running inside a workspace, with every decision logged and correlated back to the corresponding AI Gateway session.

What differentiates Coder is its infrastructure-first approach. Rather than focusing solely on model access or post hoc monitoring, Coder AI Governance governs how AI agents run on top of Coder's existing workspace infrastructure, controlling network access and model interactions instead of requiring a separate, disconnected governance tool. This enables organizations to standardize AI tooling, reduce risk, and transform experimental AI usage into secure, scalable, production-ready workflows.

## Taglines

- Safe AI starts with governed infrastructure
- Full visibility from prompt to production
- See everything your AI agents do
- Every AI coding agent needs governed infrastructure
- Govern AI development at the speed of developers
- Run AI agents with control and clarity
- The control plane for safe AI-driven development
- Secure infrastructure behind AI agents
- Bring AI development out of the shadows
- AI Governance empowers teams to safely scale AI-driven development
- Coder is safe mode for AI

## Use Cases

### Use Case 1: Secure Execution for AI Agents

**Desired Outcome:** Run AI agents in controlled environments where access to code, infrastructure, and credentials is tightly managed.

**Challenges:** Agents running on developer laptops inherit access to SSH keys, credentials, and local files. Agents can install packages, execute commands, and access networks without restrictions. A compromised or misbehaving agent can affect multiple systems.

**Coder's Solution:** Coder Workspaces already isolates agents from developer laptops by running them in ephemeral, self-hosted environments with RBAC. AI Governance adds the enforcement layer on top: Agent Firewall applies default-deny network policy, domain, HTTP method, and path rules, to agent processes running inside the workspace, limiting blast radius and enforcing least-privilege execution.

### Use Case 2: AI Activity Visibility, Audit, and Forensics

**Desired Outcome:** Maintain a complete and auditable record of AI activity for monitoring, compliance, and forensic investigation when agents misbehave.

**Challenges:** No ability to reconstruct agent behavior or investigate incidents when agents act unexpectedly or maliciously.

**Coder's Solution:** AI Gateway enables forensic analysis by providing a searchable, time-ordered record of prompts, tool usage, model interactions, and agent actions with user attribution, organized into interceptions, threads, and sessions. Agent Firewall's network decisions are correlated directly into that same session view, so teams can investigate incidents, understand root causes, and respond effectively.

### Use Case 3: Control Usage and Cost

**Desired Outcome:** Control AI usage costs with visibility into token consumption, attribution across users, and quota management.

**Challenges:** Developers use multiple AI tools across IDEs, scripts, and agents with personal API keys. Security and platform teams lack visibility into model usage and data exposure. It's hard to determine effective vs. wasteful usage. There is a lack of predictability in token usage, model consumption, and cost attribution across users.

**Coder's Solution:** AI Gateway enforces per-user and per-group budgets before requests are forwarded to a model provider, with configurable notification thresholds as spend approaches its limit. Platform teams get organization-wide spend reporting with CSV export by user, provider, and model, spend attribution down to the workspace, and Prometheus metrics for cost and enforcement, giving them the visibility to monitor, allocate, and optimize AI spend across users.

### Use Case 4: Protecting Sensitive Code and Data

**Desired Outcome:** Prevent proprietary code and internal data from being leaked or manipulated through AI agents.

**Challenges:** Agents ingest untrusted inputs such as third-party docs, dependencies, or issue threads. Prompt injection attacks can influence agent behavior. Agents with unrestricted network access can exfiltrate sensitive information.

**Coder's Solution:** Apply execution and network boundaries that restrict external communication and network access. Combined with centralized monitoring of AI interactions through AI Gateway, this reduces the conditions that enable data exfiltration and prompt injection.

### Use Case 5: Standardizing AI Tooling Across Developers

**Desired Outcome:** Provide a consistent and approved AI tooling environment for developers across teams.

**Challenges:** Developers adopt different AI tools independently. Platform teams cannot enforce approved tools or configurations. Tool fragmentation creates inconsistent environments and governance gaps.

**Coder's Solution:** Coder provides standardized AI-enabled development environments through workspace templates and centralized tooling configuration. AI Gateway centralizes which model providers are approved, and organization-scoped MCP server management lets platform teams define approved MCP tools with group and user access controls, ensuring developers use approved models, tools, and security policies.

### Use Case 6: Managing Workloads Triggered by AI Agents

**Desired Outcome:** Allow teams to manage AI agents as operational workloads with standardized infrastructure and controls.

**Challenges:** Autonomous agents run long tasks and require compute resources. Agents introduce new workloads for platform teams. Existing infrastructure is not designed to manage agent execution at scale.

**Coder's Solution:** Coder treats agents as managed workloads inside ephemeral workspaces, enabling admins to orchestrate, monitor, and isolate agent execution. For high-volume deployments, AI Gateway can also run as an independently scalable standalone service outside the Coder control plane, with its own health checks, metrics, and tracing, so gateway capacity can scale separately from `coderd` as agent-driven traffic grows.

## Value Props / Differentiators

- **Govern agents that already run in isolated Coder Workspaces**: Coder Workspaces runs agents in secure, ephemeral cloud environments instead of on developer laptops. AI Governance adds the policy, audit, and cost control layer that makes running agents there safe to do at enterprise scale.
- **Govern third-party and Coder-native AI agents**: Most tools control model access. Coder governs the environments where third-party and Coder agents run, ensuring they operate inside secure, policy-controlled infrastructure.
- **Centralize and govern AI model access**: Route model interactions through AI Gateway to manage how agents and IDEs access LLMs, whether that's OpenAI, Anthropic, AWS Bedrock, Azure OpenAI, Google, GitHub Copilot, OpenRouter, Vercel AI Gateway, or any self-hosted OpenAI-compatible endpoint.
- **Provide visibility and auditability of AI activity**: Track prompts, tool calls, and agent actions with user attribution for security monitoring and compliance.
- **Standardize secure AI development workflows**: Give developers approved environments and tools so AI usage happens inside governed infrastructure instead of unmanaged setups.
- **Scale governance independently of the control plane**: Deploy AI Gateway as a standalone, horizontally scalable service when gateway traffic needs to scale beyond what the embedded control plane deployment handles.

## Supporting Features

Coder enables AI governance through a set of infrastructure capabilities that control where agents run, what they can access, and how they interact with models and external systems. These features provide the safeguards required to safely deploy and scale agents within enterprise development environments.

### Infrastructure Layer

**Coder Workspaces (Cloud Development Environments & Workspace Templates):** Self-hosted ephemeral workspaces defined through infrastructure-as-code templates that standardize development environments, dependencies, and security configurations for agents and developers.

### AI Governance Layer

Coder AI Governance provides centralized control and visibility over how AI agents and models are used, enabling secure and compliant adoption.

**AI Gateway:** A policy-aware intermediary that brokers, authenticates, and logs all model interactions.

- Runs embedded in the Coder control plane by default, or as an independently scalable standalone service with its own Helm chart, health checks, and metrics for high-volume deployments.
- Centralizes authentication so users authenticate with their existing Coder credentials instead of managing individual provider API keys, with optional bring-your-own-key (BYOK) support for personal provider or subscription credentials.
- Connects to OpenAI, Anthropic, AWS Bedrock (including a native Anthropic-passthrough mode), GitHub Copilot, Azure OpenAI and Google via their OpenAI-compatible endpoints, OpenRouter, Vercel AI Gateway, and any self-hosted OpenAI-compatible endpoint, with automatic key-pool failover across up to five centralized keys per provider.
- Enforces per-user and per-group spend budgets before requests are forwarded, with configurable notification thresholds and organization-wide spend reporting.

**Observability & Tool Governance:** Capture prompts, reasoning, and tool usage, correlating them into searchable sessions and threads to show how AI actions occur. Session views also surface Agent Firewall's network activity for that session, so prompt-level and network-level activity can be reviewed together. Metrics and traces export to Prometheus, Grafana, and OpenTelemetry, and structured records can feed existing log pipelines.

**MCP Governance:** Organization-scoped MCP server management with group and user access controls, tool allow/deny lists, and configurable availability policies, giving platform teams a way to define approved MCP tools and servers that all users can access in a consistent, auditable way.

### Agent Execution Layer

**Agent Firewall:** A process-level, default-deny network firewall for agent processes running inside a workspace. It enforces domain, HTTP method, and URL path rules, and every policy decision is logged to the control plane and correlated with the corresponding AI Gateway session for a unified view of prompt and network activity.

**Identity, Access, and Audit Controls:** Role-based access control, audit logging, and user attribution that track prompts, tool calls, and agent actions for governance and incident response.

## Governance Scope

- **Network policy granularity**: Governance is enforced through workspace isolation, infrastructure boundaries, and domain/method/path-level network controls. Per-directory or per-file runtime policy is not part of the current model.
- **SIEM integration path**: Prometheus, Grafana, OpenTelemetry, and structured log export are the supported observability path today. Purpose-built, native integrations with specific enterprise SIEM platforms are on the roadmap.
- **MCP governance model**: Coder Agents' organization-scoped MCP server management is the current, actively developed governance path for MCP tools; AI Gateway's original in-gateway MCP tool injection has been superseded by it.
- **Agent Firewall enforcement depth**: Agent Firewall enforces domain, method, and path-level policy on HTTP and HTTPS. Rules cannot express ports, CIDRs, or protocols, so non-HTTP TCP is blocked rather than policy-controlled, and UDP is not mediated under the landjail backend. Process-level isolation and UDP control are active areas of investment.
- **Positioning AI Governance**: AI Governance (GA'ed February 2026) manages and audits AI agents within development environments. It is one layer of a broader security posture, not a standalone solution for every class of AI-related risk.
- **Industry-specific requirements**: Security requirements vary by industry, and highly regulated sectors such as federal and financial services often require controls beyond any single vendor's default configuration. Coder is frequently deployed alongside complementary security tooling for this reason.

## Competitive Position

Our competitors in AI governance for software development are not always direct product equivalents. Most competitors fall into three adjacent categories: AI gateways, agentic IDEs, and developer AI platforms with governance features. Competitors are attempting to bolt governance onto AI tools after the fact. Coder approaches the problem from the opposite direction: Coder meets customers where they are, whichever AI provider or AI tool they want to use, we'll support it.

**General positioning:** Most AI governance solutions focus on model inputs and outputs, such as prompt filtering, detection, and model-level controls. Coder provides a unified platform where developers and AI agents can operate within governed infrastructure. Rather than attempting to secure agents directly, Coder ensures all development and agent execution happens within approved, policy-controlled environments with observable, auditable, and cost-controlled access to AI services. This enables organizations to adopt AI while maintaining consistent governance and operational control.

**Coder vs. lightweight sandboxes:** A sandbox is not a solution to agent governance, it's a feature of AI development infrastructure. Isolating an agent's execution reduces the blast radius of a single session, but it doesn't provide model access control, prompt and tool-use logging, user attribution, or organization-wide policy enforcement. Coder Workspaces already isolates agent execution the way a sandbox would; AI Governance is what makes that isolation auditable, policy-enforced, and consistent across every workspace, not just resilient within one.

**Coder vs. Cursor:** Cursor connects to Coder in two different ways, and governance coverage differs between them. Developers can point their local Cursor IDE at a Coder workspace over SSH to access files, but in that mode the Cursor agent itself still runs on the developer's local machine; worktrees, agent orchestration, and terminal execution happen client-side, not inside the Coder workspace, so none of Coder's governance applies to that activity. Alternatively, Cursor's cloud agent can execute inside a self-hosted Coder workspace through Coder Agent Relay, keeping agent orchestration and inference in Cursor's cloud while tool execution, and the source code, tools, and credentials it touches, runs on infrastructure Coder governs. In that mode, workspace-level controls (network policy via Agent Firewall, secrets, RBAC) apply to the execution environment. Either way, Cursor isn't a supported AI Gateway client today, so its LLM calls bypass AI Gateway's model-level auditing regardless of deployment mode. Coder's value is infrastructure governance over wherever agent execution actually happens; visibility into the model orchestration and reasoning inside Cursor itself is out of scope in both cases.

**Coder vs. LiteLLM:** LiteLLM standardizes how applications access LLMs through routing, unified APIs, and usage tracking. It manages model access, not execution. Coder governs both: agents already run inside isolated Coder Workspaces, and AI Governance layers centralized model access via AI Gateway and network policy via Agent Firewall on top of that, controlling agent behavior, data access, and network communication in a way a model-routing tool alone cannot.

**Coder vs. Devin:** Devin is primarily delivered as multi-tenant cloud SaaS, though Cognition also offers a dedicated, single-tenant VPC deployment for enterprise customers, connected via AWS PrivateLink or an IPSec tunnel. That VPC is still hosted and operated by Cognition, not the customer. Cognition lists on-prem and air-gapped operation only for the Devin CLI and desktop editor, and its federal FAQ describes those versions as still being finalized; Devin's reasoning layer (the "brain") always runs in Cognition's cloud, including in the VPC deployment, and Cognition does not document an air-gapped option for that cloud-hosted agent. Model choice is also limited to the models Devin offers rather than an open model-access layer. Coder enables organizations to run AI agents on infrastructure they fully own and operate, self-hosted, on-prem, or air-gapped, including the agent loop itself, and AI Governance adds the audit trail, model access controls, and network policy enforcement needed to meet enterprise security and data residency requirements that Devin's Cognition-hosted model doesn't fully address.

## Target Market / ICP

AI Governance is a Coder solution that provides control over how AI agents run, what they can access, and how they interact with models and external systems. It adds enforceable policies and auditability to existing development workflows.

The primary ICP aligns with Coder's CDE audience: mid-size to large enterprises with 2,000+ employees and 200+ developers, especially those with ML or data teams.

However, AI agent adoption is the strongest signal. Organizations actively experimenting with or deploying AI agents are the most likely early adopters, regardless of company size.

**Organizations deploying** Cursor, Claude Code, GitHub Copilot, or internal agents are high-intent opportunity targets.

## Buyer Personas

See [Buyer Personas](../../audiences/personas/overview.md) for the canonical definition of each persona. The application to AI Governance is below.

### Protectionist

**Common pain points:** Lack of governance over AI agents accessing sensitive code and internal data. Shadow AI usage across engineering teams. Limited visibility and auditability of prompts, model usage, and agent actions. Risk of data exfiltration, prompt injection, and uncontrolled model access.

Coder AI Governance gives Protectionists control over the security risks introduced by AI agents in software development. Coder Workspaces already moves agents off developer laptops and into isolated, ephemeral environments, removing unrestricted access to local credentials and files. AI Governance is what makes running agents there auditable and controlled at the enterprise level: AI Gateway centralizes model access and logs prompts, tool usage, and user attribution for audit and incident response, while Agent Firewall's network boundaries reduce the risk of data exfiltration, prompt injection, and unauthorized actions. This allows the organization to adopt agentic AI while maintaining governance, visibility, and a reduced attack surface.

- Coder Workspaces already isolates agents from developer laptops; AI Governance adds the audit trail and policy enforcement on top
- Centralized logging of prompts, tool usage, and user attribution for audit and incident response
- Network boundaries that reduce the risk of data exfiltration, prompt injection, and unauthorized agent actions

### Opportunist

**Common pain points:** Pressure to enable AI adoption while maintaining platform security and standards without adding operational overhead. Fragmented AI tooling across teams creating cost and complexity. No centralized visibility into AI usage or spend.

Coder enables Opportunists to standardize AI adoption instead of managing it team by team. Agents already run in standardized, ephemeral Coder Workspaces; AI Governance adds the policy controls and centralized model access that make that standardization enforceable and auditable at scale, without the operational overhead of managing API keys and access per team.

- Standardized, ephemeral workspaces as the baseline, with AI Governance policy controls enforced on top for both developers and AI agents
- Centralized model access and infrastructure policy enforcement across engineering teams
- Reduced operational overhead from managing AI tooling and access team by team

### Caring Provider

**Common pain points:** Running agents locally exposes credentials and repositories. Inconsistent environments across AI tools. Managing API keys and model access across tools. Lack of safe environments for their developers to experiment with agents.

Coder lets Caring Providers, whether a platform team supporting a developer population or a developer supporting themselves, use AI agents without exposing a laptop, credentials, or repositories, since agents already run in isolated cloud workspaces rather than locally. AI Governance is what makes that safe at the platform level without slowing developers down: model requests go through AI Gateway, which logs prompts and tracks usage, without developers needing to manage their own API keys. Developers keep the speed of AI-assisted development while avoiding API key sprawl, shadow AI, and unsafe agent execution, and platform teams get a consistent developer experience that doesn't trade safety for adoption.

- Isolated cloud workspaces as the baseline, so agents never touch a laptop, credentials, or local repositories
- Model requests routed through AI Gateway, with no personal API keys to manage
- The speed of AI-assisted development without shadow AI or unsafe agent execution

## Vertical Messaging

### Government

Coder enables government agencies to run AI agents inside secure, controlled infrastructure rather than unmanaged developer environments. Coder Workspaces already isolates agents in ephemeral, self-hosted environments; AI Governance adds the strict network restrictions and audit logging required for oversight. AI Gateway centralizes model access and records prompts, tool usage, and user attribution for oversight and incident response, while Agent Firewall enforces the network policy boundaries. This architecture reduces data exposure, prevents unauthorized model access, and enforces policy boundaries. Agencies can adopt AI for software development while maintaining data sovereignty, operational control, and compliance with government security requirements.

### FinServ

Coder lets financial services teams run AI agents inside controlled development infrastructure that meets enterprise security and compliance requirements. Coder Workspaces already runs agents in isolated, ephemeral environments with strict access controls; Coder AI Governance adds the network restrictions and full audit logging on top, centralizing model access and capturing prompts, tool usage, and user attribution for governance and investigation. This reduces the risk of source code leakage, unauthorized data exposure, and uncontrolled model usage. Engineering teams can adopt AI to accelerate development while maintaining regulatory compliance, data protection, and operational risk controls.

## Partner Narrative

### AWS x Coder

Coder extends AWS by enabling organizations to run AI-native development environments and agents directly on AWS infrastructure. Using services like EKS and EC2, Coder provisions isolated, ephemeral workspaces that keep development and agent execution inside the customer's AWS environment while driving consumption of AWS compute and storage.

Coder also complements Amazon Bedrock by providing a governed runtime where developers and agents interact with models, including a native Anthropic-passthrough mode for Bedrock that keeps model selection with the client while AI Gateway still handles authentication and logging. With Coder AI Governance controlling and logging model access, enterprises can safely integrate Bedrock models into development workflows while maintaining security, visibility, and operational control. With Kiro orchestrating agents, Coder governs where they run, controlling access to data, tools, and networks while making activity observable.

### Azure / GCP

The same dynamic applies on Azure and Google Cloud. Azure customers can run AI Governance on Azure infrastructure, routing model traffic through Azure OpenAI's OpenAI-compatible endpoint while AI Gateway centralizes authentication, auditing, and cost controls. GCP customers can do the same through Google's OpenAI-compatible endpoint. Coder is cloud-agnostic, so wherever development and agent execution run, AI Governance applies the same policy enforcement, auditing, and cost controls regardless of which cloud is underneath.

### IDE and AI Tool Vendors (Cursor, JetBrains, VS Code, etc.)

AI Governance is not a competitor to IDEs or coding agents; it's the governed infrastructure they connect to. AI Gateway supports a broad set of clients directly, including Claude Code, Codex, VS Code, JetBrains AI Assistant, OpenCode, Zed, and GitHub Copilot (via AI Gateway Proxy), centralizing authentication, auditing, and cost control for each. For tools that don't yet integrate directly with AI Gateway, such as Cursor, workspace-level network controls still apply to any agent activity running inside a Coder workspace, and Agent Firewall applies to the agent processes it wraps. As the agentic tooling landscape evolves, AI Governance is the constant layer underneath whichever tools developers choose.
