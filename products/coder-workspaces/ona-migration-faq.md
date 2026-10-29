# Moving from Ona to Coder FAQ

This FAQ helps Coder teams support organizations moving off Ona, formerly Gitpod. It covers who is affected, how to talk about the change, and how a move to Coder works. For the full product comparison, see [Coder and Ona](../../market-landscape/ona.md).

Facts about Ona here are current as of 2026-10-29 and link to Ona's own announcements and docs. Recheck them before reusing this content.

## What Changed

**What did Ona announce?**
On October 13, 2026, Ona announced that [Ona Cloud shuts down on October 31, 2026](https://ona.com/stories/ona-core-shutdown). New signups are closed, existing users can keep using Ona Cloud until that date, and Ona refunds October payments and unused purchased credits. The announcement follows Ona [becoming part of OpenAI on August 10, 2026](https://ona.com/stories/ona-joins-openai), where the team works with Codex.

**Do Ona environments move anywhere automatically?**
No. Ona says environments [do not move to Codex automatically](https://ona.com/stories/ona-core-shutdown). Users need to push their code and back up any other files before October 31. Ona points users to Codex Cloud as its suggested path.

**Who is affected?**
- **Ona Cloud users.** Ona Cloud is the managed infrastructure for [Ona's Core plans](https://ona.com/docs/ona/runners/ona-cloud). These users have a hard deadline of October 31, 2026.
- **Ona Enterprise customers.** Enterprise runners deploy in [the customer's AWS or GCP account](https://ona.com/docs/ona/runners/overview). The shutdown notice covers Ona Cloud, and as of 2026-10-29 we found no published end date for Enterprise runners. Ona's docs now [recommend Codex Agent for new sessions and automations](https://ona.com/docs/ona/agents).
- **Former Gitpod customers.** Gitpod [rebranded as Ona in September 2025](https://ona.com/stories/gitpod-is-now-ona), so most former Gitpod customers fall into one of the two groups above.

## Talking About the Change

**How should we bring up the shutdown?**
State the dated facts and link to Ona's own notice. Lead with the customer's deadline and requirements, not with Ona. For Ona Cloud users, the conversation is about where to go before October 31. For Enterprise customers, it's about planning a move on their own timeline, not urgency.

**What should we avoid saying?**
- Don't say or imply that Ona Enterprise is shutting down. Ona hasn't announced that.
- Don't speculate about OpenAI's plans for Ona, Codex, or existing contracts.
- Don't comment on Ona's motives or quality. Describe what changed and what Coder does.
- Don't promise a migration timeline or an automatic import. Coder doesn't import Ona environments directly.

**What's the short version for a customer?**
Ona Cloud closes on October 31, 2026, and environments don't move automatically. Coder is an open-source, self-hosted platform for development environments where developers work and AI agents run, on the customer's own cloud or data center, with the IDEs, agents, and models the team chooses. Teams can reuse their existing Dev Container configurations.

## Fit

**Which Ona customers are a good fit for Coder?**
Teams that need to run development environments and agents on infrastructure they control, including Azure, on-premises, or air-gapped environments, which Ona's runners [don't document](https://ona.com/docs/ona/runners/overview). Teams that need more than one model provider, or a control plane they operate themselves, are also a good fit. Coder works best with a platform team that can operate infrastructure. See the [Coder Workspaces playbook](./playbook.md#good-fit-signals), which lists a discontinued hosted cloud development environment as a good-fit signal.

**Which Ona customers may be better served elsewhere?**
Ona Cloud was built for [individuals, small teams, and organizations that want to start immediately](https://ona.com/docs/ona/runners/overview). Coder is always self-hosted, so the customer runs the control plane and the compute. Organizations with fewer than about 50 developers, or no one to operate infrastructure, may be better served by a hosted option, as the [playbook](./playbook.md#poor-fit-or-another-approach) notes. Small teams that still want to self-host can start with Coder Community, which is free and open source.

**What should we ask an Ona customer?**
- Are you on Ona Cloud or Enterprise runners, and when do you need to move?
- Which cloud do you run on today, and do you need Azure, on-premises, or air-gapped environments?
- How many developers and agents use Ona, and who would operate a self-hosted platform?
- Do your repositories have `devcontainer.json` files, and do you rely on Ona tasks, services, prebuilds, or automations?
- Which models and agents do you need, such as Codex, Claude Code, Gemini, or self-hosted models?
- Which IDEs, Git providers, and identity provider do you use?
- What security, audit, or data residency requirements apply?

## Moving to Coder

**How does a move from Ona to Coder work?**
1. Install Coder in the customer's cloud or data center. Community installs with the [quickstart](https://coder.com/docs/@main/get-started), and a free 30-day trial is available at [coder.com/trial](https://coder.com/trial).
2. Create a template for the target infrastructure, such as Kubernetes, VMs, or Docker. The [Coder Registry](https://registry.coder.com) has starting templates and modules.
3. Enable the [Dev Containers integration](https://coder.com/docs/@main/admin/integrations/devcontainers) so workspaces build from existing `devcontainer.json` files.
4. Connect the Git provider and identity provider, then invite developers.
5. Add the agents and models the team has approved. Premium includes AI Governance for auditing and controlling AI tool usage.

**Do Dev Container configurations carry over?**
Mostly. Ona environments are [provisioned from a Dev Container configuration](https://ona.com/docs/ona/runners/overview), and Coder [supports the Dev Container specification](https://coder.com/docs/@main/admin/integrations/devcontainers), so existing `devcontainer.json` files can be reused on Linux workspaces. The Dev Containers integration isn't supported in Windows or macOS workspaces. Test each repository's configuration during the evaluation.

**What doesn't carry over?**
Ona-specific configuration has no automatic equivalent in Coder. That includes [tasks and services](https://ona.com/docs/ona/configuration/tasks-and-services/overview), [prebuilds](https://ona.com/docs/ona/projects/prebuilds), automations, and Ona's [Slack](https://ona.com/docs/ona/integrations/configure-slack) and [Linear](https://ona.com/docs/ona/integrations/configure-linear) integrations. Teams rebuild what they need as part of the move, for example in Coder templates, with [prebuilt workspaces](https://coder.com/docs/@main/admin/templates/extending-templates/prebuilt-workspaces) (Premium), or by triggering Coder Agents through its API from CI, as described in the [Coder Agents message house](../coder-agents/message-house.md).

**Can teams keep using Codex?**
Yes. Codex runs inside Coder workspaces using the [Coder Registry Codex module](https://registry.coder.com/modules/coder-labs/codex), alongside Claude Code and other agents. Coder Agents can also use OpenAI models.

**Can teams use Claude or other models?**
Yes. Claude Code runs inside Coder workspaces, and Coder Agents connects to [Anthropic, OpenAI, Google, Azure, AWS Bedrock, or any OpenAI-compatible endpoint](https://coder.com/docs/@main/ai-coder/agents/architecture), including self-hosted models. Admins choose which providers and models are available.

**Why not move to Codex Cloud?**
Codex Cloud is Ona's suggested path, and it suits teams that accept OpenAI-hosted execution and standardize on OpenAI models. Codex Cloud runs in OpenAI-hosted environments and documents no option for non-OpenAI models. Coder fits teams that need execution on their own infrastructure, a choice of models, or development environments for developers as well as agents. See [Coder and Codex](../../market-landscape/codex.md).

**What if the team doesn't want to run infrastructure?**
That's a real tradeoff. Coder is self-hosted, so the customer runs the control plane, a PostgreSQL database for production, and the compute, as listed in the [playbook](./playbook.md#packaging-and-prerequisites). In return, environments, source code, and agent execution stay on infrastructure the customer controls. If running infrastructure isn't feasible, a hosted option may be the better fit.

**How can a team evaluate Coder?**
The free Community edition installs with the [quickstart](https://coder.com/docs/@main/get-started). A free, unlimited 30-day trial is available at [coder.com/trial](https://coder.com/trial), and teams can [contact sales](https://coder.com/contact/sales) to plan a larger move.

## Related

- [Coder and Ona](../../market-landscape/ona.md) for the full comparison
- [Coder and Codex](../../market-landscape/codex.md) for Codex Cloud
- [Coder Workspaces playbook](./playbook.md) and [FAQ](./faq.md)
- [Coder Agents message house](../coder-agents/message-house.md)
