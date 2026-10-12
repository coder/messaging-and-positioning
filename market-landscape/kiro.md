# Coder and Kiro

| Field | Value |
|---|---|
| Date generated | 2026-10-12 |
| Last reviewed | 2026-10-12 |
| Category | Complementary |

*Kiro CLI is the successor to the Amazon Q Developer CLI ([Kiro docs](https://kiro.dev/docs/upgrade-guides/migrating-from-q/)), and AWS points Amazon Q Developer customers to Kiro ahead of Q Developer end of support on April 30, 2027 ([AWS](https://aws.amazon.com/blogs/devops/amazon-q-developer-end-of-support-announcement/)).*

## One-Line Positioning

Kiro is the AWS agentic development tool developers use to plan and write code, and Coder is the self-hosted platform on AWS where Kiro connects to governed development environments that reach internal systems, alongside Coder Agents and Amazon Bedrock.

## Strategic Themes and Patterns

- **Relationship.** Complementary. Kiro ships as an IDE, a CLI, a web app, and other surfaces built on one agent harness ([Kiro docs](https://kiro.dev/docs/how-kiro-works/)). Coder publishes a verified [Kiro module](https://registry.coder.com/modules/coder/kiro) that opens the Kiro IDE against a Coder workspace, and the Kiro CLI installs into workspaces through a community [Kiro CLI module](https://registry.coder.com/modules/harleylrn/kiro-cli).
- **AWS partnership.** Coder holds AWS Software Competencies in AI, DevOps, Government, and Migration and Modernization ([Coder AWS partner page](https://coder.com/partners/aws), [Coder announcement](https://coder.com/blog/coder-achieves-aws-generative-ai-and-devops-competencies)) and is sold through [AWS Marketplace](https://aws.amazon.com/marketplace/pp/prodview-laypqph2nuvaq). Coder runs on Amazon EKS and EC2 ([Coder docs](https://coder.com/docs/install/server/cloud/aws-marketplace)), and Kiro runs its inference on Amazon Bedrock ([Kiro docs](https://kiro.dev/docs/privacy-and-security/data-protection/)).
- **Where the products overlap.** Kiro Web and its autonomous mode run agent tasks in Kiro-managed cloud sandboxes and open pull requests ([Kiro docs](https://kiro.dev/docs/web/sandbox/), [Kiro docs](https://kiro.dev/docs/web/autonomous-mode/)). Coder Agents also runs background agent tasks, with the agent loop in the customer's own Coder control plane ([Coder docs](https://coder.com/docs/ai-coder)). Customers can run both.
- **Choice, Control, Consistency.** Not a substitution decision. Kiro's IDE and CLI use Kiro's managed model catalog ([Kiro docs](https://kiro.dev/docs/models/)). Coder adds Choice by running Kiro next to other agents and Coder Agents, which supports Bedrock and other providers ([Coder docs](https://coder.com/docs/ai-coder/agents/models)).
- **How they work together.** Platform teams define Kiro-ready workspaces as Terraform templates on AWS. Developers open them from the Kiro IDE or run the Kiro CLI inside them. Kiro's admin console governs models and MCP servers, and Coder governs the environment and network around the agent.

## Coder's Strengths Here

- **Kiro-ready environments on AWS.** Coder workspaces run in the customer's AWS account on EKS or EC2, so Kiro works against repositories, build tools, and internal services inside the VPC instead of on a laptop ([Coder docs](https://coder.com/docs/install/server/cloud/aws-marketplace), [Why Coder](../company/why-coder.md)).
- **One-click Kiro IDE access.** The Kiro module adds a button that opens the Kiro IDE connected to a workspace and can write MCP server configuration to `~/.kiro/settings/mcp.json` at startup ([Coder Registry](https://registry.coder.com/modules/coder/kiro)).
- **Network policy for the Kiro CLI.** Agent Firewall restricts and audits the domains and HTTP methods that terminal-based agents can reach ([Agent Firewall docs](https://coder.com/docs/ai-coder/agent-firewall)), which covers the Kiro CLI running in a workspace.
- **Private connectivity to Kiro.** Kiro supports AWS PrivateLink endpoints in us-east-1, eu-central-1, and AWS GovCloud (US) ([Kiro docs](https://kiro.dev/docs/privacy-and-security/vpc-endpoints/)), so workspaces in a private VPC can reach Kiro without public internet egress.
- **Public sector on both sides.** Kiro is authorized at FedRAMP High and DoD IL-4/5 in AWS GovCloud (US) ([AWS](https://aws.amazon.com/about-aws/whats-new/2026/06/kiro-fedramp-high-dod-il-4-5-govcloud-us/)), and Coder supports GovCloud and air-gapped deployments ([AWS Marketplace listing](https://aws.amazon.com/marketplace/pp/prodview-laypqph2nuvaq), [Coder docs](https://coder.com/docs/install/prepare/airgap)).
- **Bedrock-backed agents on the same platform.** Coder Agents and Coder AI Gateway both support Amazon Bedrock with IAM-based authentication ([Coder docs](https://coder.com/docs/ai-coder/agents/models), [AI Gateway provider docs](https://coder.com/docs/ai-coder/ai-gateway/providers)), so teams can run Kiro and self-hosted background agents on one AWS footprint.

## Kiro Overview

- **What it is.** An agentic development tool from AWS with spec-driven development, steering files, hooks, custom agents, sub-agents, and MCP support ([Kiro docs](https://kiro.dev/docs/steering/), [Kiro docs](https://kiro.dev/docs/custom-agents/subagents/), [Kiro docs](https://kiro.dev/docs/mcp/)).
- **Surfaces.** The IDE and CLI are generally available ([Kiro](https://kiro.dev/blog/general-availability/)). Kiro Web and cloud sessions reached general availability in September 2026 ([Kiro](https://kiro.dev/blog/agentic-engineering-in-the-cloud/)), and Kiro Crew is an open-source agent that runs on the user's own hardware ([Kiro](https://kiro.dev/blog/introducing-kiro-crew/)).
- **Architecture.** The IDE and CLI run the agent harness locally, and Kiro Web runs it in a managed cloud sandbox in us-east-1 ([Kiro docs](https://kiro.dev/docs/how-kiro-works/), [Kiro docs](https://kiro.dev/docs/web/)). Inference runs on Amazon Bedrock with cross-region inference in US, EU, and GovCloud regions ([Kiro docs](https://kiro.dev/docs/privacy-and-security/data-protection/)).
- **Headless use.** The CLI runs non-interactively with a `KIRO_API_KEY` for pipelines and automation ([Kiro docs](https://kiro.dev/docs/cli/headless/)).
- **Enterprise controls.** SSO through IAM Identity Center, Okta, or Microsoft Entra ID, admin controls for models, MCP servers, web tools, and API keys, and prompt logging to a customer S3 bucket ([Kiro docs](https://kiro.dev/docs/enterprise/identity-provider/), [Kiro docs](https://kiro.dev/docs/enterprise/governance/), [Kiro docs](https://kiro.dev/docs/enterprise/monitor-and-track/prompt-logging/)).
- **Target customer.** Individual developers through enterprises, including AWS GovCloud customers ([Kiro pricing](https://kiro.dev/pricing/), [Kiro docs](https://kiro.dev/docs/models/govcloud/)).
- **Deployment model.** SaaS on AWS, with local execution for the IDE and CLI and Kiro-managed sandboxes for Kiro Web.

## Coder Overview for This Comparison

- **Coder Workspaces.** Self-hosted development environments defined with Terraform templates, running on infrastructure the customer controls, including EKS and EC2 ([Coder docs](https://coder.com/docs/install/server/cloud/aws-marketplace), [Why Coder](../company/why-coder.md)).
- **Agents in workspace templates.** Admins install terminal agents such as the Kiro CLI into templates through registry modules ([Coder docs](https://coder.com/docs/ai-coder)).
- **AI Governance.** AI Gateway for model-level audit and policy and Agent Firewall for process-level network policy, included with Coder Premium ([Coder docs](https://coder.com/docs/ai-coder/ai-governance)).
- **Coder Agents.** Coder's native agent, whose agent loop runs in the self-hosted Coder control plane and supports Amazon Bedrock among other providers ([Coder docs](https://coder.com/docs/ai-coder/agents/models), [Coder Agents message house](../products/coder-agents/message-house.md)).

## Known Limitations in Kiro's Approach

- **No custom inference endpoint (as of 2026-10-12).** Kiro's IDE and CLI use Kiro's managed model catalog, and Coder's AI Gateway documentation lists Kiro as unsupported because it has no option to override the base URL ([Kiro docs](https://kiro.dev/docs/models/), [AI Gateway client docs](https://coder.com/docs/ai-coder/ai-gateway/clients)). Kiro's admin console and prompt logging cover the model layer instead.
- **Remote IDE connection uses a community extension (as of 2026-10-12).** Kiro supports Open VSX extensions and treats community remote SSH extensions as third-party ([Kiro docs](https://kiro.dev/docs/upgrade-guides/migrating-from-vscode/)). The Coder Kiro module connects through the Coder Remote extension and the Open VSX `open-remote-ssh` extension ([Coder Registry](https://registry.coder.com/modules/coder/kiro)).
- **Kiro Web runs in Kiro's cloud (as of 2026-10-12).** Kiro Web sandboxes run in us-east-1, and self-managed GitLab must be reachable from the internet ([Kiro docs](https://kiro.dev/docs/web/), [Kiro docs](https://kiro.dev/docs/web/gitlab/)).

## Common Questions

- **Does Coder replace Kiro?** No. Kiro is the tool developers use to plan and write code, and Coder provides the environments it connects to ([Coder Registry](https://registry.coder.com/modules/coder/kiro)).
- **How does the Kiro IDE connect to a Coder workspace?** Through the Coder Kiro module, which adds a one-click button that opens Kiro connected to the workspace ([Coder Registry](https://registry.coder.com/modules/coder/kiro), [Coder AWS partner page](https://coder.com/partners/aws)).
- **How does the Kiro CLI sign in inside a workspace?** Interactively through Kiro's device flow, which works on remote machines without port forwarding but not with Okta or Entra sign-in. For automation, it signs in headlessly with a `KIRO_API_KEY` on paid plans once an admin enables keys ([Kiro docs](https://kiro.dev/docs/getting-started/authentication/), [Kiro docs](https://kiro.dev/docs/cli/headless/)).
- **Can Kiro's model traffic go through Coder AI Gateway?** Not today. Kiro does not expose a base URL override ([AI Gateway client docs](https://coder.com/docs/ai-coder/ai-gateway/clients)). Teams govern models and MCP servers in Kiro's admin console and use Coder workspace network controls and Agent Firewall around the agent ([Kiro docs](https://kiro.dev/docs/enterprise/governance/), [Agent Firewall docs](https://coder.com/docs/ai-coder/agent-firewall)).
- **Can Kiro traffic stay private on AWS?** Yes. Kiro supports AWS PrivateLink endpoints, and on-premises access can route through a VPN ([Kiro docs](https://kiro.dev/docs/privacy-and-security/vpc-endpoints/)).
- **What about environments with no path to AWS?** Kiro's inference runs on Amazon Bedrock ([Kiro docs](https://kiro.dev/docs/privacy-and-security/data-protection/)). Coder supports fully air-gapped deployments, where Coder Agents can use self-hosted models ([Coder docs](https://coder.com/docs/install/prepare/airgap), [Coder Agents message house](../products/coder-agents/message-house.md)).
- **What should Amazon Q Developer customers know?** New Q Developer signups ended May 15, 2026, and Q Developer IDE plugins and paid subscriptions reach end of support on April 30, 2027 ([AWS](https://aws.amazon.com/blogs/devops/amazon-q-developer-end-of-support-announcement/)). Kiro CLI is the next version of the Q CLI ([Kiro docs](https://kiro.dev/docs/upgrade-guides/migrating-from-q/)).

## Pricing and Packaging

- **Kiro.** Public per-user tiers from Free to Power, priced in monthly credits, with Kiro Web sessions drawing from the same credits ([Kiro pricing](https://kiro.dev/pricing/)).
- **Coder.** See [coder.com/pricing](https://coder.com/pricing) for current tiers and prices, and [Packaging](../company/packaging.md) for the reasoning behind them. Coder is also available through [AWS Marketplace](https://aws.amazon.com/marketplace/pp/prodview-laypqph2nuvaq).

## Sources

- **[Kiro docs: How Kiro works](https://kiro.dev/docs/how-kiro-works/).** Primary. Surfaces and where the agent harness runs. Accessed 2026-10-12.
- **[Kiro: General availability](https://kiro.dev/blog/general-availability/), [Agentic engineering in the cloud](https://kiro.dev/blog/agentic-engineering-in-the-cloud/), [Introducing Kiro Crew](https://kiro.dev/blog/introducing-kiro-crew/).** Primary. Availability of the IDE, CLI, Kiro Web, cloud sessions, and Crew. Accessed 2026-10-12.
- **[Kiro docs: Web](https://kiro.dev/docs/web/), [Sandbox](https://kiro.dev/docs/web/sandbox/), [Autonomous mode](https://kiro.dev/docs/web/autonomous-mode/), [GitLab](https://kiro.dev/docs/web/gitlab/).** Primary. Kiro Web region, sandboxes, autonomous mode, GitLab reachability. Accessed 2026-10-12.
- **[Kiro docs: Data protection](https://kiro.dev/docs/privacy-and-security/data-protection/), [Models](https://kiro.dev/docs/models/), [GovCloud models](https://kiro.dev/docs/models/govcloud/).** Primary. Bedrock inference regions and managed model catalog. Accessed 2026-10-12.
- **[Kiro docs: VPC endpoints](https://kiro.dev/docs/privacy-and-security/vpc-endpoints/).** Primary. PrivateLink endpoints and on-premises access. Accessed 2026-10-12.
- **[Kiro docs: Headless mode](https://kiro.dev/docs/cli/headless/), [Authentication](https://kiro.dev/docs/getting-started/authentication/).** Primary. `KIRO_API_KEY`, device flow, admin enablement. Accessed 2026-10-12.
- **[Kiro docs: Steering](https://kiro.dev/docs/steering/), [Subagents](https://kiro.dev/docs/custom-agents/subagents/), [MCP](https://kiro.dev/docs/mcp/).** Primary. Agent capabilities. Accessed 2026-10-12.
- **[Kiro docs: Governance](https://kiro.dev/docs/enterprise/governance/), [Identity provider](https://kiro.dev/docs/enterprise/identity-provider/), [Prompt logging](https://kiro.dev/docs/enterprise/monitor-and-track/prompt-logging/).** Primary. Enterprise controls. Accessed 2026-10-12.
- **[Kiro docs: Migrating from Q](https://kiro.dev/docs/upgrade-guides/migrating-from-q/), [Migrating from VS Code](https://kiro.dev/docs/upgrade-guides/migrating-from-vscode/).** Primary. Q CLI succession and Open VSX extension support. Accessed 2026-10-12.
- **[Kiro pricing](https://kiro.dev/pricing/).** Primary. Tiers and credits. Accessed 2026-10-12.
- **[AWS: Amazon Q Developer end of support](https://aws.amazon.com/blogs/devops/amazon-q-developer-end-of-support-announcement/).** Primary. Signup cutoff, end of support date, Kiro as successor. Accessed 2026-10-12.
- **[AWS What's New: Kiro FedRAMP High and DoD IL-4/5 in GovCloud](https://aws.amazon.com/about-aws/whats-new/2026/06/kiro-fedramp-high-dod-il-4-5-govcloud-us/).** Primary. GovCloud authorization. Accessed 2026-10-12.
- **[Coder Registry: Kiro module](https://registry.coder.com/modules/coder/kiro), [Kiro CLI module](https://registry.coder.com/modules/harleylrn/kiro-cli).** Primary. Kiro IDE connection, MCP configuration, CLI install. Accessed 2026-10-12.
- **[Coder AWS partner page](https://coder.com/partners/aws), [Coder AWS competencies announcement](https://coder.com/blog/coder-achieves-aws-generative-ai-and-devops-competencies), [AWS Marketplace listing](https://aws.amazon.com/marketplace/pp/prodview-laypqph2nuvaq).** Primary. AWS competencies, Marketplace availability, GovCloud support. Accessed 2026-10-12.
- **[Coder docs: AWS install](https://coder.com/docs/install/server/cloud/aws-marketplace), [Air-gapped deployments](https://coder.com/docs/install/prepare/airgap).** Primary. EKS and EC2 deployment and air-gapped support. Accessed 2026-10-12.
- **[Coder docs: AI coding agents](https://coder.com/docs/ai-coder), [Coder Agents models](https://coder.com/docs/ai-coder/agents/models), [AI Governance](https://coder.com/docs/ai-coder/ai-governance), [AI Gateway providers](https://coder.com/docs/ai-coder/ai-gateway/providers), [AI Gateway clients](https://coder.com/docs/ai-coder/ai-gateway/clients), [Agent Firewall](https://coder.com/docs/ai-coder/agent-firewall).** Primary. Coder Agents, Bedrock support, AI Gateway client compatibility, Agent Firewall. Accessed 2026-10-12.
- **[Why Coder](../company/why-coder.md), [Coder Agents message house](../products/coder-agents/message-house.md), [Packaging](../company/packaging.md).** Primary (Coder's vetted positioning). Accessed 2026-10-12.
