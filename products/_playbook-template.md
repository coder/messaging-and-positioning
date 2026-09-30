# [Product Name] Playbook

> Template for product playbooks. Copy this file to `products/<product>/playbook.md`, replace the bracketed guidance in each section with real content, and delete this note. A playbook helps people support organizations evaluating a product. It should link to the product's message house, FAQs, and other existing pages rather than restate them, and only add what those pages don't cover. This repository is public, so everything in a playbook is public the moment it merges. Include only information that is safe to share publicly, and refer to customers by anonymized type (for example, "a large financial institution") unless they have publicly agreed to be named. Where a section can't be filled accurately yet, mark it `TBD` with the open question rather than inventing a claim.

> A shared reference for understanding where [Product Name] fits, how it works, and how to support organizations evaluating or adopting it.

For positioning, messaging, and value propositions, see the [[Product Name] message house](./message-house.md). For detailed product questions, see [link the product FAQ, if one exists, or delete this sentence].

---

## 1. Quick Reference

| | |
|---|---|
| **The product** | [One-sentence description.] |
| **Best fit** | [One-sentence description of the ideal organization.] |
| **Common signal** | "[Phrase or requirement commonly heard.]" |
| **Key question** | "[Question that quickly clarifies need.]" |
| **Core value** | [Short value statement.] |
| **Important limitation** | [Most important boundary or qualification.] |
| **Status** | [Preview / Early access / Beta / GA.] |
| **Journey stage** | [Migrate, Modernize, or Multiply, linking to the [customer journey](../../company/customer-journey.md).] |
| **Next step** | [Recommended next action for someone evaluating the product.] |

---

## 2. Overview

[Two or three short paragraphs covering what the product is, the problem it addresses, and why it matters now. Link to the message house for the full narrative instead of repeating it.]

---

## 3. How It Works

### Architecture summary

[Explain the architecture at a high level.]

### Components and responsibilities

| Component | Responsibility |
|---|---|
| [Component] | [Responsibility] |
| [Component] | [Responsibility] |

### Typical workflow

If the product has more than one primary user, such as developers and template admins, include one short workflow for each.

1. **[Step].** [Description.]
2. **[Step].** [Description.]
3. **[Step].** [Description.]

### Deployment model

[Describe where different components run and who operates them.]

### Data and trust boundaries

[Explain what data crosses boundaries, what remains within customer-controlled infrastructure, and any important architectural nuances.]

---

## 4. Boundaries and Terminology

Link to wherever the product's limits are already documented, such as a message house "Known Limitations" or "Scope and Tradeoffs" section, or an FAQ's "what it is and isn't" section.

### What the product does not do

- [Unsupported capability or common misconception]
- [Unsupported capability or common misconception]

### Recommended terminology

| Preferred | Avoid | Why |
|---|---|---|
| "[Approved phrasing]" | "[Potentially misleading phrasing]" | [Reason] |

---

## 5. Fit

Link to the message house's target market section for the full ideal customer profile.

### Use cases

[One line listing the product's primary use cases, linking to the matching pages in [`use-cases/`](../../use-cases/) and the message house's use case section rather than restating them.]

### Good-fit signals

- [Organizational characteristic, environment, or observable signal]
- [Organizational characteristic, environment, or observable signal]

### Poor fit or another approach

- **[Situation].** [Why, and what may fit better.]
- **[Situation].** [Why, and what may fit better.]

### Discovery questions

- **[Topic].** [Question.]
- **[Topic].** [Question.]

---

## 6. Audiences

One short block per role. Link to the role pages in [`audiences/`](../../audiences/) and to the message house's persona section rather than restating them.

| Role | Cares most about | Useful framing |
|---|---|---|
| [Role](../../audiences/[role].md) | [Goal and main concern] | "[Short framing]" |
| [Role](../../audiences/[role].md) | [Goal and main concern] | "[Short framing]" |

---

## 7. Alternatives and Related Products

Two or three lines per alternative, linking to the relevant `market-landscape/` page or message house section for detail.

- **[Alternative approach or product].** [How it differs, and when it may be the better choice.] See [link].
- **[Alternative approach or product].** [How it differs, and when it may be the better choice.] See [link].

---

## 8. Common Questions

Only include questions the product FAQ doesn't already answer, and link to the FAQ for everything else. If the product has no FAQ, this section is the main place for common questions.

### "[Common question]"

[Concise, factual answer.]

> Useful follow-up: "[Question that helps clarify requirements.]"

---

## 9. Evaluation and Demo

### Evaluation stages

| Stage | Goals | Typically involved |
|---|---|---|
| Initial exploration | [Goal] | [Role] |
| Technical evaluation | [Goal] | [Role] |
| Security and architecture review | [Areas evaluated] | [Role] |
| Production planning | [Topics] | [Role] |

### Pilot setup

- [Scope, stakeholders, environment, prerequisites, and timeline]

### Success criteria

- [Criterion]
- [Criterion]

### Demo flow

1. [Step]
2. [Step]
3. [Step]

Tailor emphasis to the audiences in section 6. Avoid over-emphasizing [area].

---

## 10. Commercial, Partners, and Contacts

### Packaging and prerequisites

- [Tier or package required, and which capabilities need which tier]
- [What changes between tiers, such as limits, caps, or usage-based pricing]
- [Other prerequisites]

Link to [Packaging](../../company/packaging.md) rather than restating it.

### Evaluation access

[How organizations get access, such as a self-serve trial or free tier, a sales-led pilot, or a limited preview.]

### Partners

[How partners fit, in a sentence or two. Link to the message house's partner narrative. Omit if not applicable.]

### Contacts

List only people or teams who have agreed to be named publicly as contacts for this product.

| Topic | Contact / Team |
|---|---|
| [Topic] | [Owner] |

---

## 11. Resources

- [Product documentation]
- [Message house and FAQ, if one exists]
- [Related use case pages]
- [Announcements and blog posts]
- [Related market landscape pages]
- [Public evidence, such as anonymized customer examples, research, or ecosystem developments]

---

## Document Maintenance

**Owner:** [Team / Person]  
**Last updated:** [Date]  
**Version:** [Version]

Update this playbook when the product's architecture, packaging, supported integrations, boundaries, or public evidence change, or when new questions recur.
