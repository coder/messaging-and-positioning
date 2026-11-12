# Why Coder

This describes the fundamental reasons enterprises choose Coder, independent of any single product or integration announcement, and why Coder doesn't face the kind of direct, feature-for-feature competition most vendors do. Use this as the foundation when introducing a new capability. Lead with why enterprises choose Coder in the first place, then show how the new capability is an expression of that, not a break from it.

## The five fundamentals

At its core, Coder moves development environments off individual laptops and onto centralized, self-hosted infrastructure the enterprise controls. What Coder has done for human developers for years extends naturally to AI agents. Five fundamentals describe why enterprises make that move, and they expand on the [message house](./message-house.md)'s Control, Choice, and Consistency pillars into the specific reasons that show up in a buying decision.

- **Self-hosted.** Coder runs on infrastructure the customer controls, including environments with very strict network and data requirements, up to fully air-gapped. This is the clearest expression of Control.
- **Neutral.** Coder doesn't force a specific cloud, model, or developer tool. That flexibility reduces lock-in risk, letting an enterprise make a long-term infrastructure bet on Coder without making the same bet on any individual cloud, model, or tool. This is Choice.
- **Standardized.** Instead of every developer managing a bespoke environment on a laptop, platform teams provision reproducible environments consistently across teams, defined as code. This is Consistency.
- **Connected.** Those environments securely reach the private code, networks, tools, and internal systems developers and agents need to do their jobs, resources that are often unavailable externally.
- **Governed.** Identity, access, policy, isolation, auditability, and lifecycle controls are centralized instead of scattered across individual machines. Alongside Self-hosted, this is the other clear expression of Control.

Together, these are the fundamental Coder story, giving developers and agents the environments they need, while giving the enterprise control over where and how that work happens.

## Where Coder competes and complements

Coder's relationships with other vendors depend on the product and workload. A vendor can supply models or tools used with Coder while also competing for a particular agent or infrastructure decision.

**Legacy CDEs are collapsing, not competing.** Several major cloud development environment products have been deprecated, discontinued, or closed to new customers in recent years, and the remaining SaaS-first options are either locked to a single cloud or pivoting away from their CDE roots. See the [Coder Workspaces message house](../products/coder-workspaces/message-house.md) for the specifics.

**Specialized products can overlap without replacing the whole platform.** AI gateways, agentic IDEs, sandboxing products, and agent platforms address different parts of development infrastructure. Self-hosted Claude Managed Agents overlaps with Coder Agents for unattended coding workflows and supplies its own harness, console, and sandbox deployment tooling. Customers still operate that infrastructure. Coder's distinction is supported model and agent choice, development-workspace management, and controls across supported workflows, not that Anthropic supplies no environments. Teams can choose Managed Agents for an automation workload while retaining Coder Workspaces for developers; a direct Managed Agents execution integration is not documented as supported ([Coder and Claude Managed Agents](../market-landscape/claude-managed-agents.md)). See each product's Market Landscape or Competitive Position section for its specific overlap.

**Organizations already running a constrained SaaS CDE are often the best-informed prospects, not the hardest to win.** A team that has spent real time on a single-cloud, opinionated CDE has already felt firsthand what it costs to lose choice, control, and consistency. That experience tends to accelerate a conversation about Coder rather than slow it down.

**Building in-house is one alternative, not the only one.** Organizations can build and maintain development infrastructure themselves, assemble specialist products, or adopt a platform such as Coder. Compare the required capabilities and ongoing operating responsibilities rather than assuming that every narrower product is either a complete substitute or irrelevant.

**What makes that hard to replicate is the same thing that makes Coder valuable, adaptability without a single fixed configuration.** Coder runs as adaptable, self-hosted infrastructure across radically different customer environments and constraints. Unlike a hosted SaaS product that runs one configuration for every customer, no two Coder deployments look alike, which is precisely what a self-hosted, cloud-agnostic product has to be able to do.

## Related

- [Coder Message House](./message-house.md) for the Control, Choice, and Consistency pillars these fundamentals expand on.
- [Customer Journey](./customer-journey.md) for how these fundamentals carry through Migrate, Modernize, and Multiply.
- [Packaging](./packaging.md) for how new capability typically extends existing tiers rather than introducing new competition to track.
