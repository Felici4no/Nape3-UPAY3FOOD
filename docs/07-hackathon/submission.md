# Submission — Crypto World's Fair (Colosseum)

Updated 2026-10-12. Submitted to Colosseum and to the Earn sidetracks below; the
answers in this note are the ones that were sent.

| Submission | Link |
|---|---|
| Colosseum project | https://colosseum.com/arena/projects/upay3food |
| Pitch video (1:49) | https://youtu.be/4YkGsZAVUtc |
| Demo video, live product (~2:00) | https://youtu.be/6PwKFDQjmXU |

> [!NOTE]
> Traction was submitted as "pre-users": no user metrics were reported, because none were measured yet.

## Deadline

| Where | Closes | We aim for |
|---|---|---|
| Colosseum main submission | Oct 12, 11:59 PM PDT (Oct 13, 06:59 UTC), confirmed on the Colosseum review screen | submitted Oct 12 |
| Superteam Brasil wiki says | Oct 12, 23:59 Brasília (Oct 13, 02:59 UTC) | submitted Oct 12 |
| Superteam Earn sidetracks | Oct 13, 06:59 UTC | submitted Oct 12 |

## Every prize we enter (one project)

| Prize | Pool | How | Fit |
|---|---|---|---|
| Colosseum Grand Prize / top 20 | $30k / 20 × $15k | Colosseum form | open, very competitive |
| **Solana ecosystem track** | 10 × $10k (on top of global) | Colosseum form | strong: USDC + Cloak shield on mainnet, memo anchors, RPC Fast |
| **University Prize** | $5k | Colosseum form; state student status and university in team fields | strong if eligible (criteria not published; email hackathon@colosseum.com if unsure) |
| **Public Good Prize** | $5k | Colosseum form | public MCP server, open methodology anchored on Solana, open source |
| **Superteam Brasil × SolarEcoFund** | 5,000 USDG | separate Earn submission; base country = Brazil on Colosseum | strong |
| **RPC Fast Infrastructure** | ~$10.5k in RPC credits (21 teams) | separate Earn submission + RPC Fast form; follow @rpcfast, join their Telegram/Discord, 2–3 posts/month for 2 months | strong technically (all on-chain traffic goes through RPC Fast) |
| AkcaVPN credits | 3,500 USDG in VPN credits (10 teams) | Earn; open to any Crypto World's Fair project; judged on need for a private connection (handling wallets/funds, remote work) | fits: mainnet wallet and Cloak shield |
| Solami "live on Solana data" | 3,000 USDG | Earn; needs a Solami data path + live mainnet video | not built |

