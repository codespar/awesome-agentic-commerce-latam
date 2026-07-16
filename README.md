<p align="center">
  <h1 align="center">Awesome Agentic Commerce LATAM 🌎</h1>
  <p align="center">
    <strong>The builder's index to AI agents that move money in Latin America.</strong><br>
    <em>Pix and account-to-account rails, regulated cross-border, fiscal (NF-e), and the agent-payment protocols (x402, ACP, AP2, UCP, MPP) as they actually land in the region.</em>
  </p>
  <p align="center">
    <a href="https://awesome.re"><img src="https://awesome.re/badge.svg" alt="Awesome" /></a>
    <img src="https://img.shields.io/badge/license-MIT-blue.svg" alt="MIT License" />
    <img src="https://img.shields.io/badge/scope-LATAM-0FA968.svg" alt="LATAM" />
  </p>
</p>

Vendor-neutral. Maintained by [CodeSpar](https://codespar.dev). Contributions welcome, including your competitors and ours: the value of this list is that it is honest and complete. See [Contributing](CONTRIBUTING.md).

## Why this list

The global agentic-commerce and x402 lists are excellent, and mostly written from the US and from crypto. They barely touch the rails most of the world actually pays on: Pix and account-to-account, boleto, regulated cross-border FX, and the tax document a purchase legally needs. In Latin America an autonomous agent does not need a card to pull; it needs a scoped, capped, revocable mandate and a rail that settles instantly with finality. This list curates the protocols, rails, tools, providers, and the regulation for building agent commerce here. Global tools are included when they matter for building in the region.

If you only read one thing, read the [Regulation & policy](#regulation--policy) section. It is the part no other list covers, and it is where the next two years are being decided.

## Contents

- [Protocols & standards](#protocols--standards)
- [Facilitators & gateways](#facilitators--gateways)
- [x402 services & endpoints](#x402-services--endpoints)
- [Wallets, mandates & spend controls](#wallets-mandates--spend-controls)
- [Agent identity & receipts](#agent-identity--receipts)
- [Rails (LATAM)](#rails-latam)
- [LATAM providers & infrastructure](#latam-providers--infrastructure)
- [Fiscal & compliance](#fiscal--compliance)
- [SDKs, runtimes & MCP](#sdks-runtimes--mcp)
- [Demos & live paywalls](#demos--live-paywalls)
- [Regulation & policy](#regulation--policy)
- [Market maps & landscapes](#market-maps--landscapes)
- [Related lists](#related-lists)
- [Reading & research](#reading--research)

## Protocols & standards

- [x402](https://github.com/coinbase/x402) - HTTP 402 Payment Required, revived by Coinbase. Pay-per-request, settled in stablecoin, no account and no human checkout. The machine-payment primitive.
- [Agentic Commerce Protocol (ACP)](https://github.com/agentic-commerce-protocol/agentic-commerce-protocol) - OpenAI + Stripe. Delegated payment for agentic checkout. Card-first today.
- [Agent Payments Protocol (AP2)](https://cloud.google.com/blog/products/ai-machine-learning/announcing-agents-to-payments-ap2-protocol) - Google. Mandate-centric, "Human Not Present" pre-authorized payments; contributed to the FIDO Alliance.
- [Universal Commerce Protocol (UCP)](https://github.com/Universal-Commerce-Protocol/ucp) - open agentic-commerce protocol co-developed by Google and Shopify (announced January 2026); agents discover products, fill carts, and check out. Spec at [ucp.dev](https://ucp.dev).
- [Machine Payments Protocol (MPP)](https://mpp.dev) - open machine-to-machine payment standard co-authored by Tempo and Stripe, proposed to the IETF. HTTP 402-based, with a "sessions" primitive that streams micropayments under an upfront spending limit; settles in stablecoins (Tempo), cards (Stripe/Visa), and Lightning.
- [agentic-payments-standards](https://github.com/codespar/agentic-payments-standards) - CodeSpar's open proposals: a KYA agent-identity format with a dependency-free offline verifier, a push-rail / mandate-delegated payment handler proposed for ACP (Pix as the reference implementation), and a Pix + delivery-record + mandate proposal for Open Agentic Commerce.

## Facilitators & gateways

- [Coinbase CDP x402 Facilitator](https://docs.cdp.coinbase.com/x402) - reference x402 facilitator and the Bazaar marketplace of agent-payable endpoints, on Base.
- [xpay](https://xpay.sh) - two-sided MCP-native marketplace and payment layer; runs a public x402 facilitator, supports MPP and cards. US and crypto-first, no Pix or regulated LATAM rails.
- [CodeSpar Gateway](https://docs.codespar.dev) - turns any endpoint into an agent-payable one (x402 on Base mainnet), paired with a signed mandate and a hash-chained receipt, and bridged to Pix so a local service can be paid in BRL while the agent pays in USDC.
- [Cloudflare x402](https://blog.cloudflare.com/x402/) - edge facilitator with payment verification and deferred settlement.

## x402 services & endpoints

The x402 endpoint economy is global, crypto-settled, and moving fast: hundreds of paid APIs are live and the set changes weekly. Latin America is barely represented here yet, which is the opening. Start from the directories, then a representative sample.

Directories:

- [Coinbase Bazaar](https://docs.cdp.coinbase.com/x402) - the official CDP registry of x402-payable endpoints.
- [x402scan](https://www.x402scan.com) - community-maintained directory of live x402 services.
- [Agent402 Index](https://agent402.tools) - a public routing index of agent-payable tools.

Representative services, pay-per-call in USDC on Base:

- [Superhighway](https://superhighway.walls.sh) - web search for agents, five tools at $0.001 per query.
- [Arch Tools](https://archtools.dev) - 58 API tools for agents (web scraping, crypto data, OCR).
- [PayAPI Market](https://payapi.market) - a marketplace of x402 APIs, 65 endpoints ($0.001-$0.01).
- [LogicNodes](https://logicnodes.io) - 619 deterministic microservices ($0.001-$0.50).
- [tx402.ai](https://tx402.ai) - LLM inference gateway across 20+ EU models ($0.002-$0.05).
- [glim.sh](https://glim.sh) - live web, social, and GitHub data via 11 MCP tools.
- [img402](https://img402.dev) - image hosting for agents ($0.01-$1.00).
- [x402 Video](https://x402-video.com) - AI video generation ($0.05-$0.50 per video).
- [EconDash](https://econdash.org) - global macroeconomic data across 15 endpoints.
- [AIsa](https://aisa.network) - an x402 payment processor reporting 10.5M+ transactions.

## Wallets, mandates & spend controls

- [CodeSpar wallet + mandate engine](https://codespar.dev) - multi-slot wallet (BRL + USDC, per-currency caps, no synthetic FX) with signed mandates enforced before any payment: per-transaction cap, total cap, expiry, agent match, and a payee allowlist so a leaked mandate cannot be redirected.
- [Crossmint](https://www.crossmint.com) - agent wallets and stablecoin payments infrastructure.
- [Skyfire](https://skyfire.xyz) - identity and payments for AI agents; a KYA-style verification plus settlement.
- [Catena Labs](https://catenalabs.com) - agent-native financial institution and mandate tooling.
- [Payman](https://paymanai.com) - human-in-the-loop payment controls for AI agents.
- [MoltsPay](https://github.com/Yaqing2023/moltspay) - payment infrastructure for AI agents with spending limits and framework integrations (LangChain, CrewAI); settles USDC.

## Agent identity & receipts

- [KYA (Know Your Agent)](https://codespar.dev/trust) - CodeSpar's signed-mandate and receipt format plus a dependency-free offline verifier. Ed25519 keypair per agent, `did:web` identity, and a hash-chained receipt (mandate → quote → payment → delivery) that anyone can verify offline. "Know the agent, trust the money."
- [ERC-8004: Trustless Agents](https://eips.ethereum.org/EIPS/eip-8004) - Ethereum standard extending A2A with three on-chain registries (Identity, Reputation, Validation) so agents can be discovered and trusted across organizations. Deployed on mainnet and 20+ networks.
- FIDO Alliance, Agentic Authentication working groups - device-bound agent authentication feeding AP2.

## Rails (LATAM)

- [Pix](https://www.bcb.gov.br/en/financialstability/pix_en) - Brazil's instant account-to-account rail. Real-time, no chargeback, above 76% of Brazilian adults, roughly R$35 trillion cleared in 2025. The default rail for agent payments in Brazil.
- [Pix Automático](https://www.bcb.gov.br/en/financialstability/pix_en) - the recurring standing-authorization modality of Pix (live since 2025). A signed, capped, revocable standing consent, which is structurally the agent mandate.
- Boleto - the cash / bank-slip rail, still meaningful for the underbanked buyer.
- [USDC on Base](https://www.circle.com/usdc) - the stablecoin settlement rail for cross-border and x402.
- SPEI (Mexico), PSE (Colombia), Transferencias 3.0 (Argentina), and other account-to-account rails across the region.

## LATAM providers & infrastructure

- [Celcoin](https://www.celcoin.com.br) - banking-as-a-service, Pix and boleto in Brazil.
- [Iniciador](https://iniciador.com.br) - Pix payment initiation (ITP) under Open Finance; a complementary Pix-under-mandate rail.
- [Pluggy](https://pluggy.ai) and [Belvo](https://belvo.com) - Open Finance data (read, and increasingly write) across LATAM.
- [Bridge](https://www.bridge.xyz) - stablecoin orchestration and settlement substrate.
- Mercado Pago, dLocal, EBANX - large PSPs and cross-border money-movement in the region.

## Fiscal & compliance

- [NFE.io](https://nfe.io) and [Focus NFe](https://focusnfe.com.br) - programmatic Brazilian e-invoice (NF-e / NFS-e) issuance. A purchase is not legal in Brazil without the tax document, and no agent-payment protocol issues one, so this is a required layer for the sell-side.
- KYC / KYB providers for onboarding the merchant and the agent operator.

## SDKs, runtimes & MCP

- [codespar](https://github.com/codespar/codespar) - MIT-licensed, self-hostable agent runtime and channel adapters for commerce agents (`pip install codespar`).
- [MCP Dev LATAM](https://github.com/codespar/mcp-dev-latam) - 127 MCP servers wrapping LATAM commerce APIs (payments, fiscal, logistics, banking, ERP), live in the official MCP Registry.
- [Model Context Protocol (MCP)](https://modelcontextprotocol.io) - the tool-calling standard agents use to reach these APIs.
- [Composio](https://composio.dev) - global tool-calling / integration layer for agents.
- x402 SDKs - [TypeScript](https://github.com/coinbase/x402/tree/main/typescript), [Python](https://pypi.org/project/x402/), and [Rust](https://github.com/x402-rs/x402-rs) implementations of the x402 protocol.

## Demos & live paywalls

- [CodeSpar x402 paywall](https://basescan.org/tx/0x739d2d12de75bb90fd92c2297b83c1da297b39cfb06fb0e24e09f4d5f32b1b8f) - a paywall on Base mainnet; here an agent pays $0.001 for a third-party API it discovered, verifiable on Basescan.
- Vibe payments (CodeSpar) - an agent reads its balance, checks the mandate, pays a real store via Pix, and returns an audited receipt.

## Regulation & policy

The part no other list curates. This is where the rails get decided.

- **Resolução BCB 561** (Brazil, effective 1 October 2026) - restricts cross-border FX (eFX) to licensed institutions and prohibits settling it in stablecoin with a foreign counterparty. It closes the crypto shortcut and pushes agent cross-border flows onto licensed orchestration. The payment institution may act as eFX provider up to US$10k per operation without a separate FX license.
- **Pix Automático** (Brazil, live since 2025) - mandatory for all Pix participants to support; a native recurring standing-authorization framework that maps directly onto the agent mandate primitive.
- **GENIUS Act** (US, law since July 2025) - the stablecoin framework driving issuers like Circle toward national trust bank charters.
- **OCC bank & trust charters** - the wave of fintechs, stablecoin issuers, and digital-asset firms becoming regulated US institutions (Circle, Ripple, Paxos, BitGo, Fidelity Digital Assets, and Brazil's Nubank with a conditional approval). The same "money goes through the front door" pattern as Res 561, in the northern hemisphere.
- Central bank instant-payment mandates across LATAM (SPEI, PSE, Transferencias 3.0) - the regional context for account-to-account agent payments.

## Market maps & landscapes

- [CodeSpar Agentic Commerce Map](https://codespar.dev/map) - 236 companies across the agentic-commerce stack, with the LATAM execution layer flagged.
- Agentic Commerce Map (agenticcommercemap.com) - a third-party map of the space.

## Related lists

Neutral by design, including competitors' lists.

- [xpaysh/awesome-x402](https://github.com/xpaysh/awesome-x402) - the reference x402 list (by xpay). Deep on SDKs and facilitators, US and crypto-first.
- [Merit-Systems/awesome-agentic-commerce](https://github.com/Merit-Systems/awesome-agentic-commerce) - general agentic-commerce resources.
- [bitrefill/awesome-agentic-payments](https://github.com/bitrefill/awesome-agentic-payments) - protocols, specs, SDKs, and tools for the agentic-commerce stack.
- [tsubasakong/awesome-agent-payments-protocol](https://github.com/tsubasakong/awesome-agent-payments-protocol) - AP2, A2A, and x402 resources.
- [RiccardoBiosas/awesome-agentic-payments](https://github.com/RiccardoBiosas/awesome-agentic-payments) - agentic-payments resources.
- [sudeepb02/awesome-erc8004](https://github.com/sudeepb02/awesome-erc8004) - curated resources for ERC-8004 trustless agents.

## Reading & research

- CodeSpar, "Rails for Robots" - why every agent action eventually settles as a payment, and why a payment is a Pix in São Paulo, USDC over x402 on Base, and a card to a SaaS vendor. [codespar.dev/blog](https://codespar.dev/blog)
- CodeSpar, Defensibility - the runtime that proves a transaction was authorized, in-mandate, and delivered is what a buyer cannot route around. [codespar.dev/blog](https://codespar.dev/blog)

---

## Contributing

Add what is missing, fix what is wrong, and include tools that compete with the maintainers. A list that hides competitors is marketing, not a resource. See [CONTRIBUTING.md](CONTRIBUTING.md).

## License

[MIT](LICENSE). The curated content is offered for free reuse; attribution appreciated, not required.

## Maintainers

Curated by [CodeSpar](https://codespar.dev), the Pix-native agentic-payments runtime for Latin America. This list is independent of CodeSpar's products; entries earn their place on merit, not on who made them.
