# Coder Workspaces Message House

Coder Workspaces is the Migrate stage of the [customer journey](../../company/customer-journey.md), and the foundation the Modernize and Multiply stages build on.

## Status Quo

### Without Coder

Software development today happens in fragments. Developers work from laptops, each with its own configuration, credentials, and tool sprawl. Platform teams spend enormous effort trying to enforce consistency across hundreds of machines they don't control.

AI tools have compounded this problem dramatically. Developers now run AI coding agents (Cursor, Claude Code, GitHub Copilot, and others) on local machines where those agents inherit ambient credentials, have full network access, and operate entirely outside any platform team's visibility. Many security teams have already moved to restrict or outright prohibit AI coding tools on unmanaged endpoints. What was once a developer environment problem has become a blocker on AI adoption itself.

Beyond local machines, cloud-hosted agent platforms (Cursor Agents, Codex, Claude Managed Agents) introduce a second failure mode: source code routes through third-party infrastructure the organization does not own or control.

Local development is ungoverned. Cloud-hosted agent platforms send your code to someone else's servers. Coder solves both.

This results in:

- **Environment inconsistency**: causes bugs, slows onboarding, and burns platform team time. New developers spend days setting up machines that will drift from teammates' setups within weeks.
- **Local compute bottlenecks** prevent teams from handling large monorepos, GPU workloads, or compute-intensive CI at the speed AI-augmented development demands.
- **Shadow sprawl** means source code, credentials, and context are flowing to third-party cloud services with no audit trail and no organizational visibility.
- **No path to AI adoption** exists when development happens on devices the organization doesn't control. You can't safely enable what you can't see.

Organizations that delay centralizing their development environments are not standing still, they are actively accumulating infrastructure debt and AI risk while competitors move faster.

## The 3 Whys

### Why Do Anything?

Local development is risky. With AI, it's negligent. Laptops are ungoverned endpoints where AI tools run with developer-level credentials, full network access, and zero audit trail. At the same time, the productivity leverage available from AI-augmented development, background agents, multi-agent parallelization, autonomous task execution, is only achievable on real, powerful, cloud-based infrastructure. Lightweight sandboxes can't run monorepos. Laptops aren't capable of running 10 parallel agents, and even if they were, no platform team would want unsupervised agents running on ungoverned endpoints. The environment layer is the prerequisite for everything else.

### Why Now?

Three forces are converging:

- AI agents are no longer an experiment, they are being deployed in production by early adopters, and the competitive gap is compounding every quarter.
- Security and compliance teams are beginning to mandate governance over AI tooling, and the window for ungoverned adoption is closing.
- The CDE market is contracting around providers who didn't build for AI. Former leaders have been deprecated, discontinued, or pivoted away from their core CDE offering, leaving enterprises without a committed platform. The consolidation window is now.

### Why Coder Workspaces?

Coder Workspaces is built for enterprise-grade complexity from day one, not retrofitted for it. It's self-hosted on any cloud or on-premises, Terraform-provisioned, and IDE- and agent-agnostic. Critically, Coder Workspaces doesn't require you to re-platform when models change and new tools emerge. When your organization is ready to scale autonomous agents with Coder Agents, Coder Workspaces is already the infrastructure underneath.

## Messaging Statement

### Short

Coder Workspaces is the open-source platform that provisions secure, self-hosted development environments where developers work and AI agents execute tasks. It runs in your cloud or on-premises infrastructure, supports any team and any AI tool or LLM, and gives platform teams centralized control over standardized environments where both developers and AI agents operate. It supports today's tools and tomorrow's stack, always on infrastructure you own.

### Medium

Most enterprises have rigorous standards for production infrastructure. Almost none have equivalent standards for where code is actually written.

Coder Workspaces closes that gap. It shifts development from ungoverned laptops to self-hosted infrastructure that platform teams define, provision, and control via Terraform. Every developer starts from a consistent, policy-enforced baseline. AI agents provision workspaces only when compute is required. Source code never leaves your infrastructure. Developers keep the tools they already use: VS Code, Cursor, JetBrains, and others.