Not eligible, checked against each listing on Oct 12: regional tracks
(Australia, Argentina, Spain/La Familia, UK, India and the rest are residents
only); Adevar Labs ("Solana/Rust submissions only"); CertiK (judged on programs
to audit and value at risk; we have no on-chain program); Meteora, Panta, peaq,
KASE and iDos (need their integrations). Tempo/Base tracks need another chain.
Sources: [sidetrack research](benchmark.md), solanabr/wiki PR #3, SuperteamDAO/earn FAQ,
[all sidetracks](https://superteam.fun/earn/hackathon/crypto-worlds-fair).

## Fields

**Project name:** UPAY3FOOD

**One-liner (EN):** Unit pricing for food delivery. You pay three times for food — the food, the fees and the difference to the cheapest option; UPAY3FOOD shows all three on iFood, adds the unit prices supermarkets must show (per 100 g, per litre, per person), outlines the item worth buying, and lets any AI agent do the same through a public MCP server. The rules are anchored on Solana.

**One-liner (PT):** Você paga 3 vezes pela comida. O UPAY3FOOD mostra as três no iFood, traz o preço por unidade que o supermercado é obrigado a mostrar (por 100 g, por litro, por pessoa), marca o item que compensa e deixa qualquer agente de IA fazer o mesmo via MCP; as regras ficam registradas na Solana.

**Problem.** Brazil's delivery market is in a subsidy war (iFood ~R$24 bn, Keeta R$5.6 bn, 99Food R$2 bn). Menu prices hide what you pay: delivery and service fees, coupons and sizes that are not comparable. No platform exposes consumer checkout prices through an API, and in 2026 Senacon started requiring price breakdowns. In the EU and Australia, supermarkets must show the price per kilo or litre so shoppers can compare sizes; delivery menus show none. In one real São Paulo shop, the dearest item costs 94% more per litre than the cheapest, and the fees on one order are worth 175 ml of the product.

**Solution.**
- **Browser extension** that reads the user's own page, observe-only:
  - "Você paga 3 vezes": food, fees and the difference;
  - "Raio-X do preço": per 100 ml, per litre, per 100 g, per person, and the fees expressed in product;
  - unit prices for the whole menu: burgers per 100 g of meat (with combo extras priced), dishes sold by weight per 100 g, food sold by volume per 100 ml;
  - every drink per litre within its kind;
  - outlines of the best item on iFood's own menu.
- **Explainable agent** ("quero hambúrguer até R$40", "quero açaí 500ml até R$25"): the cheapest estimated checkout, the best unit price, and a link straight to the item.
- **Public MCP server** (`https://upay3food.com/api/mcp`, 9 tools + 1 prompt) so Claude, ChatGPT or Cursor can read shop pages and get the same answers.
- **Solana:**
  - USDC funding shielded through Cloak (1 USDC shielded on mainnet, slot 453687294);
  - the methodology and calculation code hashed and anchored on mainnet via SPL Memo (/transparencia);
  - all RPC traffic through RPC Fast.
- **Docs vault** (https://docs.upay3food.com): every Markdown note in the repository with a graph of how they link, backlinks and search; decisions, incidents and proofs included.

**How Solana is used (be concrete).**
1. Private funding:
   - USDC shield into Cloak from Phantom, signature `4xa8vKZL…asQfx` ([proof](../08-proofs/2026-10-05-mainnet-shield.md));
   - a relay guard enforces one signature, no wallet-funded lookup tables, and fresh quotes.
2. Transparency anchor:
   - SHA-256 of `price-calculations.md` and of the engine sources, written as an SPL Memo;
   - anyone can verify it on /transparencia or with `sha256sum`;
   - memo signature `3NcV2SHoB2cvcg15goPEVxk3crjrAjbntXhC5bhc8SAr8uiaQm5f1axFxRzyNLfQr8Vh7BzUGVaPJQaB1u5QaRaK`, slot 455501588 ([proof](../08-proofs/2026-10-11-transparency-anchor.md)).
3. RPC Fast:
   - the same-origin proxy (`/api/solana-rpc`) has a method allowlist and failure classification;
   - no key reaches the browser.

**Tech.** TypeScript monorepo (pnpm):
- Chrome MV3 extension (React);
- Next.js 16 site on Vercel, in English (the extension UI is in Portuguese, for Brazilian users);
- MCP server (`mcp-handler`, Streamable HTTP);
- `@solana/kit` + web3.js and `@cloak.dev/sdk`;
- private Vercel Blob for the dev bridge;
- 501 tests (vitest), run in GitHub Actions on every push and PR;
- regression fixtures derived from real sanitized iFood captures (commercial data only).

**Open source.** https://github.com/Felici4no/Nape3-UPAY3FOOD (public, MIT). The default branch `main` carries the full build; the README is written for reviewers.

**Prior work / third-party code (disclose).**
- The repository was created on 2026-10-03, inside the hackathon window, and every commit is from then on.
- Development was AI-assisted: many commits are co-authored with Claude (Anthropic's coding assistant), under the founder's direction and review. The README says the same.
- Third-party code: `@cloak.dev/sdk` (used as a dependency, with adapter code in `packages/payments/src/cloak`), `mcp-handler`, `@solana/kit`, `@solana/web3.js`, fontsource fonts.

**Team.** Solo builder, Brazilian university student [course / university], a daily iFood user. Plan after the hackathon: keep building full-time, with a first hire for data partnerships.

**Business model (hypotheses, see [report](../06-business/business-model-and-pitch.pt-BR.md)).**
1. Free for consumers.
2. Revenue now: a CPA per verified first order routed to entrant platforms (Keeta, 99Food, Rappi), cheaper than the R$99–250 coupons they spend today, with the same terms offered to all platforms and disclosed in the UI.
3. Revenue later: aggregated, auditable price data for restaurants, funds and alt-data vendors.
4. Neutrality rules come from three precedents: Taxômetro (2026), Trivago (A$44.7 m) and Honey.

**Go-to-market.**
- University communities and Superteam Brasil first (students order delivery often and are price-sensitive).
- Then creators who compare delivery prices.
- The MCP server reaches users of AI agents with zero distribution cost.

**Traction (fill only with measured numbers).** Testers [N] · shops read [X] · items compared [Y] · estimated savings [R$Z] (popup → "Seus números" → "Copiar meus números").

**Links.**
- Site: https://upay3food.com
- Install: https://upay3food.com/instalar
- Agents: https://upay3food.com/agentes
- Transparency: https://upay3food.com/transparencia
- Docs: https://docs.upay3food.com
- MCP: https://upay3food.com/api/mcp
- GitHub: https://github.com/Felici4no/Nape3-UPAY3FOOD

**Videos.**
- Pitch (1:49): https://youtu.be/4YkGsZAVUtc
- Demo, live product, one take (~2:00): https://youtu.be/6PwKFDQjmXU
- Scripts: [video scripts](video-scripts.md). Both voiceovers are AI voices (ElevenLabs); the video descriptions say so.

## Checklist

- [x] Repository public (MIT)
- [x] PR #1 merged, so `main` (the default branch) shows the project
- [x] GitHub "About": website `https://upay3food.com`, description and topics
- [x] Colosseum: project registered, base country Brazil, student status in team fields
- [x] Transparency anchor signed on mainnet (slot 455501588), listed on /transparencia and in the field above
- [ ] 10+ testers via /instalar; numbers collected with "Copiar meus números"
- [x] Pitch video and demo video uploaded (hide the iFood delivery address)
- [x] Colosseum form submitted, with the accelerator application
- [x] Earn: Superteam Brasil × SolarEcoFund submitted
- [x] Earn: RPC Fast submitted
- [ ] Earn: AkcaVPN credits submitted
- [ ] RPC Fast community: follow @rpcfast, join Telegram/Discord, 2–3 posts a month for 2 months
- [ ] Re-sign the transparency anchor: the engine changed after slot 455501588, so /transparencia lists it as an earlier version
