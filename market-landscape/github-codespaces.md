# Coder and GitHub Codespaces

| Field | Value |
|---|---|
| Date generated | 2026-09-28 |
| Category | Competitive |

## One-Line Positioning

GitHub Codespaces is a GitHub-hosted cloud development environment attached to GitHub repositories, while Coder is a self-hosted platform that provisions development environments for developers and AI agents on infrastructure the customer runs, in any cloud, on-premises, or air-gapped.

## Strategic Themes and Patterns

- **Relationship.** Competitive. Both products provide the infrastructure development environments run on. Each codespace is [hosted by GitHub in a Docker container, running on a virtual machine](https://docs.github.com/en/codespaces/about-codespaces/what-are-codespaces), and Coder [provisions workspaces on infrastructure the customer controls](https://coder.com/docs/install/airgap). An organization standardizing on one generally does not need the other for the same developers.
- **Choice, Control, Consistency.** Both products address Consistency through environments defined as code ([dev containers](https://docs.github.com/en/codespaces/about-codespaces/what-are-codespaces) for Codespaces, [Terraform templates](https://coder.com/docs/templates/tour) for Coder). The tradeoffs are in Control and Choice. Codespaces runs on GitHub-managed Azure virtual machines ([GitHub Docs](https://docs.github.com/en/codespaces/about-codespaces/what-are-codespaces)), so the customer does not choose the cloud, operate the compute, or run the service in an air-gapped network. Coder is [self-hosted and cloud-agnostic](../company/why-coder.md).
- **Lock-in risk.** Codespaces is tied to GitHub as the source host and to GitHub's hosted compute. An organization that later needs to move source control, add on-premises or multi-cloud compute, or run disconnected would need to re-platform its development environments rather than reconfigure them. Codespaces and Coder both read `devcontainer.json` ([Coder Docs](https://coder.com/docs/admin/integrations/devcontainers/integration)), which lowers the cost of moving existing Codespaces configurations to Coder.
- **Build versus buy.** For organizations that need self-hosted environments and have outgrown or can't adopt a hosted CDE, the realistic alternative to Coder is usually building an internal platform on VMs, Kubernetes, and dev containers, not another hosted vendor. See [Why Coder](../company/why-coder.md).
- **Where Codespaces is sufficient on its own.** Teams whose code already lives on GitHub, whose work runs on Linux, and who have no requirement to self-host or restrict egress can get consistent, pay-as-you-go environments with no infrastructure to operate.

## Coder's Strengths Here

- **Self-hosted, including air-gapped.** Coder runs on infrastructure the customer controls, and [all Coder features are supported in air-gapped and offline deployments](https://coder.com/docs/install/airgap).
- **Any cloud or on-premises.** Coder workspaces run on AWS, Azure, GCP, on-premises, or air-gapped infrastructure ([Coder Workspaces message house](../products/coder-workspaces/message-house.md)). Codespaces runs on GitHub-managed Azure virtual machines ([GitHub Docs](https://docs.github.com/en/codespaces/about-codespaces/what-are-codespaces)).
- **Workspaces sit inside the customer's network.** Because workspaces run in the customer's own VPC or data center, they can reach internal systems directly. By default, codespaces [have no access to resources on private networks](https://docs.github.com/en/codespaces/developing-in-a-codespace/connecting-to-a-private-network).
- **Egress control.** Codespaces documentation states there is [currently no way to restrict codespaces from accessing the public internet](https://github.com/github/docs/blob/main/content/codespaces/developing-in-a-codespace/connecting-to-a-private-network.md). Coder workspaces inherit the customer's own network policies, and Coder Premium adds process-level network controls through AI Governance ([Coder Workspaces message house](../products/coder-workspaces/message-house.md)).
- **Operating systems and workload shapes.** Codespaces runs Linux only and does not support [Windows or macOS for the remote development container](https://docs.github.com/en/codespaces/about-codespaces/what-are-codespaces). Coder templates can provision VMs, containers, Kubernetes pods, GPU instances, and Windows environments ([Coder Workspaces message house](../products/coder-workspaces/message-house.md)).
- **IDE choice.** Codespaces connects [from a browser, Visual Studio Code, or GitHub CLI](https://docs.github.com/en/codespaces/about-codespaces/what-are-codespaces), and GitHub [discontinued official support for its JetBrains integration](https://github.com/orgs/community/discussions/78982). Coder supports VS Code, JetBrains IDEs through the [JetBrains Toolbox plugin](https://github.com/coder/coder), and any SSH-capable editor.
- **Any Git provider.** Coder connects to GitHub, GitLab, Bitbucket, or Azure DevOps ([Coder Workspaces message house](../products/coder-workspaces/message-house.md)).
- **A foundation for governed AI agents.** Coder Agents and AI Governance run on the same workspace infrastructure, and third-party agents such as Claude Code and Codex [run isolated in Coder workspaces](https://github.com/coder/coder) ([Coder Workspaces message house](../products/coder-workspaces/message-house.md)).

## GitHub Codespaces Overview

- **What it is.** A [development environment hosted in the cloud](https://docs.github.com/en/codespaces/about-codespaces/what-are-codespaces), created from a template or from any branch or commit in a repository.
- **Architecture.** Each codespace is a Docker container on a GitHub-hosted virtual machine, with machine types from 2 cores, 8 GB RAM, and 32 GB storage up to 32 cores, 128 GB RAM, and 128 GB storage ([GitHub Docs](https://docs.github.com/en/codespaces/about-codespaces/what-are-codespaces)). Each codespace runs on [its own newly built VM with its own isolated virtual network](https://docs.github.com/en/codespaces/reference/security-in-github-codespaces). Environments are configured with dev container files committed to the repository.
- **Target customer.** Individual developers (personal accounts get a [monthly free quota](https://docs.github.com/en/codespaces/about-codespaces/what-are-codespaces)) and organizations on GitHub Team and Enterprise plans, whose owners can [pay for members' usage](https://docs.github.com/en/codespaces/about-codespaces/what-are-codespaces) and [enable or disable Codespaces for private and internal repositories](https://docs.github.com/en/enterprise-cloud@latest/codespaces/managing-codespaces-for-your-organization/enabling-github-codespaces-for-your-organization).
- **Deployment model.** SaaS only, operated by GitHub. Since April 2026, Codespaces is [generally available for GitHub Enterprise Cloud with data residency](https://github.blog/changelog/2026-04-01-codespaces-is-now-generally-available-for-github-enterprise-with-data-residency/), limited to organization- or enterprise-owned codespaces.

## Coder Overview for This Comparison

- **Self-hosted workspaces.** The Coder server runs a Terraform apply [each time a workspace is created, started, or stopped](https://coder.com/docs/templates/tour), so platform teams define workspaces as code on whatever infrastructure Terraform can manage.
- **Dev container support.** Coder can start dev containers through the `coder_devcontainer` Terraform resource or [discover `devcontainer.json` files automatically](https://coder.com/docs/admin/integrations/devcontainers/integration). This gives teams already using Codespaces configurations a migration path.
- **Air-gapped operation.** Documented in [Air-gapped Deployments](https://coder.com/docs/install/airgap).
- **Governance.** SSO through OIDC, RBAC, and, in Premium, audit logging, SCIM, and multi-organization access control ([Coder Workspaces message house](../products/coder-workspaces/message-house.md)).

## Where GitHub Codespaces Is Strong or Coder Has a Gap

- **No infrastructure to operate.** GitHub creates and manages the VMs. With Coder, [the customer operates both the control plane and the compute](https://infragap.com/tools/coder/) (secondary source), which requires platform engineering capacity.
- **Native to GitHub.** Codespaces launches from the repository page on GitHub, and GitHub issues each codespace [a new, automatically expiring GitHub token](https://docs.github.com/en/codespaces/reference/security-in-github-codespaces) on create or restart.
- **Low barrier to start.** Personal accounts can start [without changing settings or providing payment details](https://docs.github.com/en/codespaces/about-codespaces/what-are-codespaces), and pricing is published and metered.
- **Terraform skills required for Coder.** Coder templates are Terraform, and a secondary review notes teams [will be editing them](https://infragap.com/tools/coder/). Codespaces configuration is limited to dev container files.
- **Startup latency.** Coder notes that [complex templates can have provisioning latency](../products/coder-workspaces/message-house.md), mitigated by prebuilt workspace pools. Codespaces offers [prebuilds](https://docs.github.com/en/enterprise-cloud@latest/codespaces/developing-in-a-codespace/using-github-codespaces-in-your-jetbrains-ide) for the same purpose.

## Known Limitations in GitHub Codespaces' Approach

- **Linux only (as of 2026-09-28).** Windows and macOS are [not supported for the remote development container](https://docs.github.com/en/codespaces/about-codespaces/what-are-codespaces).
- **No self-hosted or air-gapped option (as of 2026-09-28).** Codespaces runs only on GitHub-hosted virtual machines ([GitHub Docs](https://docs.github.com/en/codespaces/about-codespaces/what-are-codespaces)).
- **Private network access requires workarounds (as of 2026-09-28).** Codespaces has no private network access by default. GitHub's CLI gateway extension is [closing down and no longer supported](https://docs.github.com/en/codespaces/developing-in-a-codespace/connecting-to-a-private-network), and GitHub recommends VPN tools such as OpenVPN. Azure VNet private networking for Codespaces was [still in beta as of April 2024](https://github.blog/news-insights/product-news/bringing-enterprise-level-security-and-even-more-power-to-github-hosted-runners/). Its current status is unclear from public sources.
- **No egress restriction; IP allow lists block creation (as of 2026-09-28).** GitHub documents that there is [no way to restrict codespaces from accessing the public internet](https://github.com/github/docs/blob/main/content/codespaces/developing-in-a-codespace/connecting-to-a-private-network.md), and that codespace creation is disabled when IP allow lists are enabled, because codespace IPs are assigned dynamically.
- **Limited IDE support (as of 2026-09-28).** Official access is through the browser, VS Code, or GitHub CLI ([GitHub Docs](https://docs.github.com/en/codespaces/about-codespaces/what-are-codespaces)). The JetBrains Gateway integration, previously in beta, [is no longer officially supported](https://github.com/orgs/community/discussions/78982).
- **GitHub-hosted source (inferred).** GitHub's documentation describes codespaces created from GitHub repositories. We found no documented support for repositories hosted on other Git providers, but also no explicit statement ruling it out.

## Common Questions

- **We already use Codespaces. Can we reuse our dev container configurations in Coder?** Yes. Coder supports `devcontainer.json` through the `coder_devcontainer` resource or automatic discovery ([Coder Docs](https://coder.com/docs/admin/integrations/devcontainers/integration)). Dev containers are not currently supported in Windows or macOS Coder workspaces.
- **Does Codespaces support data residency?** Yes, for GitHub Enterprise Cloud with data residency, [generally available since April 2026](https://github.blog/changelog/2026-04-01-codespaces-is-now-generally-available-for-github-enterprise-with-data-residency/). Data stays in the selected region, but it still runs on GitHub-operated infrastructure rather than the customer's own.
- **Can Codespaces run in an air-gapped network?** No public documentation describes this. Codespaces runs on GitHub-hosted virtual machines ([GitHub Docs](https://docs.github.com/en/codespaces/about-codespaces/what-are-codespaces)). Coder supports [air-gapped deployments with all features](https://coder.com/docs/install/airgap).
- **Do we need GitHub to use Coder?** No. Coder works with GitHub, GitLab, Bitbucket, and Azure DevOps ([Coder Workspaces message house](../products/coder-workspaces/message-house.md)).
- **Which is cheaper?** It depends on usage and existing infrastructure. Codespaces bills per core-hour plus storage on GitHub's compute. With Coder, the customer pays its own cloud or data center for compute, plus a Coder Premium license if needed. See Pricing and Packaging below.

## When GitHub Codespaces Alone Is Enough

- **GitHub-centric teams without self-hosting requirements.** Teams with code on GitHub, Linux-based workloads, and no need to restrict egress or reach private networks directly.
- **Open source, education, and short-lived work.** Contributors to public repositories, courses, and workshops benefit from starting from a repository page with a personal free quota ([GitHub Docs](https://docs.github.com/en/codespaces/about-codespaces/what-are-codespaces)).
- **Organizations without platform engineering capacity.** Teams that don't want to operate infrastructure or maintain Terraform templates.

## Pricing and Packaging

- **Codespaces is metered.** A codespace incurs [compute charges while active and storage charges while it exists](https://docs.github.com/billing/managing-billing-for-github-codespaces/about-billing-for-github-codespaces). Compute cost scales with cores, so a 16-core machine costs eight times as much per hour as a 2-core machine. A 2-core machine is [$0.18 per hour](https://github.com/orgs/community/discussions/195353) (secondary source), and storage is [$0.07 per GiB per month](https://github.com/pricing/calculator).
- **Codespaces free quota.** Personal accounts on Free and Pro include a [monthly free quota](https://docs.github.com/en/codespaces/about-codespaces/what-are-codespaces). A secondary source lists [120 core-hours and 15 GB-month for Free, and 180 core-hours and 20 GB-month for Pro](https://infragap.com/tools/github-codespaces/). Organization usage is billed to the organization when configured.
- **Coder.** Coder Community Edition is free and open source. Coder Premium pricing is not public and is available by quote. See [coder.com/pricing](https://coder.com/pricing) and [Packaging](../company/packaging.md). Compute is billed separately by the customer's own cloud or infrastructure provider.

## Sources

- **[What are GitHub Codespaces? (GitHub Docs)](https://docs.github.com/en/codespaces/about-codespaces/what-are-codespaces).** Architecture, machine types, Linux-only, connection methods, free quota, org billing. Primary. Accessed 2026-09-28.
- **[Security in GitHub Codespaces (GitHub Docs)](https://docs.github.com/en/codespaces/reference/security-in-github-codespaces).** Per-codespace VM and network isolation, token behavior. Primary. Accessed 2026-09-28.
- **[Connecting to a private network (GitHub Docs)](https://docs.github.com/en/codespaces/developing-in-a-codespace/connecting-to-a-private-network) and [source file](https://github.com/github/docs/blob/main/content/codespaces/developing-in-a-codespace/connecting-to-a-private-network.md).** Private network defaults, deprecated CLI extension, VPN guidance, IP allow list and egress limitations. Primary. Accessed 2026-09-28.
- **[GitHub Codespaces billing (GitHub Docs)](https://docs.github.com/billing/managing-billing-for-github-codespaces/about-billing-for-github-codespaces).** Compute and storage billing model. Primary. Accessed 2026-09-28.
- **[GitHub Pricing Calculator](https://github.com/pricing/calculator).** Storage rate. Primary. Accessed 2026-09-28.
- **[Codespaces GA for GitHub Enterprise with data residency (GitHub Changelog, 2026-04-01)](https://github.blog/changelog/2026-04-01-codespaces-is-now-generally-available-for-github-enterprise-with-data-residency/).** Data residency availability and ownership requirements. Primary. Accessed 2026-09-28.
- **[Bringing enterprise-level security to GitHub-hosted runners (GitHub Blog, 2024-04)](https://github.blog/news-insights/product-news/bringing-enterprise-level-security-and-even-more-power-to-github-hosted-runners/).** Azure private networking for Codespaces in beta. Primary. Accessed 2026-09-28.
- **[Enabling or disabling GitHub Codespaces for your organization (GitHub Docs)](https://docs.github.com/en/enterprise-cloud@latest/codespaces/managing-codespaces-for-your-organization/enabling-github-codespaces-for-your-organization).** Organization controls. Primary. Accessed 2026-09-28.
- **[Codespaces provider not available on JetBrains Gateway (GitHub Community discussion)](https://github.com/orgs/community/discussions/78982).** GitHub staff statement discontinuing official JetBrains support. Primary (GitHub staff reply on GitHub's forum). Accessed 2026-09-28.
- **[Codespaces bill for a 2-core workflow (GitHub Community discussion)](https://github.com/orgs/community/discussions/195353).** $0.18 per hour for 2-core. Secondary. Accessed 2026-09-28.
- **[GitHub Codespaces Review (Infragap)](https://infragap.com/tools/github-codespaces/) and [Coder Review (Infragap)](https://infragap.com/tools/coder/).** Free quota figures, Coder operating model, Terraform skill requirement, quote-only Premium pricing. Secondary. Accessed 2026-09-28.
- **[Air-gapped Deployments (Coder Docs)](https://coder.com/docs/install/airgap).** Air-gapped support. Primary. Accessed 2026-09-28.
- **[Dev Containers Integration (Coder Docs)](https://coder.com/docs/admin/integrations/devcontainers/integration).** Dev container support and limitations. Primary. Accessed 2026-09-28.
- **[Templates guided tour (Coder Docs)](https://coder.com/docs/templates/tour).** Terraform-based provisioning. Primary. Accessed 2026-09-28.
- **[coder/coder README](https://github.com/coder/coder).** JetBrains Toolbox plugin, coding agents in workspaces. Primary. Accessed 2026-09-28.
- **[Coder pricing](https://coder.com/pricing).** Editions. Primary. Accessed 2026-09-28.
- **[Coder Workspaces message house](../products/coder-workspaces/message-house.md), [Why Coder](../company/why-coder.md), [Message House](../company/message-house.md).** Coder positioning, deployment targets, Git providers, governance features. Primary (Coder). Accessed 2026-09-28.
