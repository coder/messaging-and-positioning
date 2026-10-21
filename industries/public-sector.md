# Public Sector

## Summary

Government agencies, defense organizations, and the contractors and laboratories that support them build mission software under some of the strictest security and accreditation requirements anywhere. Coder gives them self-hosted, governed development environments that run inside their own authorization boundary, from government clouds to fully air-gapped classified networks, so developers, data scientists, and AI agents can move faster without code or data leaving infrastructure the organization controls.

## Who This Is For

Public sector organizations share security, accreditation, and sovereignty constraints, but they differ in mission, size, and how strict those constraints are. Defense and national security organizations face the strictest requirements, and that is where Coder's fit is strongest.

| Segment | Examples | What they need most |
| :---- | :---- | :---- |
| Defense departments and military services | Military departments and services, combatant and functional commands, defense agencies, software factories | Development on government cloud and classified networks, accreditation inherited from a shared platform |
| Intelligence and national security agencies | Intelligence agencies, national security components, and their platform and mission engineering teams | Disconnected environments on each network, with consistent tooling and fast onboarding |
| Defense industrial base and government contractors | Defense primes, mid-tier contractors, systems integrators, subcontractors | Keeping controlled unclassified information (CUI) and export-controlled code off laptops, onboarding contractors without issuing hardware |
| National laboratories and research centers | National laboratories, federally funded research and development centers (FFRDCs), university-affiliated research centers | Governed research, data science, and ML compute across classified and unclassified work |
| Civilian federal agencies | Federal departments and agencies outside defense and intelligence | Keeping source code off endpoints, modern development on government-furnished equipment |
| State, local, and regional government | State agencies, municipalities, regional authorities | Environments a small team can run, with code and data under the government's own control |
| Allied and international government and defense | Ministries of defense, national security agencies, government IT organizations | Sovereignty over where development and AI run, on national infrastructure |

The same groups benefit in every segment:

- **Platform and developer experience teams:** [platform engineers](../audiences/platform-engineer.md), software factory and DevSecOps platform teams, and [developer experience leads](../audiences/developer-experience-lead.md) who provide environments as a shared service and want to stop rebuilding and re-accrediting infrastructure for every team.
- **Technology and security leadership:** the [CTO](../audiences/cto.md), [CIO](../audiences/cio.md), and [CISO](../audiences/ciso.md), plus the authorizing officials and security assessors whose approval gates any new development infrastructure. In the public sector, accreditation shapes technology decisions more than in almost any other industry.
- **Builders:** [developers](../audiences/developer.md), [ML engineers](../audiences/ml-engineer.md), and [data scientists](../audiences/data-scientist.md), plus analysts, researchers, and mission engineers who write code without thinking of themselves as software engineers.

## Signs of a Strong Fit

These build on the [Ideal Customer Profile](../company/ideal-customer-profile.md) and show up across public sector segments:

- Development has to happen on air-gapped, classified, or government cloud networks such as AWS GovCloud, where SaaS development tools can't be used.
- Developers work on government-furnished equipment that can't run development tools without lengthy approvals, or on VDI that slows them down.
- Individual teams or programs pursue their own Authority to Operate (ATO) for development infrastructure, duplicating effort.
- A central platform team, such as a software factory, offers shared services to multiple mission teams or tenant organizations.
- Contractors, surge staff, or partners join and leave often, and CUI or export-controlled code can't sit on their devices.
- Data scientists and analysts need GPU compute next to sensitive data.
- Leaders want AI coding agents, but approval depends on approved models, an audit trail, and network controls inside the boundary.

## Why the Public Sector Needs Coder

These pressures apply across segments, most strongly in defense and national security.

### Development has to happen where the mission is

