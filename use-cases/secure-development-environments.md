# Secure Development Environments

## Summary

Coder moves development off unmanaged laptops and onto self-hosted, governed infrastructure, so source code, credentials, and tooling stay inside the organization's control instead of scattered across individual machines.

## Who This Is For

- **CISOs**, responsible for the organization's overall security posture and under constant pressure to strengthen controls against new threats.
- **CTOs**, balancing the introduction of new technologies and developer tooling against the risk those changes might introduce.
- **CIOs**, managing IT infrastructure with a focus on service reliability and operational efficiency.
- **Platform engineers**, who have to build security into the core of their systems without degrading the developer experience, while keeping pace with internal and external compliance requirements.

## The Problem

Source code, credentials, and development tools often live on developer laptops, outside centralized visibility or control. As teams grow, that creates unmanaged access and inconsistent security practices: developers left to provision their own environments may not know, or follow, internal security guidelines. Centralized approvals for new local tooling can take weeks, slowing developers down without necessarily making them safer. Keeping software and dependencies patched across a fleet of laptops is difficult to enforce centrally, and every unpatched machine is an exposure window. Meeting data residency and regulatory requirements (GDPR, HIPAA, FIPS, PCI DSS) is much harder when sensitive data is distributed across decentralized machines instead of consolidated in infrastructure the organization actually controls. Virtual desktop infrastructure (VDI) keeps code off laptops, but developers then work through a streamed desktop, and container tools such as Docker Desktop need [nested virtualization and a persistent desktop](https://docs.docker.com/desktop/setup/vm-vdi/) to run inside one. See [Coder and VDI](../market-landscape/vdi.md).

## Desired Outcome

Source code, credentials, and tooling stay inside infrastructure the organization manages, never on an endpoint laptop. Every workspace and agent action is attributed to a named user, with audit events flowing into the organization's existing SIEM. Network policy is defined centrally in templates rather than left to individual machine configuration, and that same policy extends to AI coding agents, not just human developers. New tooling and security patches roll out to the entire fleet of workspaces at once instead of requiring per-laptop approval and update cycles.

## How Coder Solves It

### Source Code Containment

Workspaces run on the organization's own cloud, on-prem, or air-gapped infrastructure. Source code, credentials, and tooling stay inside that perimeter, and secrets remain in the organization's existing vault rather than spreading across laptops and scripts.

### Network Isolation

Platform teams decide in each Terraform template what workspaces can reach on the network, using the controls their infrastructure already provides, such as Kubernetes network policies, cloud security groups and VPC rules, and existing egress proxies. The workspace is the network boundary, so that policy applies to every process inside it, including AI coding agents, and dedicated agent templates can apply stricter egress than developer templates.

### Identity and Audit

SSO and SCIM integration with the organization's existing identity provider applies uniformly across developers and agents. Every workspace and agent action is attributed to a named user, audit events export to the organization's SIEM, and Coder itself is SOC 2 Type II certified.

## Products Involved

- **Coder Workspaces** — the self-hosted execution environment that keeps source code, credentials, and tooling inside the organization's perimeter, with network access defined in each template.

## Proof Points

- "One or two clicks and developers can start working. Sharing reports, exposing ports. It's all built-in. And because it's hosted remotely, we don't need expensive laptops or worry about local Docker vulnerabilities." — Sumeet Roy, DevOps Engineer at payabl
- A U.S. defense intelligence organization runs Coder self-hosted on AWS GovCloud inside a fully air-gapped network. Onboarding dropped from multiple days to 3-5 minutes, developer adoption grew 500% over a multi-year deployment, and leadership gained full audit trails for compliance verification ([Defense Intelligence success story](https://coder.com/success-stories/defense-intelligence-organizations)).
- A separate U.S. Defense Intelligence platform runs the U.S. military's first true multi-tenant Coder deployment, giving 2,500+ developers pre-approved environments that inherit a centralized, platform-level ATO instead of each mission team certifying its own ([U.S. Defense Intelligence Organization success story](https://coder.com/success-stories/u-s-defense-intelligence-organization)). Coder's [defense sovereignty blog](https://coder.com/blog/ai-agent-security-sovereignty-defense) describes these as two separate organizations, so keep their metrics separate.
- Skydio reduced cloud computing costs by 90% after moving development onto Coder-managed infrastructure ([Skydio success story](https://coder.com/success-stories/skydio)), a case study Coder also features on its Secure Development Environments page.

## Known Limitations

Coder's controls govern the workspace, network, and identity layer; they don't replace an organization's broader endpoint security or compliance program, and SOC 2 Type II certification covers Coder itself, not a customer's own compliance posture. Network controls come from the template and the organization's network infrastructure: if a template doesn't restrict outbound access, its workspaces have full internet access, and the granularity and logging of allowed or blocked connections depend on that infrastructure, not on Coder.

## Related Use Cases

- [Developer Experience](./developer-experience.md)
- [Deploy AI Coding Agents](./deploy-ai-coding-agents.md)

## Related Audiences

- [Platform Engineer](../audiences/platform-engineer.md)
- [CISO](../audiences/ciso.md)
- [CTO](../audiences/cto.md)
