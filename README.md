# Stomatology — children's dentistry site prep

**Status as of 2026-08-25.** Run of the `client-site-prep` skill against
`https://stomatology.axiomthemes.com/childrens-dentistry/`.

| | |
|---|---|
| Phases closed | **8 of 19** (P0.0 → P6) |
| Current phase | **P7 — readiness** — template conversion through **8 adversarial rounds**; build unblocked, final verdict pending |
| Owner gates passed | **3 of 4** — positioning (Rev 3), site plan (6 pages), content/claims briefs |
| Gates verified | 9 — G0 → G7 plus the build's CTA-singularity gate — each run against the real files, with negative controls |
| Skill bugs found + fixed | **8** — all verified; all 8 were wiped by a redeploy and restored |
| Adversarial reviews that returned FLAWED | **13** — every one caught something real; see §4, §7, §11, §12 |
| Spec size | 6 briefs, ~654 KB, 41 sections, **474 swap markers**, 179-name derived index |
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
| P5 | SEO enrichment | **done** — six rows, G5 green, three §0 blockers closed |
| P6 | Typed content briefs | **done** — six typed briefs, G6 green, owner-approved 2026-08-25 |
| P7 | Readiness verdict | **committed NO-GO** — 21 blockers; 9 agent-clearable in progress |

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
| 7 | G6 registered on `Write` only — same Edit bypass as #3, on the brief gate | reported |
| 8 | G5 accepts a 301 pair with a status token on only **one** side | reported |

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

## 7. Owner-facing defects — found by audit, now closed

The placeholder audit found four defects in the artifacts the owner actually reads. All four are
fixed, and the fix pass surfaced two more:

| defect | resolution |
|---|---|
| Currency prompts (`USD, GBP, EUR…`, a `"from $X"` exemplar) suggested to the owner | fixed **in the template**, so regeneration cannot restore them |
| Two invented example names reached a spec file | removed |
| An unsupported claim about one crawled page, labelled "verified" | corrected — that page carries **0** of the markers claimed, while two sibling pages carry 11 and 9 |
| A testimonial roster whose count didn't match its own list | corrected — see below |
| *(found during the fix)* a comparative-pricing promise, template-resident | removed from template and artifact |
| *(found during the fix)* a banner contradicting five of its own fields | reworded |

**On the testimonial count.** The document said "seven" and named six. The correction brief handed
to the agent said "determine whether it is six or seven." The true figure, counted from the
snapshots, is **15 instances carrying 8 unique names across 5 pages** — so the original was wrong,
and *the correction brief was also wrong*. It was caught only because the agent counted from source
instead of accepting either number on offer.

Regeneration was then verified end-to-end: template and generated artifact are both clean, and
running the generator twice produces byte-identical output.

**Still genuinely open:** the practice's own data, and the jurisdiction. Both need a human.

---

## 8. P5 — SEO enrichment: gate-green, not finished

The six-row SEO table clears **G5** on the first attempt. Measured independently, twice, with two
different engines rather than taking the authoring agent's numbers: titles 48–55 characters against
a 60 ceiling, metas 131–147 against 160, and the primary keyword at index 0 on every row against a
30-character window. The 301 ordinance reconciles exactly — 18 mapped, 1 with no target, 24 dropped,
43 total.

**It is still not finished**, because passing the gate and being correct are different things.

**Three §0 blockers, found by the compliance audit:**

1. **The children's-dentistry claim, asserted without its receipt — for the third time.** The
   content bible permits that claim only against the owner's confirmation of the service mix, which
   does not exist. It appears in 6 of 6 titles, 6 of 6 metas and 5 of 6 keywords. The file
   *discloses* the ambiguity and then resolves it in favour of the copy — and §0.7 says ambiguity
   resolves *against* the copy, every time. **Disclosure is not compliance.**
2. **False provenance.** Four metas state that content "is owner-supplied." Nothing is: the audit
   record reads "owner_supplied — NONE SUPPLIED," and the intake-reviewed flag is false. One row
   phrases it correctly, which is how we know it's a slip rather than a convention.
