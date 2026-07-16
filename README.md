<p align="center">
  <h1 align="center">Awesome Agentic Commerce LATAM 🌎</h1>
  <p align="center">
    <strong>The builder's index to AI agents that move money in Latin America.</strong><br>
    <em>The commerce layer (ACP, UCP, AP2), the rails beneath it (Pix, x402, cards, stablecoins), the governance that makes agent spend safe, and the regulation that decides all of it.</em>
  </p>
  <p align="center">
    <a href="https://awesome.re"><img src="https://awesome.re/badge.svg" alt="Awesome" /></a>
    <img src="https://img.shields.io/badge/license-MIT-blue.svg" alt="MIT License" />
    <img src="https://img.shields.io/badge/scope-LATAM-0FA968.svg" alt="LATAM" />
  </p>
</p>

Vendor-neutral. Maintained by [CodeSpar](https://codespar.dev). Contributions welcome, including your competitors and ours: the value of this list is that it is honest and complete. See [Contributing](CONTRIBUTING.md).

## Why this list

The global agentic-commerce and x402 lists are excellent, and mostly written from the US and from crypto. They barely touch the rails most of the world actually pays on: Pix and account-to-account, boleto, regulated cross-border FX, and the tax document a purchase legally needs.

There is a layering worth keeping straight. The **commerce layer** is where an agent discovers a merchant, negotiates, and checks out (ACP, UCP, AP2). The **rails** sit beneath it and move the money (Pix, cards, stablecoins, x402). Any commerce protocol can plug into any rail. In Latin America the interesting rail is Pix, not a card, and an autonomous agent needs a scoped, capped, revocable mandate rather than a bearer credential. This list is organized that way.

For the market view alongside this builder's index, CodeSpar maps the whole space, 236 companies across the stack, at [codespar.dev/map](https://codespar.dev/map).

If you only read one thing, read the [Regulation & policy](#regulation--policy) section. It is the part no other list covers, and it is where the next two years are being decided.

## Glossary

Agentic commerce has an acronym-collision problem. In this list:

- **ACP** - Agentic Commerce Protocol (OpenAI + Stripe). Not IBM's Agent Communication Protocol.
- **UCP** - Universal Commerce Protocol (Google + Shopify).
- **AP2** - Agent Payments Protocol (Google).
- **MCP** - Model Context Protocol (Anthropic), how agents call tools. Not a payment protocol.
- **MPP** - Machine Payments Protocol (Tempo + Stripe).
- **x402** - the HTTP 402 pay-per-request rail (Coinbase), settled in stablecoin.
- **KYA** - Know Your Agent: a verifiable agent identity plus a signed mandate and receipt.
- **Mandate** - a signed, capped, revocable authorization an agent spends under.
- **Pix / Pix Automático** - Brazil's instant account-to-account rail / its recurring standing-authorization modality.
- **ITP** - Iniciador de Transação de Pagamento, Pix payment initiation under Open Finance.
- **eFX** - electronic FX (câmbio), the regulated cross-border rail (see Resolução BCB 561).
- **NF-e / NFS-e** - the Brazilian product / service electronic invoice.

## Pick a rail or protocol

A rough decision guide. Mix freely; a protocol and a rail are different choices.

- Selling into ChatGPT, or already on Stripe? Use **ACP**.
- Targeting Google surfaces (Search, Gemini)? Use **UCP**.
- Autonomous agent-to-agent, or machine-to-machine at the HTTP layer? **AP2** or **x402**.
- Charging per API call or per tool? **x402** (USDC), or **MPP**.
- Buyer in Brazil, human or agent? **Pix**; if it recurs, **Pix Automático**.
- Cross-border settlement? Stablecoin (**USDC** over x402), or licensed **eFX** where the regulator requires it (see [Regulation](#regulation--policy)).
- Need the buyer to be governable, with a cap, an allowlist, and a receipt? Put a **signed mandate** on top of whichever rail you chose.

## Contents

- [Commerce layer](#commerce-layer)
- [Rails & settlement](#rails--settlement)
- [Governance & trust](#governance--trust)
- [LATAM providers & fiscal](#latam-providers--fiscal)
- [Regulation & policy](#regulation--policy)
- [Discovery & anti-patterns](#discovery--anti-patterns)
- [Working examples](#working-examples)
- [Maintainer's packages](#maintainers-packages)
- [Related lists](#related-lists)
- [Reading & research](#reading--research)

## Commerce layer

Where an agent discovers a merchant, fills a cart, and checks out.

### Protocols

- [Agentic Commerce Protocol (ACP)](https://github.com/agentic-commerce-protocol/agentic-commerce-protocol) - OpenAI + Stripe. Delegated payment for agentic checkout, card-first today. Live in ChatGPT.
- [Universal Commerce Protocol (UCP)](https://github.com/Universal-Commerce-Protocol/ucp) - Google + Shopify (announced January 2026). Discovery, cart, checkout, orders, delivery. Spec at [ucp.dev](https://ucp.dev).
- [Agent Payments Protocol (AP2)](https://cloud.google.com/blog/products/ai-machine-learning/announcing-agents-to-payments-ap2-protocol) - Google. Mandate-centric, "Human Not Present" pre-authorized payments; contributed to the FIDO Alliance.

### Platforms (LATAM)

- [VTEX](https://vtex.com) - enterprise commerce platform across LATAM; launched WhatsApp-plus-Pix checkout with Meta.
- [Nuvemshop / Tiendanube](https://www.nuvemshop.com.br) - the largest SMB commerce platform in the region ([tiendanube.com](https://www.tiendanube.com) in Spanish markets).
- [Mercado Libre](https://www.mercadolibre.com) - the region's dominant marketplace and payments network (Mercado Pago).

### Compatibility (platform x protocol x rail)

A best-effort snapshot. The pattern is the point: the LATAM-native platforms have the rails but not the agentic protocols yet, while the protocol-forward platforms need a local gateway to reach Pix. That gap is the opening. Corrections and additions welcome.

| Platform | Pix | Card / boleto | ACP | UCP | AP2 | x402 |
|---|---|---|---|---|---|---|
| VTEX | yes | yes | emerging | emerging | no | no |
| Nuvemshop / Tiendanube | yes | yes | no | no | no | no |
| Mercado Livre | yes | yes | no | no | no | no |
| Shopify | via gateway | yes | yes | yes | no | no |
| WooCommerce | via plugin | yes | via plugin | via plugin | via plugin | no |

"emerging" = announced or piloted, not generally available. "via gateway/plugin" = through a payment gateway or a community plugin, not native. x402 is a rail any platform can add; none of these ship it natively today.

## Rails & settlement

These sit below the commerce layer and move the money. No FX: each rail carries its own price.

### Local rails

- [Pix](https://www.bcb.gov.br/en/financialstability/pix_en) - Brazil's instant account-to-account rail. Real-time, no chargeback, above 76% of Brazilian adults, roughly R$35 trillion cleared in 2025. The default rail for agent payments in Brazil.
- [Pix Automático](https://mobileecosystemforum.com/2025/06/03/brazils-payment-revolution-accelerates-pix-automatico-launches/) - the recurring standing-authorization modality of Pix (live since 2025). A signed, capped, revocable standing consent, which is structurally the agent mandate.
- Boleto - the cash / bank-slip rail, still meaningful for the underbanked buyer.
- SPEI (Mexico), PSE (Colombia), Transferencias 3.0 (Argentina) - the other account-to-account rails across the region.

### Cards & stablecoins

- [USDC on Base](https://www.circle.com/usdc) - the stablecoin settlement rail for cross-border and x402.
- Card networks - Visa (Intelligent Commerce) and Mastercard (Agent Pay), now live with Brazilian issuers.

### x402

The HTTP 402 pay-per-request rail. An agent hits an endpoint, is asked for a few cents, pays in stablecoin, and gets the resource. The endpoint economy is global, crypto-settled, and moving fast; LATAM is barely represented, which is the opening.

- [x402](https://github.com/coinbase/x402) - the protocol, by Coinbase. SDKs in [TypeScript](https://github.com/coinbase/x402/tree/main/typescript), [Python](https://pypi.org/project/x402/), and [Rust](https://github.com/x402-rs/x402-rs).

Facilitators:

- [Coinbase CDP x402 Facilitator](https://docs.cdp.coinbase.com/x402) - the reference facilitator and the Bazaar marketplace of agent-payable endpoints.
- [xpay](https://xpay.sh) - a two-sided MCP-native marketplace running a public x402 facilitator. US and crypto-first.
- [Cloudflare x402](https://blog.cloudflare.com/x402/) - edge facilitator with payment verification and deferred settlement.

Directories of live endpoints:

- [Coinbase Bazaar](https://docs.cdp.coinbase.com/x402) - the official CDP registry.
- [x402scan](https://www.x402scan.com) - community-maintained directory.
- [Agent402 Index](https://agent402.tools) - a public routing index of agent-payable tools.

A representative slice of live services (pay-per-call in USDC on Base); browse the directories for the full set.

- [Superhighway](https://superhighway.walls.sh) - web search for agents, five tools at $0.001 per query.
- [Arch Tools](https://archtools.dev) - 58 API tools (web scraping, crypto data, OCR).
- [glim.sh](https://glim.sh) - live web, social, and GitHub data via 11 MCP tools.
- [DevDrops](https://devdrops.run) - 22 data APIs for agents.
- [Crest x402 Data](https://data.crestsystems.ai) - wallet profiling and crypto data.
- [2s.io](https://2s.io) - 35 JSON API endpoints, sub-cent to $0.03.
- [EconDash](https://econdash.org) - global macroeconomic data.
- [Mercury402](https://mercury402.uk) - US Treasury and macro data.
- [Usenami](https://usenami.io) - perp funding and RWA spread API.
- [Stratalize](https://www.stratalize.com) - 100+ financial-intelligence tools.
- [x402 Trust Oracle](https://x402oracle.com) - pre-trade trust checks.
- [GlobalAPI](https://globalapi.dev) - 43 compliance endpoints.
- [tx402.ai](https://tx402.ai) - LLM inference gateway across 20+ EU models.
- [zeroreader](https://api.zeroreader.com) - 74 endpoints for LLM, generation, and crypto.
- [img402](https://img402.dev) - image hosting for agents.
- [x402 Video](https://x402-video.com) - AI video generation.
- [hundun.app](https://hundun.app) - AI document summarization.
- [PayAPI Market](https://payapi.market) - a marketplace of x402 APIs, 65 endpoints.
- [LogicNodes](https://logicnodes.io) - 619 deterministic microservices.
- [x402engine](https://x402engine.app) - 74 endpoints across LLMs, generation, crypto, and travel.
- [agentsvc.io](https://agentsvc.io) - 20 utility tools.
- [AIsa](https://aisa.network) - an x402 payment processor reporting 10.5M+ transactions.

### MPP

- [Machine Payments Protocol (MPP)](https://mpp.dev) - an open machine-to-machine payment standard co-authored by Tempo and Stripe, proposed to the IETF. HTTP 402-based, with a "sessions" primitive for streaming micropayments; settles in stablecoins (Tempo), cards (Stripe/Visa), and Lightning.

## Governance & trust

What makes it safe to hand a rail to an autonomous agent.

### Wallets & mandates

- [Crossmint](https://www.crossmint.com) - agent wallets and stablecoin payments infrastructure.
- [Skyfire](https://skyfire.xyz) - identity and payments for AI agents.
- [Catena Labs](https://catenalabs.com) - agent-native financial institution and mandate tooling.
- [Payman](https://paymanai.com) - human-in-the-loop payment controls for AI agents.
- [MoltsPay](https://github.com/Yaqing2023/moltspay) - payment infrastructure for agents with spending limits and framework integrations.

### Agent identity & receipts

- [ERC-8004: Trustless Agents](https://eips.ethereum.org/EIPS/eip-8004) - Ethereum standard extending A2A with Identity, Reputation, and Validation registries. Deployed on mainnet and 20+ networks.
- FIDO Alliance, Agentic Authentication working groups - device-bound agent authentication feeding AP2.

## LATAM providers & fiscal

- [Celcoin](https://www.celcoin.com.br) - banking-as-a-service, Pix and boleto in Brazil.
- [Iniciador](https://iniciador.com.br) - Pix payment initiation (ITP) under Open Finance; a complementary Pix-under-mandate rail.
- [Pluggy](https://pluggy.ai) and [Belvo](https://belvo.com) - Open Finance data, read and increasingly write, across LATAM.
- [Bridge](https://www.bridge.xyz) - stablecoin orchestration and settlement substrate.
- Mercado Pago, dLocal, EBANX - large PSPs and cross-border money-movement in the region.
- [NFE.io](https://nfe.io) and [Focus NFe](https://focusnfe.com.br) - programmatic Brazilian e-invoice (NF-e / NFS-e) issuance. A purchase is not legal in Brazil without the tax document, and no agent-payment protocol issues one, so this is a required layer for the sell-side.

## Regulation & policy

The part no other list curates. This is where the rails get decided.

- **Resolução BCB 561** (Brazil, effective 1 October 2026) - restricts cross-border FX (eFX) to licensed institutions and prohibits settling it in stablecoin with a foreign counterparty. It closes the crypto shortcut and pushes agent cross-border flows onto licensed orchestration. The payment institution may act as eFX provider up to US$10k per operation without a separate FX license.
- **Pix Automático** (Brazil, live since 2025) - mandatory for all Pix participants to support; a native recurring standing-authorization framework that maps directly onto the agent mandate primitive.
- **GENIUS Act** (US, law since July 2025) - the stablecoin framework driving issuers like Circle toward national trust bank charters.
- **OCC bank & trust charters** - the wave of fintechs, stablecoin issuers, and digital-asset firms becoming regulated US institutions (Circle, Ripple, Paxos, BitGo, Fidelity Digital Assets, and Brazil's Nubank with a conditional approval). The same "money goes through the front door" pattern as Res 561.

## Discovery & anti-patterns

How an agent finds what a commerce surface offers, and what not to ship. Real, externally verifiable standards.

| Path or standard | Spec | Purpose |
|---|---|---|
| `/llms.txt` | [llmstxt.org](https://llmstxt.org) | A Markdown site map an LLM reads first. |
| `/.well-known/agent-card.json` | [a2a-protocol.org](https://a2a-protocol.org) | The A2A agent card; the path is in [IANA's well-known registry](https://www.iana.org/assignments/well-known-uris). |
| schema.org JSON-LD | [schema.org](https://schema.org) | `Product`, `Offer`, and `AggregateOffer` markup an agent parses. |
| `/robots.txt` | [RFC 9309](https://www.rfc-editor.org/rfc/rfc9309) | Allow or block the agent crawlers: GPTBot, ClaudeBot, Google-Extended, PerplexityBot, CCBot, Amazonbot. |
| `/.well-known/oauth-protected-resource` | [RFC 9728](https://www.rfc-editor.org/rfc/rfc9728) | Agent OAuth resource metadata. |
| `/.well-known/ucp` | [UCP guide](https://developers.google.com/merchant/ucp) | UCP capability negotiation (no `.json`); the on-the-wire version is a YYYY-MM-DD date. |
| `did:web` / `did.json` | W3C DID | Resolvable agent identity a counterparty verifies offline, the KYA approach. |
| MCP `tools/list` | [modelcontextprotocol.io](https://modelcontextprotocol.io) | How an agent discovers the callable tools a server exposes. |

x402 is the exception: it delivers its payment terms inline in the HTTP 402 response, not via a well-known file.

Do not emit. These show up in blog posts and plugin output but are in no active spec: `/.well-known/agentic-commerce.json`, `/.well-known/acp.json`, `/.well-known/ap2.json`, `/.well-known/mcp.json`, `/.well-known/ucp.json` (the real UCP path has no extension), `/.well-known/ai-plugin.json` (a deprecated GPT-plugin manifest), `/agents.txt`, `/ai.txt`.

Protocol anti-patterns:

- ACP without `delegate_payment` is just a cart API; the delegated-payment flow is what makes it agentic.
- UCP without [RFC 9421](https://www.rfc-editor.org/rfc/rfc9421) HTTP message signatures ships a shape any server can serve but no agent can trust.
- AP2 mandates without verifiable-credential verification are decorative JSON; the verification is the whole authorization argument.
- Vendoring a spec at HEAD instead of a dated release breaks reproducibility. Pin a dated snapshot.
- Claiming NF-e in production when it is only homologation-grade. In Brazil the tax document is not optional, and it is not shipped by faking one.

## Working examples

- [CodeSpar x402 Monetization Examples](https://github.com/codespar/x402-monetization-examples) - a cookbook for both sides: charge an agent (API, MCP server, or payment link) and pay a paywall (CLI under a mandate, or a runnable `@x402/fetch` buyer), settled in USDC over x402 with a Pix leg.
- [x402 vending machine](https://github.com/coinbase/x402) - the canonical per-call agent example from the x402 repo.

## Maintainer's packages

CodeSpar maintains this list. Its own tools are collected here, so the sections above stay vendor-neutral.

- [codespar/codespar](https://github.com/codespar/codespar) - MIT, self-hostable agent runtime for commerce agents (`pip install codespar`, `@codespar/sdk`).
- [MCP Dev LATAM](https://github.com/codespar/mcp-dev-latam) - 127 MCP servers wrapping LATAM commerce APIs, live in the MCP Registry.
- [agentic-payments-standards](https://github.com/codespar/agentic-payments-standards) - open proposals: the KYA agent-identity format with an offline verifier, a push-rail extension proposed for ACP with Pix as reference, and a Pix-plus-mandate proposal for Open Agentic Commerce.
- [x402 Monetization Examples](https://github.com/codespar/x402-monetization-examples) - seller-side gateway, MCP, and payment-link examples, plus a governed buyer (CLI) and a runnable x402 client.
- [Trust / KYA](https://codespar.dev/trust) - "know the agent, trust the money": verifiable identity, signed mandates, hash-chained receipts.
- [Agentic Commerce Map](https://codespar.dev/map) - 236 companies across the stack, with the LATAM execution layer flagged.

## Related lists

- [xpaysh/awesome-x402](https://github.com/xpaysh/awesome-x402) - the reference x402 rail list (by xpay).
- [xpaysh/awesome-agentic-commerce](https://github.com/xpaysh/awesome-agentic-commerce) - the commerce-layer companion (by xpay), with a strong protocol comparison and platform matrix.
- [Merit-Systems/awesome-agentic-commerce](https://github.com/Merit-Systems/awesome-agentic-commerce) - general agentic-commerce resources.
- [bitrefill/awesome-agentic-payments](https://github.com/bitrefill/awesome-agentic-payments) - protocols, specs, SDKs, and tools.
- [tsubasakong/awesome-agent-payments-protocol](https://github.com/tsubasakong/awesome-agent-payments-protocol) - AP2, A2A, and x402 resources.
- [RiccardoBiosas/awesome-agentic-payments](https://github.com/RiccardoBiosas/awesome-agentic-payments) - agentic-payments resources.
- [sudeepb02/awesome-erc8004](https://github.com/sudeepb02/awesome-erc8004) - ERC-8004 trustless agents.

## Reading & research

- [CodeSpar: Rails for Robots](https://codespar.dev/blog/rails-for-robots) - why every agent action eventually settles as a payment, and why a payment is a Pix in São Paulo, USDC over x402 on Base, and a card to a SaaS vendor.
- [CodeSpar: Defensibility](https://codespar.dev/blog/defensibility) - the runtime that proves a transaction was authorized, in-mandate, and delivered is what a buyer cannot route around.

---

## Contributing

Add what is missing, fix what is wrong, and include tools that compete with the maintainers. A list that hides competitors is marketing, not a resource. See [CONTRIBUTING.md](CONTRIBUTING.md).

## License

[MIT](LICENSE). The curated content is offered for free reuse; attribution appreciated, not required.

## Maintainers

Curated by [CodeSpar](https://codespar.dev), the Pix-native agentic-payments runtime for Latin America. This list is independent of CodeSpar's products; entries earn their place on merit, not on who made them.
