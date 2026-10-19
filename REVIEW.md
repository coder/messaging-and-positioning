# Review

Run this check on any content about Coder that you create or edit using this repository, before you return it. It applies whether or not the person asked for a review. Most people using this repository through an AI tool don't know this file exists, so the check has to happen on its own.

## What it covers

Any content someone could publish, send, present, or reuse: web pages, blog posts, social posts, emails, ads, decks, one-pagers, sales enablement, RFP and questionnaire answers, press materials, and edits to any of these.

Skip it when you're only answering a question about Coder's positioning and not producing content.

## What failure looks like

The content misleads someone about Coder. Check for these, in order:

1. **Unsupported facts.** Every capability, integration, metric, version, availability statement, and customer claim must be supported by this repository or authoritative product documentation such as [coder.com/docs](https://coder.com/docs). Don't fill gaps from general knowledge.
2. **Pricing and packaging.** Tier names, what each tier includes, and prices come from [coder.com/pricing](https://coder.com/pricing), with [Packaging](./company/packaging.md) for the narrative. Don't state prices from memory.
3. **Roadmap promises.** Don't describe unreleased features as available, and don't commit to dates or future capabilities.
4. **Competitor claims.** Claims about other vendors must match their page in `market-landscape/`. If a vendor has no page, don't make specific claims about it. No disparaging language.
5. **Names and terminology.** Use current product and feature names as written in `products/` and `company/`, for example AI Gateway (not AI Bridge) and Agent Firewall (not Agent Boundaries). Mention a former name only to help a reader who knows the old one.
6. **Positioning drift.** The content must not contradict the [message house](./company/message-house.md) or the relevant product message house, for example by calling an included capability an add-on or describing a product's scope differently.
7. **Non-public information.** No customer names, logos, quotes, or results unless they're already public, and no internal metrics or plans.
8. **New messaging presented as established.** Proposed messaging is fine, but label it as proposed rather than as Coder's current position.

Don't flag tone, style, length, or word choice unless it changes the meaning. Keep the review about accuracy.

## What to do with findings

- Fix what you can using this repository or product documentation.
- If you can't verify a claim, remove it or mark it `[needs source]` in the content, and tell the person why.
- If the repository doesn't answer something the content needs, say so plainly instead of inventing a position.

After the content, and separate from it so it isn't pasted into the final piece, add one line:

`Checked against Coder messaging: <N> fixed, <N> flagged.`

If nothing needed changing, write `Checked against Coder messaging: no issues found.` A missing line means the check didn't run.

## Improving this check

If the same problem keeps showing up, the fix belongs in this repository, not in each piece of content. Raise it with Product Marketing or open a pull request.