3. **Service mix asserted while the menu conflict is open** — the crawled services page advertises
   ten general and adult treatments.

**Why the first one matters most.** That same claim was caught and removed from the intake, then
caught again in the page inventory, and has now appeared in the SEO. It keeps returning because the
project *is* about children's dentistry and every author reaches for it. It is a systemic pull, not
three coincidences, and it is only caught because something adversarial reads every artifact.

**Two more gate holes**, found by negative control rather than inspection:

- A 301 pair carrying a status token on only *one* side passes. Deleting the target-side token and
  leaving the source-side token exits 0 — so half of every pair in the file is unenforced.
- The ordinance scanner skips any line without a path, so it covers 42 of 43 lines.

**And a self-reported trap worth recording.** The titles are measured with placeholder tokens in
place, and headroom to the 60-character ceiling is only 12/6/6/5/10/6. A real city plus a real
practice name is around 29 characters combined — which **breaks four of the six titles.** These
titles pass the gate today and will fail it the moment the placeholders are substituted. The
authoring agent volunteered that; a less honest file would have banked the green.

---

## 9. P6 — six typed content briefs, owner-approved

All six briefs authored and passing **G6**: `index` 12 sections, `team` 8, `faq` 8, `services` 7,
`about` 6, `contact` 4 — every count inside its type's window, zero duplicated fact-owners, zero
broken internal links. The owner signed them off on 2026-08-25 against a rendered claims preview
carrying **293 claim lines and 227 owner placeholders** — a ratio that is itself the honest picture
of where this spec stands.

**The same defect recurred a fourth time, and this round finally found its root.** An audience-worded
phrase kept reappearing in different artifacts. It was not authors reaching for it: the phrase was
baked into a **navigation label written at P3**, before the claim was ever ruled on, and every
artifact that renders nav labels inherited it. Renaming the label at source, then propagating to all
seven carriers, closed it.

**And it exposed something structural: no gate compares labels.** The IA gate checks that each
navigation row cites a source. The page-list gate reconciles counts. Neither compares label *values*
across artifacts — so every downstream copy could contradict the source of truth while every gate
stayed green, and they all did. That claim was never caught by machinery; it was caught four times by
an adversarial reader, which is not a control that scales.

---

## 10. P7 — a committed NO-GO, and why that is the right answer

The readiness verdict is a **NO-GO**: not cleared to build, **21 blockers**. The handoff gate refuses
the kickoff and prints the count, which is the gate working rather than failing. The same gate was
run in the opposite direction with a synthetic clean manifest and returned a pass — proving it
discriminates rather than always blocking.

**What a build today would produce: nothing.** The build stops before writing its first file,
because six of the twelve required handoff documents did not exist.

**The finding that matters most is about placeholders.** Filling every unknown with a visible marker
was right *for the spec* — it is how fabrications stayed out. But the build has an honesty gate whose
banned-content list contains that very marker, commented *"must never reach the visitor."* Proven by
execution against the real briefs, with clean controls. **The placeholder register is a spec
instrument, not a render instrument**, and that reclassified two more pages to blocked — all six.

Worth recording: the first attempt to verify this returned a pass, and it was **fail-open** — the
gate had exited early on an out-of-scope path. An unengaged gate is not a passing gate, and it was
very nearly reported as a refutation.

**Two defects in the verdict's own reasoning**, caught by an adversarial challenge: the arithmetic
did not derive — it printed one total while its own chain produced another, because a finding was
counted twice — and a shopping-list item told the owner to obtain a five-field declaration **without
saying what the five fields are**. Both corrected; three independent derivations now agree.

The verdict refuses euphemism, including against itself: *"There is no owner data. Not 'some gaps' —
none."* And it names the worst credible outcome squarely: **a team page showing three strangers
presented as the practice's clinicians** — the single most damaging thing this project could ship.

