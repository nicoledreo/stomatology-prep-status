# Stomatology — children's dentistry site prep

**Status as of 2026-08-24.** Run of the `client-site-prep` skill against
`https://stomatology.axiomthemes.com/childrens-dentistry/`.

| | |
|---|---|
| Phases closed | **5 of 19** (P0.0, P0, P1, P2, P3) |
| Current phase | **P5 — SEO enrichment**, unblocked 2026-08-24 |
| Owner gates passed | **2 of 4** — P2 positioning (Rev 3), P4 site plan (6 pages) |
| Gates verified | 6 — G0, G1, G1b, G2, G3, G4 — each run against the real files, with negative controls |
| Skill bugs found + fixed | **4** (+2 more reported, 1 patched on request) |
| Spec root | `Code/client-site-prep/stomatology/_spec/` *(gitignored — see the last section)* |

---

## 1. The finding that shapes everything

**The client's "current site" is a WordPress theme demo published by AxiomThemes, not an operating
practice.** Every business fact on it is vendor filler: the address resolves to Berlin, the phone
carries a `+1` country code in European digit grouping, the testimonials are invented people, the
awards table is fabricated, and roughly two-thirds of the body copy is lorem.

Everything downstream follows from that. There is no first-party truth to build on, so the prep
runs on a strict split: **competitive evidence is grounded and snapshot-locked; client evidence is
absent and must never be invented.**

---

## 2. Phases

### Prep — `client-site-prep`

| # | Phase | State |
|---|---|---|
| P0.0 | Supply & audit | **done** — 43 pages crawled, Existing-A model built |
| P0 | Intake & rails | **done** — filled with visibly-placeholder values (see §6) |
| P1 | Market research | **done** — 7 competitors, 30 snapshot-locked pages |
| P2 | Positioning | **done, Rev 3** — owner-approved after two rewrites |
| P3 | Architecture / IA | **done** — 6 nav nodes, 3 reserved, 43-page reconciliation |
| P4 | Page list | **done** — 6 pages, owner-approved 2026-08-24 |
| P5 | SEO enrichment | **next** — unblocked |
| P6 | Typed content briefs | pending (owner gate) |
| P7 | Readiness verdict | pending (owner gate) |

### Build — `client-site-build`

Not started. Blocked on P7.

---

## 3. What the positioning went through

The wedge was rewritten twice, both times because verification refuted it — not because taste
changed.

**Rev 1 — "fear-first."** Refuted. The claim was that no competitor positions on a child's fear.
Adding the missing solo-practice class killed it: one competitor carries 33 verbatim fear/comfort
strings, a named behaviour technique, a dedicated comfort page, parent-coaching about the parent's
own fear, **and** a published CDT-coded fee table. Fear language is table stakes, not a
differentiator. Rev 1's second-best wedge, cost transparency, died to the same competitor.

**Rev 2 — "decide before you call."** Survived on evidence, then failed a different check. It was
built on four decision inputs — cost, location, insurance, first visit. Its own companion document
forbids two of them: the content bible holds every price figure and every insurance list while the
regulatory jurisdiction is unknown. A grep of Rev 2 for any reference to that halt returned one
incidental hit. The plan had never reconciled against the rules it inherited.

**Rev 3 — same wedge, honest staging.** The wedge is unchanged. What changed is what can ship:
cost, insurance **and** language access are all staged — designed and reserved in the IA, marked
held, released only by a named amendment. Two wedges ship without owner data at all: findability
(correct schema, heading integrity) and an information architecture that is unambiguously for
children.

**An unresolved contradiction is recorded, not papered over.** The bible mandates a
sedation-disclosure sentence on every page addressing a frightened child, and separately holds all
sedation language while the jurisdiction is unknown. The mandated sentence is itself held. Any
fear-facing page is currently undeliverable, and that is written into the plan with its unlock
condition rather than absorbed.

---

## 4. A correction the agent owes the record

At one point the recommendation was to adopt **"United States"** as a working jurisdiction, on the
stated basis of "USD pricing and NANP phone format." **Both signals failed verification.**

