# Stomatology — children's dentistry site prep

**Status as of 2026-08-21.** Run of the `client-site-prep` skill against
`https://stomatology.axiomthemes.com/childrens-dentistry/`.

**Live status page:** https://claude.ai/code/artifact/d9f70ed4-b922-4690-9ed2-87b222a1f394

| | |
|---|---|
| Phases closed | **3 of 19** (P0.0, P0, P1) |
| Current phase | **P2 — positioning**, sent back by its own adversarial review |
| Gates verified | 4 of 4 (G0, G1, G1b, G2) — each run, exit codes recorded |
| Open blockers | **19** from the P2 review |
| Spec root | `Code/client-site-prep/stomatology/_spec/` *(gitignored — see "Why the spec isn't in this repo")* |

---

## 1. The finding that shapes everything

**The client's "current site" is a WordPress theme demo published by AxiomThemes, not an operating
dental practice.** This is first-party evidence, not inference:

1. The site root's own `<title>` reads *"Stomatology – Dentist & Dental Clinic WordPress Theme"*.
2. **29 of 43 pages (67%)** contain lorem-ipsum body copy.
3. All four social links point to the theme vendor's own accounts (`facebook.com/AxiomThemes`,
   `x.com/ThemesAxiom`, `dribbble.com/AxiomThemes`, `instagram.com/axiom_themes`).
4. The contact block pairs a **German address with a US phone** — *"785 15h Street, Office 478,
   Berlin, De 81566"* / `+1 840 841 25 69`.
5. Both email addresses are Cloudflare-obfuscated placeholders decoding to `info@website.com` and
   `info@email.com`.
6. Pricing sells dentistry as **SaaS subscription tiers** — Silver/Gold/Platinum at $50/$70/$90 per
   month — with literal lorem feature bullets.
7. A **fabricated awards table** claims four consecutive industry awards, 2019–2022, with no
   awarding body, citation, or link.
8. Seven testimonials carry stock names over identical lorem bodies. Blog content is dated **April 2020**.