**Current state:** the 21 blockers split into 8 needing owner data, 4 needing a doctrine ruling, and
9 the agent can clear alone. The nine are in progress; four of the missing handoff documents have
already landed. The owner has scoped the remainder as a **template build** — see §11, which is where
that decision stopped being a footnote and became the shape of the work.

---

## 11. The re-scope: from *honest and empty* to *honest and finished*

Everything above optimised for one thing: never assert what nobody had confirmed. The visible `⚠`
marker was how that discipline was enforced. It produced a spec that was completely honest and, as a
website, completely unfinished-looking.

The owner then supplied the missing piece of context — **this is a template**, and real practice
information replaces the placeholder content when it arrives — with a specific instruction:

> *"i don't want the placeholders to be visibly and obviously swappable in the actual site build
> (i.e. blank images, lorem ipsum text etc), i want it to look like a finished site with complete
> info."*

That is not a request to lower the bar. It changes which artifact is being built, and the safety
argument has to be re-derived rather than repeated.

### Why the objection genuinely doesn't apply — and where it still does

The danger in invented content was always **false attribution**: a fabricated clinician is a real
person's name on a practice they don't work at; a plausible telephone number is one a parent
actually calls. **A template is not published as anyone's practice, so it attributes nothing.**
Every commercial site template ships realistic demo content — that is how a design gets evaluated.

But that argument covers *identity*, not *evidence*. So the line was redrawn rather than erased:

| | |
|---|---|
| **Identity, structure, copy** — name, address, services, FAQ answers, the about story | realistic template content |
| **Proof** — testimonials, ratings, review counts, awards, statistics | **still prohibited, under every scope** |

A fabricated review is a lie about other people's experiences, and no scope makes it not one.

### The build gate turned out to answer the question exactly

Rather than guessing at the honesty gate, it was read at source, and two mechanics decided the whole
design:

1. It computes visible text by **stripping HTML comments first**, with the source comment reading
   *"placeholders/markers in a comment are INVISIBLE to the visitor."* So a swappable marker in a
   comment is invisible to the visitor **and** to the gate.
2. It is **brief-driven**. It only forces a visible *"representative example"* label onto a section
   whose brief marks it as fabricated proof. A section not so marked carries no such requirement.

So realistic copy plus comment markers is not a workaround — it is the sanctioned path. And the only
content the gate would have forced an ugly visible label onto was proof, which is exactly the
content that was prohibited anyway. **The two rules met in the same place.**

### The design call: omit the proof, don't label it

A finished dental site with no reviews section is completely ordinary. A site showing
`★★★★★ — representative example` is visibly broken *and* still displays a fake review. So every
proof block was deleted outright — proof strips, data points, persona proof, proof logos — rather
than shipped with a disclaimer.

**Verified, live, this pass:** all fabricated proof gone from all six briefs; all six of the gate's
fabricated markers at **zero**; **G6 exit 0 on all six briefs** and **G4 exit 0** on the page
inventory and sitemap — each with asserted payload byte counts and four negative controls, including
two that confirm the fail-open traps rather than assuming them. Three briefs now sit *exactly* on
their type-window floor, so nothing further can be deleted.

### The mistake worth publishing: a shared value with no owner

The conversion was run as two agents working **in parallel** — one on the page inventory, one on the
briefs. Both finished green. Both passed their own gates. The adversarial verifier returned
**FLAWED** on the first line of its report:

> *"THE SITE HAS TWO IDENTITIES."*

Each agent had independently invented a practice name, city, address, phone and email — and written
them into files that **cross-reference each other**. Every brief pointed at a register that declared
different strings. A build reading both would emit a site whose wordmark disagrees with its own body
copy: the single most obviously-unfinished thing a page can do.

No gate caught it, and no gate *could* have. G4 checks that page counts reconcile. G6 checks section
counts, ownership and link resolution. **Neither compares a value in one file against the same value
in another.** This is the second time in this project that class of hole has appeared — the earlier
one let a struck claim survive in seven downstream files because no gate compares nav *labels*.