Mission software is built on networks that can't reach the public internet: air-gapped data centers, classified networks, and government cloud regions. SaaS development tools aren't an option there. Coder Workspaces is fully self-hosted with no SaaS component, validates license keys locally, and lets telemetry be disabled, so it runs in disconnected environments ([Coder docs: air-gapped deployments](https://coder.com/docs/install/prepare/airgap)). Organizations deploy it on their own government cloud, on-premises, or air-gapped infrastructure. See [Secure Development Environments](../use-cases/secure-development-environments.md).

### Accreditation sets the pace

New software on a government network needs a security review and an ATO, and accreditation can take longer than the technical work. When every team builds its own development stack, every team repeats that process. Coder runs inside the organization's authorization boundary, under its ATO. A central platform team can accredit one Coder deployment and offer standardized, pre-approved environments to many teams, which inherit the platform's controls instead of certifying their own. For DoD environments, Coder publishes a hardened container image built on Red Hat UBI9 through Iron Bank, the DoD's hardened container registry ([Coder docs](https://coder.com/docs/install/server/rpm#hardened-base-images)). See [Coder and Red Hat](../market-landscape/red-hat.md) for the accreditation-reuse pattern.

### Government endpoints weren't built for development

Government-furnished laptops are locked down, and getting development tools approved on them can take months. VDI protects code but slows engineers down. Coder moves compute and tooling onto governed infrastructure, so developers keep using government-furnished equipment without modification while working in pre-configured workspaces with their preferred IDEs, and source code stays off endpoints. See [Coder and VDI](../market-landscape/vdi.md).

### Contractors and surge staff need access without the risk

Government work depends on contractors, subcontractors, and surge staff who join and leave quickly. Issuing and managing hardened laptops for each of them is slow and costly, and CUI or export-controlled code can't be left on their own devices. With Coder, a new team member gets a workspace from an approved template in minutes, code and data stay on infrastructure the organization controls, and SSO, RBAC, and audit logs support the access control and audit practices that assessments such as CMMC cover.

### Cleared engineers are scarce, and AI has to run inside the boundary

Cleared engineering talent is hard to hire and slow to onboard, which makes AI coding agents one of the few ways to multiply what existing teams deliver. But approved models differ by organization and network, and AI tools have to run inside the same boundary as the code. Coder Agents and AI Gateway are model-agnostic: they connect to providers such as AWS Bedrock and Azure OpenAI, or to self-hosted models through OpenAI-compatible endpoints, so organizations can use the models approved for each network. Coder Agents runs the agent on the organization's own infrastructure, including air-gapped environments, and AI Gateway records prompts, tool use, and user attribution for oversight. See [Deploy AI Coding Agents](../use-cases/deploy-ai-coding-agents.md) and [AI Governance](../products/coder-ai-governance/message-house.md).

### One platform, many teams

Large public sector organizations run central platforms that serve many mission teams, programs, or tenant organizations. Coder can isolate operations per organization within a single deployment, so one platform can support contractors, separate teams, or sensitive projects from one control plane, while templates push tool updates and security patches to every workspace at once.

### Builders aren't only software engineers

Data scientists, analysts, researchers, and mission engineers write code too, often next to sensitive data. Coder gives them governed environments with GPU-backed compute, tools such as JupyterLab or VS Code, and automatic shutdown of idle resources. See [ML Operations](../use-cases/ml-operations.md).

## How Each Segment Benefits

### Defense departments and military services

**What they look like:** Large organizations with thousands of developers across many programs, central software factories and DevSecOps platforms, and work that spans unclassified and classified networks.

**What they need:** One accredited development platform many mission teams can use, on government cloud and classified networks, and a governed path to super intelligence (SI) for software development.

**How Coder helps:** Self-hosted deployment on AWS GovCloud and classified regions, multi-tenant deployments where mission teams inherit the platform's ATO, and standardized templates that push tool updates and security patches to every workspace. AI Gateway and Coder Agents bring SI tools inside the boundary with an audit trail.

### Intelligence and national security agencies

**What they look like:** Highly classified, disconnected networks, strict identity and access management, small specialized engineering teams, and priorities that can shift quickly.

**What they need:** Development infrastructure with no external dependencies, identical environments for every engineer, fast onboarding when priorities change, and evidence for auditors.

**How Coder helps:** Coder runs entirely inside air-gapped networks, so code, credentials, and metadata stay on government-controlled systems. Templates give every engineer an identical, pre-approved environment in minutes, and audit trails show what infrastructure exists and who has access to it. Because Coder is model-agnostic, agencies can bring SI tools only to the networks and models they've approved.

### Defense industrial base and government contractors

**What they look like:** Prime contractors, mid-tier firms, systems integrators, and subcontractors building for government customers, handling CUI and export-controlled technical data, and staffing programs with changing teams.

**What they need:** CUI and export-controlled code kept off laptops and personal devices, subcontractors onboarded without issuing hardware, and support for requirements such as CMMC and NIST SP 800-171.

**How Coder helps:** Workspaces run on infrastructure the contractor or program controls, so code stays in one governed place while engineers connect from approved devices. SSO, RBAC, and audit logs support the access control and audit practices a CMMC assessment covers. Governed SI tools give program teams agent productivity without moving code outside the boundary.

### National laboratories and research centers

**What they look like:** Scientists, engineers, and data scientists doing research, modeling, and ML, often across classified and unclassified work, with demanding compute needs and strong open-source cultures.

**What they need:** On-demand CPU and GPU compute next to sensitive data, environments researchers can customize, and control over where code and data live.

**How Coder helps:** GPU-backed templates on the lab's own infrastructure, ephemeral workspaces that shut down when idle, and centrally managed data protection such as encryption through cloud key management services. SI tooling with model choice fits research teams that need specific or self-hosted models, and Coder's open-source foundation fits teams that prefer tools they can inspect and run themselves.

### Civilian federal agencies

**What they look like:** Departments and agencies modernizing mission and citizen-facing systems, with developers on standard government-furnished equipment and security teams focused on keeping code and data off endpoints.

**What they need:** A faster path from onboarding to first commit, and central control over source code.

**How Coder helps:** Self-hosted workspaces keep source code in the agency's environment instead of on laptops, and pre-configured templates let developers start on day one. AI Gateway gives agencies one place to approve models and audit SI use.

### State, local, and regional government

**What they look like:** Smaller IT and development teams, data residency and sovereignty obligations, and growing interest in AI under public scrutiny.

**What they need:** Environments a small team can operate, control over where code and data live, and a governed way to adopt AI.

**How Coder helps:** Templates let a small platform team define approved environments once and offer them to every developer. Self-hosted deployment keeps code and data in the government's chosen cloud or data center, and AI Governance provides a record of model access and agent activity.

### Allied and international government and defense

**What they look like:** Ministries of defense, national security agencies, and government IT organizations that must keep development on national or sovereign infrastructure and follow national security guidance, such as the UK's National Cyber Security Centre (NCSC) guidelines.

**What they need:** Sovereignty over where code, development, and AI run, and a straightforward path through national accreditation.

**How Coder helps:** Because Coder is self-hosted and open source, organizations deploy it on infrastructure they choose, including air-gapped networks, and can inspect what they run, which simplifies accreditation in the US and European regions. AI Gateway and Coder Agents keep model access and agent execution inside the same boundary.

## Products Involved

- **Coder Workspaces**: self-hosted, standardized environments that run inside the organization's authorization boundary, including air-gapped and classified networks, and keep code off endpoints.
- **Coder Agents**: coding agents that run on the organization's own infrastructure with the models it approves, with model traffic routed through AI Gateway.
- **AI Governance (AI Gateway and Agent Firewall)**: centralized model access, auditing, and network policy for agents running in workspaces.

## Proof Points

All published by Coder. Coder's public sector customers keep their use of Coder confidential, so these stories are anonymized ([Coder blog](https://coder.com/blog/coder-secures-and-accelerates-mission-critical-innovation-in-public-sector)).

- A **U.S. defense intelligence organization** runs Coder self-hosted on AWS GovCloud inside a fully air-gapped network. Onboarding dropped from multiple days to 3-5 minutes, developer adoption grew 500% over a multi-year deployment, and leadership gained full audit trails for compliance verification. ([Defense Intelligence success story](https://coder.com/success-stories/defense-intelligence-organizations))
- A separate **U.S. Defense Intelligence platform** runs the U.S. military's first true multi-tenant Coder deployment, giving 2,500+ developers pre-approved environments that inherit a centralized, platform-level ATO instead of each mission team certifying its own. ([U.S. Defense Intelligence Organization success story](https://coder.com/success-stories/u-s-defense-intelligence-organization))
- A **U.S. Department of Defense software development group** deployed Coder on AWS GovCloud (US) and regions supporting IL6 and above, moving source code off laptops and automating tool updates and security patches across environments at multiple classification levels. ([DoD software development group success story](https://coder.com/success-stories/us-department-of-defense-software-development-group))
- A **U.S. Department of Defense command** uses Coder on AWS GovCloud to give hundreds of developers and data scientists ephemeral, GPU-enabled workspaces across classified and unclassified domains, with training data encrypted through AWS KMS and idle resources shut down automatically. ([DoD AI/ML group success story](https://coder.com/success-stories/us-dod-ai-ml-group))

## Known Limitations

Coder runs inside an organization's authorization boundary and supports its accreditation, but it doesn't grant an ATO or make an organization compliant: authorization is granted by the operating organization to its own deployment. FedRAMP authorizes cloud service offerings, and Coder is self-hosted software, so it runs under the customer's ATO rather than holding its own authorization.

Coder Workspaces runs fully disconnected. Two capabilities need outbound connectivity. Coder Agents reports Agent Time usage to Coder over HTTPS, and air-gapped deployments can send a manually exported usage bundle instead ([Coder Agents FAQ](../products/coder-agents/faq.md)). Agent Relay connects workspaces to cloud-hosted agents, so it needs connectivity to the agent provider. Agent Firewall applies only to agent processes launched through it and enforces policy on HTTP and HTTPS; Coder Agents' network boundary is the workspace itself. See the AI Governance message house's Governance Scope for current specifics.

## Messaging Guidance

- Describe what Coder does, not compliance outcomes, following the Coder docs style guide:
  - Say Coder "runs inside your authorization boundary, under your ATO." Don't say FedRAMP compliant, FedRAMP ready, or IL5 certified.
  - Say Coder is "available in Iron Bank, as a hardened and scanned container image." Don't say Iron Bank certified or accredited.
  - Say Coder "supports the access control and audit practices" a CMMC assessment covers. Don't say CMMC compliant or certified.
  - Claim FIPS 140-3 only with the module name and an active CMVP certificate number. Don't say FIPS compliant or certified.
  - Don't say STIG compliant, STIG certified, or DISA approved.
- Say Coder Workspaces runs fully air-gapped. Don't say every Coder capability runs disconnected; see Known Limitations.
- In US federal-facing content, including the federal segment sections above, say "super intelligence (SI)" instead of "AI." Product names such as AI Gateway and AI Governance don't change. State, local, and international content keeps "AI."
- Don't name public sector customers or state how many agencies use Coder. Use the anonymized descriptions from published stories.
- Lead with secure development environments for developers and other builders, and present AI Governance as extending the same control to agents. Only claim AI governance controls that exist today.
- Use "public sector" as the umbrella term, and "government" where the audience or search expects it.
- Recognize builders beyond software engineers: analysts, researchers, data scientists, and mission engineers.

## Related Use Cases

- [Secure Development Environments](../use-cases/secure-development-environments.md)
- [Deploy AI Coding Agents](../use-cases/deploy-ai-coding-agents.md)
- [ML Operations](../use-cases/ml-operations.md)
- [Developer Experience](../use-cases/developer-experience.md)
- [Compute / Resource Optimization](../use-cases/compute-resource-optimization.md)

## Related Audiences

- [CISO](../audiences/ciso.md)
- [CIO](../audiences/cio.md)
- [CTO](../audiences/cto.md)
- [Platform Engineer](../audiences/platform-engineer.md)
- [Data Scientist](../audiences/data-scientist.md)
- [ML Engineer](../audiences/ml-engineer.md)
- [Protectionist persona](../audiences/personas/protectionist.md)
