# Coder and OpenCode

| Field | Value |
|---|---|
| Date generated | 2026-09-28 |
| Last reviewed | 2026-09-28 |
| Category | Complementary |

*OpenCode is built by Anomaly, the team behind SST, and was previously hosted at `github.com/sst/opencode` ([Developers Digest](https://www.developersdigest.tech/blog/opencode-developer-guide-2026)). It now lives at [github.com/anomalyco/opencode](https://github.com/anomalyco). A separate, earlier Go project at [github.com/opencode-ai/opencode](https://github.com/opencode-ai/opencode) shares the name. This page covers the Anomaly project.*

## One-Line Positioning

OpenCode is an open-source, model-agnostic coding agent, and Coder provides the self-hosted workspaces, AI Gateway, and Agent Firewall that let an organization run OpenCode, alongside any other agent, on infrastructure it controls.

## Strategic Themes and Patterns

- **Relationship.** Complementary. OpenCode is agent software that developers install and run in a terminal, desktop app, or IDE ([OpenCode docs](https://opencode.ai/docs/)), and it does not provision development infrastructure. Coder publishes an OpenCode module for workspace templates ([Coder Registry](https://registry.coder.com/modules)) and documents how to route OpenCode through AI Gateway ([Coder docs](https://coder.com/docs/ai-coder/ai-gateway/clients/opencode)).
- **Where the two overlap.** The main overlap is at the agent layer. Coder Agents is a native coding agent whose loop runs in the Coder control plane ([Coder docs](https://coder.com/docs/ai-coder)), so an organization can choose OpenCode, Coder Agents, or both. A narrower overlap is at the gateway layer. OpenCode Console is an optional hosted service with an LLM gateway for an organization's own provider keys, usage tracking, budget controls, and team-wide policies ([OpenCode Console](https://opencode.ai/v2/docs/console/)). OpenCode Enterprise adds a central config with SSO and an internal AI gateway ([OpenCode Enterprise](https://opencode.ai/docs/enterprise/)). Neither supplies environments, network controls, or execution infrastructure.
- **Choice, Control, Consistency.** Not a tradeoff here, since the products aren't substitutes. Both favor Choice. OpenCode connects to 75+ providers and local models ([Developers Digest](https://www.developersdigest.tech/blog/opencode-developer-guide-2026)), and Coder doesn't force a specific cloud, model, or developer tool ([Why Coder](../company/why-coder.md)).
- **How they work together.** OpenCode runs inside a Terraform-defined Coder workspace instead of on a laptop. Its model traffic routes through Coder AI Gateway for audit and cost controls, and Agent Firewall restricts which domains the OpenCode process can reach. OpenCode supplies the agent experience. Coder supplies the environment, identity, network boundary, and audit trail around it.

## Coder's Strengths Here

- **A governed place to run the agent.** Coder workspaces are defined with Terraform and connected through a secure WireGuard tunnel on self-hosted infrastructure ([coder/coder](https://github.com/coder/coder)), so OpenCode runs with the same tools and access controls as every other workspace instead of with a developer's laptop permissions.
- **Packaged OpenCode integration.** The Coder Registry lists an OpenCode module for templates ([Coder Registry](https://registry.coder.com/modules)). It builds on Coder's AgentAPI module to expose OpenCode as a web app and an optional CLI app in the workspace ([module source](https://github.com/coder/registry/blob/main/registry/coder-labs/modules/opencode/main.tf)).
- **Centralized LLM audit across every agent.** AI Gateway provides audit trails of prompts, token usage, and tool invocations ([Coder docs](https://coder.com/docs/ai-coder/ai-governance)). OpenCode connects by setting custom base URLs for its Anthropic and OpenAI providers ([Coder docs](https://coder.com/docs/ai-coder/ai-gateway/clients/opencode)). The same gateway covers Claude Code, Codex, Cline, and other clients ([Coder docs](https://coder.com/docs/ai-coder/ai-gateway/clients)).
- **Spend enforcement.** AI Gateway cost controls stop a user's gateway-routed requests once spend reaches a budget and report approximate spend per user and group ([Coder docs](https://coder.com/docs/ai-coder/ai-gateway/cost-controls)).
- **Network enforcement outside the agent's own config.** Agent Firewall is a process-level firewall that works with any terminal-based agent, blocks domains and HTTP verbs, and streams audit logs to the control plane ([Coder docs](https://coder.com/docs/ai-coder/agent-boundaries)).
- **Air-gapped operation.** Coder license keys validate locally with no outbound connection, so licenses work in air-gapped deployments ([Coder docs](https://coder.com/docs/admin/licensing)).

## OpenCode Overview

- **What it is.** An open source AI coding agent available as a terminal interface, desktop app, or IDE extension ([OpenCode docs](https://opencode.ai/docs/)). It is MIT licensed ([Fastino](https://fastino.ai/blog/the-complete-guide-to-opencode-open-source-ai-coding-agents), secondary).
- **Adoption.** OpenCode's homepage reports over 208,000 GitHub stars, 950 contributors, and over 16M monthly developers ([opencode.ai](https://opencode.ai/)). These are company-reported. Earlier secondary sources cite lower figures from earlier in 2026.
- **Architecture.** A TypeScript and Bun server talks to model providers, runs tools, and manages state. The TUI, desktop app, IDE extension, and web client all connect to that server, and `opencode serve` runs it headless ([DataCamp](https://www.datacamp.com/blog/what-is-opencode), secondary). OpenCode states it does not store code or context data, and processing happens locally or through direct calls to the user's AI provider ([OpenCode Enterprise](https://opencode.ai/docs/enterprise/)).
- **Model access.** Users bring their own keys from 75+ providers or local models ([Developers Digest](https://www.developersdigest.tech/blog/opencode-developer-guide-2026), secondary). OpenCode also offers two optional hosted model services. Zen is a curated, pay-as-you-go catalog ([Zen docs](https://opencode.ai/docs/zen/)), and Go is a subscription focused on open models ([OpenCode Go](https://opencode.ai/go)). Zen models are hosted in the US ([OpenCode Zen](https://opencode.ai/zen)).
- **Team service.** OpenCode Console is an optional hosted service that gives teams an LLM gateway for their own provider keys, member budgets, and policies that apply to every connected OpenCode v2 client ([OpenCode Console](https://opencode.ai/v2/docs/console/)). For bring-your-own-key connections, Console stores the provider credential and forwards requests through a gateway URL at opencode.ai ([Console BYOK](https://opencode.ai/v2/docs/console/byok/)).
- **Agent controls.** Per-tool permissions can be set to allow, ask, or deny, with wildcard patterns ([OpenCode permissions](https://opencode.ai/docs/permissions/)).
- **Automation.** A GitHub integration runs OpenCode in GitHub Actions, triggered by `/opencode` or `/oc` comments, PR events, issues, or schedules ([OpenCode GitHub docs](https://opencode.ai/docs/github/)).
- **Target customer.** Individual developers first, with OpenCode Enterprise for organizations that want code and data to stay inside their infrastructure ([OpenCode Enterprise](https://opencode.ai/docs/enterprise/)).
- **Deployment model.** Client software installed where developers work. OpenCode Enterprise adds a single central config for the organization that integrates with SSO and restricts users to an internal AI gateway ([OpenCode Enterprise](https://opencode.ai/docs/enterprise/)).

## Coder Overview for This Comparison

- **Coder Workspaces.** Self-hosted development environments defined with Terraform ([coder/coder](https://github.com/coder/coder)). This is where OpenCode runs when paired with Coder.
- **OpenCode registry module.** Adds OpenCode to a template in a few lines of Terraform ([Coder Registry](https://registry.coder.com/modules)). The module accepts an OpenCode `auth.json` for non-interactive authentication ([module source](https://github.com/coder/registry/blob/main/registry/coder-labs/modules/opencode/main.tf)).
- **AI Gateway.** Coder's LLM gateway, with a documented OpenCode client configuration ([Coder docs](https://coder.com/docs/ai-coder/ai-gateway/clients/opencode)).
- **Agent Firewall.** Process-level network policy and audit for agents in workspaces, previously named Agent Boundaries ([Coder docs](https://coder.com/docs/ai-coder/agent-firewall)).
- **Coder Agents.** A native agent whose loop runs in the control plane, so workspaces can be fully network isolated ([Coder docs](https://coder.com/docs/ai-coder)), with no API keys in workspaces ([coder/coder](https://github.com/coder/coder)). This is the Coder product that overlaps with OpenCode at the agent layer. See the [Coder Agents message house](../products/coder-agents/message-house.md).

## Known Limitations in OpenCode's Approach

- **Permissions default to open (as of 2026-09-28).** By default, all tools are enabled and don't need permission to run ([OpenCode tools](https://opencode.ai/docs/tools/)). Most permissions default to allow, while `doom_loop` and `external_directory` default to ask ([OpenCode permissions](https://opencode.ai/docs/permissions/)). These controls apply to the agent's own tool calls. Coder's guidance is that network-level boundaries are firmer than restricting individual commands, since an agent can reach the same result through other commands ([Coder docs](https://coder.com/docs/ai-coder/agents/platform-controls/template-optimization)). Running OpenCode in a network-restricted workspace or under Agent Firewall adds that layer.
- **Share pages are hosted by OpenCode (as of 2026-09-28).** If a user enables `/share`, the conversation and associated data are sent to opencode.ai and cached on a CDN edge network. OpenCode recommends disabling it for trials, and self-hosting share pages is on its roadmap ([OpenCode Enterprise](https://opencode.ai/docs/enterprise/)). In the GitHub integration, session sharing defaults to true for public repositories ([OpenCode GitHub docs](https://opencode.ai/docs/github/)).
- **Credentials live in the workspace when OpenCode runs there (as of 2026-09-28).** Coder's OpenCode setup for AI Gateway places a Coder API token in the OpenCode config and provider keys in `auth.json` ([Coder docs](https://coder.com/docs/ai-coder/ai-gateway/clients/opencode)). By contrast, Coder Agents keeps LLM credentials in the control plane ([coder/coder](https://github.com/coder/coder)).
- **Documented AI Gateway coverage (as of 2026-09-28).** Coder's OpenCode client guide covers the Anthropic and OpenAI providers ([Coder docs](https://coder.com/docs/ai-coder/ai-gateway/clients/opencode)). Other OpenCode providers aren't covered in that guide.

## Common Questions

- **Is OpenCode a Coder competitor?** Mostly no. OpenCode is agent software, and Coder is the infrastructure it runs on, with a registry module and AI Gateway guide for OpenCode ([Coder Registry](https://registry.coder.com/modules), [Coder docs](https://coder.com/docs/ai-coder/ai-gateway/clients/opencode)). The main overlap is with Coder Agents, which is an alternative agent, and OpenCode Console overlaps with AI Gateway in part ([OpenCode Console](https://opencode.ai/v2/docs/console/)).
- **Can we run OpenCode in Coder today?** Yes. Add the OpenCode module to a workspace template ([Coder Registry](https://registry.coder.com/modules)). Coder's README lists OpenCode alongside Claude Code and Codex as agents that run isolated in Coder workspaces ([coder/coder](https://github.com/coder/coder)).
- **Can Coder audit what OpenCode sends to models?** Yes, for providers routed through AI Gateway. Point OpenCode's Anthropic and OpenAI base URLs at AI Gateway ([Coder docs](https://coder.com/docs/ai-coder/ai-gateway/clients/opencode)), which records prompts, token usage, and tool invocations ([Coder docs](https://coder.com/docs/ai-coder/ai-governance)).
- **How is OpenCode Enterprise different from Coder?** OpenCode Enterprise centrally configures the OpenCode agent with SSO and an internal AI gateway ([OpenCode Enterprise](https://opencode.ai/docs/enterprise/)). Coder provides the environments, network enforcement, and LLM gateway for any agent. Because OpenCode accepts custom provider base URLs, an OpenCode Enterprise central config could likely target Coder AI Gateway as the internal gateway. This is an inference, and neither company documents it.
- **Does OpenCode Console or Zen replace AI Gateway?** They overlap in part but don't replace it for self-hosted or cross-agent governance. Zen is a hosted model catalog that OpenCode serves from the US ([OpenCode Zen](https://opencode.ai/zen)). Console adds a gateway for the team's own provider keys, member budgets, and policies, and it runs at opencode.ai rather than on the organization's infrastructure ([Console BYOK](https://opencode.ai/v2/docs/console/byok/), [Console budgets](https://opencode.ai/v2/docs/console/budgets/)). AI Gateway is a self-hosted proxy that audits prompts, token usage, and tool invocations across Claude Code, Codex, OpenCode, and other clients ([Coder docs](https://coder.com/docs/ai-coder/ai-governance), [Coder docs](https://coder.com/docs/ai-coder/ai-gateway/clients)).
- **Should we standardize on OpenCode or Coder Agents?** It depends on requirements, and both can coexist. Coder Agents keeps credentials and the agent loop in the control plane, so workspaces need no agent software or LLM access ([Coder docs](https://coder.com/docs/ai-coder)). OpenCode offers terminal, desktop, and IDE clients and a large open-source community ([opencode.ai](https://opencode.ai/)). Both are model-agnostic.

## Pricing and Packaging

- **OpenCode client.** Free and open source. Users pay only for model usage ([Developers Digest](https://www.developersdigest.tech/blog/opencode-developer-guide-2026), secondary).
- **OpenCode Zen.** Pay-as-you-go per-token pricing. Credit card fees of 4.4% + $0.30 per transaction are passed through at cost ([Zen docs](https://opencode.ai/docs/zen/)).
- **OpenCode Go.** $10/month, with Go Plus at $40/month for higher limits ([OpenCode Go](https://opencode.ai/go)).
- **OpenCode Enterprise.** Per-seat pricing through sales. OpenCode does not charge for tokens when the organization uses its own LLM gateway ([OpenCode Enterprise](https://opencode.ai/docs/enterprise/)).
- **Coder.** A free Community edition and a Premium edition priced through sales ([G2](https://www.g2.com/products/coder/pricing), secondary). See `coder.com/pricing` for current tiers and [Packaging](../company/packaging.md) for the narrative. Community deployments do not include AI Gateway or Agent Firewall; AI Governance is included with a Premium license rather than sold as a separate add-on ([AI Governance message house](../products/coder-ai-governance/message-house.md), [Packaging](../company/packaging.md)).

## Sources

- **[OpenCode docs intro](https://opencode.ai/docs/).** Product definition and surfaces. Primary. Accessed 2026-09-28.
- **[opencode.ai homepage](https://opencode.ai/).** Company-reported adoption figures. Primary. Accessed 2026-09-28.
- **[OpenCode Enterprise docs](https://opencode.ai/docs/enterprise/).** Central config, SSO, internal gateway, data handling, share pages, per-seat pricing. Primary. Accessed 2026-09-28.
- **[OpenCode Zen docs](https://opencode.ai/docs/zen/) and [Zen page](https://opencode.ai/zen).** Zen model service, US hosting, pricing model. Primary. Accessed 2026-09-28.
- **[OpenCode Go](https://opencode.ai/go).** Go and Go Plus pricing. Primary. Accessed 2026-09-28.
- **[OpenCode Console docs](https://opencode.ai/v2/docs/console/), [BYOK](https://opencode.ai/v2/docs/console/byok/), and [Budgets](https://opencode.ai/v2/docs/console/budgets/).** Hosted team gateway, credential storage, member budgets, team-wide policies. Primary. Accessed 2026-09-28.
- **[OpenCode permissions](https://opencode.ai/docs/permissions/) and [tools](https://opencode.ai/docs/tools/).** Permission model and defaults. Primary. Accessed 2026-09-28.
- **[OpenCode GitHub docs](https://opencode.ai/docs/github/).** GitHub Actions integration and share default. Primary. Accessed 2026-09-28.
- **[Anomaly GitHub org](https://github.com/anomalyco).** Current repository location. Primary. Accessed 2026-09-28.
- **[DataCamp, What Is OpenCode](https://www.datacamp.com/blog/what-is-opencode).** Client/server architecture. Secondary. Accessed 2026-09-28.
- **[Developers Digest OpenCode guide](https://www.developersdigest.tech/blog/opencode-developer-guide-2026).** Provider count, prior `sst/opencode` location, pricing model. Secondary. Accessed 2026-09-28.
- **[Fastino OpenCode guide](https://fastino.ai/blog/the-complete-guide-to-opencode-open-source-ai-coding-agents).** MIT license. Secondary. Accessed 2026-09-28.
- **[Coder docs, AI Gateway OpenCode client](https://coder.com/docs/ai-coder/ai-gateway/clients/opencode).** OpenCode configuration for AI Gateway. Primary. Accessed 2026-09-28.
- **[Coder docs, AI Gateway clients](https://coder.com/docs/ai-coder/ai-gateway/clients).** Supported clients. Primary. Accessed 2026-09-28.
- **[Coder docs, AI Governance](https://coder.com/docs/ai-coder/ai-governance).** AI Gateway audit, Community limits. Primary. Accessed 2026-09-28.
- **[Coder docs, AI Gateway cost controls](https://coder.com/docs/ai-coder/ai-gateway/cost-controls).** Budgets and Premium packaging. Primary. Accessed 2026-09-28.
- **[Coder docs, Agent Boundaries](https://coder.com/docs/ai-coder/agent-boundaries) and [Agent Firewall](https://coder.com/docs/ai-coder/agent-firewall).** Process-level network enforcement and rename. Primary. Accessed 2026-09-28.
- **[Coder docs, Run AI Coding Agents](https://coder.com/docs/ai-coder).** Coder Agents architecture. Primary. Accessed 2026-09-28.
- **[Coder docs, Template Optimization](https://coder.com/docs/ai-coder/agents/platform-controls/template-optimization).** Network-level versus command-level boundaries. Primary. Accessed 2026-09-28.
- **[Coder docs, Licensing](https://coder.com/docs/admin/licensing).** Offline license validation. Primary. Accessed 2026-09-28.
- **[coder/coder README](https://github.com/coder/coder).** Platform summary, OpenCode support, no API keys in workspaces. Primary. Accessed 2026-09-28.
- **[Coder Registry modules](https://registry.coder.com/modules) and [OpenCode module source](https://github.com/coder/registry/blob/main/registry/coder-labs/modules/opencode/main.tf).** OpenCode module. Primary. Accessed 2026-09-28.
- **[G2, Coder pricing](https://www.g2.com/products/coder/pricing).** Community and Premium tiers. Secondary. Accessed 2026-09-28.
- **[Coder AI Governance message house](../products/coder-ai-governance/message-house.md) and [Packaging](../company/packaging.md).** AI Governance included with Premium, not sold separately. Primary (this repository). Accessed 2026-09-28.