The failure was not agent judgment. It was **a shared value with no owner**, and the fix is
structural, not a matter of trying harder: the canonical identity is now decided up front in a
single file that every agent reads and none may override, and the repair runs *sequentially*.

The general lesson, which generalises past this project: **never fan out concurrent agents over
files that reference each other's invented values.** Parallelism is safe for independent work and
quietly corrupting for shared state.

### Two more things the verifier caught

**Blank images were still blank, just restyled.** Every image slot on every page specified *"a flat
brand-coloured panel or a neutral non-representational field."* That is the owner's stated problem
wearing a nicer outfit. Replaced with real imagery — and, for team cards, **monogram avatars rather
than generated faces.** A generated face misattributes nobody, but it is still a photograph of a
human presented as this practice's staff, and every one would have to be hunted down when the real
team arrives. A monogram reads as a deliberate design choice and degrades honestly.

**Three instructions still built the old page.** The worst was on the homepage, which was still told
to *"mark every unfinished slot as unfinished"* so that *"nothing on it is mistaken for finished"* —
the flat opposite of the re-scope, on the front door.

### Two judgment calls recorded rather than buried

**Register-gated role words.** The page inventory proposed *Practice Principal* and *Associate
Dentist*; the briefs barred that whole family, since a role word that may be a protected title in an
undetermined jurisdiction fails closed. Two internal rules conflicted, and **the stricter one
governs** — that is what fail-closed means. The team page carries functional roles only.

**The one imperfect value, flagged not hidden.** The template email uses the IANA-reserved
`.example` TLD, which a careful reader may clock as non-real. Every alternative that reads perfectly
finished is a domain someone may own, and mail sent to it would reach them. **Misrouting a real
parent's email to a stranger is the worse failure than an odd TLD**, so the reserved form stands —
as an explicit owner decision, not a default. The address and phone needed no such compromise: a
fictional city and the reserved `555-01xx` range render as ordinary finished details that
*structurally cannot* reach a real practice or a real line.

### Where this stands right now

The repair pass — one identity, real imagery, stale instructions struck, roll-up regenerated — is
**running, not finished**, and a second adversarial round will report on it before anything is
called done. Published here as in-flight rather than as a result.

---

## 12. Eight rounds: what it took to make "finished" true

§11 recorded the re-scope as a decision. This is what executing it actually cost — **eight rounds,
seven of which came back FLAWED on adversarial review.** That ratio is the point, not an
embarrassment: every one of those seven caught something that would otherwise have shipped.

### The build was blocked, and the gate was right

Five of the six pages **could not be written at all**. The build's CTA-singularity gate refused
them:

```
chrome closing band + a body closing-CTA section
  -> exit 2  "MORE THAN ONE closing / quote-CTA band on the FULL page"
```

Read at source, that gate exists because of **a failure that already shipped once**: a live build
put two closing conversion bands on top of each other, because the old check inspected only the page
body and never saw the site chrome. Our briefs each named their final section `final-dual-cta`,
`cta`, `final-cta`, `closing-cta` — every one matches the gate's class patterns. Plus the mandatory
chrome band, that is two. The gate was correctly refusing to repeat a known failure.

The obvious fixes were both bad. Deleting those sections broke three type-window floors
(index 12→11, team 7→6, about 5→4). Waiving the chrome doctrine meant discarding the rule that
exists because of the original bug.

**The third option worked: rewrite, don't delete.** A brief needs its section *count* — it does not
need that section to be a CTA band. Each became real content with a non-CTA class:

| page | was | now renders |
|---|---|---|
| index | `final-dual-cta` | *Inside the practice* |
| about | `cta` | *When we are open* |
| team | `final-cta` | *Asking for someone by name* |
| services | `closing-cta` | *Where the work happens* |
| faq | `closing-cta` | *Before an appointment is arranged* |

Every count unchanged, no doctrine waived, verified against the real gate with asserted payload
bytes.

### The defect nobody asked about, found while fixing that one

