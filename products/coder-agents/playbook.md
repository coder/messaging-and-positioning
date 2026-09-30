# Coder Agents Playbook

> A shared reference for understanding where Coder Agents fits, how it works, and how to support organizations evaluating or adopting it.

For positioning, messaging, and value propositions, see the [Coder Agents message house](./message-house.md). For detailed product questions, see the [Coder Agents FAQ](./faq.md).

---

## 1. Quick Reference

| | |
|---|---|
| **The product** | Coder Agents is a self-hosted chat interface and API for delegating development work to Coder's own coding agent, which runs in the Coder control plane. |
| **Best fit** | Regulated or governance-sensitive organizations that want native AI coding agents without sending source code to a third-party cloud. |
| **Common signal** | "We want something like Cursor Agents, but it has to run on our infrastructure with the models we approve." |
| **Key question** | "Does the agent's orchestration need to run inside your perimeter, or only its execution?" |
| **Core value** | Developers get a modern agent experience, and platform and security teams keep orchestration, execution, and model choice on infrastructure they control. |
| **Important limitation** | Coder Agents uses its own agent. It doesn't run third-party harnesses like Claude Code or Codex. |
| **Status** | Generally available since September 1, 2026. |
| **Journey stage** | Mostly Multiply, with a partial role in Modernize. See the [customer journey](../../company/customer-journey.md). |
| **Next step** | Enable Coder Agents in an existing or proof-of-concept Coder deployment by following [Getting Started](https://coder.com/docs/ai-coder/agents/getting-started). |

---

## 2. Overview

Coder Agents is built into Coder, in the same binary as the rest of the platform. Developers describe the work they want done through chat or the API. The agent selects a template, provisions a workspace when it needs one, writes and tests code, and produces branches, commits, and pull requests.

The agent loop runs in the Coder control plane rather than inside the workspace. LLM credentials stay in the control plane, workspaces need no agent software, and the agent acts with the same permissions as the user who prompted it. Coder Agents works with any configured LLM provider, including self-hosted models, so inference can stay inside the perimeter too.

Enterprises want to adopt coding agents, but cloud-hosted agents send code outside the perimeter and agents on laptops run with ambient credentials. Coder Agents gives them a governed, self-hosted alternative. See the message house for the full [status quo and 3 Whys](./message-house.md#the-3-whys).

---

## 3. How It Works

### Architecture summary

When a user submits a prompt, the control plane sends it to the configured LLM provider, receives tool calls, and executes them in a Coder workspace over the same connection used for web terminals and IDE access. Chats that don't need a workspace, such as Q&A, planning, or pull request review, start without provisioning one. See [Coder Agents architecture](https://coder.com/docs/ai-coder/agents/architecture).

### Components and responsibilities

| Component | Responsibility |
|---|---|
| Coder control plane | Runs the agent loop, stores chat history, holds LLM credentials, and enforces models, system prompts, and tool permissions |
| LLM provider | Performs inference. Any configured provider, such as Anthropic, OpenAI, Google, Azure OpenAI, AWS Bedrock, or a self-hosted OpenAI-compatible endpoint |
| Coder workspace | Standard compute, provisioned from a Terraform template, where the agent reads files, edits code, and runs commands. It has no AI software or API keys |
| AI Gateway | Records prompts, token usage, and tool calls with user attribution, and enforces spend limits |
| Platform team | Configures providers and models, writes clear template descriptions, and defines workspace network policy |

### Typical workflow

**Developer**

1. **Prompt.** A developer describes a task in the Coder Agents chat.
2. **Provision.** If the task needs a workspace, the agent picks a template the user can access and creates one.
3. **Work.** The agent edits code, runs tests, and can spawn sub-agents for parallel work.
4. **Review.** The agent opens a pull request, and the developer reviews it or opens the workspace in an IDE such as VS Code or Cursor to refine the result.

**Automation**

1. **Trigger.** A CI system, GitHub workflow, or other tool calls the [Chats API](https://coder.com/docs/reference/api/chats).
2. **Run.** The agent works in the background under the identity of the user who owns the request.
3. **Deliver.** Results land as branches and pull requests for human review.

**Platform team**

1. **Configure.** Add LLM providers and models, and optionally a system prompt, MCP servers, and spend limits.
2. **Prepare templates.** Write descriptive template names and descriptions, and optionally create agent-specific templates with stricter network policies.
3. **Observe.** Track usage, cost, and agent activity through AI Gateway.

### Deployment model

Everything runs in the customer's Coder deployment, in a cloud VPC, on-premises, or air-gapped. There is no SaaS or managed component. Coder Agents is available in every Coder deployment without a separate install.

### Data and trust boundaries

The agent loop, chat history, and tool execution stay inside the customer's Coder deployment. Prompts and code context go to whichever LLM provider the platform team configures. With a self-hosted model, inference stays inside the perimeter too. Workspaces don't need access to LLM providers, so they can be restricted to the control plane and the git provider. AI Premium deployments report hourly Agent Hours usage, with no user or chat data, to a Coder-managed billing service. Air-gapped customers can send a manually exported usage bundle instead, or establish another usage-based agreement with their Coder sales team. See [Licensing and Usage](https://coder.com/docs/ai-coder/agents/licensing-usage).

---

## 4. Boundaries and Terminology

See the FAQ's [What Coder Agents Is and Is Not](./faq.md#3-what-coder-agents-is-and-is-not) for more.

### What the product does not do

- Wrap or run third-party agent harnesses such as Claude Code or Codex. Those run inside workspaces with AI Governance instead.
- Replace the IDE. Developers still use VS Code, Cursor, JetBrains, or other editors to review and refine work.
- Restrict network access by default. If a template allows full internet access, agent workspaces have it too.
- Provide its own models. Intelligence comes from the configured LLM provider.

### Recommended terminology

| Preferred | Avoid | Why |
|---|---|---|
| "Coder Agents" | "Agents" alone | The full name makes clear whose agent it is and where it runs. |
| "The agent loop runs in the Coder control plane" | "The agent runs in the workspace" | Workspaces are only the execution environment. |
| "Air-gap capable with a self-hosted model" | "Air-gapped" with no qualification | Inference stays in the perimeter only when the model is self-hosted. |
| "Model-agnostic" | "Includes models" | Customers bring their own LLM provider. |

---

## 5. Fit

See the message house's [Target Market / ICP](./message-house.md#target-market--icp) for the full ideal customer profile.

### Use cases

Coder Agents' primary use cases are data residency and sovereign AI, avoiding lock-in to one model provider, scaling agents on existing Coder infrastructure, headless agent workflows triggered from CI, and AI adoption observability. See the message house's [Problem Areas](./message-house.md#problem-areas) and [Deploy AI Coding Agents](../../use-cases/deploy-ai-coding-agents.md).

### Good-fit signals

- Security or compliance blocks cloud-hosted agents because code, orchestration, or inference would leave the perimeter
- An existing Coder customer whose developers are asking for agents
- The organization wants to switch or mix model providers, or run self-hosted open-weight models
- Shadow AI tools are appearing with API keys spread across laptops and workspaces
- Teams want background agents triggered from CI, GitHub, or other internal systems
- Leadership wants usage, cost, and outcome data for AI coding spend
- The organization needs a governed, standardized way to distribute agents to engineering-adjacent knowledge workers or citizen developers

### Poor fit or another approach

- **Developers are committed to a specific third-party harness.** Run Claude Code or Codex inside Coder workspaces with [AI Governance](../coder-ai-governance/message-house.md), or connect Cursor or Claude Code cloud agents through [Agent Relay](../coder-agent-relay/playbook.md).
- **The need is in-editor assistance.** AI IDEs cover autocomplete and in-editor chat, and they complement Coder Agents rather than replace it.
- **The organization is comfortable with SaaS agents and doesn't want to operate infrastructure.** A hosted agent may be simpler.

### Discovery questions

- **Current tools.** Which agents and AI tools are developers using today, and how are they governed?
- **Boundary.** Must orchestration and inference stay in the perimeter, or only execution?
- **Models.** Which LLM providers are approved, and is a self-hosted model required?
- **Coder today.** Is the organization already running Coder, and are its templates clearly named and described?
- **Network.** Can agent workspaces be restricted to the control plane and git provider?
- **Automation.** Which workflows, such as CI failures or code review, should trigger agents without a developer?
- **Scale and spend.** How many concurrent agents are expected, how many Agent Hours will background automation need, and who owns AI spend and reporting?

---

## 6. Audiences

See the message house's [Buyer Personas](./message-house.md#buyer-personas) for how each persona applies to Coder Agents.

| Role | Cares most about | Useful framing |
|---|---|---|
| [CISO and security leaders](../../audiences/ciso.md) | Keeping code, credentials, and agent activity inside the perimeter, with identity-attributed audit | "Coding agents with no API keys in workspaces and every action tied to a named user." |
| [Platform engineers](../../audiences/platform-engineer.md) | Distributing one agent experience without per-workspace installs, key distribution, or configuration drift | "Enable agents once, using the templates and RBAC you already manage." |
| [Developers](../../audiences/developer.md) | A fast, modern agent experience with the models they prefer, and background work they can review later | "Hand off the task, keep working, and review the pull request when it's ready." |
| [CTO](../../audiences/cto.md) and [CIO](../../audiences/cio.md) | Scaling AI productivity without lock-in, shadow AI, or unmeasured spend | "Throughput that scales with infrastructure, on models you choose." |

---

## 7. Alternatives and Related Products

See the message house's [Market Landscape](./message-house.md#market-landscape) and the FAQ's competitive sections for the full narrative.

- **Cursor Cloud Agents.** Orchestration and inference run in Cursor's cloud, with optional self-hosted execution. Coder Agents keeps all three in the customer's deployment. See [Coder and Cursor](../../market-landscape/cursor.md).
- **Claude Code and Codex.** Single-provider agents that run in a terminal or the provider's cloud. They can still run inside Coder workspaces with AI Governance. See [Coder and Claude Code](../../market-landscape/claude-code.md) and [Coder and Codex](../../market-landscape/codex.md).
- **Devin.** The reasoning layer runs in Cognition's cloud, including in the VPC option. See [Coder and Devin](../../market-landscape/devin.md).
- **GitHub Copilot agents.** Governance, model routing, and execution run on GitHub and Microsoft infrastructure. See [Coder and GitHub Codespaces](../../market-landscape/github-codespaces.md) and the FAQ's [VS Code Agents and GitHub Copilot](./faq.md#16-competitive-landscape-vs-code-agents-and-github-copilot) section.
- **Agentic IDEs.** Windsurf, Zed, Kiro, and similar editors complement Coder Agents as the place developers review and refine work.
- **Coder Agent Relay.** For organizations that want a specific cloud agent's experience and accept cloud orchestration and inference. Customers can use both. See the [Agent Relay playbook](../coder-agent-relay/playbook.md).

---

## 8. Common Questions

For common questions about architecture, security, pricing, licensing, and competitors, see the [Coder Agents FAQ](./faq.md).

---

## 9. Evaluation and Demo

### Evaluation stages

| Stage | Goals | Typically involved |
|---|---|---|
| Initial exploration | Understand the control-plane architecture, model options, and data boundary | Platform and security leads |
| Technical evaluation | Configure a provider and model, describe templates, and run real tasks and API triggers | Platform engineers, developers |
| Security and architecture review | Network policy for agent templates, identity and permissions, AI Gateway audit, and data sent to the LLM provider | Security, compliance |
| Production planning | Concurrency and Agent Time, spend limits, template strategy, and rollout to more teams | Platform engineering, engineering leadership |

### Pilot setup

- A Coder deployment running a current release, with at least one clearly described template
- Credentials for at least one approved LLM provider, reachable from the control plane
- A small group of developers with realistic tasks in real repositories
- At least one automated workflow, such as a CI-triggered fix or pull request review
- Named stakeholders from platform, security, and the developer group, with agreed success criteria and timeline

### Success criteria

- Developers complete real tasks and merge agent-produced pull requests
- The agent selects the right template without developer input
- Agent workspaces run with the intended network restrictions and no LLM credentials
- Every agent action is attributed to the prompting user in AI Gateway
- An API-triggered workflow runs end to end without a developer present
- Platform teams can see usage and cost by user or group

### Demo flow

1. Show the admin view, with multiple model providers configured and an organization-wide system prompt.
2. Ask a question that needs no workspace, and show the instant response.
3. Assign a coding task, and show the agent selecting a template, provisioning a workspace, and spawning sub-agents.
4. Show the resulting pull request, then open the workspace in an IDE, such as VS Code or Cursor, to review the agent's work.
5. Show the same session in AI Gateway, with prompts, tool calls, and token usage attributed to the user.

Tailor emphasis to the audiences in [section 6](#6-audiences), and use a template that provisions quickly.

---

## 10. Commercial, Partners, and Contacts

### Packaging and prerequisites

- Coder Agents is part of the Coder install, not a separate product or deployment
- Every tier can run Coder Agents, including agents triggered through the API
- Community and Premium support up to five concurrently active agents, with more agents queued
- AI Premium removes the concurrency cap and includes a deployment-wide allotment of Agent Hours that customers size and buy based on expected usage
- AI Premium deployments report usage to Coder over outbound HTTPS, or, if air-gapped, through a manually exported usage bundle or another usage-based agreement
- An API key for at least one supported LLM provider, or a self-hosted model endpoint

See [Packaging](../../company/packaging.md) and [coder.com/pricing](https://coder.com/pricing) for current tiers and prices.

### Evaluation access

Self-serve. Coder Agents is available in every Coder deployment, including Community and proof-of-concept deployments, without a separate install. For evaluations that need more than five concurrent agents, work with the Coder account team on AI Premium and Agent Hours sizing.

### Partners

Coder Agents drives compute and inference consumption for cloud and model providers such as AWS, Azure, Google Cloud, and Anthropic. See the message house's [Partner Narrative](./message-house.md#partner-narrative).

### Contacts

| Topic | Contact / Team |
|---|---|
| Messaging and positioning | Matt Vollmer, Product Marketing |
| Customer support | Coder Support |
| Everything else | Your [Coder account team](https://coder.com/contact) or [sales@coder.com](mailto:sales@coder.com) |

---

## 11. Resources

- [Coder Agents docs](https://coder.com/docs/ai-coder/agents), including [Getting Started](https://coder.com/docs/ai-coder/agents/getting-started), [Architecture](https://coder.com/docs/ai-coder/agents/architecture), [Platform Controls](https://coder.com/docs/ai-coder/agents/platform-controls), and [Licensing and Usage](https://coder.com/docs/ai-coder/agents/licensing-usage)
- [Coder Agents message house](./message-house.md) and [FAQ](./faq.md)
- [Deploy AI Coding Agents](../../use-cases/deploy-ai-coding-agents.md)
- [Coder Agents GA announcement](https://coder.com/blog/coder-agents-ga)
- Market landscape pages for [Cursor](../../market-landscape/cursor.md), [Claude Code](../../market-landscape/claude-code.md), [Codex](../../market-landscape/codex.md), [Devin](../../market-landscape/devin.md), and [GitHub Codespaces](../../market-landscape/github-codespaces.md)

Roughly 70% of Coder Agents usage so far has been triggered through the API, which indicates customers are using it for headless background orchestration. No public customer examples are available yet. When added, refer to customers by anonymized type unless they have publicly agreed to be named.
