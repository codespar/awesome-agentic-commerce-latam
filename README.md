# Awesome Agentic Commerce LATAM [![Awesome](https://awesome.re/badge.svg)](https://awesome.re)

> The builder's index to AI agents that move money in Latin America: the commerce layer, the rails beneath it, the governance that makes agent spend safe, and the regulation that decides all of it.

Vendor-neutral, maintained by [CodeSpar](https://codespar.dev). Contributions welcome, including competitors: the value of this list is that it is honest and complete. See the [contributing guide](CONTRIBUTING.md).

The global agentic-commerce and x402 lists are excellent, and mostly written from the US and from crypto. They barely touch the rails most of the world actually pays on: Pix and account-to-account, boleto, regulated cross-border FX, and the tax document a purchase legally needs. There is a layering worth keeping straight: the commerce layer is where an agent discovers a merchant and checks out (ACP, UCP, AP2); the rails sit beneath it and move the money (Pix, cards, stablecoins, x402). This list is organized that way, LATAM-first.

## Contents

- [Glossary](#glossary)
- [Pick a rail or protocol](#pick-a-rail-or-protocol)
- [Commerce layer](#commerce-layer)
- [Rails and settlement](#rails-and-settlement)
- [Governance and trust](#governance-and-trust)
- [LATAM providers and fiscal](#latam-providers-and-fiscal)
- [Regulation and policy](#regulation-and-policy)
- [Discovery and anti-patterns](#discovery-and-anti-patterns)
- [Working examples](#working-examples)
- [Maintainer's packages](#maintainers-packages)
- [Related lists](#related-lists)
- [Reading and research](#reading-and-research)

## Glossary

Agentic commerce has an acronym-collision problem. **ACP** is the Agentic Commerce Protocol (OpenAI and Stripe), not IBM's Agent Communication Protocol. **UCP** is the Universal Commerce Protocol (Google and Shopify). **AP2** is Google's Agent Payments Protocol. **MCP** is the Model Context Protocol (Anthropic), how agents call tools, not a payment protocol. **MPP** is the Machine Payments Protocol (Tempo and Stripe). **x402** is the HTTP 402 pay-per-request rail (Coinbase), settled in stablecoin. **KYA** is Know Your Agent, a verifiable agent identity plus a signed mandate and receipt. A **mandate** is a signed, capped, revocable authorization an agent spends under. **Pix** is Brazil's instant account-to-account rail, and Pix Automático is its recurring modality. **ITP** is Iniciador de Transação de Pagamento, Pix payment initiation under Open Finance. **eFX** is electronic FX, the regulated cross-border rail. **NF-e** is the Brazilian product electronic invoice, NFS-e for services.

## Pick a rail or protocol

A rough decision guide. Mix freely; a protocol and a rail are different choices.

- Selling into ChatGPT, or already on Stripe? Use ACP.
- Targeting Google surfaces (Search, Gemini)? Use UCP.
- Autonomous agent-to-agent, or machine-to-machine at the HTTP layer? Use AP2 or x402.
- Charging per API call or per tool? Use x402 (USDC), or MPP.
- Buyer in Brazil, human or agent? Use Pix; if it recurs, Pix Automático.
- Cross-border settlement? Use stablecoin (USDC over x402), or licensed eFX where the regulator requires it.
- Need the buyer to be governable, with a cap, an allowlist, and a receipt? Put a signed mandate on top of whichever rail you chose.

## Commerce layer

Where an agent discovers a merchant, fills a cart, and checks out.

- [Agentic Commerce Protocol (ACP)](https://github.com/agentic-commerce-protocol/agentic-commerce-protocol) - OpenAI and Stripe. Delegated payment for agentic checkout, card-first today, live in ChatGPT.
- [Universal Commerce Protocol (UCP)](https://github.com/Universal-Commerce-Protocol/ucp) - Google and Shopify. Discovery, cart, checkout, orders, delivery. Spec at [ucp.dev](https://ucp.dev).
- [Agent Payments Protocol (AP2)](https://cloud.google.com/blog/products/ai-machine-learning/announcing-agents-to-payments-ap2-protocol) - Google. Mandate-centric, pre-authorized payments, contributed to the FIDO Alliance.
- [VTEX](https://vtex.com) - Enterprise commerce platform across LATAM; launched WhatsApp-plus-Pix checkout with Meta.
- [Nuvemshop / Tiendanube](https://www.nuvemshop.com.br) - The largest SMB commerce platform in the region ([tiendanube.com](https://www.tiendanube.com) in Spanish markets).
- [Mercado Libre](https://www.mercadolibre.com) - The region's dominant marketplace and payments network (Mercado Pago).

LATAM-native platforms have the rails (Pix, card, boleto) but agentic-protocol adoption is still early; Shopify and WooCommerce lead on protocols but need a local gateway for Pix. That gap is the opening.

## Rails and settlement

These sit below the commerce layer and move the money. No FX: each rail carries its own price.

- [Pix](https://www.bcb.gov.br/en/financialstability/pix_en) - Brazil's instant account-to-account rail. Real-time, no chargeback, above 76% of adults, roughly R$35 trillion cleared in 2025.
- [Pix Automático](https://mobileecosystemforum.com/2025/06/03/brazils-payment-revolution-accelerates-pix-automatico-launches/) - The recurring standing-authorization modality of Pix, which is structurally the agent mandate.
- [USDC on Base](https://www.circle.com/usdc) - The stablecoin settlement rail for cross-border and x402.
- [x402](https://github.com/coinbase/x402) - The HTTP 402 pay-per-request rail, by Coinbase. SDKs in [TypeScript](https://github.com/coinbase/x402/tree/main/typescript), [Python](https://pypi.org/project/x402/), and [Rust](https://github.com/x402-rs/x402-rs).
- [Coinbase CDP Facilitator](https://docs.cdp.coinbase.com/x402) - The reference x402 facilitator and the Bazaar registry of agent-payable endpoints.
- [xpay](https://xpay.sh) - A two-sided MCP-native marketplace running a public x402 facilitator, US and crypto-first.
- [Cloudflare x402](https://blog.cloudflare.com/x402/) - Edge facilitator with payment verification and deferred settlement.
- [x402scan](https://www.x402scan.com) - Community-maintained directory of live x402 services.
- [Agent402 Index](https://agent402.tools) - A public routing index of agent-payable tools.
- [Machine Payments Protocol (MPP)](https://mpp.dev) - Open machine-to-machine payment standard co-authored by Tempo and Stripe, HTTP 402-based, settling in stablecoins, cards, and Lightning.

A representative slice of live x402 services (pay-per-call in USDC on Base); browse the directories above for the full set.

- [Superhighway](https://superhighway.walls.sh) - Web search for agents, five tools at $0.001 per query.
- [Arch Tools](https://archtools.dev) - 58 API tools (web scraping, crypto data, OCR).
- [glim.sh](https://glim.sh) - Live web, social, and GitHub data via 11 MCP tools.
- [tx402.ai](https://tx402.ai) - LLM inference gateway across 20+ EU models.
- [img402](https://img402.dev) - Image hosting for agents.
- [x402 Video](https://x402-video.com) - AI video generation.
- [PayAPI Market](https://payapi.market) - A marketplace of x402 APIs, 65 endpoints.
- [LogicNodes](https://logicnodes.io) - 619 deterministic microservices.

## Governance and trust

What makes it safe to hand a rail to an autonomous agent.

- [Crossmint](https://www.crossmint.com) - Agent wallets and stablecoin payments infrastructure.
- [Skyfire](https://skyfire.xyz) - Identity and payments for AI agents.
- [Catena Labs](https://catenalabs.com) - Agent-native financial institution and mandate tooling.
- [Payman](https://paymanai.com) - Human-in-the-loop payment controls for AI agents.
- [ERC-8004: Trustless Agents](https://eips.ethereum.org/EIPS/eip-8004) - Ethereum standard adding on-chain Identity, Reputation, and Validation registries for agents.

## LATAM providers and fiscal

- [Celcoin](https://www.celcoin.com.br) - Banking-as-a-service, Pix and boleto in Brazil.
- [Iniciador](https://iniciador.com.br) - Pix payment initiation (ITP) under Open Finance.
- [Pluggy](https://pluggy.ai) - Open Finance data across LATAM.
- [Belvo](https://belvo.com) - Open Finance data, read and increasingly write, across LATAM.
- [Bridge](https://www.bridge.xyz) - Stablecoin orchestration and settlement substrate.
- [NFE.io](https://nfe.io) - Programmatic Brazilian e-invoice (NF-e / NFS-e) issuance.
- [Focus NFe](https://focusnfe.com.br) - Brazilian e-invoice issuance API. A purchase is not legal in Brazil without the tax document, and no agent-payment protocol issues one.

## Regulation and policy

The part no other list curates. This is where the rails get decided. **Resolução BCB 561** (Brazil, effective 1 October 2026) restricts cross-border FX to licensed institutions and prohibits settling it in stablecoin with a foreign counterparty; it closes the crypto shortcut and pushes agent cross-border flows onto licensed orchestration. **Pix Automático** (Brazil, live since 2025) is mandatory for all Pix participants to support, a native recurring standing-authorization that maps onto the agent mandate. The **GENIUS Act** (US, law since July 2025) is the stablecoin framework driving issuers like Circle toward national trust bank charters. And the wave of **OCC bank and trust charters** is turning fintechs, stablecoin issuers, and digital-asset firms into regulated US institutions, including Brazil's Nubank with a conditional approval.

## Discovery and anti-patterns

How an agent finds what a site offers, and what not to ship.

- [llms.txt](https://llmstxt.org) - A file that tells an agent how to use your site.
- [schema.org](https://schema.org) - Structured product data agents parse.

Anti-patterns: do not invent well-known files that are in no spec; a checkout API without delegated payment is just a cart, not an agentic checkout; do not claim NF-e in production when it is homologation-grade.

## Working examples

- [CodeSpar x402 Monetization Examples](https://github.com/codespar/x402-monetization-examples) - Charge an agent to use an API, an MCP server, or a payment link, settled in USDC over x402, with a Pix leg.

## Maintainer's packages

CodeSpar maintains this list. Its own tools are collected here, so the sections above stay vendor-neutral.

- [codespar/codespar](https://github.com/codespar/codespar) - MIT, self-hostable agent runtime for commerce agents.
- [MCP Dev LATAM](https://github.com/codespar/mcp-dev-latam) - 127 MCP servers wrapping LATAM commerce APIs, live in the MCP Registry.
- [agentic-payments-standards](https://github.com/codespar/agentic-payments-standards) - Open KYA identity, receipt, and Pix-mandate proposals for the agent-payment standards.
- [Trust and KYA](https://codespar.dev/trust) - Verifiable agent identity, signed mandates, and hash-chained receipts.
- [Agentic Commerce Map](https://codespar.dev/map) - 236 companies across the stack, with the LATAM execution layer flagged.

## Related lists

- [xpaysh/awesome-x402](https://github.com/xpaysh/awesome-x402) - The reference x402 rail list.
- [xpaysh/awesome-agentic-commerce](https://github.com/xpaysh/awesome-agentic-commerce) - The commerce-layer companion, with a strong protocol comparison.
- [Merit-Systems/awesome-agentic-commerce](https://github.com/Merit-Systems/awesome-agentic-commerce) - General agentic-commerce resources.
- [bitrefill/awesome-agentic-payments](https://github.com/bitrefill/awesome-agentic-payments) - Protocols, specs, SDKs, and tools.
- [tsubasakong/awesome-agent-payments-protocol](https://github.com/tsubasakong/awesome-agent-payments-protocol) - AP2, A2A, and x402 resources.
- [sudeepb02/awesome-erc8004](https://github.com/sudeepb02/awesome-erc8004) - ERC-8004 trustless agents.

## Reading and research

- [Rails for Robots](https://codespar.dev/blog/rails-for-robots) - Why every agent action eventually settles as a payment, and why a payment is a Pix in one place and USDC in another.
- [Defensibility](https://codespar.dev/blog/defensibility) - The runtime that proves a transaction was authorized, in-mandate, and delivered is what a buyer cannot route around.

## Contributing

Add what is missing, fix what is wrong, and include tools that compete with the maintainers. A list that hides competitors is marketing, not a resource.

## Maintainers

Curated by CodeSpar, the Pix-native agentic-payments runtime for Latin America. This list is independent of CodeSpar's products; entries earn their place on merit.