Five briefs specified a closing CTA in the page **body**. **Not one specified the chrome band that
actually renders on every page.** The site's single most prominent ask — its heading and its verb —
would have been the build's to invent. Now specified once, reusing the existing marker name rather
than minting a new one.

### The one dishonest string this spec was on course to publish

The build doctrine **mandates a risk-reversal / guarantee line** in that same band. The content
bible **holds every guarantee** (jurisdiction undetermined). Because the spec never enumerated the
band, the build would have written that line **itself, unreviewed**.

Resolution: **no guarantee line is written.** The slot renders nothing, emits no marker, and the
hold is recorded in three separate places so the gap cannot be filled by invention. A doctrine about
design quality does not lift a content hold.

**The general lesson, and it generalises past this project: an unspecified slot inside a mandated
band is not an absence. It is a blank cheque written to whoever builds the page.**

### The recurring failure, finally named

The same defect kept coming back in new clothes, and the eighth round produced the sentence that
explains all of them at once:

> **A defect fixed at its slot instead of in its class survives wherever the class also lives.**

- Two agents each invented a practice identity → *the same value with no owner* (§11)
- Then invented staff names against a register that forbade them → *same shape, different slot*
- Then four competing label sets for the same destinations → *same shape, in link labels*
- Then the same room called two different things on one page → *same shape, in nouns*
- A held vocabulary word fixed on the staff cards, missed in a pillar two sections down

No gate catches any of it. Structural gates reconcile counts, sections and link resolution — **none
compares a value in one file against the same value in another.**

### What the copy pass had to survive

Writing ~225 body strings is where fabricated proof enters a project. It did not.

**Zero** across fifteen categories — testimonials, ratings, review counts, awards, accreditations,
statistics, head counts, years-in-practice, bare years, outcome figures, superlatives, credentials,
protected titles, prices, insurance vocabulary — each verified with a **live negative control**
proving the sweep fires on an injected fake.

Three capability claims were caught and removed: two named clinical procedures that the unresolved
service menu does not establish, and one that had crept back in from a *withdrawn* menu. Plus the
sharpest catch of the run — a room noun that, on one regional reading, **names an operation.**

Also fixed: a roll-up manifest carrying **24 stale measured values while asserting in writing that
they were freshly recomputed from disk.** Staleness is a bug. A false claim about your own
verification is worse, because it is the thing a reader trusts *instead* of checking.

### The honest gaps, stated plainly

**The team page is the largest.** The nav, the page heading and the tab title all promise *who you
will see* — and the page carries a practice manager, a treatment coordinator and a reception lead.
**Zero clinicians.** Every clinical slot renders empty by design, because inventing one is the single
most damaging thing this project could ship. As a template that is a deliberate hold. For a real
practice it needs real register entries.

**The service menu.** Four template services with descriptions. The real menu is unresolved, and at
the moment of swap an unswapped template menu becomes a false statement about what is offered.

**The swap index has no gate behind it.** Making placeholders invisible to the visitor makes them
invisible to a careless reader too. The obligation that replaces the visible marker — *grep the
build tree for swap markers before publishing; it must return zero* — is prose, and depends on a
human running it. Recorded as a known weakness rather than discovered later.

### Still open

The proposed fix for the gate that blocks the readiness verdict passed its **fifth** adversarial
attack (three earlier designs were each broken by execution, not argument). It needs changes to a
gate and to hook configuration, so it sits as a **proposal awaiting the owner** — this project does
not modify code without explicit permission.

P7 is **not closed.** The manifest that would say so is written last, from measured state, once the
final adversarial verdict lands. Given seven FLAWED rounds out of eight, writing it early is exactly
where that habit would cost something.

---

## Why the spec isn't in this repo

`Code/client-site-prep/` is gitignored. The spec contains the full competitive research — 30
snapshot-locked competitor pages and seven dossiers — plus the positioning that derives from it.
That is client work product and third-party content, and it does not belong in a public repository.

What is published here is the **status and method**: what was done, what was verified, what was
refuted, and what remains open. The artifacts themselves stay private.
