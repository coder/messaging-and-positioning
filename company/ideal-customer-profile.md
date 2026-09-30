# Ideal Customer Profile

This expands on `company/message-house.md`'s "Who We're For" section with the fuller set of signals Coder uses to identify a strong-fit organization. See each product's own "Target Market / ICP" section for how these signals narrow further by product.

## Industry

Coder's strongest fit is with Global 2000 organizations, concentrated in finance, banking, government (federal and state), software and services, technology, automotive, insurance, telecommunications, agriculture, manufacturing, marketing, research and development, retail, e-commerce, aerospace, healthcare, and consulting. The common thread across these industries is that software and data processing are central to how the organization generates revenue, not a supporting function.

## Company profile

Strong-fit organizations are mid-size to large enterprises, typically 2,000 or more employees with 200 or more in-house developers focused on mission-critical internal systems and product development. This includes privately owned and publicly traded companies as well as venture-backed companies from Series C through E. Organizationally, these companies have a tech-centric culture with in-house legal, security, compliance, DevOps, platform engineering, data, and development teams working together to drive core revenue through software and data.

A consistent history of investing in best-in-class technology and a pattern of strategic adoption based on open standards, rather than defaulting to whatever a single vendor bundles, is a positive signal.

## Technical signals

- Multi-cloud or hybrid-cloud adoption, with genuine operational proficiency across more than one cloud rather than a single vendor relationship
- A central software development lifecycle with Kubernetes, Git, SSO, and CI/CD practices already in place
- Application innovation running primarily on Linux, with a mix of distributions such as RHEL, Ubuntu, Debian, CentOS, or SUSE
- Confirmed investment in ML resources and a management culture that values novel data collection to inform decisions
- Development environment sprawl across teams, for example a mix of laptops, laptops paired with VDI, and laptops paired with shadow VMs, that has become a standardization and governance problem worth solving centrally

## Regulatory and compliance signals

A strong signal is an organization already facing audit scrutiny of its data protection practices under frameworks such as FFIEC, SOC, SOX, PCI, GLBA, BSA, NIST, HIPAA, GDPR, CCPA, or IAB TCF. Regulatory exposure is one of the clearest indicators that governance and control, not just developer experience, will matter to the buying decision.

## Business cycle signals

Organizations transitioning out of a rapid-growth or digital-disruption phase and into a profit-focused phase are a strong signal. These organizations are actively looking to unwind overly empowered, tool-sprawling engineering cultures and consolidate spend for margin, which creates a natural opening for centralizing development infrastructure.

## Strongest fit signals

- Software and data processing is central to revenue, not incidental to it
- Headcount above 2,000, with a multi/hybrid cloud posture and real Kubernetes, Git, and SSO proficiency
- More than 200 in-house developers and an ML team
- Purpose-built or proprietary technology systems rather than off-the-shelf SaaS for core development workflows
- Developer innovation happening primarily on Linux
- Auditable compliance is central to core business processes, not a marketing claim
- Existing developer tool sprawl that the organization is actively trying to contract
- A profit-focused business cycle rather than a pure growth-at-all-costs cycle

## Weaker fit signals

- Headcount below 1,000, or fewer than 50 in-house developers and ML staff
- A single cloud vendor with only basic VM proficiency
- Heavy reliance on SaaS or an external agency or managed service provider for core technology
- Limited developer innovation on Linux, with Windows prevalent. Coder supports Windows workspaces, but fit is strongest where most development happens on Linux
- Compliance treated as a marketing requirement rather than an operational one
- Uncentralized, basic developer tooling with no active push to standardize it
- A growth- or market-share-focused business cycle with little pressure yet to consolidate spend

## Signals Coder treats as a poor fit

Two additional patterns tend to signal a poor fit even when an organization otherwise matches the profile above.

- **Unwillingness to address risk already taken.** Organizations that have already deployed AI in a way that introduces real risk, for example broad AI coding tool rollout on unmanaged laptops, but aren't ready to acknowledge that risk or take steps to reduce it, are not yet ready for a governance conversation. That readiness often changes once the risk materializes.
- **No connected executive initiative.** AI infrastructure investment tends to succeed when it's tied to a strategic initiative with executive sponsorship, rather than pursued as a bottom-up, unbudgeted request.

## Related

- [Coder Message House](./message-house.md) for the condensed "Who We're For" summary.
- Each product's own "Target Market / ICP" section for product-specific fit signals, for example [Coder Workspaces](../products/coder-workspaces/message-house.md), [Coder Agents](../products/coder-agents/message-house.md), [AI Governance](../products/coder-ai-governance/message-house.md), and [Agent Relay](../products/coder-agent-relay/message-house.md).