- The literal token `USD` appears **0 times** in the text corpus. `$` is shared by CAD, AUD, NZD, SGD.
- The phone's `+1` is a NANP country code, but its **3-3-2-2 grouping is continental-European**,
  not NANP's `(NNN) NNN-NNNN`. European formatting had been described as "NANP format."
- Meanwhile **"Berlin" appears in 42 of 43 pages**, with a complete postal block. The broadest and
  most specific signal points the other way.

Worse, the content bible's own evidence table listed **five** "crawl signals" when only three come
from the crawl. Two of them — an orthography signal and a payment-model signal — were the prep's
**own vocabulary and its own fallback**, cited back as client evidence. Zero hits for either across
all 43 text files and all raw HTML snapshots.

The table has been corrected, the two false rows struck with their reasoning preserved, and the
jurisdiction left **undetermined** — which is what the rules said all along.

---

## 5. Skill bugs found and fixed

Running the skill hard surfaced defects in the skill itself. All fixes were made with explicit
permission and verified by the full smoke suites.

| # | Bug | Status |
|---|---|---|
| 1 | Dashboard tested only a legacy uppercase path, so P0.0 read "pending" forever | **fixed** — real path added, legacy kept |
| 2 | Site-plan preview fabricated a phone number in the **owner-facing** artifact | **fixed by redesign** — see below |
| 3 | G4 was registered on `Write` only, so an `Edit` bypassed page-list reconciliation entirely | **fixed** |
| 4 | G4 compared page **counts** but never **membership** | **fixed** |
| 5 | Two owner-approval gates mis-substituted `$&` when reconstructing an edit | **fixed on request** |
| 6 | Snapshot script's asset filter didn't strip query strings | reported, not patched |

**On #2, which is the instructive one.** A bare digit-run scan published a fabricated contact
number four separate ways: an ISO build date, a section reference, a warning-marked held
placeholder lifted out of a YAML comment, and finally the struck theme-demo number itself. Each
new guard simply advanced the scan to the next bad candidate — because a spec document's *job* is
to record struck and held values, so a digit scan over one will always find something, and
everything it finds is wrong. The fallback was deleted rather than guarded again: contact details
now come only from a declared `tel:`/`mailto:` link or an explicit key, and otherwise render as
held. A regression test covers all three shapes.

**On #4.** The membership check immediately failed the skill's own test suite. Its "pass" fixture
paired an inventory of twelve named pages with a sitemap of twelve **differently** named pages —
they agreed on the count and shared not one page name. It had passed for as long as it existed,
because only counts were ever compared. The fixture was the hole in miniature.

---

## 6. What "filled" does and does not mean

The intake is now fully populated, and **none of it is owner data.** Every unknown carries a
visible ⚠ marker naming what is needed — never a plausible substitute. A wrong address is worse
than no address, because it survives review by looking finished.

`owner_intake_reviewed` remains **false** and is recorded as such. A filled form is not an
answered one.

Two things still gate real content:

1. **Owner data.** Practice name, location, clinicians, service menu, fees, contact details — all
   unknown. The pages are structurally complete and factually empty.
2. **The jurisdiction.** Until it is named by the owner with a qualified adviser's countersignature,
   cost, insurance and language access stay held, and no page may address a frightened child.

---

## 7. In flight at time of writing

A verification pass is still running against four owner-facing defects found by the placeholder
audit: currency prompts that survive in the intake **template** (so regeneration restores them),
two invented example names that reached a spec file, an unsupported claim about one crawled page
that was labelled "verified," and a testimonial roster whose count doesn't match its own list.

**None of those four is fixed yet.** They are listed here because a status report that omitted
them would be the exact failure this project keeps catching.

---

## Why the spec isn't in this repo

`Code/client-site-prep/` is gitignored. The spec contains the full competitive research — 30
snapshot-locked competitor pages and seven dossiers — plus the positioning that derives from it.
That is client work product and third-party content, and it does not belong in a public repository.

What is published here is the **status and method**: what was done, what was verified, what was
refuted, and what remains open. The artifacts themselves stay private.
