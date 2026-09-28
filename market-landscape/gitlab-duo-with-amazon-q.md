# Coder and GitLab Duo with Amazon Q

| Field | Value |
|---|---|
| Date generated | 2026-09-28 |
| Category | Complementary |

*GitLab Duo with Amazon Q is a GitLab add-on built on Amazon Q Developer. AWS has announced end of support for Amazon Q Developer IDE plugins and paid subscriptions on April 30, 2027, with Kiro as the successor ([AWS](https://aws.amazon.com/blogs/devops/amazon-q-developer-end-of-support-announcement/)). As of 2026-09-28, no public statement from GitLab or AWS addresses how that change affects this add-on.*

## One-Line Positioning

GitLab is the source control and CI/CD platform that Coder workspaces and Coder Agents connect to, and GitLab Duo with Amazon Q adds AWS-hosted AI agents inside GitLab issues and merge requests, while Coder provides the self-hosted, model-agnostic environments where developers and agents actually write and run code.

## Strategic Themes and Patterns

- **Relationship.** Complementary at the platform level, with a partial overlap at the coding agent layer. GitLab Duo with Amazon Q embeds Amazon Q agents into GitLab's DevSecOps platform ([GitLab press release](https://about.gitlab.com/press/releases/2025-04-17-gitlab-announces-general-availability-of-gitlab-duo-with-amazon-q/)), and Coder integrates with GitLab as a Git provider for workspaces and for Coder Agents merge requests ([Coder docs](https://coder.com/docs/admin/external-auth), [Coder Agents git providers](https://coder.com/docs/ai-coder/agents/platform-controls/git-providers)). Coder does not provide source control, CI/CD, or issue tracking. The overlap is narrower. Both products offer an agent that turns an issue or task into a merge request ([AWS](https://aws.amazon.com/about-aws/whats-new/2025/04/gitlab-duo-amazon-q-generally-available)).
- **Choice, Control, Consistency.** Not a direct tradeoff, since a customer can run both. Where the agent layers overlap, the difference is Choice and Control. GitLab Duo with Amazon Q is powered by Amazon Q and cannot be combined with other GitLab Duo add-ons ([GitLab docs](https://docs.gitlab.com/user/duo_amazon_q/)), and Amazon Q services must reach the GitLab instance over the network ([GitLab docs](https://docs.gitlab.com/user/duo_amazon_q/setup/)). Coder Agents is LLM-agnostic and runs self-hosted ([Coder Agents message house](../products/coder-agents/message-house.md)).
- **How they work together.** Developers work in Coder workspaces that clone from and push to GitLab, authenticated through Coder external auth ([Coder docs](https://coder.com/docs/admin/external-auth)). GitLab Duo features that run in GitLab issues and merge requests continue to run there. Coder Agents can open GitLab merge requests and read their diffs and status checks when configured with the `write_repository` and `read_api` scopes ([Coder docs](https://coder.com/docs/ai-coder/agents/platform-controls/git-providers)), so GitLab stays the system of record for code review whichever agent produced the change.

## Coder's Strengths Here

- **Where code gets executed.** GitLab Duo with Amazon Q works through GitLab issues, merge requests, and chat ([AWS docs](https://docs.aws.amazon.com/amazonq/latest/qdeveloper-ug/gitlab-with-amazon-q.html)). Coder adds reproducible, Terraform-defined workspaces where developers and agents build, test, and run code on customer infrastructure ([Coder Agents message house](../products/coder-agents/message-house.md)).
- **Air-gapped operation.** Coder states that all its features are supported air-gapped or offline ([Coder docs](https://coder.com/docs/install/airgap)). GitLab Duo with Amazon Q requires inbound network access from Amazon Q services to the GitLab instance ([GitLab docs](https://docs.gitlab.com/user/duo_amazon_q/setup/)).
- **Model choice for agents.** Coder Agents supports Anthropic, OpenAI, Google, Azure OpenAI, AWS Bedrock, and any OpenAI-compatible endpoint, including self-hosted models ([Coder Agents message house](../products/coder-agents/message-house.md)). GitLab Duo with Amazon Q features are powered by Amazon Q ([GitLab blog](https://about.gitlab.com/blog/gitlab-duo-with-amazon-q-agentic-ai-optimized-for-aws/)).
- **Cloud neutrality.** Coder runs on the customer's choice of cloud or on-premises infrastructure ([Why Coder](../company/why-coder.md)). GitLab Duo with Amazon Q requires a GitLab Self-Managed instance running on AWS infrastructure ([GitLab product page](https://about.gitlab.com/gitlab-duo/duo-amazon-q/)).

## GitLab Duo with Amazon Q Overview

- **What it is.** An add-on that embeds Amazon Q Developer agents into GitLab for feature development, code review, test generation, pipeline troubleshooting, and Java upgrades ([AWS](https://aws.amazon.com/about-aws/whats-new/2025/04/gitlab-duo-amazon-q-generally-available)). It also includes GitLab Duo features such as code completion, chat, and vulnerability explanation, powered by Amazon Q ([GitLab blog](https://about.gitlab.com/blog/gitlab-duo-with-amazon-q-agentic-ai-optimized-for-aws/)).
- **Architecture.** Users invoke agents with quick actions such as `/q dev`, `/q review`, `/q fix`, and `/q transform` in issues and merge request comments ([AWS blog](https://aws.amazon.com/blogs/aws/introducing-gitlab-duo-with-amazon-q/)). Amazon Q reads and writes data through the GitLab instance's REST APIs. Setup requires an Amazon Q Developer profile, an OIDC identity provider, and an IAM role in the customer's AWS account ([GitLab docs](https://docs.gitlab.com/user/duo_amazon_q/setup/), [AWS docs](https://docs.aws.amazon.com/amazonq/latest/qdeveloper-ug/gitlab-concepts.html)).
- **Target customer.** GitLab Ultimate customers on GitLab Self-Managed, version 17.11 or later, with the instance running on AWS infrastructure ([GitLab product page](https://about.gitlab.com/gitlab-duo/duo-amazon-q/), [GitLab press release](https://about.gitlab.com/press/releases/2025-04-17-gitlab-announces-general-availability-of-gitlab-duo-with-amazon-q/)).
- **Deployment model.** Hybrid. The GitLab instance is self-managed, and the Amazon Q agents run as an AWS service that connects back to that instance ([GitLab docs](https://docs.gitlab.com/user/duo_amazon_q/setup/)). The add-on is not available on GitLab's SaaS offering ([GitLab product page](https://about.gitlab.com/gitlab-duo/duo-amazon-q/)) and became generally available in April 2025 ([AWS](https://aws.amazon.com/about-aws/whats-new/2025/04/gitlab-duo-amazon-q-generally-available)).

## Coder Overview for This Comparison

- **GitLab integration.** Coder supports GitLab through OAuth external auth, so workspaces can clone and push without users managing credentials by hand ([Coder docs](https://coder.com/docs/admin/external-auth)).
- **Coder Agents with GitLab.** Coder Agents can push commits, create GitLab merge requests, and read merge request diffs and status checks ([Coder docs](https://coder.com/docs/ai-coder/agents/platform-controls/git-providers)).
- **Self-hosted agents and workspaces.** Coder Agents runs the agent loop in the self-hosted Coder control plane, and each task executes in a Terraform-provisioned workspace. LLM credentials stay in the control plane, not in workspaces ([Coder Agents message house](../products/coder-agents/message-house.md)).
- **Air-gapped deployment.** Coder supports air-gapped, firewalled, and offline deployments ([Coder docs](https://coder.com/docs/install/airgap)).

## Known Limitations in GitLab Duo with Amazon Q's Approach

- **Network path into the instance (as of 2026-09-28).** Amazon Q uses the GitLab instance's REST APIs, so it must be able to reach the instance's HTTPS URL, and the certificate must not be self-signed. The instance must also allow inbound TCP/TLS traffic from a published set of Amazon Q IP addresses ([GitLab docs](https://docs.gitlab.com/user/duo_amazon_q/setup/)). An instance with no inbound network path from AWS, such as an air-gapped instance, cannot meet this prerequisite.
- **Single add-on (as of 2026-09-28).** GitLab Duo with Amazon Q cannot be combined with other GitLab Duo add-ons ([GitLab docs](https://docs.gitlab.com/user/duo_amazon_q/)).
- **Deployment scope (as of 2026-09-28).** The add-on is documented for GitLab Self-Managed on the Ultimate tier, running on AWS infrastructure ([GitLab docs](https://docs.gitlab.com/user/duo_amazon_q/), [GitLab product page](https://about.gitlab.com/gitlab-duo/duo-amazon-q/)).
- **Amazon Q Developer transition (as of 2026-09-28).** AWS blocked new Q Developer signups on May 15, 2026 and ends support for Q Developer IDE plugins and paid subscriptions on April 30, 2027. Code transformation, including Java upgrades delivered through the IDE plugins, is part of that end of support ([AWS](https://aws.amazon.com/blogs/devops/amazon-q-developer-end-of-support-announcement/)). The AWS announcement does not name GitLab Duo with Amazon Q, so the effect on this add-on is unclear from public sources.

## Common Questions

- **Does Coder replace GitLab?** No. Coder does not provide source control, CI/CD, or issue tracking. It connects to GitLab as a Git provider for workspaces and Coder Agents ([Coder docs](https://coder.com/docs/admin/external-auth)).
- **Can we use GitLab Duo with Amazon Q and Coder at the same time?** Yes. Duo quick actions run inside GitLab issues and merge requests ([AWS docs](https://docs.aws.amazon.com/amazonq/latest/qdeveloper-ug/gitlab-with-amazon-q.html)), while developers write and run code in Coder workspaces connected to the same GitLab instance ([Coder docs](https://coder.com/docs/admin/external-auth)).
- **Where do the two overlap?** Both offer an agent that takes a task and produces a merge request. Duo with Amazon Q does this from a GitLab issue with Amazon Q ([AWS](https://aws.amazon.com/about-aws/whats-new/2025/04/gitlab-duo-amazon-q-generally-available)). Coder Agents does it in a self-hosted workspace with the customer's choice of model ([Coder Agents message house](../products/coder-agents/message-house.md), [Coder docs](https://coder.com/docs/ai-coder/agents/platform-controls/git-providers)).
- **Can GitLab Duo with Amazon Q run air-gapped?** GitLab's setup documentation requires inbound access from Amazon Q services, which an air-gapped instance cannot provide ([GitLab docs](https://docs.gitlab.com/user/duo_amazon_q/setup/)). GitLab offers a separate product, GitLab Duo Agent Platform Self-Hosted, that runs offline with self-hosted models ([GitLab docs](https://docs.gitlab.com/administration/gitlab_duo_self_hosted/offline_deployment/)). Coder supports air-gapped deployment ([Coder docs](https://coder.com/docs/install/airgap)).
- **Does GitLab have its own development environments?** Yes. GitLab Workspaces is available on Premium and Ultimate and runs on a Kubernetes cluster through the GitLab agent for Kubernetes ([GitLab docs](https://docs.gitlab.com/user/workspace/gitlab_agent_configuration/)). That product is separate from GitLab Duo with Amazon Q and outside the scope of this page.
- **What happens to this add-on as Amazon Q Developer is retired?** Public sources don't say as of 2026-09-28. AWS's end-of-support announcement covers Q Developer IDE plugins and paid subscriptions and points customers to Kiro ([AWS](https://aws.amazon.com/blogs/devops/amazon-q-developer-end-of-support-announcement/)). Buyers should confirm the roadmap directly with GitLab and AWS.

## Pricing and Packaging

- **GitLab Duo with Amazon Q.** Pricing is not public. GitLab directs buyers to their account executive, requires the Ultimate tier, and also sells the add-on through AWS Marketplace ([GitLab docs](https://docs.gitlab.com/user/duo_amazon_q/), [AWS Marketplace](https://aws.amazon.com/marketplace/pp/prodview-utssgzylm7isg)).
- **Coder.** See [coder.com/pricing](https://coder.com/pricing) for current tiers and prices, and [Packaging](../company/packaging.md) for the reasoning behind them.

## Sources

- **[GitLab Duo with Amazon Q, GitLab Docs](https://docs.gitlab.com/user/duo_amazon_q/).** Primary. Tier, offering, add-on exclusivity, GitLab 17.11 requirement, how to buy. Accessed 2026-09-28.
- **[Set up GitLab Duo with Amazon Q, GitLab Docs](https://docs.gitlab.com/user/duo_amazon_q/setup/).** Primary. REST API access, certificate requirement, inbound network requirement from published Amazon Q IP addresses, IAM and OIDC setup, instance and group controls. Accessed 2026-09-28.
- **[GitLab Duo with Amazon Q, GitLab product page](https://about.gitlab.com/gitlab-duo/duo-amazon-q/).** Primary. Requirement to run on AWS infrastructure, network access to Amazon Q services, Self-Managed only availability. Accessed 2026-09-28.
- **[GitLab Duo with Amazon Q general availability, GitLab blog](https://about.gitlab.com/blog/gitlab-duo-with-amazon-q-agentic-ai-optimized-for-aws/).** Primary. Features powered by Amazon Q, Self-Managed deployment on AWS. Accessed 2026-09-28.
- **[GitLab general availability press release](https://about.gitlab.com/press/releases/2025-04-17-gitlab-announces-general-availability-of-gitlab-duo-with-amazon-q/).** Primary. Bundle for GitLab Ultimate Self-Managed customers on AWS. Accessed 2026-09-28.
- **[GitLab Duo with Amazon Q is now generally available, AWS What's New](https://aws.amazon.com/about-aws/whats-new/2025/04/gitlab-duo-amazon-q-generally-available).** Primary. GA date and agent capabilities. Accessed 2026-09-28.
- **[Introducing GitLab Duo with Amazon Q, AWS blog](https://aws.amazon.com/blogs/aws/introducing-gitlab-duo-with-amazon-q/).** Primary. Quick action workflow for development, review, fix, and Java transformation. Accessed 2026-09-28.
- **[GitLab Duo with Amazon Q, Amazon Q Developer User Guide](https://docs.aws.amazon.com/amazonq/latest/qdeveloper-ug/gitlab-with-amazon-q.html).** Primary. Feature list and availability. Accessed 2026-09-28.
- **[GitLab Duo concepts, Amazon Q Developer User Guide](https://docs.aws.amazon.com/amazonq/latest/qdeveloper-ug/gitlab-concepts.html).** Primary. Q Developer profile, OIDC provider, and IAM role requirements. Accessed 2026-09-28.
- **[Amazon Q Developer end-of-support announcement, AWS DevOps blog](https://aws.amazon.com/blogs/devops/amazon-q-developer-end-of-support-announcement/).** Primary. Signup cutoff, end-of-support date, code transformation scope, Kiro as successor. Accessed 2026-09-28.
- **[GitLab Duo with Amazon Q, AWS Marketplace](https://aws.amazon.com/marketplace/pp/prodview-utssgzylm7isg).** Primary. Marketplace availability. Accessed 2026-09-28.
- **[Deploy GitLab Duo Agent Platform Self-Hosted offline, GitLab Docs](https://docs.gitlab.com/administration/gitlab_duo_self_hosted/offline_deployment/).** Primary. Offline option for GitLab's separate self-hosted agent product. Accessed 2026-09-28.
- **[GitLab agent for Kubernetes configuration for Workspaces, GitLab Docs](https://docs.gitlab.com/user/workspace/gitlab_agent_configuration/).** Primary. GitLab Workspaces tier and Kubernetes requirement. Accessed 2026-09-28.
- **[External Auth for Git Providers, Coder Docs](https://coder.com/docs/admin/external-auth).** Primary. Coder's GitLab integration. Accessed 2026-09-28.
- **[Git Providers, Coder Agents Platform Controls, Coder Docs](https://coder.com/docs/ai-coder/agents/platform-controls/git-providers).** Primary. Coder Agents GitLab merge request support and scopes. Accessed 2026-09-28.
- **[Air-gapped Deployments, Coder Docs](https://coder.com/docs/install/airgap).** Primary. Coder air-gapped support. Accessed 2026-09-28.
- **[Coder Agents Message House](../products/coder-agents/message-house.md), [Why Coder](../company/why-coder.md).** Primary (Coder's vetted positioning). Coder Agents architecture, model support, and cloud neutrality. Accessed 2026-09-28.
