# Customer Journey

Organizations don't adopt AI development infrastructure all at once. They move through recognizable stages, and Coder's product line maps to that progression rather than existing as unrelated point products. This document describes that arc, called Migrate, Modernize, and Multiply, and how it connects to the product line and buyer personas described elsewhere in this repository.

## Migrate

Migrate is the shift from local development on developer laptops to centrally managed infrastructure. Development environments and source code move off laptops and onto infrastructure the organization controls, addressing the environment inconsistency, local compute limits, and lack of visibility that come with unmanaged, laptop-based development.

This stage maps to [Coder Workspaces](../products/coder-workspaces/message-house.md).

## Modernize

Modernize is the addition of AI governance once development is centralized. With development environments already consolidated, organizations gain a natural point to add model access control, auditing, and policy enforcement over how AI agents and developers use AI in those environments.

Migrate and Modernize are frequently adopted together rather than as two separate purchase decisions, since most organizations arrive at both needs around the same time. They want to move off laptops, and they want AI governed once they do. This is why Coder Premium bundles Coder Workspaces and AI Governance into a single offering rather than selling them as separate products.

This stage maps to [Coder Workspaces](../products/coder-workspaces/message-house.md) and [Coder AI Governance](../products/coder-ai-governance/message-house.md).

## Multiply

Multiply is scaling development output with coding agents, including agents that operate with a human in the loop and, increasingly, headless or agent-driven execution that runs without one. This is the leading edge of the journey, depending on the governed, centralized foundation established in Migrate and Modernize, and it's where organizations begin treating agent capacity as infrastructure to provision rather than a tool an individual developer runs locally.

This stage maps to [Coder Agents](../products/coder-agents/message-house.md) and [Coder Agent Relay](../products/coder-agent-relay/message-house.md).

## This isn't strictly linear

Not every organization moves through all three stages, and few move through them in a fixed order or timeline. Most of the market is still in Migrate and Modernize, and Multiply represents where the market is heading rather than where most organizations already are. Treat this as a framework for understanding how Coder's products relate to each other and to a customer's maturity, not a required sequence every customer must complete.

## Related personas

The [buyer personas](../audiences/personas/overview.md) described elsewhere in this repository tend to show up differently at each stage. Caring Providers, motivated by giving their users a great experience, are frequently the ones who first adopt Coder through open source and drive early validation, most often during Migrate. Opportunists and Protectionists, motivated by cost and risk respectively, more often hold the budget and final decision authority needed to move an organization through Modernize and into Multiply. A durable business case for any stage usually needs to speak to whichever of these two motivations is present, not just the technical one.
