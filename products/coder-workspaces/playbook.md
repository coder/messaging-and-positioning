# Coder Workspaces Playbook

> A shared reference for understanding where Coder Workspaces fits, how it works, and how to support organizations evaluating or adopting it.

For positioning, messaging, and value propositions, see the [Coder Workspaces message house](./message-house.md). For detailed product questions, see the [Coder Workspaces FAQ](./faq.md).

---

## 1. Quick Reference

| | |
|---|---|
| **The product** | Coder Workspaces is a self-hosted platform that provisions governed development environments, defined as code with Terraform, where developers work and AI agents execute tasks. |
| **Best fit** | Mid-size to large enterprises with hundreds of developers, strict security or data residency requirements, and a platform team ready to standardize development environments. |
| **Common signal** | "Our code lives on hundreds of laptops we don't control, and security won't approve AI tools on them." |
| **Key question** | "Where does your source code live while developers and agents work on it today?" |
| **Core value** | Development moves off laptops onto infrastructure the organization controls, and developers keep the tools they already use. |
| **Important limitation** | The customer operates Coder. It isn't a hosted service or a lightweight sandbox for sub-second agent runtimes. |
| **Status** | Generally available. |
| **Journey stage** | Migrate, and the foundation Modernize and Multiply build on. See the [customer journey](../../company/customer-journey.md). |
| **Next step** | Install the free Community edition with the [quickstart](https://coder.com/docs/get-started), or request a Premium trial at [coder.com/trial](https://coder.com/trial). |

---

## 2. Overview

Coder Workspaces moves development environments off individual laptops and onto centralized, self-hosted infrastructure the enterprise controls. Platform teams define environments as Terraform templates, and each developer gets a consistent workspace, such as a VM, a Kubernetes pod, or a Docker container, in any cloud, on-premises, or air-gapped. Developers connect with the IDEs and tools they already use.

Local development leaves source code, credentials, and tooling scattered across machines the organization doesn't control, and AI coding tools make that risk larger. Security teams are restricting AI tools on unmanaged endpoints, and several hosted cloud development environments have been discontinued or pivoted. Coder Workspaces gives enterprises a governed environment layer for developers today, and the same layer runs [AI Governance](../coder-ai-governance/message-house.md) and [Coder Agents](../coder-agents/message-house.md).

See the message house for the full [status quo and 3 Whys](./message-house.md#the-3-whys), and [Why Coder](../../company/why-coder.md) for the five fundamentals.

---

## 3. How It Works

### Architecture summary

The Coder control plane (`coderd`) serves the dashboard and API, stores state in PostgreSQL, and runs provisioners that apply Terraform templates to create workspaces. A workspace agent runs inside each workspace and provides SSH, port forwarding, and startup scripts. Developers connect over end-to-end encrypted connections built on WireGuard, directly when possible and through the control plane's relay otherwise. See [Architecture](https://coder.com/docs/install/plan/architecture) and [Networking](https://coder.com/docs/admin/networking).

### Components and responsibilities

| Component | Responsibility |
|---|---|
| Control plane (`coderd`) | Dashboard, API, authentication, workspace apps, and connections between users and workspaces |
| PostgreSQL | Stores deployment state. An external PostgreSQL 13+ database is recommended for production |
| Provisioners | Apply Terraform templates to create, update, and delete workspace infrastructure. External provisioners (Premium) run builds outside the control plane |
| Templates | Terraform code that defines each type of workspace, versioned and updated centrally. The [Coder Registry](https://registry.coder.com) provides reusable templates and modules |
| Workspace agent | Runs inside each workspace and provides SSH, port forwarding, IDE connections, and startup scripts on any OS, architecture, or cloud |
| Workspace proxies (Premium) | Relay workspace traffic for teams in other regions to reduce latency |
| Identity provider | Signs users in through OIDC or GitHub, with SCIM provisioning and group sync on Premium |

### Typical workflow

**Developer**

1. **Create.** Pick a template, fill in any parameters or choose a preset, and create a workspace. With prebuilt workspaces (Premium), a ready workspace is claimed from a pool.
2. **Connect.** Open the workspace in VS Code, a JetBrains IDE, Cursor, a browser IDE, or over SSH.
3. **Work.** Code, build, and test with access to the internal repositories and services the template allows.
4. **Stop or discard.** The workspace stops automatically when idle, and a broken workspace can be replaced from the template.

**Platform team**

1. **Deploy.** Install Coder on Kubernetes, VMs, or Docker in the organization's own cloud, data center, or air-gapped network.
2. **Integrate.** Connect the identity provider and Git providers.
3. **Define.** Write Terraform templates for each team or workload, starting from starter templates or the Coder Registry.
4. **Govern.** Set permissions, schedules, quotas, and audit logging, and push template updates to every workspace.

### Deployment model

The customer installs and operates every component on its own infrastructure. Kubernetes is recommended for production. Supported options include Kubernetes, OpenShift, Rancher, Docker, RPM packages, and VMs on AWS, Azure, or GCP, with marketplace listings on AWS and GCP. Coder documents validated architectures for deployments of up to 10,000 users, and high availability (Premium) runs multiple control plane replicas in one region. See [Install](https://coder.com/docs/install/server) and [Scale Coder](https://coder.com/docs/install/plan/sizing).

### Data and trust boundaries

Source code, build artifacts, and credentials stay in workspaces on the customer's infrastructure. Developers connect to workspaces rather than copying code to their devices, and browser-only mode (Premium) can restrict access to web IDEs and the web terminal. All Coder features are supported in air-gapped and offline deployments, with license checks performed offline. Deployment telemetry is on by default and can be disabled, along with update checks. See [Air-gapped deployments](https://coder.com/docs/install/prepare/airgap) and [Telemetry](https://coder.com/docs/admin/setup/telemetry).

---

## 4. Boundaries and Terminology

See the message house's [Scope and Tradeoffs](./message-house.md#scope-and-tradeoffs) for more.

### What the product does not do

- Run as a hosted service. The customer deploys and operates Coder.
- Replace the IDE. Coder is the environment IDEs connect to.
- Serve as a lightweight sandbox optimized for sub-second, disposable agent runtimes.
- Govern LLM calls made by an IDE running on a developer's own machine, such as Cursor connected over SSH. Code still stays in the workspace.
- Support the Dev Containers integration in Windows or macOS workspaces.
- Spread the control plane across regions. High availability runs in one region, and workspace proxies serve other regions.

### Recommended terminology

| Preferred | Avoid | Why |
|---|---|---|
| "Self-hosted development environments" | "Hosted CDE" or "SaaS" | The customer operates the platform on its own infrastructure. |
| "Workspaces defined as code with Terraform" | "Virtual desktops" or "VDI" | Workspaces are reproducible development environments, not remote desktops. |
| "Telemetry and update checks can be disabled" | "No call-home" with no qualification | Telemetry is on by default until an administrator disables it. |
| "OIDC single sign-on" | "SAML support" | The docs document OIDC and GitHub sign-in, not SAML. |
| "Prebuilt workspaces (Premium)" | "Instant workspaces" in Community | Prebuilt workspace pools require a Premium license. |

---

## 5. Fit

See the message house's [Target Market / ICP](./message-house.md#target-market--icp) and the company [Ideal Customer Profile](../../company/ideal-customer-profile.md) for the full profile.

### Use cases

Coder Workspaces' primary use cases are consistent development environments, secure source code, enabling an AI agents strategy, and compute cost optimization. See the message house's [Use Cases](./message-house.md#use-cases), [Developer Experience](../../use-cases/developer-experience.md), [Secure Development Environments](../../use-cases/secure-development-environments.md), [Compute Resource Optimization](../../use-cases/compute-resource-optimization.md), and [ML Operations](../../use-cases/ml-operations.md).

### Good-fit signals

- Regulated industries, such as financial services, government, healthcare, and defense, with data residency or air-gap requirements
- More than 200 in-house developers, with Kubernetes, infrastructure-as-code, Git, and SSO proficiency
- A platform team under pressure to standardize development tooling and reduce onboarding time
- Large or complex workloads, such as monorepos, GPU work, or Windows environments, that strain laptops
- Security is restricting AI coding tools on unmanaged laptops, or AI tools are spreading without governance
- A hosted cloud development environment has been discontinued, or can't meet self-hosting or network requirements
- Interest in Coder Agents or AI Governance, which run on Coder Workspaces

### Poor fit or another approach

- **Small teams without a platform function.** Organizations with fewer than about 50 developers, or no one to operate infrastructure, may be better served by a hosted development environment.
- **No requirement to self-host.** If a hosted CDE such as GitHub Codespaces meets security and network needs, Coder's advantages matter less.
- **Disposable sandboxes for programmatic agents.** Products like Daytona and E2B optimize for sub-second ephemeral runtimes. See [Coder and Daytona](../../market-landscape/daytona.md) and [Coder and E2B](../../market-landscape/e2b.md).
- **No executive sponsor or acknowledged risk.** See the company ICP's [poor-fit signals](../../company/ideal-customer-profile.md#signals-coder-treats-as-a-poor-fit).

### Discovery questions

- **Today's environments.** Where do developers work today, such as laptops, VDI, or a hosted CDE, and how long does onboarding take?
- **Infrastructure.** Which clouds, Kubernetes platforms, or data centers would workspaces run on, and is any environment air-gapped?
- **Workloads.** Do teams need monorepos, GPUs, Windows, or specific operating systems?
- **Tools.** Which IDEs, Git providers, and identity provider do teams use?
- **Security.** What are the data residency, audit, and network requirements, and are AI tools allowed on laptops?
- **Scale.** How many developers would use Coder, and how many workspaces would run at the same time?
- **Cost.** How is development compute budgeted and attributed today?
- **AI plans.** Which AI coding tools or agents are in use or planned?

---

## 6. Audiences

See the message house's [Buyer Personas](./message-house.md#buyer-personas) for how each persona applies to Coder Workspaces.

| Role | Cares most about | Useful framing |
|---|---|---|
| [CISO and security leaders](../../audiences/ciso.md) | Getting source code and credentials off unmanaged laptops, with identity-attributed audit | "Code stays on infrastructure you control, and every workspace action is attributable." |
| [Platform engineers](../../audiences/platform-engineer.md) | Standardized, self-service environments they can update centrally, without laptop firefighting | "Define environments once in Terraform and push updates to every workspace." |
| [Developers](../../audiences/developer.md) | Fast onboarding, powerful compute, and keeping their preferred IDE | "A ready-to-code workspace in your own editor, without setting up your laptop." |
| [ML engineers](../../audiences/ml-engineer.md) and [data scientists](../../audiences/data-scientist.md) | On-demand GPUs and keeping sensitive data off personal hardware | "GPU workspaces on demand, with data kept inside the perimeter." |
| [CTO](../../audiences/cto.md) and [CIO](../../audiences/cio.md) | Faster delivery, lower compute cost, and a governed path to AI adoption | "One governed environment layer for developers today and AI agents tomorrow." |

---

## 7. Alternatives and Related Products

See the message house's [Competitive Position](./message-house.md#competitive-position) for the full narrative.

- **Local laptops.** The status quo. Coder moves code, credentials, and compute off unmanaged endpoints. See [Secure Development Environments](../../use-cases/secure-development-environments.md).
- **Building in-house.** Teams can assemble VMs, Kubernetes, and dev containers themselves, but take on the platform work Coder provides. See [Why Coder](../../company/why-coder.md).
- **GitHub Codespaces.** GitHub-hosted, Linux-only, and tied to GitHub. See [Coder and GitHub Codespaces](../../market-landscape/github-codespaces.md).
- **Ona (formerly Gitpod).** A vendor-operated platform now part of OpenAI, with runners in AWS or GCP. See [Coder and Ona](../../market-landscape/ona.md).
- **Sandbox platforms.** Daytona and E2B serve programmatic agent execution rather than developer environments. See [Coder and Daytona](../../market-landscape/daytona.md) and [Coder and E2B](../../market-landscape/e2b.md).
- **Related Coder products.** [AI Governance](../coder-ai-governance/message-house.md) is included with Premium and governs AI tools inside workspaces. [Coder Agents](../coder-agents/playbook.md) and [Agent Relay](../coder-agent-relay/playbook.md) run agents on the same workspace infrastructure.

---

## 8. Common Questions

For common questions about developer experience, infrastructure, security, cost, and packaging, see the [Coder Workspaces FAQ](./faq.md).

---

## 9. Evaluation and Demo

### Evaluation stages

| Stage | Goals | Typically involved |
|---|---|---|
| Initial exploration | Understand the self-hosted model, supported infrastructure, and IDE support | Platform lead, engineering leadership |
| Technical evaluation | Deploy Coder, connect the identity provider and Git provider, and build templates for real repositories | Platform engineers, developers |
| Security and architecture review | Network paths, authentication, RBAC, audit logging, air-gap needs, and telemetry settings | Security, compliance, infrastructure |
| Production planning | Sizing, high availability, workspace proxies, template ownership, cost controls, and rollout | Platform engineering, engineering leadership |

### Pilot setup

- A deployment on the infrastructure the organization would use in production, following [Prepare your deployment](https://coder.com/docs/install/prepare), with DNS, TLS, PostgreSQL, and an identity provider
- One or two templates for real repositories and workloads, including any that strain laptops
- A pilot group of developers across the IDEs the organization uses
- A Premium trial license if the evaluation covers Premium features
- Named stakeholders from platform, security, and the developer group, with agreed success criteria and timeline

### Success criteria

- The deployment is healthy, and someone other than the installer can build a workspace ([Validate your deployment](https://coder.com/docs/install/validate))
- Developers go from sign-in to a working environment in minutes, in their preferred IDE
- Workspaces reach internal repositories and services while source code stays off developer devices
- A template update reaches every pilot workspace without developer action
- Autostop and quotas reduce idle compute, and usage is visible by user and template
- Security signs off on authentication, audit logging, and network paths

### Demo flow

1. Show the Workspaces page, with workspaces running on the customer's infrastructure across different templates.
2. Create a workspace from a template, choosing parameters or a preset, and show how quickly it's ready.
3. Open the workspace in VS Code, a JetBrains IDE, or Cursor, and in the browser, to show developers keep their tools.
4. Update the template and show the new version reaching workspaces centrally.
5. Show platform controls such as autostop schedules, quotas, template permissions, and audit logs.
6. Close by showing that the same workspaces run AI agents, as the bridge to AI Governance and Coder Agents.

Tailor emphasis to the audiences in [section 6](#6-audiences), and use a template that provisions quickly or a prebuilt workspace.

---

## 10. Commercial, Partners, and Contacts

### Packaging and prerequisites

- Community is free and open source (AGPL v3.0), with unlimited self-hosted workspaces
- Premium, priced per user annually, adds enterprise controls, high availability, workspace proxies, multi-organization support, and AI Governance
- AI Premium adds uncapped Coder Agents with a deployment-wide allotment of Agent Hours
- Infrastructure to run the control plane, a PostgreSQL database for production, DNS and TLS, and an identity provider

See [Packaging](../../company/packaging.md) and [coder.com/pricing](https://coder.com/pricing) for current tiers and prices.

### Evaluation access

Self-serve. The Community edition installs in under 10 minutes with the [quickstart](https://coder.com/docs/get-started). Premium trials are available at [coder.com/trial](https://coder.com/trial).

### Partners

Every workspace runs on the customer's cloud or data center, so Coder drives consumption on AWS, Azure, and Google Cloud. IDE and AI tool vendors connect to Coder rather than compete with it. See the message house's [Partner Narrative](./message-house.md#partner-narrative).

### Contacts

| Topic | Contact / Team |
|---|---|
| Messaging and positioning | Matt Vollmer, Product Marketing |
| Customer support | Coder Support |
| Everything else | Your [Coder account team](https://coder.com/contact) or [sales@coder.com](mailto:sales@coder.com) |

---

## 11. Resources

- [Coder docs](https://coder.com/docs), including [Architecture](https://coder.com/docs/install/plan/architecture), [Install](https://coder.com/docs/install/server), [Templates](https://coder.com/docs/admin/templates), [Access workspaces](https://coder.com/docs/user-guides/workspace-access), [Scale Coder](https://coder.com/docs/install/plan/sizing), and [Air-gapped deployments](https://coder.com/docs/install/prepare/airgap)
- [Coder Registry](https://registry.coder.com) for templates and modules
- [Coder Workspaces message house](./message-house.md), including its [Proof Points](./message-house.md#proof-points), and [FAQ](./faq.md)
- Use cases for [Developer Experience](../../use-cases/developer-experience.md), [Secure Development Environments](../../use-cases/secure-development-environments.md), [Compute Resource Optimization](../../use-cases/compute-resource-optimization.md), and [ML Operations](../../use-cases/ml-operations.md)
- Market landscape pages for [GitHub Codespaces](../../market-landscape/github-codespaces.md), [Ona](../../market-landscape/ona.md), [Daytona](../../market-landscape/daytona.md), and [E2B](../../market-landscape/e2b.md)
- [Coder on GitHub](https://github.com/coder/coder)
