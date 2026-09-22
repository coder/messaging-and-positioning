# Developer Experience

## Summary

Coder gets developers contributing in hours, not weeks, by replacing manual local environment setup, approval bottlenecks, and environment drift with pre-configured, self-hosted workspaces that work on day one.

## Who This Is For

- **Individual developers** who are blocked or frustrated by slow onboarding or a poor local development experience. Onboarding isn't a one-time cost: it's paid again every time a developer switches projects.
- **Platform, IT, DevOps, and SecOps teams** who absorb the time-consuming work of provisioning, approving, and troubleshooting local environments.
- **Engineering leadership** concerned with the business-level impact: inefficient use of developer time directly affects velocity and the ability to scale headcount to meet output demands, and a poor developer experience hurts retention and the ability to attract talent.

## The Problem

Onboarding a new developer, or moving an existing developer to a new project, is slow and expensive because of manual provisioning, security approvals, and local environment troubleshooting that typically falls on the developer. Local and production environments drift out of sync over time, producing the familiar "it works on my machine, but not in production" failure mode. Local hardware limits build, test, and filesystem performance, slowing feedback loops and time to market. Rolling out new tools and best practices to every developer's machine is slow and inconsistent at any real scale, so platform teams struggle to keep pace with what developers are asking for.

## Desired Outcome

New hires and contractors reach their first commit in hours, not days or weeks. Developers spend their time writing code, not configuring environments or waiting on approvals or tickets. Environments stay consistent across the team and closely mirror production, so problems surface earlier instead of after deployment. Platform teams roll out new tools, dependencies, and security policies to every developer at once, instead of machine by machine.

## How Coder Solves It

### Faster Onboarding

Coder Workspaces are defined as code and pre-provisioned, so a developer's environment is ready with the tools and dependencies they need before they open a terminal. Developers create a workspace in one click from an approved template, with no tickets or waiting on IT. New hires and contractors get a ready environment on day one, and existing developers can self-service a new workspace when they switch projects instead of rebuilding their setup from scratch.

### Consistent Environments

Because workspaces are defined as code with Terraform, every developer starts from the same reproducible environment, and that environment can be provisioned close to production, reducing the frequency of changes that work locally but fail once deployed. Since workspaces run in the cloud or on-prem rather than on a laptop, developers get access to compute that's typically far more powerful than local hardware, speeding up builds, tests, and everyday filesystem operations like installs and clones. The same standardized model extends to AI agents: workspace-based agents and Coder Agents running natively on the control plane both benefit from the same day-one-ready, reproducible environment, without requiring a separate platform.

### Centralized Control

Platform teams update the entire fleet of workspaces from a single template change, whether that's a new tool, a security patch, or a policy update, instead of pushing changes machine by machine. Source code lives on infrastructure the organization controls rather than on developer laptops or third-party services, and identity and audit apply consistently across both developers and AI agents. Auto-stop policies scale idle compute down automatically, so standardization doesn't come at the cost of runaway infrastructure spend.

## Products Involved

- **Coder Workspaces** — the core self-hosted, Terraform-provisioned environments that eliminate manual setup and environment drift.
- **Coder Agents** — extends the same day-one-ready, standardized environment model to AI agents running natively on the control plane.
- **AI Governance** — included in Coder Premium for organizations that want centralized visibility and policy control over AI tooling as part of the broader developer experience.

## Proof Points

- "One or two clicks and developers can start working. Sharing reports, exposing ports. It's all built-in. And because it's hosted remotely, we don't need expensive laptops or worry about local Docker vulnerabilities." — Sumeet Roy, DevOps Engineer at payabl
- Abridge rearchitected its developer infrastructure using Coder and transformed developer onboarding time from days to minutes. — Taruj Goyal, Senior ML/Infrastructure Engineer at Abridge
- Palantir reduced time-to-first-commit from 15 days to one hour after adopting Coder ([Palantir success story](https://coder.com/success-stories/palantir)).
- Skydio streamlined developer onboarding from a week to as little as an hour, alongside a 90% reduction in cloud computing costs ([Skydio success story](https://coder.com/success-stories/skydio)).
- Discord migrated its development process to Coder-powered cloud development environments to improve developer experience across operating systems ([Discord success story](https://coder.com/success-stories/discord)).
- A global fintech modernized onboarding for 15,000+ engineers, described as moving "from Day 30 to Day One" ([case study referenced on coder.com/use-cases/developer-experience](https://coder.com/use-cases/developer-experience)).

## Known Limitations

The onboarding and consistency gains depend on template quality and upkeep. A poorly maintained or infrequently updated template can reintroduce the same drift and setup friction Coder is meant to eliminate, so the benefit scales with how well platform teams invest in their templates over time.

## Related Use Cases

- [Secure Development Environments](./secure-development-environments.md)
- [Compute / Resource Optimization](./compute-resource-optimization.md)

## Related Audiences

- [Developer](../audiences/developer.md)
- [Platform Engineer](../audiences/platform-engineer.md)
