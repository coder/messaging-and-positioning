# Coder and OpenAI Codex

| Field | Value |
|---|---|
| Date generated | 2026-09-28 |
| Category | Competitive (Codex cloud) and Complementary (Codex CLI, IDE extension, Remote SSH) |

*(On July 9, 2026, OpenAI merged the standalone Codex desktop app into the new ChatGPT desktop app, where Codex remains a dedicated coding mode. The Codex CLI, IDE extension, and Codex cloud keep the Codex name. See [Wikipedia](https://en.wikipedia.org/wiki/OpenAI_Codex_(AI_agent)) and [Developers Digest](https://www.developersdigest.tech/blog/chatgpt-work-codex-desktop-app).)*

## One-Line Positioning

Codex is OpenAI's coding agent, and it runs well inside a Coder workspace, but Codex cloud is an OpenAI-managed execution environment, so organizations that need agent orchestration, execution, and model choice on their own infrastructure use Coder instead.

## Strategic Themes and Patterns

- **Relationship.** Codex has two parts that relate to Coder differently. Codex cloud is an "OpenAI-managed execution environment" where tasks run in OpenAI-hosted containers ([Agent37 quoting OpenAI's glossary](https://www.agent37.com/blog/codex-cloud), [OpenAI cloud environments docs](https://developers.openai.com/codex/cloud/environments)), which competes with Coder Workspaces and Coder Agents for the background-agent buying decision. The Codex CLI and IDE extension are clients that run wherever they are installed, including inside a Coder workspace, which is complementary ([Coder AI docs](https://coder.com/docs/ai-coder), [Coder Registry Codex module](https://registry.coder.com/modules/coder-labs/codex)).
- **Choice, Control, Consistency.** Choosing Codex cloud instead of Coder trades off Control, because code and execution run on OpenAI's infrastructure with no documented self-hosted option for Codex cloud. It also trades off Choice, because Codex cloud is part of ChatGPT plans and documents no option for non-OpenAI models, while Coder Agents connects to Anthropic, OpenAI, Google, AWS Bedrock, or any OpenAI-compatible endpoint ([Coder Agents docs](https://coder.com/docs/ai-coder/agents)). Consistency is partly covered. Codex cloud environments are configured with setup scripts on a universal base image, one container per task ([OpenAI cloud environments docs](https://developers.openai.com/codex/cloud/environments)), not Terraform-defined templates.
- **Lock-in risk.** Standardizing background agents on Codex cloud ties environment definitions, agent history, usage data, and spend to one model vendor's platform and to ChatGPT workspace administration ([OpenAI admin rollout guide](https://developers.openai.com/codex/enterprise/admin-setup)). Moving to a different model provider later means moving to a different agent platform. With Coder, switching models is a configuration change ([Coder Agents solution page](https://coder.com/solutions/agents)).
- **Build versus buy.** Teams that want Codex's local tools with governed, self-hosted execution often try to build it themselves, running the Codex CLI on self-managed VMs or devboxes and wiring up identity, network policy, and audit. This mirrors the build-versus-buy framing in [Why Coder](../company/why-coder.md). Coder provides this layer through Terraform-provisioned workspaces, AI Gateway, and Agent Firewall.
- **Where Codex is sufficient on its own.** Teams that accept OpenAI-hosted execution and standardize on OpenAI models get a complete agent experience without running infrastructure. See "When Codex Alone Is Enough" below.
- **How they work together.** Coder publishes a Codex CLI module that installs and configures Codex in a workspace ([Coder Registry](https://registry.coder.com/modules/coder-labs/codex)). AI Gateway can route Codex CLI model traffic through Coder for centralized authentication and auditing, using either centrally managed API keys or each user's ChatGPT subscription ([Coder AI Gateway Codex docs](https://coder.com/docs/ai-coder/ai-gateway/clients/codex)). Codex also connects to SSH-accessible remote hosts from the ChatGPT desktop app ([OpenAI Remote connections docs](https://developers.openai.com/codex/remote-connections)). Using this with Coder workspaces over SSH is inferred and not yet verified.

## Coder's Strengths Here

- **Fully self-hosted agent loop.** Coder Agents has no SaaS or managed component. The agent loop, chat history, and tool execution all run in the customer's Coder deployment ([Coder Agents docs](https://coder.com/docs/ai-coder/agents)).
- **Air-gapped operation.** All Coder features are supported in air-gapped and offline deployments ([Coder air-gap docs](https://coder.com/docs/install/airgap)). With self-hosted models, inference can stay inside the perimeter too ([Coder Agents message house](../products/coder-agents/message-house.md)).
- **Model neutrality.** Coder Agents works with Anthropic, OpenAI, Google, Azure, AWS Bedrock, or any OpenAI-compatible endpoint, and admins can configure several providers at once ([Coder Agents docs](https://coder.com/docs/ai-coder/agents), [Coder 2.33 changelog](https://coder.com/changelog/coder-2-33)).
- **Governance for Codex itself.** When Codex runs in a Coder workspace, AI Gateway gives Codex CLI centralized authentication, and the registry module keeps OpenAI API keys out of the workspace when AI Gateway is enabled ([Coder Registry Codex module](https://registry.coder.com/modules/coder-labs/codex), [Coder AI Gateway Codex docs](https://coder.com/docs/ai-coder/ai-gateway/clients/codex)).
- **Environments defined as code.** Workspaces are provisioned from Terraform templates onto any infrastructure the customer chooses, from VMs to Kubernetes pods ([Coder Registry announcement](https://coder.com/blog/introducing-the-coder-registry)).
- **Network isolation.** Because the Coder Agents loop runs in the control plane, workspaces can be completely network isolated ([Coder AI docs](https://coder.com/docs/ai-coder)).

## Codex Overview

- **What it is.** OpenAI describes Codex as its coding agent for writing, reviewing, and debugging code, used from the IDE, the CLI, web and mobile, or CI/CD pipelines through the SDK ([OpenAI code generation guide](https://developers.openai.com/api/docs/guides/code-generation)).
- **Architecture.** Local surfaces (ChatGPT desktop app, Codex CLI, IDE extension) run on the user's machine or on a connected SSH host ([OpenAI Remote connections docs](https://developers.openai.com/codex/remote-connections)). Codex cloud creates a container, checks out the repository, runs a setup script, and then runs the agent loop ([OpenAI cloud environments docs](https://developers.openai.com/codex/cloud/environments)). Cloud tasks can start from the web, GitHub, GitLab, Linear, or Slack ([OpenAI Codex cloud docs](https://developers.openai.com/codex/cloud)).
- **Open source components.** The Codex CLI is open source under Apache 2.0, and the desktop app is proprietary ([Wikipedia](https://en.wikipedia.org/wiki/OpenAI_Codex_(AI_agent)), secondary). The app-server is open source in the openai/codex repository ([OpenAI App Server docs](https://developers.openai.com/codex/app-server)).
- **Model support.** Codex CLI can use local providers such as Ollama or LM Studio, plus custom model providers defined by base URL ([OpenAI advanced configuration docs](https://developers.openai.com/codex/config-advanced)). Since February 2026, custom providers must support the OpenAI Responses API ([Codex Knowledge Base](https://codex.danielvaughan.com/2026/04/23/codex-cli-custom-model-providers-configuration-guide/), secondary).
- **Enterprise controls.** Admins can set requirements that users cannot override, plus configuration defaults, for the ChatGPT desktop app, Codex CLI, and IDE extension ([OpenAI managed configuration docs](https://developers.openai.com/codex/enterprise/managed-configuration)). Cloud agents have internet access turned off by default, and admins can allow limited or unrestricted access per environment ([OpenAI internet access docs](https://developers.openai.com/codex/cloud/internet-access)).
- **Target customer.** Codex ships with every ChatGPT plan, from Free and Go up to Plus, Pro, Business, and Enterprise ([Codex pricing](https://chatgpt.com/codex/pricing/)). That covers individual developers through enterprises already on ChatGPT.
- **Deployment model.** SaaS for Codex cloud. Local clients install on developer machines or remote hosts, with sign-in through ChatGPT or an API key ([OpenAI admin rollout guide](https://developers.openai.com/codex/enterprise/admin-setup)).

## Coder Overview for This Comparison

- **Coder Workspaces.** Self-hosted development environments for developers and their agents, provisioned from Terraform templates on infrastructure the customer controls ([Coder AI docs](https://coder.com/docs/ai-coder), [Coder Workspaces message house](../products/coder-workspaces/message-house.md)).
- **Coder Agents.** A standalone agent written in Go that runs inside the Coder control plane. It is not a wrapper around Claude Code or Codex ([Coder Agents docs](https://coder.com/docs/ai-coder/agents)). Developers use it through the web UI or REST API ([Coder AI docs](https://coder.com/docs/ai-coder)).
- **AI Governance.** AI Gateway and Agent Firewall are part of AI Governance, which is included with a Premium license ([Coder AI Gateway Codex docs](https://coder.com/docs/ai-coder/ai-gateway/clients/codex)). AI Gateway supports Codex CLI as a client ([Coder AI Gateway clients](https://coder.com/docs/ai-coder/ai-gateway/clients)).
- **Agent Relay.** Connects cloud-hosted agent sessions to self-hosted Coder workspaces. Cursor Cloud Agents is the first supported provider, and Codex is not currently supported ([Coder AI docs](https://coder.com/docs/ai-coder)).

## Where Codex Is Strong or Coder Has a Gap

- **No infrastructure to run.** Codex cloud is hosted by OpenAI. Coder is self-hosted, so the customer runs both the control plane and the compute ([Coder install docs](https://coder.com/docs/install)). Some reviewers say this makes Coder a poor fit for small teams without dedicated DevOps ([G2 review](https://www.g2.com/products/coder/pricing), secondary).
- **Breadth of surfaces.** Codex spans the desktop app, CLI, IDE extension, web, mobile, and task triggers from GitHub, GitLab, Linear, and Slack ([OpenAI Codex cloud docs](https://developers.openai.com/codex/cloud), [OpenAI Remote connections](https://openai.com/index/work-with-codex-from-anywhere/)).
- **First-party access to OpenAI models.** Codex gets new OpenAI models as they launch, including Codex-tuned models ([freeCodeCamp Codex Handbook](https://www.freecodecamp.org/news/the-codex-handbook-a-practical-guide-to-openai-s-coding-platform/), secondary).
- **Bundled with ChatGPT.** Organizations already paying for ChatGPT Business or Enterprise get Codex in their existing plan ([Codex pricing](https://chatgpt.com/codex/pricing/)).
- **Hosted code review.** Codex offers optional hosted workflows such as code review ([OpenAI admin rollout guide](https://developers.openai.com/codex/enterprise/admin-setup)).
- **Coder gaps.** Agent Relay does not support Codex cloud today ([Coder AI docs](https://coder.com/docs/ai-coder)). Community and Premium cap Coder Agents at 5 concurrent agents, and AI Premium removes the cap ([Coder pricing](https://coder.com/pricing)).

## Known Limitations in Codex's Approach

- **No self-hosted Codex cloud (as of 2026-09-28).** Codex cloud runs on hosted environments ([OpenAI admin rollout guide](https://developers.openai.com/codex/enterprise/admin-setup)). The self-hosted options OpenAI documents are local clients and SSH-connected remote hosts ([OpenAI Remote connections docs](https://developers.openai.com/codex/remote-connections)).
- **Setup-phase network access (as of 2026-09-28).** Setup scripts in Codex cloud run with internet access ([OpenAI cloud environments docs](https://developers.openai.com/codex/cloud/environments)). One secondary source reports no documented way to restrict that access ([WorkOS](https://workos.com/blog/agent-sandbox-egress-defaults), secondary).
- **Shared caches (as of 2026-09-28).** For Business and Enterprise, cached environments are shared by everyone with access to the environment ([OpenAI cloud environments docs](https://developers.openai.com/codex/cloud/environments)).
- **Local usage and compliance export (as of 2026-09-28).** A secondary source reports that the Compliance API does not cover local Codex usage ([PromptArmor](https://www.promptarmor.com/resources/configuring-codex-securely-across-every-platform-and-use-case), secondary).
- **Managed configuration scope (as of 2026-09-28).** Managed configuration covers local runtime behavior. It doesn't grant workspace access or replace workspace RBAC ([OpenAI managed configuration docs](https://developers.openai.com/codex/enterprise/managed-configuration)).
- **Custom model protocol (as of 2026-09-28).** Custom providers must support the Responses API. Providers that only offer Chat Completions need a translation proxy ([Codex Knowledge Base](https://codex.danielvaughan.com/2026/04/23/codex-cli-custom-model-providers-configuration-guide/), secondary).

## Common Questions

- **Can we run Codex inside Coder?** Yes. The Codex CLI module installs and configures Codex in a workspace, and AI Gateway can route its model requests ([Coder Registry](https://registry.coder.com/modules/coder-labs/codex), [Coder AI Gateway Codex docs](https://coder.com/docs/ai-coder/ai-gateway/clients/codex)).
- **Can developers keep their ChatGPT subscription with Coder?** Yes. AI Gateway supports a ChatGPT subscription flow for Codex CLI that authenticates with each user's ChatGPT login ([Coder AI Gateway Codex docs](https://coder.com/docs/ai-coder/ai-gateway/clients/codex), [Coder AI Gateway providers](https://coder.com/docs/ai-coder/ai-gateway/providers)).
- **Is Codex locked to OpenAI models?** Codex cloud documents no option for non-OpenAI models. The Codex CLI can use local or custom providers ([OpenAI advanced configuration docs](https://developers.openai.com/codex/config-advanced)).
- **Can Codex cloud run on our infrastructure?** OpenAI does not document a self-hosted Codex cloud. Remote SSH lets the desktop app work on a remote host, and files, commands, credentials, network access, and compute stay on that machine ([OpenAI Developers on X](https://x.com/OpenAIDevs/status/2044828473060139208)). Model inference still goes through OpenAI unless a custom provider is configured.
- **How is Coder Agents different from Codex?** Coder Agents runs its agent loop, chat history, and tool execution entirely in the customer's Coder deployment and works with any configured LLM provider ([Coder Agents docs](https://coder.com/docs/ai-coder/agents)).
- **Does Coder Agent Relay work with Codex?** Not today. Cursor Cloud Agents is the first supported provider ([Coder AI docs](https://coder.com/docs/ai-coder)).

## When Codex Alone Is Enough

- **ChatGPT-standardized teams.** Organizations already on ChatGPT Business or Enterprise that are comfortable with OpenAI-hosted execution and OpenAI models.
- **Individuals and small teams.** Developers who want a capable agent without running infrastructure, using the local CLI sandbox or Codex cloud.
- **No self-hosting or air-gap requirement.** Teams without data residency, air-gap, or model-neutrality requirements that go beyond what OpenAI's hosted controls provide ([OpenAI managed configuration docs](https://developers.openai.com/codex/enterprise/managed-configuration)).

## Pricing and Packaging

- **Codex.** Included in ChatGPT Free, Go, Plus, Pro, Business, and Enterprise plans. Enterprise and Edu with flexible pricing have no fixed rate limits and usage draws on credits ([Codex pricing](https://chatgpt.com/codex/pricing/)). Enterprise pricing is not public. Secondary sources give different Business per-seat prices, so none is stated here.
- **Codex billing model.** Since April 2026, Codex usage is billed in credits tied to input, cached input, and output tokens ([Verdent](https://www.verdent.ai/guides/codex-pricing-2026), secondary). OpenAI stopped offering new pay-as-you-go Codex seats on Business plans on June 24, 2026 ([OpenAI](https://openai.com/index/codex-flexible-pricing-for-teams/)).
- **Coder.** Coder Community is free and open source. Premium includes AI Governance. AI Premium removes the concurrent Coder Agents cap ([Coder pricing](https://coder.com/pricing)). Coder does not publish a Premium price ([InfraGap](https://infragap.com/tools/coder/), secondary). See [Packaging](../company/packaging.md) for the narrative.
- **Combined cost.** Running Codex CLI in Coder means paying for Coder, the compute workspaces run on, and model usage, either through ChatGPT plans or API keys.

## Sources

All accessed 2026-09-28.

- **[OpenAI cloud environments docs](https://developers.openai.com/codex/cloud/environments).** Primary. Codex cloud container lifecycle, setup scripts, internet access defaults, shared caches.
- **[OpenAI agent internet access docs](https://developers.openai.com/codex/cloud/internet-access).** Primary. Agent-phase internet access defaults and per-environment configuration.
- **[OpenAI Codex cloud docs](https://developers.openai.com/codex/cloud).** Primary. Task triggers from web, GitHub, GitLab, Linear, Slack.
- **[OpenAI admin rollout guide](https://developers.openai.com/codex/enterprise/admin-setup).** Primary. Hosted environments, surfaces, hosted code review.
- **[OpenAI managed configuration docs](https://developers.openai.com/codex/enterprise/managed-configuration).** Primary. Admin requirements and defaults, scope.
- **[OpenAI advanced configuration docs](https://developers.openai.com/codex/config-advanced).** Primary. OSS mode and custom model providers.
- **[OpenAI Remote connections docs](https://developers.openai.com/codex/remote-connections).** Primary. SSH host connections.
- **[OpenAI App Server docs](https://developers.openai.com/codex/app-server).** Primary. Open source app-server.
- **[OpenAI code generation guide](https://developers.openai.com/api/docs/guides/code-generation).** Primary. Codex product definition and surfaces.
- **[Work with Codex from anywhere](https://openai.com/index/work-with-codex-from-anywhere/).** Primary. Remote SSH general availability.
- **[OpenAI Developers on X](https://x.com/OpenAIDevs/status/2044828473060139208).** Primary. What stays on the remote machine with Remote Connection.
- **[Codex pricing](https://chatgpt.com/codex/pricing/).** Primary. Plans that include Codex and Enterprise credit model.
- **[Codex flexible pricing for teams](https://openai.com/index/codex-flexible-pricing-for-teams/).** Primary. Pay-as-you-go seat change on June 24, 2026.
- **[Coder Agents docs](https://coder.com/docs/ai-coder/agents).** Primary. Self-hosted architecture and model support.
- **[Coder AI docs](https://coder.com/docs/ai-coder).** Primary. Network isolation, Agent Relay provider support.
- **[Coder AI Gateway Codex docs](https://coder.com/docs/ai-coder/ai-gateway/clients/codex).** Primary. Codex CLI routing and ChatGPT subscription flow.
- **[Coder AI Gateway clients](https://coder.com/docs/ai-coder/ai-gateway/clients).** Primary. Supported clients.
- **[Coder AI Gateway providers](https://coder.com/docs/ai-coder/ai-gateway/providers).** Primary. ChatGPT provider with per-user OAuth.
- **[Coder Registry Codex module](https://registry.coder.com/modules/coder-labs/codex).** Primary. Installing Codex in workspaces.
- **[Coder air-gap docs](https://coder.com/docs/install/airgap).** Primary. Air-gapped support.
- **[Coder install docs](https://coder.com/docs/install).** Primary. Self-hosted installation.
- **[Coder 2.33 changelog](https://coder.com/changelog/coder-2-33).** Primary. Multiple provider endpoints.
- **[Coder Agents solution page](https://coder.com/solutions/agents).** Primary. Model switching as configuration.
- **[Coder Registry announcement](https://coder.com/blog/introducing-the-coder-registry).** Primary. Terraform templates.
- **[Coder pricing](https://coder.com/pricing).** Primary. Editions and Coder Agents concurrency cap.
- **[Wikipedia, OpenAI Codex](https://en.wikipedia.org/wiki/OpenAI_Codex_(AI_agent)).** Secondary. App merger date, licenses.
- **[Developers Digest](https://www.developersdigest.tech/blog/chatgpt-work-codex-desktop-app).** Secondary. Desktop app merger details.
- **[Agent37](https://www.agent37.com/blog/codex-cloud).** Secondary. Quotes OpenAI's Codex cloud glossary definition.
- **[Codex Knowledge Base](https://codex.danielvaughan.com/2026/04/23/codex-cli-custom-model-providers-configuration-guide/).** Secondary. Responses API requirement for custom providers.
- **[freeCodeCamp Codex Handbook](https://www.freecodecamp.org/news/the-codex-handbook-a-practical-guide-to-openai-s-coding-platform/).** Secondary. Codex model lineup.
- **[WorkOS](https://workos.com/blog/agent-sandbox-egress-defaults).** Secondary. Setup-phase egress.
- **[PromptArmor](https://www.promptarmor.com/resources/configuring-codex-securely-across-every-platform-and-use-case).** Secondary. Compliance API coverage of local usage.
- **[Verdent](https://www.verdent.ai/guides/codex-pricing-2026).** Secondary. Token-based credit billing.
- **[G2](https://www.g2.com/products/coder/pricing).** Secondary. Reviewer view of Coder operational overhead.
- **[InfraGap](https://infragap.com/tools/coder/).** Secondary. Coder Premium price not published.
