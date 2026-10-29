# Coder and Ona

| Field | Value |
|---|---|
| Date generated | 2026-09-28 |
| Last reviewed | 2026-10-29 |
| Category | Competitive |

*Ona was previously named Gitpod. The company [rebranded as Ona on September 2, 2025](https://ona.com/stories/gitpod-is-now-ona), and Ona [became part of OpenAI when the acquisition closed on August 10, 2026](https://ona.com/stories/ona-joins-openai). Ona's docs still note that "Gitpod" may appear in the product [during the transition](https://ona.com/docs/ona/runners/overview). On October 13, 2026, Ona announced that [Ona Cloud, its managed infrastructure, shuts down on October 31, 2026](https://ona.com/stories/ona-core-shutdown).*

## One-Line Positioning

Ona is a vendor-operated platform for running background agents, now part of OpenAI and centered on Codex, with Enterprise runners in your AWS or GCP account. Its managed Ona Cloud [shuts down on October 31, 2026](https://ona.com/stories/ona-core-shutdown). Coder is self-hosted infrastructure where the customer operates the control plane, the workspaces, and the agent loop on any cloud, on-premises, or air-gapped, with any model provider.

## Strategic Themes and Patterns

- **Relationship.** Competitive. Ona provides its own infrastructure, describing itself as a platform that [provides isolated environments and runs background agents](https://ona.com/docs/ona/understanding/how-ona-works), and it competes for the same decision as [Coder Workspaces](../products/coder-workspaces/message-house.md) and [Coder Agents](../products/coder-agents/message-house.md). The Coder Workspaces message house already lists [Ona/Gitpod among the remaining SaaS-first competitors](../products/coder-workspaces/message-house.md).
- **Choice, Control, Consistency.** Ona involves a tradeoff on Choice and Control. On Choice, Ona [recommends Codex Agent for new sessions and automations](https://ona.com/docs/ona/agents), and customer-managed runners need [OpenAI model access through Ona Intelligence or an OpenAI-compatible integration](https://ona.com/docs/ona/agents/codex); runners deploy only in [AWS or GCP](https://ona.com/docs/ona/runners/overview). On Control, Ona's [management plane is hosted by Ona](https://ona.com/docs/ona/understanding/how-ona-works) even when runners are in the customer's VPC. Consistency is not a clear tradeoff, since Ona environments are [provisioned from a Dev Container configuration](https://ona.com/docs/ona/understanding/how-ona-works).
- **Lock-in risk.** Adopting Ona ties the environment and agent layer to one vendor's hosted management plane and, as of this writing, to one model provider's recommended agent. If the organization later wants a different primary model, cloud, or deployment boundary, that becomes a platform change rather than a configuration change. Coder's positioning is the reverse, [a long-term infrastructure bet without the same bet on any individual cloud, model, or tool](../company/why-coder.md).
- **Product direction under new ownership.** Ona's own docs mark the [Anthropic harness as deprecated](https://ona.com/docs/ona/agents) and [AWS Bedrock Runtime integrations for Claude as deprecated and maintenance-only](https://ona.com/docs/ona/agents/llm-providers/bedrock). OpenAI states the Ona team will [work with the Codex team to scale Codex to more enterprises](https://openai.com/index/openai-to-acquire-ona/); Ona then [announced it is winding down Ona Cloud on October 31, 2026](https://ona.com/stories/ona-core-shutdown), closed new signups, and points Ona Cloud users to Codex Cloud. Environments do not move to Codex automatically. The shutdown notice covers Ona Cloud, and as of 2026-10-29 Ona's docs still describe [Enterprise runners in the customer's AWS or GCP account](https://ona.com/docs/ona/runners/overview).
- **Build versus buy.** For organizations that require a customer-operated control plane or air-gapped operation, the realistic alternative to Coder is building in-house, not Ona, consistent with [Why Coder](../company/why-coder.md). Ona itself frames background agents as something [leading companies built themselves and Ona delivers as a managed platform](https://ona.com/).
- **Where Ona is sufficient on its own.** Teams that are comfortable with a vendor-hosted management plane, run on AWS or GCP, and are standardizing on Codex and OpenAI models can deploy Enterprise runners in [their own AWS or GCP account](https://ona.com/docs/ona/runners/overview).
- **Prior product transitions are part of the history here.** Gitpod [discontinued its self-managed product in December 2022](https://www.gitpod.io/blog/self-hosted-not-self-managed), rebranded as Ona in 2025, joined OpenAI in 2026, and [set Ona Cloud to shut down on October 31, 2026](https://ona.com/stories/ona-core-shutdown). Buyers evaluating a multi-year self-hosted commitment may reasonably factor a vendor's history of deployment-model changes into their evaluation, the same way they would for any vendor.

## Coder's Strengths Here

- **Customer-operated control plane.** Coder is self-hosted, and [Coder Agents has no SaaS or managed component](https://coder.com/docs/ai-coder/agents). The agent loop, chat history, and tool execution all run within the customer's Coder deployment.
- **Air-gapped operation.** Coder documents that [all features are supported in air-gapped, disconnected, or offline environments](https://coder.com/docs/install/airgap). Ona's docs describe a hosted management plane, and we did not find a documented air-gapped option.
- **Model choice.** Coder Agents works with [Anthropic, OpenAI, Google, Azure, AWS Bedrock, or any OpenAI-compatible endpoint](https://coder.com/docs/ai-coder/agents/architecture), including self-hosted models, and is [not a wrapper around Claude Code or Codex](https://coder.com/docs/ai-coder/agents).
- **Any infrastructure.** Coder Workspaces run on [AWS, Azure, GCP, on-prem, or air-gapped](../products/coder-workspaces/message-house.md). Ona runners deploy in [AWS or GCP](https://ona.com/docs/ona/runners/overview).
- **No LLM credentials in workspaces.** Because the Coder Agents loop runs in the control plane, [provider credentials never enter the workspace](https://coder.com/docs/ai-coder/agents) and workspaces can be [completely network isolated](https://coder.com/docs/ai-coder).
- **Open source.** Coder Community is [free and open source under AGPL v3.0](../products/coder-workspaces/message-house.md), and Premium is [based on the same code](https://coder.com/blog/coder-community-open-source).
- **Enterprise workload depth.** Coder supports [VMs, containers, Kubernetes, GPU workloads, and Windows environments](../products/coder-workspaces/message-house.md) defined as Terraform templates.

## Ona Overview

- **What it is.** Ona is [the platform for running background agents at scale](https://ona.com/docs/ona/understanding/how-ona-works), with isolated environments pre-configured with code, tools, and dependencies. Its homepage describes [one governed way to run Ona, Codex, and other agents](https://ona.com/).
- **Architecture.** A [management plane hosted by Ona](https://ona.com/docs/ona/understanding/how-ona-works) handles authentication, organization settings, guardrails, and coordination. Runners provision environments, access source code, inject secrets, and execute agents. Ona states that source code, credentials, and build artifacts [never reach the management plane](https://ona.com/docs/ona/understanding/how-ona-works).
- **Environments.** Each task gets [an isolated VM provisioned from a Dev Container configuration](https://ona.com/docs/ona/understanding/how-ona-works). Environments are ephemeral, and prebuilds shorten startup.
- **Agents.** [Codex Agent runs the open-source Codex harness](https://ona.com/docs/ona/agents/codex) in an Ona environment. Ona also documents that [Claude Code can be installed inside an Ona environment](https://ona.com/pricing) with Claude billing handled by Anthropic.
- **Target customer.** Ona Cloud, which [shuts down on October 31, 2026](https://ona.com/stories/ona-core-shutdown), targets [individuals, small teams, and organizations that want to move fast](https://ona.com/docs/ona/runners/overview). Runners in the customer's cloud target enterprises with security, compliance, or data residency requirements. Ona cites [production use at a large US bank, a European pharma company, and an Asian sovereign wealth fund](https://ona.com/stories/ona-joins-openai).
- **Deployment model.** Hybrid. [Ona Cloud](https://ona.com/docs/ona/runners/ona-cloud) is fully vendor-managed and [shuts down on October 31, 2026](https://ona.com/stories/ona-core-shutdown). On Enterprise, runners deploy in [the customer's AWS or GCP account](https://ona.com/docs/ona/runners/overview) while the management plane stays with Ona.
- **Editors and integrations.** Ona supports [VS Code, VS Code Browser, Cursor, Windsurf, JetBrains, and Zed](https://ona.com/docs/ona/organizations/overview), plus [Slack and Linear agents](https://ona.com/docs/llms-full.txt).

## Coder Overview for This Comparison

- **Coder Workspaces.** [Self-hosted, Terraform-provisioned development environments](../products/coder-workspaces/message-house.md) for developers and agents, IDE-agnostic, running on any cloud or on-prem.
- **Coder Agents.** A [self-hosted coding agent whose loop runs in the Coder control plane](https://coder.com/docs/ai-coder/agents), with admin-controlled providers, models, and system prompts that are [enforced server-side](https://coder.com/docs/ai-coder/agents/platform-controls).
- **AI Governance.** Included with Premium, adding [AI Gateway for authentication, prompt and tool audit trails, and policy enforcement](https://coder.com/docs/ai-coder).
- **Third-party agents.** Agents like [Claude Code, Codex, and OpenCode can run isolated in Coder workspaces](https://github.com/coder/coder).

## Where Ona Is Strong or Coder Has a Gap

- **No control plane for the customer to run.** Ona [hosts the management plane](https://ona.com/docs/ona/understanding/how-ona-works), so Enterprise customers operate only runners. Coder is always self-hosted and requires the customer to operate it, and some reviewers cite [operational overhead for small teams without dedicated DevOps](https://www.g2.com/products/coder/pricing) (secondary source).
- **Ephemeral VM per task.** Ona gives each task [a dedicated VM with its own compute, storage, and networking](https://ona.com/docs/ona/understanding/how-ona-works). Coder supports ephemeral workspaces, but isolation level depends on how each template is written.
- **Event-driven automations.** Ona automations can be [triggered by PRs, schedules, or webhooks](https://ona.com/docs/ona/runners/aws/enterprise-runner/overview), with Slack and Linear entry points. Coder Agents can be triggered via API from CI, as described in the [Coder Agents message house](../products/coder-agents/message-house.md), but Ona ships more prebuilt triggers.
- **Tight Codex integration.** For organizations standardized on OpenAI, Ona offers native Codex features such as [goal mode](https://ona.com/docs/ona/agents/codex).
- **Mobile access.** Ona [works on your phone](https://ona.com/stories/gitpod-is-now-ona) for starting and reviewing tasks.

## Known Limitations in Ona's Approach

- **Hosted management plane.** As of 2026-09-28, [authentication, organization settings, guardrails, and coordination are hosted by Ona](https://ona.com/docs/ona/understanding/how-ona-works) in every deployment model. We found no documented customer-operated control plane.
- **Two clouds for customer runners.** As of 2026-09-28, customer runners deploy in [AWS or GCP](https://ona.com/docs/ona/runners/overview). We found no documented Azure or on-premises runner.
- **No documented air-gapped option.** As of 2026-09-28, we did not find air-gapped deployment in Ona's docs. GCP runners need outbound access to [Ona's control plane and release endpoints](https://ona.com/docs/ona/runners/gcp/detailed-access-requirements).
- **Model access on customer runners.** As of 2026-09-28, Codex Agent on customer-managed runners requires [OpenAI model access through Ona Intelligence or an OpenAI-compatible LLM integration](https://ona.com/docs/ona/agents/codex). Custom token providers for Ona's own agent are [available by exception for Enterprise customers](https://ona.com/docs/ona/agents/llm-providers/overview).
- **Deprecated Claude paths.** As of 2026-09-28, the [Anthropic harness is deprecated](https://ona.com/docs/ona/agents), Ona-managed Anthropic model access is [no longer available on Ona Cloud](https://ona.com/docs/ona/agents/llm-providers/overview), and Bedrock Runtime, Google Vertex AI, and direct Anthropic API integrations are [deprecated and maintenance-only](https://ona.com/docs/ona/agents/llm-providers/overview). New direct LLM integrations [use AWS Bedrock, AWS Bedrock Mantle, or OpenAI](https://ona.com/docs/llms-full.txt).

## Common Questions

- **Isn't Ona self-hosted too?** Ona runners can run in [your AWS or GCP account](https://ona.com/docs/ona/runners/overview), but the [management plane is hosted by Ona](https://ona.com/docs/ona/understanding/how-ona-works). With Coder, the control plane, workspaces, and [agent loop all run in your deployment](https://coder.com/docs/ai-coder/agents).
- **What changed with the OpenAI acquisition?** Ona [joined OpenAI on August 10, 2026](https://ona.com/stories/ona-joins-openai), and OpenAI says the team will [work with the Codex team](https://openai.com/index/openai-to-acquire-ona/). Ona's docs now [recommend Codex Agent for new sessions](https://ona.com/docs/ona/agents), and [Ona Cloud shuts down on October 31, 2026](https://ona.com/stories/ona-core-shutdown). As of 2026-10-29, we found no published end date for Enterprise runners.
- **What happens to Ona Cloud users?** Ona Cloud [shuts down on October 31, 2026](https://ona.com/stories/ona-core-shutdown), and new signups are closed. Environments do not move to Codex automatically, and Ona points users to Codex Cloud. Ona environments are [provisioned from a Dev Container configuration](https://ona.com/docs/ona/runners/overview), and Coder [supports the Dev Container specification](https://coder.com/docs/@main/admin/integrations/devcontainers), so teams moving to Coder can reuse their existing `devcontainer.json` files. See the [Moving from Ona to Coder FAQ](../products/coder-workspaces/ona-migration-faq.md) for discovery questions and migration steps.
- **Can we use Claude or Gemini with Ona?** Claude Code can be [installed inside an Ona environment](https://ona.com/pricing) with separate Anthropic billing. Ona's native Claude paths are closed to new use, since [Ona Agent and Ona-managed Anthropic model access are no longer available on Ona Cloud](https://ona.com/docs/ona/agents/llm-providers/overview) and [Google Vertex AI integrations are deprecated and new ones cannot be created](https://ona.com/docs/ona/google-vertex). Coder Agents supports [Anthropic, OpenAI, Google, Azure, Bedrock, and OpenAI-compatible endpoints](https://coder.com/docs/ai-coder/agents/architecture) natively.
- **Can Coder run Codex?** Yes. Coder runs [Codex, Claude Code, and OpenCode isolated in Coder workspaces](https://github.com/coder/coder), and Coder Agents can use OpenAI models among others.
- **We're on Azure or on-prem. Does Ona work?** Ona documents runners for [AWS and GCP](https://ona.com/docs/ona/runners/overview). Coder runs on [AWS, Azure, GCP, on-prem, or air-gapped](../products/coder-workspaces/message-house.md).
- **Do both keep source code in our network?** Ona states that with a runner in your VPC, [source code, credentials, and build artifacts stay in your network](https://ona.com/docs/ona/understanding/how-ona-works). Coder keeps source code in your perimeter and also keeps orchestration and [LLM credentials in your control plane](https://coder.com/docs/ai-coder/agents).

## When Ona Alone Is Enough

- **OpenAI-standardized teams on AWS or GCP.** Organizations that have chosen Codex and OpenAI models and accept a vendor-hosted management plane get a managed path with native Codex features.
- **Background agent automations without strict boundary requirements.** Teams mainly after PR, schedule, or webhook-triggered agents, without air-gap or customer-operated control plane requirements, may find Ona's prebuilt automations sufficient.

## Pricing and Packaging

- **Ona.** Ona's Core tier runs on Ona Cloud, which [shuts down on October 31, 2026](https://ona.com/stories/ona-core-shutdown). Ona says it refunds October payments and unused purchased credits. As of 2026-10-29, ona.com/pricing redirects to [Ona's sales contact page](https://ona.com/contact/sales). Enterprise runners deploy in [the customer's AWS or GCP account](https://ona.com/docs/ona/runners/overview), are [available by contacting sales](https://ona.com/docs/ona/runners/gcp/overview), and Enterprise usage is [billed in credits](https://ona.com/docs/ona/billing/usage). Runners in the customer's account also put infrastructure costs on the customer's cloud bill, and Ona's cost guides list the [AWS](https://ona.com/docs/ona/runners/aws/aws-runner-costs) and [GCP](https://ona.com/docs/ona/runners/gcp/gcp-runner-costs) resources each runner deploys.
- **Coder.** Coder Community is free and open source, Premium is quote-based, and [AI Premium removes the 5 concurrent Coder Agents limit](https://coder.com/pricing) that applies to Community and Premium. See [coder.com/pricing](https://coder.com/pricing) for current tiers and [Packaging](../company/packaging.md) for the narrative.

## Sources

- **[Gitpod is now Ona](https://ona.com/stories/gitpod-is-now-ona).** Rebrand date, tiers, VPC deployment, mobile access. Primary. Accessed 2026-09-28.
- **[Ona is joining OpenAI](https://ona.com/stories/ona-joins-openai).** Acquisition close date, customer references. Primary. Accessed 2026-09-28.
- **[OpenAI to acquire Ona](https://openai.com/index/openai-to-acquire-ona/).** Acquisition terms and post-close plans. Primary (acquirer). Accessed 2026-09-28.
- **[How Ona Works](https://ona.com/docs/ona/understanding/how-ona-works).** Management plane and runner architecture, environment model. Primary. Accessed 2026-09-28.
- **[Ona runners overview](https://ona.com/docs/ona/runners/overview).** Ona Cloud versus AWS and GCP runners. Primary. Accessed 2026-09-28.
- **[Ona Cloud](https://ona.com/docs/ona/runners/ona-cloud).** Managed runner option. Primary. Accessed 2026-09-28.
- **[GCP Runner](https://ona.com/docs/ona/runners/gcp/overview) and [GCP Runner Access Requirements](https://ona.com/docs/ona/runners/gcp/detailed-access-requirements).** Enterprise availability, outbound requirements. Primary. Accessed 2026-09-28.
- **[Enterprise AWS Runner](https://ona.com/docs/ona/runners/aws/enterprise-runner/overview).** Automation triggers. Primary. Accessed 2026-09-28.
- **[Agents in Ona](https://ona.com/docs/ona/agents) and [Codex Agent](https://ona.com/docs/ona/agents/codex).** Codex as recommended agent, model access on runners, deprecated Anthropic harness. Primary. Accessed 2026-09-28.
- **[LLM providers overview](https://ona.com/docs/ona/agents/llm-providers/overview), [AWS Bedrock Runtime (deprecated)](https://ona.com/docs/ona/agents/llm-providers/bedrock), [Google Vertex (deprecated)](https://ona.com/docs/ona/google-vertex).** Model provider options, deprecated Anthropic and Vertex paths. Primary. Accessed 2026-09-28.
- **[Ona Organizations docs](https://ona.com/docs/ona/organizations/overview).** Supported editors, SSO providers. Primary. Accessed 2026-09-28.
- **[Ona changelog](https://ona.com/docs/llms-full.txt).** Slack and Linear agents, model gateway headers, providers for new direct LLM integrations. Primary. Accessed 2026-09-28.
- **[Ona Cloud is shutting down on October 31, 2026](https://ona.com/stories/ona-core-shutdown).** Ona Cloud shutdown date, closed signups, no automatic migration, Codex Cloud as the suggested path, refunds. Primary. Accessed 2026-10-29.
- **[Ona pricing](https://ona.com/pricing).** Claude Code billing. Primary. Accessed 2026-09-28. Redirects to Ona's sales contact page as of 2026-10-29.
- **[Ona Cost & Budgets](https://ona.com/docs/ona/billing/usage).** OCU billing for Core and credit billing for Enterprise. Primary. Accessed 2026-10-29.
- **[Ona homepage](https://ona.com/).** Current positioning. Primary. Accessed 2026-09-28.
- **[Self-hosted, not self-managed](https://www.gitpod.io/blog/self-hosted-not-self-managed).** Discontinuation of self-managed Gitpod in 2022. Primary. Accessed 2026-09-28.
- **[AWS runner costs](https://ona.com/docs/ona/runners/aws/aws-runner-costs) and [GCP runner costs](https://ona.com/docs/ona/runners/gcp/gcp-runner-costs).** Runner resources billed to the customer's cloud account. Primary. Accessed 2026-10-29.
- **[G2 Coder reviews](https://www.g2.com/products/coder/pricing).** Reviewer feedback on operational overhead. Secondary. Accessed 2026-09-28.
- **[Coder Agents docs](https://coder.com/docs/ai-coder/agents), [Architecture](https://coder.com/docs/ai-coder/agents/architecture), [Platform Controls](https://coder.com/docs/ai-coder/agents/platform-controls), [AI Coder overview](https://coder.com/docs/ai-coder).** Coder Agents architecture, providers, governance. Primary. Accessed 2026-09-28.
- **[Coder air-gapped deployments](https://coder.com/docs/install/airgap).** Air-gap support. Primary. Accessed 2026-09-28.
- **[Coder Dev Containers](https://coder.com/docs/@main/admin/integrations/devcontainers).** Dev Container specification support. Primary. Accessed 2026-10-29.
- **[Coder pricing](https://coder.com/pricing) and [Coder Community blog](https://coder.com/blog/coder-community-open-source).** Tiers and agent limits. Primary. Accessed 2026-09-28.
- **[coder/coder on GitHub](https://github.com/coder/coder).** Third-party agent support. Primary. Accessed 2026-09-28.
- **[Coder Workspaces message house](../products/coder-workspaces/message-house.md), [Coder Agents message house](../products/coder-agents/message-house.md), [Why Coder](../company/why-coder.md).** Coder positioning. Primary (this repository). Accessed 2026-09-28.