**Consequence:** there is no real business information to build on — no practice name, location,
clinician, fee, or provable claim. The prep therefore runs on representative placeholders
(`fabricated-fallback`, the skill's documented default), every one tagged `[CRAWLED]` / `[DERIVED]` /
`⚠OWNER`. **The build is structurally complete and factually fictional until the owner supplies real
material.**

---

## 2. Phases

### Prep — `client-site-prep`

| Phase | State | Evidence |
|---|---|---|
| **P0.0** Supply & Audit | done | 43 pages + 106 assets snapshotted; `existing-a-model.md`; 12 owner-flags, 31 verification-flags |
| **P0** Intake & rails lock | done | G0 live-fired → exit 0; §F 1 resolved / 2 waived / 0 pending |
| **P1** Market & competitor research | done | 5 dossiers, 23 snapshots, G1 + G1b 5/5 pass, 27 adversarial corrections, 0 fabricated quotes |
| **P2** Positioning SSOT | **revision required** | G2 → exit 0 (structurally valid); owner approved; **gate NOT flipped** — review returned 19 blockers |
| P3 Architecture / IA | pending | |
| P4 Closed page list + sitemap | pending | owner gate |
| P5 SEO enrichment | pending | |
| P6 Typed content briefs | pending | owner gate |
| P7 Readiness falsification | pending | GO / NO-GO |

### Build — `client-site-build`

P7.5 asset intake · P8 design foundation · P9–P14 build, verify, publish — all pending.

---

## 3. Gate verification

Every phase transition is blocked by a fail-closed hook. These were **run**, not assumed.

| Gate | Blocks | Result | How it was proven |
|---|---|---|---|
| `G0` | research before intake | exit 0 | live-fired with a simulated market-intel write |
| `G1` | ungrounded competitor block | 5/5 exit 0 | pre-tested with a deliberately bad fixture → exit 2 first |
| `G1b` | missing deep dossier | 5/5 exit 0 | services ≥3, SEO title + ≥3 keywords, content index ≥3 |
| `G2` | uncited positioning | exit 0 | 5/5 axes cited + annotated; 10 matrix rows resolve |

---

## 4. Competitor research (P1)

Five real competitors, 23 snapshot-locked pages, each dossier put through an independent
falsification pass.

| Competitor | Type | Positions on | Published price |
|---|---|---|---|
| D4C Dental Brands | national DSO (B2B) | scale — 198 practices | none |
| Kids Dental Brands | 40+ practice network | scale — "50+ offices, 7 states" | none |
| American Pediatric Dental Group | regional, S. Florida | capability — 19 named providers | **$99** |
| Pediatric Dental Group | regional, Colorado | longevity — "since 1977" | hidden off-site |
| Boston Children's Hospital | hospital dept. (incumbent) | clinical authority | none |

---

## 5. What the P2 adversarial review returned

Four independent critics, each given a different lens and told to break the positioning.
**All four returned FLAWED. 19 blockers, 17 degrades, 9 notes.**

| Lens | Verdict | The finding that mattered most |
|---|---|---|
| Evidence | FLAWED | The "no competitor positions on fear" claim is **refuted by two of the five dossiers** |
| Strategy | FLAWED | Fear-first is a *conversion* wedge being sold as a *search* wedge — parents search "pediatric dentist near me", not the emotional job |
| Regulatory risk | FLAWED | The content bible has **no rule about sedation, nitrous oxide or general anaesthesia** — on a site positioned around child anxiety |
| Completeness | FLAWED | Two of the five "competitors" are B2B DSOs that don't compete for patients, so every "X of 5" count uses the wrong denominator |

### The refutation, specifically

The positioning claimed *"none of the five competitors positions on a child's fear"*. Our own
snapshots say otherwise:

- **Boston Children's** publishes a parent-facing video, *"How can I make dentist visits less scary
  for my child?"*, and offers *"sedation for healthy patients who have anxiety"* — explicitly
  separating anxious-but-healthy children from medically-complex ones, the exact distinction the
  plan said they never make.
- **Pediatric Dental Group's** homepage promises *"caring guidance that eases fears and builds
  confidence"* and a *"stress-free"* visit, with a parent testimonial reading *"He's a high anxiety
  kiddo and they are great with him."* **Its dossier recorded none of this** — an upstream P1 defect
  inherited without re-testing.

Three further corrections propagate backwards into P1: PDG's `/first-visit` page, its
`MedicalBusiness` schema, and its technical-hygiene grade were all logged wrongly.

### The wedge isn't dead — it's narrower

Comfort language is near-universal across the set. But nobody **leads** with it, and nobody
**operationalises** it: no named protocol, no pre-visit process page, no anxiety-specific proof.
That remains a real position — honestly argued this time.

### Why the gate stayed shut after approval

The owner approved the positioning. The review was already running when that approval arrived, so
the flag was **held rather than flipped** — approving on information under active check is a race
condition, not consent. The findings landed minutes later and vindicated the hold.

---

## 6. Two bugs found in the skill itself

Both are the same species: path-contract drift between the scripts and the documented output layout.
**Reported, not patched** — `.claude/rules/04-code-modification.md` requires owner sign-off for code
changes.

1. **`snapshot-site.sh`** — the internal-link extractor drops asset URLs by file extension but does
   not strip `?ver=` query strings first, so `style.css?ver=10.0.6` survives as a "page". Its crawl
   found 5 real pages; the true count is 43. Routed around by extracting the page list from the
   fetched HTML directly.
2. **`dashboard-gen.mjs:63`** — the P0.0 detector tests for `<slug>/EXISTING-A-MODEL.md` (uppercase,
   slug root), but the skill writes `_spec/existing-a-model.md` (lowercase, in `_spec/`). The P0.0
   row therefore never turns green even when the phase is complete. Cosmetic; P0's row is correct
   because its detector reads manifest flags rather than filenames.

---

## 7. What unblocks the most work

1. **Real practice name and city** — drives local SEO, the category line, and every title/meta pair.
2. **Children only, or adults too?** — the source site contradicts itself (a paediatric homepage
   over an adult general-dentistry services page). This decides the entire information architecture.
3. **Real fee structure and accepted insurers** — the $50/$70/$90 monthly "packs" cannot ship.
4. **Real clinicians** — names, qualifications, registration numbers, consented photography.
5. **Anything in `_inbox/`** — rate card, brand book, photos, transcripts. Supplied material
   supersedes everything derived from the crawl.

Also outstanding: **image rights.** All 106 crawled assets are theme-bundled stock. A theme licence
does not transfer image rights to an end client — assume none are usable.

---

## Why the spec itself isn't published

The prep artifacts live in a private workspace. Two reasons they stay there:

1. The spec tree is excluded from version control by design, and
2. the bulk of what sits on disk is ~18 MB of **third-party content** — 43 pages of AxiomThemes'
   site, 106 of their stock images, and 23 scraped competitor pages. None of it is the client's work
   product, and the audit above specifically flags those image rights.

This report carries the findings without redistributing the material they were derived from.