It encodes the four standards enterprises are missing: how environments are packaged and connected, how work is placed and resourced, how activity is governed and audited, and how all of it extends to AI agents as development evolves.

### Long

Local development is the last major holdout of ungoverned enterprise infrastructure, and AI has made that untenable. Developers work from inconsistent machines with ambient credentials. AI agents route source code through third-party clouds. Platform teams have no visibility, no enforcement, and increasingly, no ability to allow AI tooling at all on devices they don't control.

The root cause is structural. Enterprises have rigorous standards for how applications are deployed, how data is stored, how networks are secured. Almost none have equivalent standards for where software is actually built. That gap didn't matter much when development meant a developer and a laptop. It matters enormously when AI agents are executing code autonomously at scale.

Coder provides that missing standard. Its control plane provisions Coder Workspaces, the self-hosted environments where developers work and AI agents execute tasks, through Terraform, so every builder starts from a consistent, policy-enforced baseline. Source code never leaves your infrastructure. Developers keep the tools they already use: VS Code, Cursor, JetBrains, and others.

The control plane encodes these foundational standards:

- **Package & Connect**: a universal, repeatable way to define environments, bundle dependencies, and connect developers and agents consistently across teams.
- **Place & Resource**: a standard for where work runs, how compute is provisioned and right-sized, and how cost is controlled through quotas, scheduling, and attribution.
- **Govern & Audit**: a standard for who can do what, where code runs, and how all activity, human and agent, is observed, attributed, and audited.
- **Normalize Workflows**: the emerging standard for how agent workflows are defined and executed consistently, built on the three layers above.

Together, these address the two things that make AI development transformation hard: getting every builder operating from the same governed baseline, and making the economics of AI-driven development legible and controllable.

## Taglines

### General

- Built for developers. Ready for their agents.
- Where developers work and AI agents run, on infrastructure you control
- Don't just experiment. Govern and scale AI agents in your development workflow.
- Safely run AI-native development on your self-hosted environments
- Self-hosted development environments built for the AI era

### Security-focused

- Self-hosted environments for secure, compliant development at scale
- Self-hosted and governed AI development infrastructure

### Community

- Self-hosted, open-source environments for agentic software development
- Self-hosted, open-source environments for builders and agents

## Use Cases

### Use Case 1: Consistent Development Environments

**Desired Outcome:** Developer productivity is improved. They onboard in minutes rather than days, spend their time writing code rather than configuring environments, and discard broken setups instead of debugging them. Platform teams stop firefighting environment issues and push updates to all workspaces centrally; no patch relies on developer intervention to propagate.

**Pain Points:** Most development problems, slow onboarding, broken builds, "it works on my machine," trace back to the same root cause: environments that aren't defined, enforced, or reproducible.

**Coder's Solution:** Workspaces are Terraform-provisioned from templates, so every developer starts from an identical, policy-enforced baseline. Platform teams define and update environments centrally; developers claim ready-to-use workspaces instantly from prebuilt pools. Cloud-based compute eliminates local hardware bottlenecks. Large monorepos, GPU jobs, intensive builds, and model training run on cloud CPUs and GPUs rather than developer laptops. Ephemeral workspaces let developers discard and spin up fresh environments instead of debugging broken ones.

### Use Case 2: Secure Source Code

**Desired Outcome:** Source code and development activity move off developer laptops and onto centrally managed infrastructure, reducing exfiltration risk, closing audit gaps, and making compliance posture enforceable by design rather than by policy.

**Pain Points:** Storing source code on developer laptops creates persistent exfiltration risk and makes data sovereignty difficult to enforce. Platform teams have no reliable audit trail, and managing security patches across hundreds of distributed machines is slow and inconsistent. Every unpatched laptop is an exposure window.

**Coder's Solution:** Coder Workspaces runs self-hosted in the enterprise's VPC, on-prem data center, or fully air-gapped enclave. Source code never leaves the perimeter; developers connect via SSH from any device, but code stays in the workspace. SSO/OIDC integration, RBAC, and audit logging give platform teams full visibility into workspace access and activity. Security patches push to all workspaces centrally in minutes, without relying on developer intervention. Coder supports any cloud, on-premises, and fully air-gapped deployments, and integrates with existing SIEM and SOC tooling rather than requiring new compliance infrastructure.

