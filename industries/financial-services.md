# Financial Services

## Summary

Financial institutions run on software, data, and models, and they answer to regulators for every part of it. Coder gives banks, asset managers, trading firms, insurers, and fintechs self-hosted, governed environments where developers, quants, data scientists, and AI agents can move fast without code, data, or models leaving infrastructure the firm controls.

## Who This Is For

Financial services isn't one kind of organization. The segments below share regulatory pressure and a dependence on software, but they differ in size, culture, and what they need most from Coder.

| Segment | Examples | What they need most |
| :---- | :---- | :---- |
| Global and investment banks | Universal banks, investment banks, systemically important institutions | Control at scale, VDI replacement, governed AI rollout across thousands of engineers |
| Regional and commercial banks | Regional, retail, and commercial banks | Modernization with a small platform team, examiner-ready controls |
| Asset and wealth managers | Mutual fund and ETF managers, wealth managers, custodians | Governed environments for research and data science next to sensitive data |
| Hedge funds and quantitative trading firms | Multi-strategy funds, quant funds, proprietary trading firms | Speed for researchers, protection for strategy code, on-demand compute |
| Private equity and alternative asset managers | PE firms, private credit, infrastructure and real estate investors | Giving analysts and operators, not just engineers, governed access to AI |
| Insurance | Life, property and casualty, health, and specialty insurers, reinsurers | Data science on policyholder data, legacy core system modernization |
| Payments and fintech | Payment processors, card networks, digital banks, fintech platforms | Fast onboarding for a growing team, PCI-grade controls, cost efficiency |

The same groups benefit in every segment:

- **Platform and developer experience teams:** [platform engineers](../audiences/platform-engineer.md), [developer experience leads](../audiences/developer-experience-lead.md), and the engineering leaders who provide development environments and want to stop maintaining laptop builds and VDI images.
- **Technology and security leadership:** the [CTO](../audiences/cto.md), [CIO](../audiences/cio.md), and [CISO](../audiences/ciso.md), who are accountable for productivity, risk, and regulatory evidence. In financial services, security and risk functions shape technology decisions more than in most industries.
- **Builders:** [developers](../audiences/developer.md), [ML engineers](../audiences/ml-engineer.md), and [data scientists](../audiences/data-scientist.md), plus roles specific to the industry: quants, researchers, actuaries, and analysts who write code but don't think of themselves as software engineers.

## Signs of a Strong Fit

These build on the [Ideal Customer Profile](../company/ideal-customer-profile.md) and show up across financial services segments:

- Software, data, and models are central to how the institution makes money, not a back-office function.
- Development happens on hardened laptops or VDI, and engineers say it slows them down.
- The institution faces audit scrutiny under frameworks such as DORA, SOX, PCI DSS, GLBA, or FFIEC guidance, and needs to show where code and data live.
- A large modernization program, such as moving core systems off mainframes, needs many developers productive quickly.
- Quants, data scientists, or actuaries need GPU or large CPU compute next to sensitive data.
- Teams want AI coding assistants and agents, but security or risk teams are holding them back until there are controls and an audit trail.
- Engineering teams span regions with different data residency requirements.

## Why Financial Services Needs Coder

These pressures apply across every segment, in different proportions.

### Regulators expect control and evidence

Financial institutions operate under frameworks such as DORA, SOX, PCI DSS, GLBA, FFIEC guidance, GDPR, and prudential supervision from bodies such as the ECB. They need to show where code and data live, who accessed what, and how changes were controlled. Development spread across laptops makes that hard to prove. Coder runs entirely on the firm's own cloud, on-premises, or air-gapped infrastructure, integrates with existing SSO and SCIM, attributes every workspace and agent action to a named user, and exports audit events to the firm's SIEM. See [Secure Development Environments](../use-cases/secure-development-environments.md).

### The code and the models are the business

Trading strategies, pricing and risk models, underwriting logic, and fraud detection are core intellectual property. Self-hosted workspaces keep source code, credentials, and data inside the firm's perimeter instead of on endpoints, and template-defined network policies scope what each workspace can reach.

### Locked-down endpoints make development slow

To reduce risk, many institutions harden laptops with endpoint scanners, enterprise proxies, and restricted admin rights, or put developers on VDI. Both protect the firm but slow engineers down. Coder moves the compute and tooling into governed infrastructure, so developers keep their preferred IDEs while builds and dependency resolution run on server-grade hardware. See [Coder and VDI](../market-landscape/vdi.md).

