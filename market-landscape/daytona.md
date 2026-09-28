# Coder and Daytona

| Field | Value |
|---|---|
| Date generated | 2026-09-28 |
| Category | Competitive |

*(Daytona began as an open-source development environment manager and repositioned around sandboxed AI code execution in early 2025, per [Morph](https://www.morphllm.com/comparisons/daytona-alternative) and [Northflank](https://northflank.com/blog/top-daytona-io-alternatives-for-running-ai-code-in-secure-sandboxed-environments). The company name is unchanged.)*

## One-Line Positioning

Daytona is a managed API for creating fast, programmable sandboxes that agents and AI products call at high volume, while Coder is self-hosted, Terraform-defined infrastructure where an enterprise's developers and coding agents work under the enterprise's own identity, network, and audit controls.

## Strategic Themes and Patterns

- **Relationship.** Competitive, with a narrow overlap. Daytona runs its own sandbox infrastructure and control plane ([Daytona docs](https://www.daytona.io/docs/en/)), and it publishes guides for running [Cursor self-hosted machines](https://www.daytona.io/docs/en/guides/cursor/cursor-self-hosted-machines/) and [Claude Managed Agents self-hosted environments](https://www.daytona.io/docs/en/guides/claude/claude-managed-agents/) on Daytona sandboxes. Coder addresses the same need with [Agent Relay](https://coder.com/docs/ai-coder/agent-relay/cursor). Most of Daytona's other use cases, such as code interpreters inside AI products, reinforcement learning, and computer use ([Daytona Series A post](https://www.daytona.io/dotfiles/daytona-raises-24m-series-a-to-give-every-agent-a-computer)), are outside Coder's scope.
- **Choice, Control, Consistency.** The main tradeoff is Control. On Daytona's managed cloud, code and execution data run on Daytona-operated infrastructure. With [customer managed compute](https://www.daytona.io/docs/en/runners/), the runners move to the customer, but [Daytona provides the control plane](https://www.daytona.io/). Coder runs both the control plane and the workspaces on customer infrastructure, including [air-gapped deployments](https://coder.com/docs/install/airgap). Consistency is a smaller tradeoff. Daytona environments are built from Docker images and snapshots ([Daytona docs](https://www.daytona.io/docs/en/)), while Coder environments are Terraform templates that can target VMs, Kubernetes, containers, and Windows ([Coder Workspaces](https://coder.com/solutions/workspaces)).
- **Lock-in risk.** Agents built against Daytona's SDK and lifecycle API (create, snapshot, fork, resume) depend on that API. In June 2026 Daytona moved core development to a private codebase and stopped updating the public AGPL repository ([daytonaio/daytona README](https://github.com/daytonaio/daytona), [Daytona blog](https://www.daytona.io/dotfiles/updates/daytona-is-going-closed-source)). Teams that relied on self-hosting the open-source stack now have to choose between the frozen v0.190.0 release, a community fork such as [Nightona](https://github.com/nightona-co/nightona), or Daytona's managed offerings. For an executive, the question is whether they can still change course if the vendor's licensing or deployment model changes again.
- **Build versus buy.** For enterprises that want coding agents to run inside their own perimeter, the realistic alternative to Coder is usually an internal platform. That means building environment provisioning, identity, network policy, and audit on top of Kubernetes or VMs, and possibly wiring in a sandbox API like Daytona's as one component. Consistent with [Why Coder](../company/why-coder.md), building and maintaining that layer well is only realistic for a small number of organizations with substantial platform engineering capacity.
- **Where Daytona is sufficient on its own.** A team building an AI product that needs to run untrusted, model-generated code at high volume, with per-second billing and fast startup, is Daytona's core audience ([Daytona pricing](https://www.daytona.io/pricing)). That team usually isn't asking for governed, self-hosted developer environments.

## Coder's Strengths Here

- **Fully self-hosted, including the control plane.** Coder runs on customer infrastructure and supports all features in air-gapped and offline environments ([Coder air-gapped docs](https://coder.com/docs/install/airgap)). Daytona's customer managed compute keeps the control plane with Daytona ([Daytona homepage](https://www.daytona.io/), [Daytona runners docs](https://www.daytona.io/docs/en/runners/)).
- **Same platform for developers and agents.** Coder workspaces serve human developers in VS Code, JetBrains, Cursor, and other IDEs, as well as agents ([Coder Workspaces](https://coder.com/solutions/workspaces), [Coder AI docs](https://coder.com/docs/ai-coder)). Daytona is designed primarily for programmatic use through SDKs, API, and CLI ([Daytona docs](https://www.daytona.io/docs/en/)).
- **Agent loop can run on customer infrastructure.** Coder Agents runs the agent loop in the Coder control plane on the customer's infrastructure, so workspaces can be fully network isolated ([Coder AI docs](https://coder.com/docs/ai-coder)).
- **AI-specific governance.** AI Gateway provides centralized authentication, audit trails of prompts and tool invocations, and policy enforcement against LLM providers. Agent Firewall adds process-level network and command policies ([Coder AI docs](https://coder.com/docs/ai-coder), [Agent Firewall docs](https://coder.com/docs/ai-coder/agent-firewall)). AI Governance is included with a Premium license rather than sold as a separate add-on ([AI Governance message house](../products/coder-ai-governance/message-house.md)).
- **Agent Relay for cloud agents.** Agent Relay runs Cursor and Claude Code agent tool calls in self-hosted Coder workspaces, with audit records that tie each run to the agent session and user ([Agent Relay for Cursor](https://coder.com/docs/ai-coder/agent-relay/cursor), [Claude Code announcement](https://coder.com/blog/agent-relay-claude-code-agentic-development)).
- **Workspace-level access control.** Coder offers predefined roles, OIDC SSO, and template permissions ([Coder Workspaces](https://coder.com/solutions/workspaces)). Daytona documents that organization roles don't govern what a member can do inside a running sandbox, and that every member of an organization can reach that organization's running sandboxes ([Daytona organizations docs](https://www.daytona.io/docs/en/organizations/)).

## Daytona Overview

- **What it is.** Daytona describes itself as "secure and elastic infrastructure for running AI-generated code." It provides sandboxes with a dedicated kernel, filesystem, network stack, and allocated compute ([Daytona docs](https://www.daytona.io/docs/en/)).
- **Architecture.** Sandboxes run as Linux containers by default. Daytona also offers Linux VM, Windows, GPU, and macOS sandboxes ([Daytona sandboxes docs](https://www.daytona.io/docs/en/sandboxes/)). Daytona says it uses Sysbox as its container runtime ([Daytona security exhibit](https://www.daytona.io/docs/en/security-exhibit/)). Some secondary sources describe the default isolation differently ([Northflank](https://northflank.com/blog/top-daytona-io-alternatives-for-running-ai-code-in-secure-sandboxed-environments)).
- **Speed and state.** Daytona says sandboxes start in under 90ms and support snapshots, persistence, and parallel runs ([Daytona docs](https://www.daytona.io/docs/en/)).
- **Governance features.** Audit logs cover sandbox lifecycle and user activity ([Daytona audit logs](https://www.daytona.io/docs/en/audit-logs/)). Per-sandbox network allow lists and block-all rules are available, and custom rules require higher billing tiers ([Daytona network limits](https://www.daytona.io/docs/en/network-limits/)). Daytona says it meets HIPAA, SOC 2, and GDPR standards ([Daytona homepage](https://www.daytona.io/)).
- **Target customer.** Teams building coding agents, computer-use systems, and reinforcement learning infrastructure ([Daytona Series A post](https://www.daytona.io/dotfiles/daytona-raises-24m-series-a-to-give-every-agent-a-computer)). Named customers include LangChain, Turing, Writer, and SambaNova (same source).
- **Deployment model.** The primary offering is a managed cloud. Daytona also offers [customer managed compute](https://www.daytona.io/docs/en/runners/), where the customer runs the runners and Daytona runs the control plane, and [single tenant deployment](https://www.daytona.io/dotfiles/single-tenant) as a managed, isolated instance. In January 2026, Custom Regions were invite-only and experimental ([Daytona January 2026 update](https://www.daytona.io/dotfiles/updates/what-s-new-at-daytona-january-2026)). Their current status isn't publicly confirmed.
- **Source availability.** Daytona was AGPL-3.0 open source until June 2026, when core development moved to a private codebase. The public repository stays available at v0.190.0 without updates ([daytonaio/daytona README](https://github.com/daytonaio/daytona), [Daytona blog](https://www.daytona.io/dotfiles/updates/daytona-is-going-closed-source)). It's unclear from public sources whether a fully self-hosted control plane is offered for current, closed-source releases.
- **Company.** Daytona raised a $24M Series A led by FirstMark in February 2026 ([PR Newswire](https://www.prnewswire.com/news-releases/daytona-raises-24m-series-a-to-give-every-agent-a-computer-302680740.html)).

## Coder Overview for This Comparison

- **Coder Workspaces.** Self-hosted development environments defined as Terraform templates, with prebuilt workspace pools to reduce startup time ([Prebuilt workspaces docs](https://coder.com/docs/admin/templates/extending-templates/prebuilt-workspaces)). See the [Coder Workspaces message house](../products/coder-workspaces/message-house.md).
- **Coder Agents.** A native coding agent whose loop runs in the Coder control plane and provisions workspaces for tool execution ([Coder AI docs](https://coder.com/docs/ai-coder)). See the [Coder Agents message house](../products/coder-agents/message-house.md).
- **Coder Agent Relay.** Connects cloud-hosted agent sessions to self-hosted Coder workspaces. The provider keeps orchestration and inference, and a worker in the workspace executes tool calls ([Coder AI docs](https://coder.com/docs/ai-coder)). See [Coder Agent Relay](../products/coder-agent-relay/).
- **AI Governance.** AI Gateway and Agent Firewall ([Agent Firewall docs](https://coder.com/docs/ai-coder/agent-firewall)). See the [AI Governance message house](../products/coder-ai-governance/message-house.md), which covers the difference between a sandbox and agent governance.

## Where Daytona Is Strong or Coder Has a Gap

- **Startup time.** Daytona says sandboxes start in under 90ms ([Daytona docs](https://www.daytona.io/docs/en/)). Coder workspace provisioning time depends on template complexity. Prebuilt workspaces bring complex templates down to under a minute ([Coder blog](https://coder.com/blog/launch-week-2025-instant-infrastructure)), which is still slower for high-volume, short-lived execution.
- **Snapshot and fork primitives.** Daytona exposes stateful snapshots and forking as first-class API operations for agents ([PR Newswire](https://www.prnewswire.com/news-releases/daytona-raises-24m-series-a-to-give-every-agent-a-computer-302680740.html)). Coder does not market an equivalent per-sandbox fork primitive.
- **Sandbox types beyond Linux.** Daytona offers macOS sandboxes on Apple silicon and computer-use desktops for Linux, Windows, and macOS ([Daytona sandboxes docs](https://www.daytona.io/docs/en/sandboxes/), [Daytona homepage](https://www.daytona.io/)). Coder supports Windows workspaces. Coder's public docs don't market macOS sandboxes or computer-use desktops.
- **Zero-ops start.** Daytona offers self-serve signup with $200 in free compute and per-second billing ([Daytona pricing](https://www.daytona.io/pricing)). Coder is self-hosted, so the customer runs and operates the deployment.
- **Embedding in products.** Daytona's SDKs are designed for developers who embed code execution in their own AI products ([Daytona docs](https://www.daytona.io/docs/en/)). Coder is built for an organization's internal developers and agents, not as a runtime for third-party end users.

## Known Limitations in Daytona's Approach

- **Control plane stays with Daytona under customer managed compute (as of 2026-09-28).** Daytona's homepage says customer managed compute runs sandboxes in the customer's cloud while Daytona provides the control plane ([Daytona homepage](https://www.daytona.io/)).
- **Open-source stack no longer maintained (as of 2026-09-28).** The public repository gets no further updates, fixes, or releases ([daytonaio/daytona README](https://github.com/daytonaio/daytona)). The last open release, v0.190.0, shipped on June 23, 2026 ([Daytona changelog](https://www.daytona.io/changelog)).
- **Organization roles don't restrict in-sandbox access (as of 2026-09-28).** Any member of an organization can run processes, read and write files, and use the terminal in that organization's running sandboxes ([Daytona organizations docs](https://www.daytona.io/docs/en/organizations/)).
- **Network policy depends on billing tier (as of 2026-09-28).** Organizations on Tier 1 and Tier 2 cannot override network policy at the sandbox level ([Daytona network limits](https://www.daytona.io/docs/en/network-limits/)).
- **Audit log export not yet available (as of 2026-09-28).** Daytona's audit log docs list compliance export as coming soon ([Daytona audit logs](https://www.daytona.io/docs/en/audit-logs/)).

## Common Questions

- **Isn't Daytona just a faster Coder?** No. Daytona is an API for short-lived or stateful sandboxes that programs call ([Daytona docs](https://www.daytona.io/docs/en/)), while Coder provides governed environments for developers and agents on the customer's infrastructure ([Coder Workspaces](https://coder.com/solutions/workspaces)).
- **Can Daytona run on our own infrastructure?** Partly. With customer managed compute, runners are yours and Daytona runs the control plane ([Daytona runners docs](https://www.daytona.io/docs/en/runners/)). The fully self-hosted open-source stack is frozen at v0.190.0 ([daytonaio/daytona README](https://github.com/daytonaio/daytona)). Coder runs entirely on your infrastructure, including air-gapped ([Coder air-gapped docs](https://coder.com/docs/install/airgap)).
- **We want to run Cursor or Claude cloud agents on our own infrastructure. Which should we use?** Both publish an approach. Daytona has guides for [Cursor](https://www.daytona.io/docs/en/guides/cursor/cursor-self-hosted-machines/) and [Claude Managed Agents](https://www.daytona.io/docs/en/guides/claude/claude-managed-agents/), with a customer-run orchestrator. Coder Agent Relay provisions a workspace from a platform-managed template for each session and logs which session and user it served ([Agent Relay for Cursor](https://coder.com/docs/ai-coder/agent-relay/cursor)).
- **Does Daytona's sandbox isolation cover agent governance?** Only partly. Daytona provides isolation, network allow lists, and audit logs ([Daytona network limits](https://www.daytona.io/docs/en/network-limits/), [Daytona audit logs](https://www.daytona.io/docs/en/audit-logs/)). Coder adds LLM-level audit of prompts and tool calls through AI Gateway ([Coder AI docs](https://coder.com/docs/ai-coder)).
- **Can we use both?** Yes. A team can use Daytona as the code-execution runtime inside a customer-facing AI product, and use Coder for its internal developers and coding agents. The two serve different workloads.

## When Daytona Alone Is Enough

- **AI products that run model-generated code.** A company adding a code interpreter or agent runtime to its own product, where users are external and workloads are short and high volume ([Daytona docs](https://www.daytona.io/docs/en/)).
- **Reinforcement learning and evaluation.** Teams that need to create many parallel, disposable environments for RL rollouts or benchmarks ([Daytona Series A post](https://www.daytona.io/dotfiles/daytona-raises-24m-series-a-to-give-every-agent-a-computer)).
- **Teams without self-hosting requirements.** Organizations comfortable running code on vendor-managed infrastructure that don't need governed developer environments or air-gapped deployment.

## Pricing and Packaging

- **Daytona.** Usage-based, billed per second, with $200 in free compute. vCPU is listed at $0.0504/h, and GPU and Windows rates are listed separately ([Daytona pricing](https://www.daytona.io/pricing)). A secondary source reports memory at $0.0162/GiB-h ([Tech Insider](https://tech-insider.org/e2b-vs-modal-vs-daytona-2026/)). Customer managed compute and single tenant pricing aren't public.
- **Coder.** Community is free and open source. Premium pricing isn't public. AI Governance (AI Gateway and Agent Firewall) is included with Premium, not sold as a separate add-on ([AI Governance message house](../products/coder-ai-governance/message-house.md), [Packaging](../company/packaging.md)). AI Premium removes the concurrent-agent limit of 5 that applies on Community and Premium ([Coder pricing](https://coder.com/pricing)). Coder doesn't charge for compute. Customers pay their own cloud or on-prem costs.
- **Structural difference.** Daytona charges for the compute it runs. Coder is licensed software running on compute the customer already buys, so a direct price comparison depends on workload and isn't meaningful at list price.

## Sources

- **[Daytona documentation home](https://www.daytona.io/docs/en/).** Product definition, sandbox model, startup time, SDKs. Primary. Accessed 2026-09-28.
- **[Daytona sandboxes docs](https://www.daytona.io/docs/en/sandboxes/).** Sandbox types (container, VM, Windows, GPU, macOS). Primary. Accessed 2026-09-28.
- **[Daytona homepage](https://www.daytona.io/).** Customer managed compute and control plane statement, compliance claims, computer-use desktops. Primary. Accessed 2026-09-28.
- **[Daytona pricing](https://www.daytona.io/pricing).** Usage-based rates, free credits, per-second billing. Primary. Accessed 2026-09-28.
- **[Daytona customer managed compute docs](https://www.daytona.io/docs/en/runners/).** Runner and custom region model. Primary. Accessed 2026-09-28.
- **[Daytona single tenant deployment](https://www.daytona.io/dotfiles/single-tenant).** Managed isolated instance option. Primary. Accessed 2026-09-28.
- **[Daytona January 2026 update](https://www.daytona.io/dotfiles/updates/what-s-new-at-daytona-january-2026).** Custom regions invite-only and experimental status at that time. Primary. Accessed 2026-09-28.
- **[Daytona organizations docs](https://www.daytona.io/docs/en/organizations/).** Role scope and in-sandbox access. Primary. Accessed 2026-09-28.
- **[Daytona network limits docs](https://www.daytona.io/docs/en/network-limits/).** Network policy and tier restrictions. Primary. Accessed 2026-09-28.
- **[Daytona audit logs docs](https://www.daytona.io/docs/en/audit-logs/).** Audit coverage and export status. Primary. Accessed 2026-09-28.
- **[Daytona security exhibit](https://www.daytona.io/docs/en/security-exhibit/).** Container runtime (Sysbox). Primary. Accessed 2026-09-28.
- **[Daytona Cursor self-hosted machines guide](https://www.daytona.io/docs/en/guides/cursor/cursor-self-hosted-machines/).** Cursor on Daytona. Primary. Accessed 2026-09-28.
- **[Daytona Claude Managed Agents guide](https://www.daytona.io/docs/en/guides/claude/claude-managed-agents/).** Claude Managed Agents on Daytona. Primary. Accessed 2026-09-28.
- **[daytonaio/daytona repository](https://github.com/daytonaio/daytona).** Move to private codebase, repository no longer updated. Primary. Accessed 2026-09-28.
- **[Daytona is going closed source](https://www.daytona.io/dotfiles/updates/daytona-is-going-closed-source).** Daytona's announcement of the move to closed source. Primary. Accessed 2026-09-28.
- **[Daytona changelog](https://www.daytona.io/changelog).** v0.190.0 release date. Primary. Accessed 2026-09-28.
- **[Daytona Series A post](https://www.daytona.io/dotfiles/daytona-raises-24m-series-a-to-give-every-agent-a-computer).** Use cases and named customers. Primary. Accessed 2026-09-28.
- **[PR Newswire Series A release](https://www.prnewswire.com/news-releases/daytona-raises-24m-series-a-to-give-every-agent-a-computer-302680740.html).** Funding details, snapshot and fork capabilities. Primary. Accessed 2026-09-28.
- **[Nightona](https://github.com/nightona-co/nightona).** Community fork of v0.190.0. Secondary. Accessed 2026-09-28.
- **[Northflank](https://northflank.com/blog/top-daytona-io-alternatives-for-running-ai-code-in-secure-sandboxed-environments).** Pivot history, differing description of default isolation. Secondary (competitor-authored). Accessed 2026-09-28.
- **[Morph](https://www.morphllm.com/comparisons/daytona-alternative).** Pivot timeline. Secondary. Accessed 2026-09-28.
- **[Tech Insider](https://tech-insider.org/e2b-vs-modal-vs-daytona-2026/).** Memory rate. Secondary. Accessed 2026-09-28.
- **[Coder air-gapped docs](https://coder.com/docs/install/airgap).** Air-gapped support. Primary. Accessed 2026-09-28.
- **[Coder AI docs](https://coder.com/docs/ai-coder).** Coder Agents, Agent Relay, AI Gateway. Primary. Accessed 2026-09-28.
- **[Agent Relay for Cursor](https://coder.com/docs/ai-coder/agent-relay/cursor).** Relay architecture and session logging. Primary. Accessed 2026-09-28.
- **[Agent Relay Claude Code announcement](https://coder.com/blog/agent-relay-claude-code-agentic-development).** Claude Code support and audit records. Primary. Accessed 2026-09-28.
- **[Agent Firewall docs](https://coder.com/docs/ai-coder/agent-firewall).** Process-level firewall. Primary. Accessed 2026-09-28.
- **[Coder prebuilt workspaces docs](https://coder.com/docs/admin/templates/extending-templates/prebuilt-workspaces).** Prebuild pools. Primary. Accessed 2026-09-28.
- **[Coder launch week blog](https://coder.com/blog/launch-week-2025-instant-infrastructure).** Prebuilt workspace startup times. Primary. Accessed 2026-09-28.
- **[Coder Workspaces solution page](https://coder.com/solutions/workspaces).** IDE support, roles, SSO, templates. Primary. Accessed 2026-09-28.
- **[Coder pricing](https://coder.com/pricing).** Editions and agent limits. Primary. Accessed 2026-09-28.
- **[Coder AI Governance message house](../products/coder-ai-governance/message-house.md) and [Packaging](../company/packaging.md).** AI Governance included with Premium, not sold separately. Primary (this repository). Accessed 2026-09-28.