### Use Case 3: Enabling an AI Agents Strategy

**Desired Outcome:** Platform engineering has a single governed infrastructure layer that supports human developer workflows today and scales seamlessly to AI coding agents, without a new platform, new vendor assessment, or new security review cycle.

**Pain Points:** Enterprises want to deploy AI coding agents but face a governance gap: agents run on developer laptops with ambient credentials, full network access, and zero audit trail. Many security teams have already moved to restrict or prohibit AI coding tools on unmanaged endpoints. Adopting a dedicated agent platform means a new vendor, new SOC 2 assessment, and new SSO integration, adding 6 or more months of procurement. The gap drives shadow AI adoption instead.

**Coder's Solution:** Coder's platform is the substrate that Coder's full AI product suite runs on. Coder Workspaces provides the governed environment layer where both human developers and AI agents operate, already in production, already enterprise-proven, already governed. AI Governance and Coder Agents layer onto the same infrastructure Workspaces run on, with no new platform or security review required. Existing customers now extend to governed agent execution using the same templates, RBAC, and audit infrastructure they already manage, without a new platform or procurement cycle required.

### Use Case 4: Compute Cost Optimization

**Desired Outcome:** Development compute costs are visible, attributable, and controlled. Platform teams can right-size environments, enforce resource quotas, and recover idle compute without restricting developer or agent productivity.

**Pain Points:** Local development environments waste cloud and GPU budget: compute runs idle, builds are duplicated across machines, and AI agent workloads have no resource limits or attribution. Platform teams have no visibility into who is consuming what, making optimization guesswork.

**Coder's Solution:** Coder makes compute consumption attributable to specific developers, teams, agents, and projects. Auto-stop policies shut down idle workspaces automatically. Per-user and per-team resource quotas prevent runaway spend. Terraform-provisioned templates ensure right-sized environments from the start. Shared cloud infrastructure replaces per-developer compute silos, and usage data is available for showback and chargeback reporting. As AI agent workloads scale, the same resource controls that govern developer compute govern agent compute.

## Proof Points

- One F500 investment bank reported less than 5% of engineer time was spent coding before Coder.
- Palantir reduced time-to-first-commit from 15 days to one hour.
- One government agency eliminated source code from sitting on 1,500 remote laptops using Coder.
- KKR, a Coder investor and customer, went from zero AI-assisted code to more than half of commits using third-party agents happening inside Coder-managed environments within a year of deployment.
- Skydio cut its AWS bill by 90%, from $3M to $300K, after moving to Coder.

## Value Props / Differentiators

- **Self-hosted on any infrastructure**: Run on AWS, Azure, GCP, on-prem, or air-gapped. Source code never leaves your perimeter. No vendor infrastructure dependency.
- **Open source with enterprise depth**: Coder Community Edition is free, open-source (AGPL v3.0), and fully functional. Premium adds enterprise RBAC, audit logging, multi-org tenancy, workspace proxies, SCIM/OIDC group sync, and high availability. No vendor lock-in.
- **Terraform-provisioned environments**: Every workspace is defined as code. Consistent, reproducible, version-controlled, and updatable centrally. The same model that governs human workspaces governs agent workspaces.
- **Works with what you have**: Developers keep their preferred IDE. Coder supports any model provider. No forced migrations, no lock-in on either side.
- **The stable layer under a shifting AI landscape**: As the agentic IDE market shifts and consolidates, Coder Workspaces is the IDE- and model-agnostic infrastructure layer underneath whichever tools win.
- **Built for real enterprise workloads**: Large monorepos, GPU workloads, Windows environments, persistent long-running sessions. Not a lightweight sandbox. A production-grade environment platform.
- **AI-native**: Coder's control plane runs the Coder Agents agent loop, provisions workspaces on demand for tool execution, and connects to any model provider. Human developer environments and agent workloads share the same governed infrastructure, no separate platform required.

## Supporting Features

### Package & Connect

How organizational standards for environments get encoded and enforced consistently, across every developer and every agent.

