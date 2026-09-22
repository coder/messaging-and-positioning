# Packaging

This describes the shape and reasoning behind Coder's packaging, not a feature-by-feature comparison or a price list. For current tier names, included features, and pricing, always use [coder.com/pricing](https://coder.com/pricing) rather than this document, since packaging and pricing change independently of the narrative behind them.

## The three tiers

- **Community** (free) is for hobbyists and small teams joining Coder's open-source community. It includes unlimited self-hosted workspaces, environments defined as code, and support for running AI coding agents inside ephemeral workspaces from day one, with a capped number of Coder Agents able to run concurrently.
- **Premium** (per-user, annual) is for enterprises that need world-class security, scalability, and developer experience. It includes everything in Community, plus AI Governance (AI Gateway and Agent Firewall), high availability, workspace proxies, multi-organization access control, and SLA-backed support.
- **AI Premium** (custom pricing) is for enterprises scaling AI-native transformation on their own infrastructure. It includes everything in Premium, plus removing the concurrency cap on Coder Agents, headless agent execution triggered via API, and support for connecting the model providers the organization already uses.

## The packaging philosophy

A few principles guide how Coder packages new capability, rather than treating each announcement as a new product decision.

**New capability usually extends an existing tier rather than creating a new SKU.** Coder Agent Relay is a good example. It's a new integration, not a fourth tier or a separate purchase. When a new capability's core value is still choice, control, and consistency, the same ethos behind the [message house](./message-house.md)'s Why Coder pillars, it tends to show up as a feature or deployment configuration inside Community, Premium, or AI Premium rather than as its own product line.

**AI Governance is included in Premium, not sold separately.** This reflects that Migrate and Modernize are usually adopted together, as described in the [Customer Journey](./customer-journey.md). An organization moving to Premium for workspace security and scale already needs AI governed once agents and developers start using it, so there's no reason to force a second purchase decision.

**Coder Agents is metered by concurrency and usage, not gated behind a single feature flag.** Even Community and Premium customers can run Coder Agents today, up to a limited number running concurrently. AI Premium removes that concurrency cap and introduces usage-based agent runtime consumption, reflecting that this tier is for organizations that have moved into the Multiply stage of the [customer journey](./customer-journey.md) and are scaling agent usage as core infrastructure rather than experimenting with it.

**Coder Agent Relay currently doesn't introduce its own billing.** As of this writing, Agent Relay usage is included within Premium rather than charged separately, since its primary effect is to drive additional Coder Workspaces usage rather than add a capability that needs its own SKU. This is an area of active exploration, so confirm current thinking with Product Marketing before stating anything more specific.

## Related

- [Customer Journey](./customer-journey.md) for how these tiers map to Migrate, Modernize, and Multiply.
- [Coder Message House](./message-house.md) for the Choice, Control, and Consistency pillars this packaging reflects.