### AI adoption is happening under scrutiny

Engineers want AI coding assistants and agents, and leadership wants the productivity gains. Risk and compliance teams need to know which models touch code, what data leaves the perimeter, and what an agent actually did. [AI Governance](../products/coder-ai-governance/message-house.md) answers those questions: AI Gateway centralizes model access, credentials, budgets, and auditing, and Agent Firewall enforces default-deny network policy on agent processes inside a workspace. That lets institutions move from blocking AI to adopting it with a record regulators can review.

### Modernization runs alongside daily delivery

Many institutions are moving core systems from mainframes and legacy platforms to cloud-native architectures while still shipping changes every day. Large modernization programs need hundreds of developers to get productive quickly and move between projects. Coder's Terraform-based templates give every developer a consistent, pre-configured environment, so onboarding takes hours instead of weeks and switching projects means starting a different workspace.

### Teams and data span jurisdictions

Global institutions have engineering teams across regions and data residency obligations in each. Because Coder is self-hosted, firms deploy it in the regions and data centers they choose, and workspace proxies host workspaces close to developers to reduce latency.

### Builders aren't only engineers

Quants, researchers, actuaries, and analysts write code every day, often in notebooks on their own machines next to sensitive data. Coder gives them the same governed environments, with their preferred tools such as JupyterLab or VS Code, and the same path to AI agents that engineers get.

## How Each Segment Benefits

### Global and investment banks

**What they look like:** Thousands of engineers across many regions, layered security and risk functions, long-running modernization programs, and heavy use of VDI or hardened laptops for development.

**What they need:** A single, governed way to provision environments at scale; a better developer experience than VDI without loosening control; and a central place to roll out AI coding tools with consistent model configuration and auditing.

**How Coder helps:** Self-hosted deployment inside existing data centers or approved cloud accounts, workspace proxies for global teams, standardized templates that propagate tooling and security updates to every workspace at once, and AI Governance to centralize model configuration and audit AI activity as AI coding tools roll out.

### Regional and commercial banks

**What they look like:** Smaller platform teams supporting a broad application portfolio, core banking modernization, and regular examiner scrutiny.

**What they need:** Controls they can explain to examiners, and an environment platform a small team can operate without building it themselves.

**How Coder helps:** Templates let a small platform team define approved environments once and offer them to every developer, reducing setup support. Audit logs, SSO, and RBAC provide the evidence examiners ask for, and everything runs inside the bank's existing perimeter.

### Asset and wealth managers

**What they look like:** Investment research, portfolio analytics, and client platforms built by a mix of engineers, data scientists, and analysts, often working with proprietary models and sensitive client data.

**What they need:** Research and data science environments that sit next to the data instead of copying it to laptops, access to GPUs for model training, and a governed way to bring AI into research workflows.

**How Coder helps:** Workspaces run next to governed data on the firm's infrastructure, with GPU-backed templates and automatic shutdown of idle compute. Analysts keep JupyterLab or their preferred IDE. See [ML Operations](../use-cases/ml-operations.md).

### Hedge funds and quantitative trading firms

**What they look like:** Technology-driven firms where engineering and research are the competitive edge, with strong open-source cultures, high expectations for tooling, and little tolerance for friction.

**What they need:** Fast iteration for researchers and engineers, protection for strategy code that can never leak, large amounts of CPU and GPU compute on demand, and a safe way to let AI agents speed up research.

**How Coder helps:** Workspaces on the firm's own compute keep strategy code and market data inside the perimeter. Port sharing lets analysts share running models with traders directly, without fragile pipelines. AI Gateway and Agent Firewall let firms adopt coding agents while controlling which models are used and what agents can reach. Coder's open-source foundation also fits engineering cultures that prefer tools they can inspect and run themselves.

### Private equity and alternative asset managers

**What they look like:** Growing internal engineering and data teams supporting investment teams, portfolio operations, and investor reporting.

**What they need:** A governed foundation that extends AI agents beyond engineering to analysts, operators, and other builders across the firm.

**How Coder helps:** The same self-hosted environments and AI Governance controls that serve engineers can serve analysts and operators, so the firm can expand who builds with AI without creating shadow AI.

### Insurance