- **Terraform-based workspace provisioning** - every environment is defined as code, version-controlled, and updatable centrally. Platform teams push updates to all workspaces from one place; developers never wait for a patch to propagate.
- **Prebuilt workspace pools** - developers claim ready-to-use environments instantly, with no configuration lag. Onboarding takes seconds, not days.
- **IDE and tool agnosticism** - VS Code, Cursor, JetBrains, Windsurf, Jupyter, and any SSH-capable editor connect to workspaces without changing developer workflow. Official plugins for VS Code and JetBrains; browser-based access via code-server.
- **Any Git provider** - connect to GitHub, GitLab, Bitbucket, or Azure DevOps for consistent source access across teams.
- **Coder Agent Relay** - connects cloud-hosted AI agent sessions, such as Cursor and Claude Code, to self-hosted Coder workspaces, so agent orchestration and inference can stay with the provider while execution happens on infrastructure you control.
- **Support for real enterprise workloads** - VMs, containers, Kubernetes, GPU workloads, and Windows environments. Large monorepos, complex builds, and long-running sessions. Not a lightweight sandbox.

### Place & Resource

How work is placed on infrastructure and what it costs, for developers today, for agents at scale tomorrow.

- **Any-infrastructure deployment** - workspaces run on AWS, Azure, GCP, on-prem, or fully air-gapped. Compute runs wherever your organization requires, with no cloud lock-in.
- **Workspace autostart/autostop** - set workspaces to start automatically and stop after inactivity, keeping compute from running idle. Enforceable by platform teams in Premium at the template level.
- **Resource quotas per user and per organization (Premium)** - enforce compute limits across developers, teams, and agent workloads to prevent runaway spend.
- **Dormancy and cleanup policies (Premium)** - automatically flag and delete unused workspaces to recover idle compute.
- **Template usage insights** - visibility into workspace utilization across the organization, enabling right-sizing and cost attribution.
- **Workspace proxies (Premium)** - low-latency workspace access for globally distributed teams, without routing all traffic through a central control plane.
- **External provisioners (Premium)** - scale provisioning workload outside the core control plane for large deployments.

### Govern & Audit

How every builder, human or agent, is held accountable to organizational standards, with a single audit surface.

- **Role-based access control** - predefined roles (Owner, Template Admin, User Admin, Auditor) apply uniformly across workspace environments. Template permissions give platform teams fine-grained control over who can use and modify templates (Premium).
- **SSO via OpenID Connect** - identity-attributed access across the platform, available in both Community and Premium editions.
- **SCIM provisioning and deprovisioning (Premium)** - automate user lifecycle management via your existing identity provider.
- **OIDC group and role sync (Premium)** - group membership and roles stay in sync with your IdP automatically.
- **Multi-organization access control (Premium)** - manage distinct teams, business units, or tenants within a single Coder deployment.
- **Audit logging (Premium)** - full logs of all user and workspace actions. Integrates with existing SIEM and SOC tooling.
- **Connection logging (Premium)** - a complete record of workspace app connections, browser port forwarding, SSH/IDE sessions, and tunnel authorization decisions, for deeper compliance and security visibility.
- **Browser-only IDE enforcement (Premium)** - restrict workspace access to browser-based IDEs when security policy requires it.
- **Source code stays in your perimeter** - workspaces run self-hosted in your VPC, on-prem data center, or air-gapped enclave. Developers connect via SSH; code never leaves the infrastructure you control.

### Normalize Workflows

The foundation for AI agent execution, built on the three standards above. AI Governance is available as an add-on for Premium customers; the workspace infrastructure they depend on is already in place. Coder's platform is the substrate that AI governance and agent execution run on. Because the control plane already defines how environments are provisioned, who can access them, and how activity is logged, extending it to governed agent workflows requires no new platform.

- **Efficient** - Coder Agents provision workspaces only when tool execution is required for large tasks like file edits, shell commands, and builds.
- **Agnostic** - Third-party agents (Claude Code, Codex, Cursor Agents, etc.) can run inside Coder Workspaces, governed by AI Governance controls, network firewalls, prompt logging, model access control.
- **MCP server support** - available in both Community and Premium, enabling model context protocol integrations within workspaces.
- **Extensible to AI Governance** - process-level network controls and LLM gateway with prompt logging and model access control are available as a Premium add-on that layer directly onto existing workspace infrastructure. No new platform required.

