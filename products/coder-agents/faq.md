# Coder Agents FAQs

## 1. Coder Agents Overview

### Summary

**What is Coder Agents?**
Coder Agents is a new solution from Coder. It is a conversational AI experience and API built into the Coder product ([coder/coder](https://github.com/coder/coder)). It uses a native agent to execute research and coding tasks from the control plane, provisioning workspaces only when compute is required for development work.

**Why did we build it?**
Customers want the polished UX they see in tools like Cursor Agents, but with the security, governance, and infrastructure that enterprises require. Coder has already solved the harder problem of running AI-powered development workflows on self-hosted enterprise infrastructure. Now we are delivering the developer experience that matches it.

**What problem is it solving for developers and platform teams?**
Delivers the modern, conversational experience developers expect when working with agents, replacing the current CLI-wrapper approach with something intuitive and familiar. Customers no longer need to choose between enterprise governance and great UX or evaluate separate tools like Cursor to get it. They get both in one self-hosted platform.

For platform teams, it also creates a consistent agent experience across the entire development organization. Instead of individual developers experimenting with different tools, models, and configurations, platform teams can provide a standardized agent experience. That consistency makes it far easier to support developers, troubleshoot issues, and understand why something worked for one engineer but failed for another. The result is a more predictable and manageable way to introduce agents into the development workflow while still giving developers a powerful, modern interface.

**Why the name Coder Agents?**
The name is intentional and grounded in how buyers already think about this category.

The closest comparison in the market is Cursor Agents, so using the term Agents immediately places Coder in the same category. It creates an intuitive comparison for buyers: the same concept, but running on self-hosted Coder infrastructure instead of a hosted platform.

Using the term Agents alone would be ambiguous. It could refer to Anthropic's agents, OpenAI's agents, or other model-provider features. Calling it Coder Agents makes it clear whose agent it is and where it runs.

Using the full name Coder Agents consistently also reinforces the Coder brand and reduces confusion with the more generic term "agents," ensuring buyers clearly associate the capability with the Coder platform.

## 2. Current Stage, Access, and Feedback

**What stage is it in?**
Coder Agents is generally available as of September 1, 2026.

**Are there Docs?**
Yes: [https://coder.com/docs/ai-coder/agents](https://coder.com/docs/ai-coder/agents)

**How is customer support handled for Coder Agents?**
Beginning with general availability on September 1, 2026, the standard Support team owns customer support requests for Coder Agents.

## 3. What Coder Agents Is and Is Not

### What it is and what it is not (today)

**What it is**

- **Native agent for Coder deployments**
  Built directly into Coder deployments (coder/coder). It runs on the same self-hosted infrastructure customers already use.
- **Tasks replacement**
  It replaces the CLI-wrapper model with a familiar, polished UX while preserving Git-native workflows and enterprise controls. Coder Agents includes its own lightweight, purpose-built agent.
- **Self-hosted "Agents as a Service"**
  Coder becomes the AI interface, not just the infrastructure underneath someone else's coding agent.
- **Git-native, artifact-first**
  Coder Agent work results in branches, commits, and PRs (not state trapped inside a workspace).
- **Automation-ready**
  Coder Agents can be invoked via the API and integrated with workflows such as GitHub Actions to enable background agent execution across the SDLC.

**What it is not**

- **Not *just* a UI refresh of Tasks**
  This is an architectural shift. The agent loop runs in the coderd control plane, not inside a wrapped third-party CLI.
- **Not a wrapper around Claude Code or Codex**
  We're not proxying someone else's UX; we're building our own agent runtime and interface.
- **Not a power-user-only tool**
  This is designed to be approachable and usable by the average developer, not just AI enthusiasts. Still capable of heavy lifting.
- **Not "magic AI"**
  It still relies on model providers like Anthropic and OpenAI. Intelligence is external, orchestration and UX are ours.

**What agents are we using? Claude Code, Codex, or something else?**
None of the above. Coder Agents uses its own lightweight agent, purpose-built for this experience. It is open source, configurable, and model-agnostic. Customers can use their preferred LLM provider without worrying about lock-in.

This flexibility is important as the AI landscape evolves quickly. Developers increasingly want the freedom to switch between the latest frontier models regardless of who provides them, and Coder Agents makes that possible.

## 4. Tasks Deprecation and Migration

**How is this different from Tasks?**
Coder Agents is the successor to Coder Tasks and has replaced it. Coder Tasks was deprecated in Coder v2.34 and has since been removed, including the Tasks API. Coder Agents represents a fundamentally different philosophy, architecture, and user experience for working with AI inside Coder.

Unlike Tasks, Coder Agents is not a wrapper around third-party agents such as Claude Code or Codex. It uses Coder's own lightweight agent, giving us full control over the runtime and user experience.

The underlying architecture is also different. With Tasks, the AI loop runs inside the workspace. With Coder Agents, the agent runs in the coderd control plane and interacts with Coder workspaces the same way a developer would, through commands like read, write, edit, and exec. Workspaces become the execution environment rather than the location where the agent itself lives.

This architecture allows Coder Agents to respond immediately without provisioning compute for every interaction. A workspace is only started when the agent actually needs to perform development work such as editing code or running commands.

Like Tasks, Coder Agents still exposes an API so developers can trigger background work through automation and integrations such as CI systems, GitHub workflows, or other tooling.

**What about customers who are using Tasks?**
Coder Agents is the next generation of Tasks and has replaced it. Tasks helped validate the demand for delegating development work to AI agents inside Coder, but its architecture and CLI-wrapper UX were an early implementation.

Coder Agents introduces a fundamentally different architecture and a modern, conversational experience built directly into the platform. It is now the primary way developers interact with agents in Coder.

Coder Tasks and the Tasks API (`/api/v2/tasks`) have been removed. Customers with integrations built on the Tasks API should move them to the Chats API (`/api/v2/chats`) using the [Tasks to Chats migration guide](https://coder.com/docs/ai-coder/agents/tasks-to-chats-migration).

**Will I need to relearn everything I just learned about Tasks?**
No, absolutely not. The fundamental principles you've learned about Tasks and the value they deliver to customers still apply to Coder Agents.

For technical teams at Coder, there will be some architectural and implementation differences to understand. However, from a customer perspective we are solving the same core problem: giving enterprises a safe, controlled way to run agentic workloads on their Coder infrastructure.

What changes is how we deliver that capability. Coder Agents introduces a fundamentally better architecture and a more intuitive user experience. Early feedback from design partners and customers participating in the Early Access program already suggests the experience is significantly better.

So while the mechanics behind the scenes are evolving, the core story remains the same. Coder enables enterprises to run AI agents securely on their own infrastructure, with the governance and control platform teams require.

## 5. Architecture, Control Plane, and Workspaces

**What does it mean to run the agent loop in the coderd control plane?**
With Coder Tasks, the agent loop (LLM and tool calls) always happened in Coder workspaces. This meant that, for the agent to respond to a simple "hello," it had to start a Coder workspace. This was slow, expensive, and unnecessary.

With the new Coder Agents architecture, the agent loop runs in the coderd control plane. This means that it can make requests to LLM providers and reason without a Coder workspace. This is faster, cheaper, and the expected developer experience. The Coder Agent will still provision a Coder workspace as needed for read/write/edit/exec commands.

**Does the agent loop running in the control plane mean customers need more infrastructure?**
The Coder Agent will simply make HTTP requests to the LLM providers, which requires little to no additional overhead. In fact, the new architecture will create efficiencies for customers because, unlike with Coder Tasks, they will not need to provision workspaces for *every* chat, only when necessary for coding work.

For most customers, this should not introduce meaningful new infrastructure requirements. Larger organizations with especially high chat volume or that want more dedicated capacity for agent workloads can work with Coder to explore additional deployment options for scaling within their own environments.

**Can users run the agent inside an existing workspace that already has credentials, but with guardrails so the agent doesn't get "free access" to everything?**
Coder Agents does not run inside the workspace at all.

The agent runs in the control plane and only interacts with a workspace through commands like read, write, edit, and execute, similar to how a developer would interact with the environment through VS Code or a terminal.

Because of this architecture, no AI actually exists inside the workspace. The workspace itself is unaware that an agent is involved. The agent simply performs actions against the workspace on behalf of the user.

As a result, the agent does not gain inherent access to everything inside the workspace. It operates with the same permissions as the user invoking it and only interacts with the workspace when needed to perform specific tasks.

**Do we recommend separate "agent workspaces" vs "my main dev workspace"?**
Optional.

Platform teams may choose to create agent-specific templates with tighter network permissions or more limited access than the environments used by human developers. In some organizations, that separation can provide additional control or isolation. However, it is not a requirement. Agents can operate using the same templates and workspace patterns that developers already use today.

The most important step platform teams can take is to ensure their workspace templates are clearly named and well described. Templates should include concise descriptions explaining their purpose, who should use them, and which repositories or workloads they support. These details help the agent determine which template is most appropriate when provisioning a workspace for a task.

**How can customers leverage their existing configuration, automation, and policy for previous agents like Claude Code?**
It depends. These topics are broad, so the right answer often requires clarifying what type of configuration, policy, or automation a customer is referring to.

In general, Coder Agents manages configuration at the platform level rather than inside individual developer environments. Coder Agents uses the same workspace templates and user policies that organizations already use for their human developers. The agent simply inherits the same permissions as the Coder user who invokes it.

Platform teams can also centrally control important aspects of the agent's behavior, such as the system prompt and the tools the agent is allowed to use.

For automation, Coder Agents exposes an API that allows background tasks to be triggered from external systems such as CI pipelines, GitHub workflows, Slack, or other integrations. This allows many existing automation patterns to be replicated or adapted using the Coder Agents API.

**If the internal object is "chat," do we expose "chat" or "task" semantics externally?**
Chats. The Coder Agents API is the Chats API, available at `/api/v2/chats`.

## 6. Security, Governance, and Admin Controls

**Does running the agent in the control plane create a larger security risk since it can access many workspaces?**
No. The agent does not have broad access across workspaces.

Coder Agents operates using the same identity and permissions as the user who initiated the task. It can only interact with the workspace the user intends to use, just as if the user had created and used that workspace themselves.

In practice, the agent simply performs actions on behalf of the user. It provisions a workspace when needed and interacts with it using the same permissions the user already has. The agent does not receive elevated privileges or additional access beyond the user's existing authorization.

**How do Coder's existing AI Governance features, AI Gateway and Agent Firewall, work with Coder Agents?**
Agent Firewall was originally designed to observe and control how third-party agents (Claude Code, Codex) operate inside Coder Workspaces. In those scenarios, the agent runs directly inside the workspace environment, which means additional governance layers are needed to protect coinciding sensitive data, credentials, and network access.

Coder Agents introduces a different architecture. The agent loop, model credentials, and prompt handling run in the control plane rather than inside the workspace. This removes the need to place provider API keys or agent software in the workspace, which eliminates a meaningful class of risk.

When Coder Agents runs a shell tool call, that command executes inside the workspace, so the workspace's network access applies to it. Platform teams control that traffic through workspace-level network policy defined in the template.

Coder Agents' integration with AI Gateway focuses on observability and auditability. Agent sessions, prompts, and tool calls can be captured through AI Gateway and viewed in Coder's AI Session dashboard, or queried via a Prometheus endpoint and added to customers' Grafana dashboards.

Coder Agents also integrates with AI Gateway's cost controls, giving platform teams a centralized place to control and observe LLM spend across their Coder deployment.

**What does this mean for customers currently using AI Governance?**
AI Governance is still relevant, but its role depends on how customers choose to run agents. If they continue using third-party agents like Claude Code or Codex inside Coder workspaces, then AI Governance, including AI Gateway and Agent Firewall, remains the right solution for control and oversight.

If they adopt Coder Agents, AI Gateway continues to provide visibility, attribution, and cost governance over LLM usage, and network restrictions for agent workspaces come from template-defined network policy. Platform teams should configure that policy deliberately rather than assume the control-plane architecture removes the need for it.

**Are AI Bridge and Agent Boundaries being deprecated, and on what timeline?**
No, these features are not being deprecated. This FAQ covers how they will remain useful features for customers running third-party agents in Coder workspaces and for customers who choose to use Coder Agents. Engineering resources will continue to be allocated to advancing AI Gateway's maturity.

**Can we enforce spending limits per user/team?**
Yes, spending limits can be enforced at the user and group level through AI Gateway.

**Can we restrict internet access (or allow it only through approved tools)?**
Yes. Internet access can be controlled at the workspace level through the Terraform template used to provision the environment.

Platform teams can configure templates so that workspaces have restricted or even no external network access. In some cases, workspaces can be completely isolated from the internet.

The only external connectivity required for the broader Coder Agents system is between the Coder control plane and the LLM provider. If a customer is using a self-hosted model, even that external dependency can be removed.

**Can admins enforce approved model providers and models (Anthropic, OpenAI, etc)?**
Yes, absolutely. Administrators have full control over which model providers and specific models are available to developers.

Platform teams can define the approved models at the platform level, ensuring developers only use models that meet the organization's security, compliance, and cost requirements. Developers do not have the ability to add or remove models themselves.

**Do we have a clear framework or recommendations for when to use one LLM versus another?**
The models are fully configurable, so the Platform team can add any LLMs they pay for (and set the default). The frontier models are changing by the week; new ones come out, and existing ones get dumber, so it'll be hard for us (Coder) to be prescriptive. However, we will provide the Platform team with useful insights into how their chosen models are performing within their teams. For example, maybe backend pull requests using Codex 5.3 are merged at higher rates than those using Opus 4.6. We could surface that information, then they decide how to distribute it to their internal teams.

**Is spend enforced at the platform level or can it be per template? Can models be approved at the template level or just platform-wide?**
Today, we are designing these controls to be enforced primarily at the Group and individual level. Configuration, governance, and model access are managed centrally rather than being tied to individual templates. That said, templates may still influence behavior indirectly through environment configuration, but they are not the primary mechanism for enforcing spend or model policy.

As we continue to gather feedback, we may explore more granular controls, but the current direction is to keep enforcement centralized to ensure consistency, simplicity, and strong governance across the platform.

## 7. Positioning, Messaging, and Customer Journey

**Does this change our messaging around being agent-agnostic?**
No. Coder will remain agent-agnostic.

Supporting a broad ecosystem of developer tools is part of Coder's DNA, and we do not expect that to change. Developers and platform teams can continue using other agents such as Claude Code or Codex inside Coder workspaces, and we provide governance and infrastructure controls to help organizations do that safely.

At the same time, Coder Agents is the golden path for running agents on self-hosted Coder infrastructure. It is the native experience designed specifically for the Coder platform, and it offers advantages in security, platform consistency, and overall developer experience.

In other words, customers can still use other agents with Coder, but Coder Agents provides the ideal out-of-the-box experience for running agentic workloads on Coder infrastructure.

**How does this align with the Migrate, Modernize, Multiply customer journey framework?**
Coder Agents mostly aligns with the Multiply stage, with a partial role in Modernize.

In the Modernize phase, platform teams begin introducing AI tools and agents into developer workflows. Instead of deploying third-party agents inside Coder workspaces, teams can use Coder Agents to provide a simpler, more consistent agent experience across the organization.

In the Multiply phase, organizations begin scaling agentic workflows. Coder Agents supports this by allowing teams to run agents through APIs, automate development tasks, and operate agents across many repositories and workspaces.

## 8. Launch and GTM

**What is the launch timeline for Coder Agents?**
Coder Agents became generally available on September 1, 2026. It entered beta on May 5, 2026, supported by distribution across existing customers, prospective buyers, and the open source community. Later releases are promoted as Coder Agents reaches scalability milestones, AI Governance integration, and other feature improvements.

**How does Coder Agents fit into a customer's evaluation of Coder?**
Coder Agents is deployed as part of the existing Coder platform. It runs in the same binary and fits directly into Coder's control plane architecture, so it's available during proof-of-concept evaluations without requiring additional installation or integration.

Because Coder Agents runs in the control plane rather than inside workspaces, it also reduces the need to assess how third-party agents integrate with developer environments or access sensitive data. Teams may still want to evaluate the architecture more deeply, which is expected, but for organizations already familiar with how Coder's control plane and workspaces operate, Coder Agents fits naturally into that model.

## 9. Pricing, Packaging, Licensing, and Unit Economics

**What is the pricing model for Coder Agents?**
The Coder Agents pricing and usage model takes effect at general availability on September 1, 2026. Community and Premium licenses support up to five concurrently active agents at no additional cost. AI Premium removes the concurrency limit and includes a deployment-wide allotment of Agent Hours that customers size and buy based on expected usage. API-triggered agents are available in every tier.

Beginning September 1, 2026, Community and Premium licenses support up to five concurrently active agents. There is no limit on how long those agents can run or how many tasks they complete over time; additional agents queue whenever more than five are active. This enables individuals and small teams to experiment with Coder Agents at no cost.

AI Premium includes a deployment-wide allotment of Agent Hours, sized and purchased based on expected usage. Agent Hours are shared across the deployment, allowing any number of agents to run concurrently while consuming from a shared pool of purchased working hours. This usage-based model is designed for enterprise workloads, where large development teams, background automation, and API-triggered tasks can create highly variable bursts of agent activity without being constrained by a concurrency limit.

**Where can I find current pricing details?**
[coder.com/pricing](https://coder.com/pricing) is the source of truth for current numbers. This document covers the mechanics of the model; if it and the pricing page ever diverge, treat the pricing page as authoritative and flag the discrepancy to Product Marketing.

**How will Coder Agents be packaged?**
Coder Agents is an additional solution that will be part of the existing Coder install. Coder Agents is not a separate product or deployment.

**How will Community, Premium, and AI Premium licensing work?**
Coder Agents is shipped as part of the same open-core repository as the rest of the Coder product, but that doesn't mean all functionality is free.

Beginning September 1, 2026, Community and Premium licenses support up to five concurrently active agents. There is no limit on how long those agents can run or how many tasks they complete over time; additional agents queue whenever more than five are active. This enables individuals and small teams to experiment with Coder Agents at no cost.

AI Premium includes a deployment-wide allotment of Agent Hours, sized and purchased based on expected usage. Agent Hours are shared across the deployment, allowing any number of agents to run concurrently while consuming from a shared pool of purchased working hours. This usage-based model is designed for enterprise workloads with large development teams, background automation, and API-triggered tasks that can create highly variable bursts of agent activity.

**How do air-gapped deployments report Agent Hours usage?**
Connected deployments report hourly Agent Time totals to Coder automatically, with no user or chat data. Air-gapped customers can send a manually exported usage bundle instead, or establish another usage-based agreement with their Coder sales team.

**How is Agent Hours usage measured?**
Coder measures Agent Time, the cumulative duration of model invocations that produce Coder Agents chat messages, including sub-agents and context compaction. It excludes time spent waiting for user input, failed model calls, and work handed off to external agents. See [Licensing and Usage](https://coder.com/docs/ai-coder/agents/licensing-usage).

**What happens when a deployment runs out of Agent Hours?**
Administrators get an in-app warning as the deployment approaches its allotment, so they can buy more before the concurrency fallback takes effect.

## 10. Third-Party Agents and Agent Ecosystem

**Will Coder Agents support third-party agent harnesses like Claude Code?**
This is an active area of focus.

Customer expectations exist on a spectrum. Some think they need a specific harness for capabilities like MCP or custom skills. In many of those cases, Coder Agents already addresses the need. Organization admins can register external [MCP servers](https://coder.com/docs/ai-coder/agents/platform-controls/mcp-servers), and workspace templates can provide [skills and MCP tools](https://coder.com/docs/ai-coder/agents/extending-agents). Others have deeply integrated with a specific agent ecosystem at scale, and the switching cost is significant.

The architectural challenge is real: Coder Agents runs in the control plane, while third-party harnesses run inside the workspace. Bridging those two models in a way that delivers a coherent developer experience, not just background API execution, is a hard problem. We are not going to rush a half-functional integration that creates more problems than it solves.

Our approach is to keep closing the gaps that drive customers toward third-party harnesses in the first place, such as extensible tooling and richer UX patterns, while exploring what responsible third-party harness support could look like.

In the meantime, customers can still run third-party agents like Claude Code inside Coder Workspaces with AI Governance controls. That remains a supported path, even as Coder Agents is our recommended direction for new deployments.

**Why would a developer use Coder Agents instead of Claude Code?**
Developers would use Coder Agents when they want a safer place for agents to do work. Instead of running an agent directly on a local machine, Coder Agents can operate against network-isolated workspaces on self-hosted infrastructure, which reduces risk to the developer's own system and keeps the work inside an environment the platform team controls.

Coder Agents is also fully configurable and model-agnostic. That means teams can shape how the agent behaves and developers can move between models as the landscape evolves, rather than being locked into a single provider or agent experience.

For platform teams, that's the bigger win: they can shape the experience behind the scenes, guide which environments get used, and improve templates over time based on patterns in agent chats. So the developer gets a simpler and safer experience, while the platform team gets more control, consistency, and visibility.

**Can customers still use third-party agents like Claude Code or Codex with Coder?**
Yes. Customers can still run third-party agents like Claude Code or Codex with Coder, but they do so directly inside Coder Workspaces.

That is a fundamentally different deployment model from Coder Agents. Coder Agents runs natively in the control plane and only interacts with workspaces when needed, whereas third-party agents operate from within the workspace itself. Because of that, running third-party agents typically requires an additional layer of AI Governance to control what the agent can access and how it behaves inside the workspace.

Coder Agents is separate. It is a native capability built into Coder, not a wrapper around external agents.

## 11. Use Cases and Future Direction

**What kind of value can Coder Agents provide without running a workspace?**
Coder Agents can deliver meaningful value across the software development lifecycle even when no workspace is running.

For example, an agent can research codebases using its GitHub tools. These interactions allow developers to ask questions, explore repositories, and gather context without needing to provision a development environment.

Agents can also review pull requests. In this case, the agent can examine the changes in a PR, analyze the code, and provide feedback on quality, patterns, or potential issues without ever starting a workspace.

These types of capabilities are highly valuable to developers, especially in enterprise environments, and represent an important area where Coder Agents can deliver value independently of workspace execution.

**Can Coder Agents be used for use cases beyond coding? Do we anticipate customers will do this?**
Yes, potentially. While Coder Agents is designed for development-first use cases, it is inherently extensible.

Through mechanisms like MCP and custom tooling, organizations can extend the agent's capabilities beyond traditional coding tasks. This could include interacting with internal systems, automating workflows, or supporting adjacent use cases for technical and semi-technical users.

That said, our primary focus remains on delivering a best-in-class experience for software development. Broader use cases are possible, and we expect some customers to explore them, but they will be driven by how organizations choose to extend the platform rather than the core product direction.

## 12. Competitive Landscape: Cursor

**How does Coder Agents compare to Cursor?**
TL;DR: Coder Agents is most comparable to Cursor Agents, but the two products work in very different ways. Cursor Agents typically runs on Cursor's hosted infrastructure, while Coder Agents runs entirely on a customer's self-hosted Coder deployment. This allows enterprises to run agentic workloads on their own infrastructure with stronger security and control.

Cursor also offers a hybrid model, where agent orchestration and model inference run in Cursor's cloud while execution connects out to a self-hosted environment such as a Coder workspace through Coder Agent Relay. That's a real option for organizations willing to keep orchestration and inference off-premises, but it stops short of the fully self-hosted, air-gapped operation Coder Agents provides, where orchestration, inference, and execution all run on infrastructure the customer controls. For organizations that require everything to stay fully self-hosted and air-gapped, Cursor's hybrid model isn't viable and Coder Agents is the fit.

**How does Coder Agents compare to Cursor's IDE?**
Cursor offers several different products, so it's important not to confuse them.

Coder Agents should not be compared to Cursor's traditional AI IDE, which is essentially an AI-powered text editor. Coder Agents is not a text editor. It is a chat interface where developers interact with one or more agents in parallel while the agent workloads run on the customer's self-hosted Coder infrastructure.

## 13. Competitive Landscape: AI IDEs

**How does Coder Agents compare to AI IDEs like Cursor, Zed, Windsurf, or Kiro?**
AI IDEs like Cursor, Zed, Windsurf, and Kiro are fundamentally text editors, often forked from VS Code, with AI features layered on top. They're designed to enhance the experience of writing and editing code directly.

Coder Agents takes a different approach. It's not a text editor. Instead, it's a system for generating and executing work through agents, producing code and outcomes on behalf of the developer.

In practice, we expect these tools to coexist. Developers will continue to use IDEs as part of their workflow. They still need a place to review, refine, and work hands-on with code. What may change over time is how much time they spend in those tools. As agents take on more of the heavy lifting, developers may rely less on manual coding in IDEs and more on directing and reviewing work produced in Coder Agents.

The goal isn't to replace IDEs or make them obsolete. It's to shift where the bulk of code creation happens, while IDEs remain an important part of the overall toolchain.

## 14. Competitive Landscape: Claude Code and Codex

**How does Coder Agents compare to Claude Code or Codex?**
Coder Agents fundamentally differ from tools like Claude Code and Codex in many dimensions. Here are a few:

First, Coder Agents gives platform teams full visibility and control over how the agent works. Because it is open source, teams can inspect, configure, and extend the agent to fit their infrastructure and policies. Claude Code and Codex are closed agents with limited visibility into their internal behavior.

Second, Claude Code and Codex are typically used as terminal-based agents that run directly inside a development environment. Enterprises can deploy these tools to their developers today, and Coder already provides governance controls to make that possible. However, these agents still run within the Coder Workspace, where they may have access to critical credentials and source code.

Coder Agents uses a different architecture. The agent runs in the Coder control plane and only interacts with workspaces when necessary. It reads files, writes changes, edits code, or executes commands in the workspace the same way a developer would through a terminal or IDE. Because the Coder agent does not live in the workspace, it does not have direct visibility into credentials or AI configurations there. The workspace itself remains unaware of the AI.

This separation provides a safer and more controlled way to run agents on enterprise infrastructure. In addition, Coder Agents includes a chat-based interface and an API that allows developers and automation systems to trigger background agent work when needed.

## 15. Competitive Landscape: Anthropic and Claude Managed Agents

**Anthropic is rapidly developing Claude Cowork. Do we see that as competitive? Is there a chance they commoditize workspaces through that interface?**
We don't see Claude Cowork as a direct competitor today. It's primarily a desktop productivity tool for business users, not an agent platform designed to run on enterprise infrastructure or support platform teams.

Depending on its trajectory, this could change. If Anthropic expands Cowork into a broader agent surface with hosted development environments, workspaces could become a thin commodity layer beneath their models, similar to what Cursor has done.

That said, this scenario plays directly into our positioning. Coder is built around running agents on self-hosted, enterprise infrastructure with the security and governance large organizations require, which is the hardest part of the problem. So rather than a threat today, Cowork is a signal that model providers are moving toward agent-first experiences, reinforcing why this direction matters now.

**Is Claude Managed Agents competitive with Coder Agents?**
Not really. Claude Managed Agents ([https://platform.claude.com/docs/en/managed-agents/overview](https://platform.claude.com/docs/en/managed-agents/overview)) runs entirely on Anthropic's cloud infrastructure and only supports Claude models. Coder Agents runs on the customer's own infrastructure, VPC, on-prem, or air-gapped, and is model-provider agnostic. For enterprises that require data residency, auditability, or model flexibility, Claude Managed Agents is not a viable option and Coder Agents is the answer.

**What should I tell a customer who asks about Claude Managed Agents?**
Coder Agents and Claude Managed Agents solve different parts of the problem for different buyers. Claude Managed Agents is a good fit for teams that are comfortable running agent workloads on Anthropic's cloud and only need Claude models. Coder Agents is the right choice when the organization needs self-hosted infrastructure, model-provider flexibility, or the governance and audit controls that regulated enterprises require. Customers using Coder Agents can still connect to Anthropic's Claude models, all roads lead to LLM spend, and Coder helps enterprises get there with more control.

## 16. Competitive Landscape: VS Code Agents and GitHub Copilot

**How does Coder Agents compare to VS Code Agents?**
VS Code Agents ([https://code.visualstudio.com/updates/v1_115#_visual-studio-code-agents-preview](https://code.visualstudio.com/updates/v1_115#_visual-studio-code-agents-preview)) is a companion app for running parallel GitHub Copilot agent sessions. It lets developers manage multiple agent sessions across repos, each isolated in its own worktree, with support for local, background, and cloud execution.

GitHub has also invested in enterprise controls for Copilot agents. Enterprise AI Controls (GA as of February 2026) provides identity-attributed audit logging, premium request budgets at the org and enterprise level, centralized model and MCP allowlists, and version-controlled custom agent definitions.

The difference is where all of that runs. GitHub's governance layer, model routing, agent execution, and audit infrastructure all live on GitHub and Microsoft's cloud. Coder Agents runs entirely on the customer's own infrastructure, VPC, on-prem, or air-gapped, with model routing going directly from the customer's control plane to any provider or self-hosted endpoint, no intermediary required.

For enterprises that require data residency, self-hosted model access, or governance infrastructure that doesn't depend on a third-party cloud, that distinction is the one that matters.

**Does VS Code Agents make Coder Agents less relevant?**
No, it validates the category. Microsoft is telling the market that developers need a dedicated surface for managing parallel agent sessions, the same bet we're making with Coder Agents.

But VS Code Agents and GitHub's Enterprise AI Controls are built to govern agents within GitHub's cloud ecosystem. The admin console, audit logs, model routing, and agent execution all run on GitHub and Microsoft infrastructure. For many organizations, that's sufficient.

For enterprises that need governance infrastructure on their own network, self-hosted model endpoints, air-gapped environments, workspace provisioning controlled by Terraform templates, or headless agent execution triggered from CI/CD without a developer in an IDE, Coder Agents is the answer GitHub's ecosystem doesn't provide. Every agentic IDE feature that ships without self-hosted infrastructure reinforces the question our buyers are already asking: "How do we give developers this capability without sending our source code and agent activity to someone else's cloud?"

**If VS Code now supports multiple models via BYOK, how is Coder Agents still differentiated on model flexibility?**
VS Code does support multiple model providers through Copilot's BYOK feature. The difference is where model routing happens. VS Code's model access is mediated through GitHub Copilot's cloud infrastructure, and admins configure it via Copilot policy settings on GitHub.com. Coder Agents routes model requests directly from the customer's own control plane to whatever provider or self-hosted endpoint they configure, no intermediary, no dependency on GitHub's cloud. For customers running self-hosted open-weight models or operating in air-gapped environments, that distinction is the difference between "possible" and "not possible."

## 17. Competitive Landscape and Partnerships: AWS, Bedrock, Kiro, and Claude Platform on AWS

**How does Coder Agents impact our relationship with AWS?**
Coder Agents strengthens our alignment with AWS.

AWS is primarily focused on driving usage of EC2, EKS, and Bedrock. Coder already supports EC2 and EKS as core infrastructure for running development environments, and Coder Agents extend that value further.

With Coder Agents, there's an additional opportunity to drive Bedrock usage by enabling agent usage through the Bedrock provider. As agents take on more tasks, they naturally increase demand for LLM token usage. So rather than creating tension, Coder Agents deepen the partnership. It creates another pathway for customers to adopt and expand their use of AWS services.

The Kiro IDE is still compatible with Coder Workspaces and AI Governance. AWS is also working on a Kiro autonomous agent, and we are working with their product team to ensure compatibility with Workspaces and AI Governance as well.

**How is this different from AWS Bedrock?**
AWS Bedrock and Coder Agents are complementary, not competitive. AWS Bedrock provides access to underlying LLM models. Coder Agents sits above that layer, orchestrating how those models are used to perform real development work on self-hosted infrastructure.

In practice, customers can use AWS Bedrock to supply frontier models, while Coder Agents handles the execution, workflows, and integration with their development environments.

**Does Claude Platform on AWS compete with Coder Agents?**
Not directly. Claude Platform on AWS is a billing and access channel, it makes it easier for AWS customers to pay for and authenticate to Anthropic's hosted Claude Platform. It doesn't solve the self-hosted, air-gapped, or model-agnostic requirements that drive Coder Agents adoption. The data is still processed on Anthropic's infrastructure, outside the AWS security boundary. For enterprises that need source code to stay in their perimeter, this changes nothing.

**Does the AWS IAM and CloudTrail integration close the governance gap?**
It narrows it, but doesn't close it. Customers get IAM-based access control, CloudTrail audit logs, and consolidated billing, which is more governance than raw Claude Code usage gives you. But this is governance over access and spend, not governance over what the agent does. There's no centralized system prompt enforcement, no model-agnostic provider configuration, no workspace-level network isolation, and no infrastructure-as-code provisioning. Coder Agents provides governance at the infrastructure and execution layer, which is a fundamentally different level of control.

**Should enterprises just use Claude Platform on AWS instead of evaluating Coder Agents?**
Claude Platform on AWS is a reasonable near-term option for non-regulated buyers who want to get started with Claude quickly. Over time, as enterprises centralize Claude usage through AWS and see real adoption and token spend, they typically start asking where their code is going, whether they can run this on their own infrastructure, and how to govern what agents are doing across teams. That's the conversation where Coder Agents fits in, as a complement to Claude Platform on AWS rather than a competitor to it: Claude Platform on AWS works well for lightweight API access and experimentation, while Coder Agents is the right fit when the organization needs self-hosted execution, model flexibility, or full infrastructure governance.
