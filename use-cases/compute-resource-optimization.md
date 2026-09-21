# Compute / Resource Optimization

## Summary

Coder replaces always-on infrastructure with compute that follows a lifecycle: available the moment a developer or agent needs it, and automatically scaled back or torn down the moment they don't.

## Who This Is For

- **CTOs and CIOs**, concerned with the business impact of inefficient resource use: rising operational costs, and the compute capacity needed to keep pace with innovation.
- **Platform engineers**, responsible for the stability, scalability, and cost-efficiency of the compute underlying development and agent workloads.

## The Problem

Most development compute is provisioned to run continuously rather than to match actual demand: workspaces, virtual machines, and shared infrastructure stay up around the clock whether or not anyone is using them, and organizations pay for that idle time regardless. Without visibility into how compute is actually being used, it's hard to even tell how much of that always-on capacity is wasted or where performance bottlenecks are forming. Environments located far from the services, databases, and datasets they depend on introduce network latency, effectively wasting the compute spent waiting on it. Without a sound failover strategy, a single system failure can bring development to a standstill, an availability cost as much as a compute one. AI agents make the always-on problem worse: they introduce a new, highly variable source of compute demand, often bursty and short-lived, that most organizations have no way to attribute, cap, or automatically reclaim.

## Desired Outcome

Compute exists for as long as it's actually needed and is reclaimed automatically the moment it isn't, instead of running, and billing, around the clock by default. Platform teams have real visibility into how that compute is being used. Environments run close to the data and services they depend on, minimizing wasted latency, and infrastructure stays available even when an individual instance fails. As AI agent adoption grows, the same lifecycle model and cost controls extend to agent compute, which is often even more variable and bursty than human developer usage.

## How Coder Solves It

### Lifecycle Management, Not Always-On Infrastructure

Workspaces are resources with a lifecycle, not persistent infrastructure that runs by default. Autostart and autostop bring a workspace up when a developer needs it and shut it down automatically after inactivity, and dormancy and cleanup policies reclaim workspaces nobody's using at all. For AI agents, that same model goes further: Agent Relay provisions an ephemeral workspace per agent session and deletes it the moment the session ends, scaling to zero when no sessions are active, so agent compute exists only for as long as an agent is actually working.

### Right-Sized, Reproducible Compute

Environments are defined as code with Terraform, so compute resources are provisioned consistently and predictably instead of varying machine to machine. That consistency makes it possible to right-size infrastructure deliberately, allocating what a workload actually needs instead of over-provisioning to cover the worst case.

### Usage Visibility and Cost Control

Coder exposes Prometheus metrics so platform teams can monitor workspace health, endpoint failures, and resource utilization instead of guessing at it. Auto-stop policies shut down idle workspaces automatically, shared compute resources replace per-developer silos, and resource quotas prevent runaway spend. As agent usage scales, AI Gateway extends the same kind of budget enforcement and spend reporting to AI and agent compute specifically.

### Availability and Latency

Coder is self-hosted and cloud-agnostic, so workspaces can run on-premises or in the cloud region closest to the services, repositories, and datasets developers depend on, minimizing latency. High availability mode runs multiple server replicas, so development environments stay operational even if one instance fails.

## Products Involved

- **Coder Workspaces** — the core provisioning, scheduling, quota, and high-availability capabilities that make development compute measurable, lifecycle-managed, and controllable.
- **AI Governance (AI Gateway)** — extends budget enforcement and spend reporting to AI and agent compute as that usage scales.
- **Coder Agent Relay** — extends the same lifecycle model to cloud-hosted agent sessions, provisioning an ephemeral workspace per session and scaling to zero when idle.

## Proof Points

- Skydio reduced cloud computing costs by 90% after moving development onto Coder-managed infrastructure ([Skydio success story](https://coder.com/success-stories/skydio)).
- A financial services organization improved resource efficiency by 20% with Coder, as featured on Coder's Financial Services use case page ([coder.com/use-cases/financial-services](https://coder.com/use-cases/financial-services)).

## Known Limitations

The cost and utilization benefits depend on platform teams actually configuring and using these controls: metrics, quotas, autostart/autostop policies, and AI Gateway budgets are capabilities platform teams turn on and tune, not automatic defaults.

## Related Use Cases

- [Developer Experience](./developer-experience.md)
- [Secure Development Environments](./secure-development-environments.md)
- [Deploy AI Coding Agents](./deploy-ai-coding-agents.md)
- [ML Operations](./ml-operations.md)

## Related Audiences

- [Platform Engineer](../audiences/platform-engineer.md)
- [CTO](../audiences/cto.md)