## Known Limitations

- **Full AI governance for external IDE agents is in development** - When developers use Cursor or Windsurf connected to a Coder workspace via SSH, LLM calls still go directly from the IDE client to the model provider, bypassing Coder's AI Governance today. The infrastructure security story, source code stays in your VPC, is strong and real. Full AI governance for external IDE agents (logging, attribution, guardrails) is in active development. For complete AI governance today, the path is Coder Agents for native agent execution.
- **Workspace provisioning time varies by template complexity.** Prebuilt workspace pools mitigate this for common configurations, but complex templates with lengthy startup procedures will still have provisioning latency.
- **Coder Workspaces is a self-hosted alternative to lightweight sandbox products, not a like-for-like comparison.** Products such as Daytona and E2B optimize for sub-2-second ephemeral runtimes for simple agent experimentation. Coder Workspaces trades some of that raw startup speed for a full-featured, self-hosted environment platform with the governance, persistence, and enterprise depth those sandbox products don't provide, a tradeoff most enterprises are willing to make in exchange for control over their infrastructure.

## Competitive Position

Coder Workspaces sits at the intersection of two converging shifts: the collapse of legacy CDE platforms and the rise of AI-driven development. Five major competitors, AWS Cloud9, AWS CodeCatalyst, JetBrains Space, JetBrains CodeCanvas, and Microsoft Dev Box, have been deprecated, discontinued, or closed to new customers in the past 18 months. The remaining SaaS-first competitors (GitHub Codespaces, Ona/Gitpod) are either locked to a single cloud or actively pivoting away from their CDE roots. That leaves enterprises without a committed, enterprise-grade platform, and Coder is the natural destination.

Coder Workspaces is the only CDE that is self-hosted on any infrastructure (any cloud, on-prem, or air-gapped), IDE-agnostic, and purpose-built to serve as the foundation for both human developer workflows and AI agent execution. Where competitors offer hosted convenience with significant constraints, vendor lock-in, limited deployment options, no AI governance path, Coder offers infrastructure ownership, flexibility, and a clear runway into the AI agent development era.

In regulated industries, Coder is the only platform that can meet data residency, air-gap, and compliance requirements while also supporting modern AI tooling. For multi-cloud enterprises, it is the only CDE that works consistently across AWS, Azure, GCP, and on-prem without compromise, and for organizations already deploying AI coding tools, Coder is the only CDE that is also the foundation for a complete AI governance and agent execution stack.

## Target Market / ICP

**Primary Market:** Mid-size to large enterprises with 2,000+ employees, 200+ in-house developers, and a strong multi/hybrid cloud posture. Kubernetes proficiency and infrastructure-as-code maturity are strong signals.

**Strongest fit signals:**

- Regulated industries (financial services, government, healthcare, defense) with data residency requirements
- Organizations with large or complex codebases (monorepos, GPU workloads, Windows environments)
- Platform engineering teams under pressure to standardize development tooling across a large developer population
- Organizations just starting to figure out how to give developers access to AI tools or are actively deploying AI coding tools (Cursor, Claude Code, GitHub Copilot) who are beginning to face governance and security questions
- Organizations evaluating or already running Coder Agents or AI Governance, Workspaces is the required foundation

## Buyer Personas

See [Buyer Personas](../../audiences/personas/overview.md) for the canonical definition of each persona. The application to Coder Workspaces is below.

### Protectionist

**Voice of the persona:** "Local development is risky, and with AI, negligent. Coder gives you control."

Coder replaces the sprawl of local and cloud dev setups with one self-hosted platform the organization controls end-to-end. AI agent credentials never enter the workspace, and the agent runs in the control plane, so there is no agent software to secure inside the environment. The platform is auditable, policy-enforced, and compliant, letting the organization adopt new AI tools without compromising its security posture or data boundaries.