**What they look like:** Actuarial, pricing, and claims teams doing heavy data science alongside engineering teams modernizing legacy policy administration and claims systems.

**What they need:** Governed environments for data science on policyholder data, which can include personal and health information, plus consistency for modernization programs.

**How Coder helps:** Data stays in the insurer's environment while actuaries and data scientists get on-demand compute and familiar tools. Standardized templates support modernization teams, and audit logs support regulatory review.

### Payments and fintech

**What they look like:** Fast-growing engineering organizations with strict card-industry and data protection obligations, where onboarding speed and infrastructure cost matter.

**What they need:** New engineers productive immediately, environments that meet PCI DSS and GDPR expectations, and less compute wasted on idle machines.

**How Coder helps:** One-click, pre-configured workspaces replace manual setup, sensitive data stays on infrastructure the firm controls, and automatic shutdown of idle workspaces reduces compute spend.

## Products Involved

- **Coder Workspaces**: self-hosted, standardized environments that keep code and data inside the institution's perimeter and replace laptop-based development or VDI.
- **AI Governance (AI Gateway and Agent Firewall)**: centralized model access, auditing, budgets, and agent network policy, so institutions can adopt AI with evidence for risk and compliance teams.
- **Coder Agents**: governed coding agents that run on the institution's own infrastructure, with model traffic routed through AI Gateway.

## Proof Points

All published by Coder. Only named customers below have approved public stories.

- **DekaBank**, an ECB-regulated, systemically critical German financial institution, runs Coder on its own on-premises Kubernetes platform for 700 engineers. Onboarding fell to under 15% of its previous time, technically caused waiting time dropped 60%, and its information security team approved the deployment through standard processes without special audits. Deka is now preparing to bring AI coding agents into the same governed environment. ([DekaBank success story](https://coder.com/success-stories/dekabank))
- **KKR** runs Coder across an engineering organization of more than 500 engineers and wants to deploy coding agents to thousands of employees, including analysts, developers, and operators. ([Series C announcement](https://coder.com/blog/coders-customers-led-our-series-c-what-that-tells-me-about-ai))
- **QRT**, a quantitative trading firm operating under strict financial regulation, uses Coder to keep its trading analysts as agile and safe as its software engineers, with the same tools. ([Series C announcement](https://coder.com/blog/coders-customers-led-our-series-c-what-that-tells-me-about-ai))
- **payabl.**, a PCI DSS Level 1 and GDPR-compliant payments company, cut onboarding from one week to under a minute and improved resource efficiency by 20% with automatic shutdown of idle workspaces. ([payabl. success story](https://coder.com/success-stories/payabl))
- A **global financial technology company** with more than 15,000 engineers is moving from 15 to 30 day onboarding to first commit on day one, and doubled its active Coder users in 12 months. ([Global fintech success story](https://coder.com/success-stories/financial-services))
- A **Fortune 500 global financial services firm** with 300 developers on Coder cut onboarding from weeks to hours and switching projects from hours to minutes. ([Global investment firm success story](https://coder.com/success-stories/global-investment-firm))
- A **major investment firm** used Coder port sharing so traders could test strategies as analysts built them, shortening feedback loops during trading windows. ([Financial institutions blog](https://coder.com/blog/coder-supports-financial-institutions-in-secure-compliant-development))

## Known Limitations

Coder helps institutions meet their regulatory obligations by keeping development on infrastructure they control and producing an audit trail, but it doesn't make an institution compliant on its own, and Coder's SOC 2 Type II certification covers Coder, not the customer. Coder governs the workspace, network, identity, and model-access layers; it doesn't replace an institution's broader endpoint security, change management, or model risk management programs. For current gaps in agent governance, see the AI Governance message house's Known Limitations.

## Messaging Guidance

- Say Coder **helps** institutions meet DORA, PCI DSS, GDPR, and similar requirements. Don't say Coder makes them compliant.
- Frame Coder around fit: the problems each type of institution faces and the outcomes it gets, not how it buys. Security and risk teams care most about control and evidence; platform teams and builders care most about speed and developer experience. Strong fit means addressing both.
- Name only customers with published stories. Describe everyone else generically, for example "a global investment bank."
- Recognize the builders specific to the industry. Quants, researchers, actuaries, and analysts are users too.

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
- [Protectionist persona](../audiences/personas/protectionist.md)