- Self-hosted architecture that fits the organization's compliance and data sovereignty needs
- Fine-grained permissions and audit logs for every human and agent action
- Standardized configurations that reduce risk from local or rogue environments

### Opportunist

**Voice of the persona:** "Local development is inefficient, and with AI, causes runaway costs. Coder helps you scale sustainably."

Coder turns development environments into measurable, standardized infrastructure. By centralizing both human and AI workflows, platform teams gain visibility into cost, utilization, and performance, while reducing overhead from environment toil. It's the fastest path to improved velocity and measurable ROI from AI, transforming developer productivity into true AI-driven force multiplication where agents run background tasks and CI-triggered workflows autonomously.

- Centralized usage and cost metrics for human and AI workloads
- Easy policy management across teams, clusters, and clouds
- Compatible with existing infrastructure, so adoption doesn't disrupt operations

### Caring Provider

**Voice of the persona:** "Local development is frustrating, and with AI, unsustainable. Coder speeds up project onboarding and reduces cost."

With Coder, onboarding is instant, environments are consistent, and teams stay productive. Developers get powerful, pre-configured workspaces that "just work," whether they're coding locally, in the cloud, or alongside AI agents. Platform teams spend less time firefighting setup issues and more time empowering developers.

- Pre-configured, reproducible workspaces for frictionless onboarding
- High performance for large monorepos and complex builds
- Agent-ready environments that future-proof developer workflows

## Vertical Messaging

### Government

Coder Workspaces runs fully self-hosted with no SaaS component, no external telemetry, and no call-home requirements. Deployable in air-gapped environments at any classification level. All development and AI agent execution runs on compute your agency owns and operates. Meets the bar for ATO conversations today, self-hosted, auditable, identity-attributed, and cloud-agnostic. The path to governed AI agent development execution for classified environments runs through Coder Workspaces.

### FinServ

Source code and development execution are co-located on infrastructure you control, in the geography you specify. Data sovereignty is architectural, not a vendor promise. The same platform governs human developer environments and AI agent execution, giving compliance teams a single audit surface for all development activity. Extend to AI governance to add model access control and prompt logging without introducing a new platform.

### Tech Innovators

Ship a consistent, governed AI development environment to every developer in your organization in days. No per-developer configuration, no API key distribution, no environment drift. Developers get powerful, pre-configured workspaces that connect to the AI tools they want. Platform teams get centralized control. When the organization is ready to scale autonomous agents, Coder Agents enables parallel background tasks, multi-agent workflows, and CI-triggered agent execution all on self-hosted infrastructure your team controls.

## Partner Narrative

### AWS

Every Coder Workspace is an EC2 instance, EKS pod, or ECS task running in the customer's AWS account. More developers and agents using Coder means more compute on AWS infrastructure. Coder supports AWS Bedrock as a model provider for AI-assisted workflows. As customers' AWS footprints grow or shift across regions, accounts, or services, Coder adapts without requiring environment changes. Coder doesn't compete for the infrastructure dollar. It's the reason the infrastructure dollar gets spent.

### Azure / GCP

Same dynamic. Azure customers run workspaces on Azure VMs or AKS. GCP customers run on GCE or GKE. Coder is cloud-agnostic, so wherever the customer runs, Coder drives consumption on that cloud. Azure OpenAI and Vertex AI are supported as model providers. For organizations running multi-cloud or shifting cloud strategy over time, Coder moves with them: the same platform, the same governance, the same developer experience regardless of which cloud is underneath.

### IDE and AI Tool Vendors (Cursor, JetBrains, VS Code, etc.)

Coder Workspaces is not a competitor to IDEs. It is the environment IDEs connect to. Developers use their preferred editor. Coder provides the governed, self-hosted workspace on the other end of the SSH connection. The Coder Registry extends this further, offering a growing library of community and verified templates, modules, and scripts that teams can use to standardize and accelerate workspace provisioning. As the agentic IDE market evolves, Coder is the stable infrastructure layer underneath whichever tools developers choose.

## CTAs

- Get started with the open-source Community Edition
- Talk to our team about Coder Premium
- Read the documentation
- Join the Coder community
- Book a demo
