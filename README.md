# Stomatology — children's dentistry site prep

**Status as of 2026-09-01.** Run of the `client-site-prep` skill, and now
`client-site-build`, against
`https://stomatology.axiomthemes.com/childrens-dentistry/`.

Every count in the table below was re-derived from disk when this entry was written, rather than
carried forward from the last one. That is worth stating plainly, because during the audit that
produced this entry **the spec tree changed underneath the measurement**: a manifest that had been
unparsable was repaired mid-pass, and the phase count moved with it. Two readings taken twenty
minutes apart disagreed, and the second one is what is published here. These numbers are true as of
their derivation, not for all time — which is the same lesson §13 records about the spec's own
manifests, arriving this time in the status record itself.

| | |
|---|---|
| Phases closed | **10 of 19** by the project's own generator, run against the live folders. Step 1 is done in substance and the counter misses it: its probe reads the slug root while every other step reads the spec folder one level deeper |
| Current phase | **Page composition.** All six page bodies are built. They carry no chrome yet, by design |
| Owner gates passed | **4 of 8** canonical gates — intake, positioning, site plan, content/claims briefs. The remaining four (feel, system, chrome, flagship page) are all downstream. Three further owner decisions were taken outside that list: the GO acknowledgement, the visual direction, and the brand card |
| Verdict | **GO at TEMPLATE scope** — re-tiered, not discharged; see §14 |
| Blockers | **0** at template scope · **8** at launch scope, per the census evidence file that derives them and names the eight rows. Both are published — but **not cleanly**: the manifest carries `blocker_count_at_launch_scope` **twice**, as 8 and again as 10, and every conforming JSON parser takes the last, so a machine reading that file gets **10**. See §14. The gap to template scope is the owner debt |
| Gates verified | 20+ across prep and build, each driven live with negative controls. Four found fail-OPEN and reported as such |
| Skill bugs found | **10** — but *fixed* does not hold for all of them today, and this row used to claim it did. Bug 1 (§5) is **still open on disk**. The BL-23 gate patch that §13 records as applied and verified has been **reverted off disk** — the file is back to its pre-patch byte count and pre-patch hash, so that deadlock is live again (§14). The newest is a gate that cannot see the file its own skill writes (§14) |
| Adversarial reviews that returned FLAWED | **22** — every one caught something real; see §4, §7, §11, §12, §13, §14 |
| Spec size | 6 briefs, **906,948 bytes** and **613 swap markers**, both re-measured from disk for this entry. The previous row published "~700 KB, 41 sections, ~480 swap markers" — all three had gone stale, and the section figure also disagreed with §9's own enumeration, which sums to 45. Derived index regenerated from disk |
| Spec root | `Code/client-site-prep/stomatology/_spec/` *(gitignored — see the last section)* |
| Build root | `Code/client-sites/stomatology/` *(gitignored — same reason)* |

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
| P0.0 | Supply & audit | **done in substance** — 43 pages crawled, Existing-A model built at `_spec/existing-a-model.md`. The dashboard still scores it **pending**, and the cause is now pinned: its probe reads `<slug>/` where every other phase reads `<slug>/_spec/`, so it misses a file that is there (§5 bug 1) |
| P0 | Intake & rails | **done** — filled with visibly-placeholder values (see §6) |
| P1 | Market research | **done** — 7 competitors, 30 snapshot-locked pages |
| P2 | Positioning | **done, Rev 3** — owner-approved after two rewrites |
| P3 | Architecture / IA | **done** — 6 nav nodes, 3 reserved, 43-page reconciliation |
| P4 | Page list | **done** — 6 pages, owner-approved 2026-08-24 |
| P5 | SEO enrichment | **done** — six rows, G5 green, three §0 blockers closed. Worth recording: `_spec/seo-manifest.json` was **unparsable JSON** for part of this audit, so the generator scored P5 *pending*; it was repaired mid-pass and now reads clean |
| P6 | Typed content briefs | **done** — six typed briefs, G6 green, owner-approved 2026-08-25 |
| P7 | Readiness verdict + handoff | **done** — **GO at TEMPLATE scope**; 12 files copied under checksum |

### Build — `client-site-build`

| # | Phase | State |
|---|---|---|
| P7.5 | Asset intake + tonal lock | **done** — 9 generated template images; 106 crawled files quarantined (§14) |
| P8 | Design-system instantiation | **done** — brand card "Instrument" stamped, token sheet locked, grafted and independently verified (17 colours, all traceable to the picked concept, none invented) |
| FEEL | Feel confirm (owner) | **done** — three directions offered after the first was called too flat, each measured; the owner picked C "Low Light" |
| SYSTEM | Token lock card (owner) | not started — held by FEEL being stamped |
| P9 | Global chrome (owner) | **not started, and deliberately so.** The header, footer, navigation and the single closing CTA band are drawn ONCE against finished page bodies rather than guessed at first. This is why links between the six previews do not resolve |
| P10 | Pipeline setup | not started |
| P11 | Content + proof to briefs | not started |
| P12 | Page build | **six page BODIES composed**: home, services, about, team, questions, contact. Not yet assembled into real pages, and not yet adversarially verified: that pass is batched to the end at the owner's instruction |
| P13 | Mobile + revision loop | not started — the owner's per-page revisions land here |
| P14 | Final QA + publish | not started |

---

## 3. What the positioning went through

The wedge was rewritten twice, both times because verification refuted it — not because taste
changed.

**Rev 1 — "fear-first."** Refuted. The claim was that no competitor positions on a child's fear.
Adding the missing solo-practice class killed it: one competitor carries dozens of verbatim
fear/comfort strings, a named behaviour technique, a dedicated comfort page, parent-coaching about
the parent's own fear, **and** a published fee schedule. Fear language is table stakes, not a
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
| 1 | Dashboard tested only a legacy uppercase path, so P0.0 read "pending" forever | **still open** — re-checked for this entry: the generator probes only `EXISTING-A-MODEL.md`, `intake-completed.md` and `CLIENT-INTAKE-PREFILLED.html` at the prep root, while the file on disk is `_spec/existing-a-model.md`. This row previously read "fixed — real path added". That was wrong |
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

## 13. Rounds 9–14: the deadlock broke, and the record turned out to be the harder problem

§12 ended with the build unblocked and the verdict pending. Six more rounds followed. Blockers went
**21 → 13 → 6 spec-fixable**, total **21 → 10**, and every one of the ten now needs the owner rather
than more agent time.

### The gate that demanded a fabrication is fixed — with written permission

The standing deadlock: a gate counted 106 crawled *theme* images as "the intake supplied proof",
then required three proof categories marked *present* — on a project with **zero** proof. The only
way to satisfy it was to assert proof that does not exist.

Five remedies were designed. **Three were broken by execution, not by argument** — each added a
declaration the author writes about their own work, and a declaration the author controls is cheap
to write falsely. The fourth relocated the check instead of teaching it provenance, and survived.

The owner gave explicit permission, and it was applied. Measured across **all 130 registered
hooks**, against a 55,130-byte payload carrying the real 54,409-byte adverse verdict:

| write | before | after |
|---|---|---|
| **Adverse NO-GO verdict** | 1 gate exits 2 — *the deadlock* | **0** — the record can be written |
| **GO verdict** | 1 exits 2 | **1** — the proof requirement correctly re-arms |

> **This is a dated record of one run, and it no longer describes the disk.** Re-checked while
> preparing §14: the patched gate has been **reverted**. The file is back to its pre-patch size of
> 7,319 bytes and its pre-patch hash, and not one of the relocation markers survives. The deadlock
> is back. Everything below about how the patch was verified is true of the run it describes and
> false of the tree today — which is exactly the failure this section goes on to name.

Detection was proven **byte-identical** rather than eyeballed: the detection region hashes the same
in the pre-patch backup and the live file, `diff` empty, every difference confined to console
strings. Shipped smoke 5/0. Exactly two files changed under the tool directory.

**The asymmetry is the whole point.** An adverse finding must always be recordable; a *claim of
readiness* must still be policed. A gate that blocks you from writing down bad news is structurally
wrong however good its detection is.

**One deviation was disclosed rather than buried.** The proposal said to move the hook into an
existing block; no such block existed. The agent created one and rejected both alternatives *with
evidence* — registering it elsewhere would have blocked arbitrary shell commands (proven: exit 2 on
a plain `ls -la`), and editing another block's matcher would have silently changed the firing
surface of two unrelated hooks. It also caught that the config file's hash no longer matched what
the ruling recorded: the file had moved between ruling and apply.

### The artifact is close. The record about the artifact was the real problem.

By round 12 a pattern was unmistakable: each round reported 13–28 defects, and **almost none were
defects in the website.** They were manifests carrying stale hashes, status lines describing a state
the disk no longer had, and measurement sentences that were wrong.

The mechanism: every round wrote extensive *"verified this turn"* prose into the spec artifacts, and
that prose went stale the moment the next round edited anything. **The spec was documenting itself
faster than it could keep the documentation true.**

The proof it was structural rather than careless: three published measurements were wrong **and each
was labelled as freshly measured.** The claim of freshness was itself the stale part.

### Two attempts to end it — one worked, one was a counter wearing a checker's clothes

**What worked:** the manifests became **generated from disk**, not authored. A stale hash is now
impossible by construction instead of by diligence. Proven in place *and* in an isolated 27 MB copy,
with four mutation tests — including one that moved the **disk** rather than the manifest and was
still caught.

**What did not:** a "ratchet" meant to police measurement prose *counted occurrences* and never
re-derived any of them. So three briefs published a wrong character count, inside the ratchet's own
scope, **with the ratchet green**. One of the four titles happened to be correct, which is exactly
why counting looked adequate.

> **A checker that counts instances of a claim is not checking the claim.** It must parse the claim,
> recompute the value, and fail on mismatch — and it must report *unverifiable* as its own state,
> because a green that silently absorbs unverifiable claims is the same defect one level up.

### The defect that kept coming back, and finally got machine-enforced

*A defect fixed at its slot instead of in its class survives wherever the class also lives.* Round 13
found the sharpest instance yet: an illegal comment form was **reproduced, not described,** in 13
places — including inside **the checker's own header, in the paragraph warning against it.** Nine
further classes of the same shape were found alongside it.

It is now machine-enforced rather than written down: the checker refuses the struck form **on sight,
escaped or not**, and assembles its own detector name at runtime so the file can never carry the
form it refuses.

A boundary was drawn explicitly so the green is not over-read: the regex rows in the ban list are
**not** in that class, because a ban-list pattern is not a copyable page payload — converting them
would delete the ban list.

### Design went back to the drawing board, correctly

The first visual direction was rejected by the owner as *"too old / scrapbook"* — cream, tan, olive
and terracotta, which read as craft-heritage rather than clinic. That was the right call and a wrong
instinct on our side. Six modern directions replaced it, each a complete system with real swatches,
both typefaces set in specimen text and a working mini-page in the site's own copy. Three full
homepage layouts followed, deliberately rendered in one neutral skin so **layout is the only
variable**.

**And a verification failure worth publishing.** Seven contrast ratios were stated as fact with none
of them computed. All seven were wrong; the corrected figures changed the accessibility advice on
one option. On re-verification a *second* error surfaced — a number had been fixed while its label
still named the wrong background, which is just as false. Both are the same failure this project
keeps finding in its own record: **a measurement asserted with confidence and never actually taken.**

A near-miss followed: the first content sweep of the mockups reported *"6/8 detectors fire"* on its
positive control and nearly passed. Two classes were untested, so the sweep looked clean while
proving nothing. **A sweep not proven to fire is not evidence.**

### Where it stands

The spec's blocker list is down to **10, and 8 of them are owner-gated** — no jurisdiction
declaration, no intake, no photography, no clinician register entries, no ruling on the service
menu. Those are not agent work. `ready_for_build` remains **false** and is deliberately not being
flipped: that flag authorises a build, and it is a GO/NO-GO call for the owner, not for the process
that wants to finish.

---

## 14. P7 closed, the seam crossed, and the build started

Three days of work sit between this entry and the last one. P7 closed, the handoff crossed into the
build tree, and the build has now passed its first owner gate. The most useful things in this
section are the four places the process was wrong and something external caught it.

### The verdict changed without a single blocker being discharged

The last entry ended with **10 blockers, 8 of them owner-gated**, and `ready_for_build` deliberately
left `false`. That flag has now flipped to `true` and the verdict reads **GO**, and it is worth being
precise about why, because nothing was fixed to earn it.

The blocker census had been counting against a **launch** — a real practice, with a real address, real
clinicians and real photographs. The build that was actually authorised is a **template**: a complete,
honest, fully-designed site whose business facts are openly invented and marked for swapping. Those
are different questions, and eight of the ten blockers were only blockers for the first one.

So the census was made scope-aware and re-run. The rule it already carried, applied honestly to
closure targets read off disk: a finding counts as a blocker if and only if it is **open** and closing
it **edits a file under the spec root**. Three of them close entirely outside it — one in a settings
file, one in a skill amendment, one in neither.

| | Blockers |
|---|---|
| At **launch** scope | **8** — unchanged, every one owner-gated |
| At **template** scope | **0** |

Both numbers are published in the manifest, not just the convenient one. The gap between them is the
owner debt, and keeping it visible is the whole point: a single number would have let "GO" quietly
mean "nothing left to do."

**And then the manifest published the launch number twice, with two different values.** Found while
preparing this entry: `blocker_count_at_launch_scope` appears once as **8** and again, later in the
same file, as **10**. It is the only duplicated key in the manifest. Every conforming JSON parser
takes the last one, so any gate or script reading that file gets **10**, while the census evidence,
the manifest's own prose and this document all say **8** and name the eight rows. The derived figure
is 8; the 10 is uncorrected on disk as this is published.

**A number published twice is a number with no owner** — the same defect class this project has now
hit four times, arriving this round inside the very key that was written to stop a single number
hiding the truth. The check that would have caught it is the one this document keeps asking for and
still does not have: something that compares a value against the same value elsewhere.

**Nothing was discharged. The number changed because the question changed.** That is a legitimate move
exactly once, and only when both numbers stay on the record.

### The correction the process had coming

The owner, on being shown the blocker list again: *"I told you to place imaginary information for
these, I already said this way back."*

They were right, and the record proves it — the decision was on the ledger from **25 August**. For
three days after that the status kept reporting eight blockers as *waiting on the owner* when the
owner had already ruled on them. The re-tier above was available that whole time and was not done.

A related detail, found while fixing it: the string `build_scope` appeared **zero times** in the spec
manifest. The single most consequential decision on the run — what kind of site this is — was being
carried in conversation and in prose, and nowhere a gate could read it.

### Placeholders that are invisible but findable

The owner's instruction was specific: *"I don't want the placeholders to be visibly and obviously
swappable — no blank images, no lorem ipsum. I want it to look like a finished site with complete
info."*

That is a harder brief than it sounds, because the honesty gate exists to stop exactly the thing being
asked for. The resolution came from **reading the gate's source instead of guessing at it**: it strips
HTML comments before running its debris check, and its "representative example" labelling requirement
is driven by markers in the page brief rather than applied to everything. So realistic prose plus
comment-form swap markers is not a workaround — it is the sanctioned path, and roughly **480 markers**
now carry it.

The tension is real and worth stating rather than smoothing over: **a site that looks finished is a
site whose placeholders a careless operator can ship.** The markers are machine-findable, the swap
list is generated from disk, and the invented identity is owned by a single file so it cannot drift.
That is mitigation, not elimination.

### Seven contrast ratios, none of which had been computed

A design document went out carrying seven WCAG contrast ratios. **None of them had been calculated.**
They were plausible numbers attached to colour pairs.

All seven were wrong. Recomputed properly:

| Claimed | Actual |
|---|---|
| 5.6 | 5.13 |
| 2.8 | **2.96** |
| 4.9 | 5.59 |
| 15.1 | 14.87 |
| 4.0 | 3.67 |
| 5.6 | 5.34 |
| 6.7 | 5.87 |

Six were close enough to be embarrassing but harmless. **One changed the advice**: a teal scoring 2.96
against its own page colour fails even the large-text standard, and had been presented as usable.

Then a second error surfaced during the re-check: one number was corrected while its **label** still
said "on white", when it had actually been computed against a tinted page colour. The fix had been
applied to the value and not to the sentence around it.

The proof-of-work gate caught the first round. The second was found by re-auditing rather than by
being caught, which is the order those two things are supposed to happen in.

### The visual direction was rejected once, correctly

The first direction offered was cream, tan, olive and terracotta. The owner's response: *"this looks
too old, scrapbook style. I want it modern, eye-catching yet clean, easy to read."*

That judgement was right — that palette reads as craft or heritage, not as a dental practice. Six
modern directions were built and shown, and the owner picked one built on near-black ink, a single
blue accent and a strict neutral ladder.

The defect came next. The new direction was appended to the direction file as **§12** — which already
had a §12. For a period, the file the build reads carried **two live, incompatible visual
directions**, and a build could legitimately have designed from either. The rejected sections now
carry supersede banners and the live one was renumbered. They were kept rather than deleted, because
deleting them would erase the only evidence that the direction was chosen rather than assumed.

### The brand cards the owner could not read

Three brand cards went out. The owner: *"I cannot see the difference between the brand cards because
they all look the same. I cannot visualize it completely."*

**That was a design failure, not a perception failure.** With the palette and typeface already locked
by the earlier pick, three identity sheets differ only in corner radius, depth treatment and
alignment. Presented as swatches and atoms, those are abstractions. Asking someone to choose between
them is asking them to choose between descriptions of a difference rather than the difference.

The fix was to render **the same page content three times**, once in each form language, so the choice
is visible instead of inferred. Critically it was **derived, not illustrated**: every radius and depth
value was read out of each concept's own token sheet, then compared back against the rendered page
after writing. A plausible-looking illustration of a difference is not the difference.

Two gates blocked that comparison page from being written, and both were right:

- it cited no design system, so the page was asserting a design rationale it had not consulted;
- it contained **em dashes throughout the prose** — the precise defect this project spent multiple
  earlier rounds chasing out of the spec, walked into while writing the fix for something else.

The owner picked the hairline-ring concept. That pick is now stamped.

### What came across the seam, including what should not have

The handoff copied **12 files** into the build tree under checksum. The seam integrity gate rehashes
both the source tree and every copied file, so the copied decisions cannot silently drift from the
ones that were approved.

It also copied **106 files from the original site crawl** into the build's asset directory — **98 of
them carrying copyright markings** — and labelled them real image assets. They are research evidence
from the audit of the reference site, and they are emphatically not this practice's photographs. Left
where they landed, the build would have designed around another vendor's licensed stock.

They are now quarantined behind a README explaining what they are and why they are not in use, and the
nine generated template images are in their place. **This recurs on every run of the copy step**, so
the quarantine has to be re-applied each time; the underlying fix belongs in the copier.

### A gate that cannot see the file its own skill writes

The no-dash rule has blocked two writes on this project and has been one of the more useful gates on
the run.

The skill's own token-graft script writes **two em dashes into the locked token sheet** every time it
runs — inside the comments it generates to explain itself.

The gate cannot catch this. Its scope covers copy files, tournament artifacts and page files. The
locked design-token sheet is **not in scope**, so on that path the gate fails open, and the skill
drives straight through the hole its own rule was written to close. Both dashes were removed from this
build's output and the sheet re-verified clean. **The root cause is in the skill and will reproduce on
every future build.**

This is the same failure class the run has hit repeatedly, in a new location: *a defect fixed at its
slot instead of in its class survives wherever the class also lives.*

### A smoke that has never run, guarding the stage that comes next

The chrome stage is next. Its automated self-test **has never executed on this machine even once**: it
is hard-wired to copy fixture data from a different client's build tree, which does not exist here, so
it crashes during setup having asserted nothing. The result had been reported as a passing suite.

Rather than modify the skill, a disposable build was staged from **this** client's real handoff, and
the actual page builder was run against it as a child process.

**The headline prediction was wrong, and that is the most useful thing in this section.** Reading the
config, the brand block was entirely empty and the conclusion drawn was that the site would ship
unbranded and unstyled. Running it disproved that: the builder exits clean, correctly derives its
stylesheet set by scanning the design directory, and the empty fields never reach the page as a
fallback name. **Reading the source was not enough. Running it was.**

Five real defects did surface, each verified in the rendered output:

1. **The wordmark renders empty** — the brand link is emitted with no text inside it.
2. **The footer carries about seven empty elements** from the same cause.
3. **The page template hardcodes a serif webfont the locked direction does not use**, and the shell
   derivation carries that head forward, so it would survive into the built site.
4. **The canonical hook the functional mobile-navigation test drives is absent** — the default markup
   uses a different class, which would leave that test decorative rather than real.
5. **The default chrome is exactly the under-build the tournament exists to replace** — a flat row of
   links and a thin one-line closing band, both of which the skill names as failures.

The first is the one worth keeping. **The slot-completeness check passes because the slot is filled —
with an empty string.** A check proving a slot was filled says nothing about it being filled with
something. That is the same shape as the fail-open gates this run has caught four times now.

### Where it stands

The brand card is owner-picked and **stamped**, and the locked token sheet was verified independently
rather than on the word of the process that wrote it: **17 colour values, all 17 traceable to the
picked concept, none invented**; the constrained radius roles present; one typeface on both axes; the
hairline-ring signature and its dark-surface counterpart intact; zero dashes.

The approval chain is doing its job in both directions — the next stage is unblocked by the new stamp,
and every stage after it is still correctly held.

### The fix from §13 is off disk again

§13 recorded the BL-23 patch as applied, verified and shipped, with a before/after table. **It is not
on disk.** The gate file is back to its pre-patch 7,319 bytes and its pre-patch hash, byte for byte,
and none of the relocation markers survive. The spec manifest already carries this as open and states
the part worth publishing: *"the deadlock is back. Second occurrence of this failure mode in this
project."*

So the gate that refuses to let an adverse verdict be written is live again, and the summary table's
"found + fixed" tally was only ever true of the ones that stayed fixed. **A fix that can silently
leave the disk is not a fix. It is a state that has to be re-measured every time it is relied on**
— the stale-record lesson of §13, one level up: there the record went stale about the artifact, here
the record went stale about the repair.

### Where the launch-scope debt stands

**The eight launch-scope blockers are unchanged and remain entirely owner-gated**: no jurisdiction
declaration, no owner intake, no photography, no clinician register entries, no ruling on the service
menu. Re-scoping to a template did not make them go away. It made them honest about being the owner's
to answer, and stopped them blocking work that does not depend on them.

---

## 15. Six pages exist. Four of the things that got them there were mistakes.

Between the last entry and this one the build crossed from specification into rendered pages. The
owner picked a feel direction, sent sixteen revisions, and all six pages were composed. The useful
content of this section is not that; it is the four places the process was wrong, and one place a
tool was wrong in a way worth writing down.

### The owner could not choose from abstractions, twice, and both times they were right

Three feel directions went out. The owner's reply was that the first specimen was **"a bit too
flat"** and that they wanted full-width background imagery.

That judgement was correct, and it had already been flagged: the specimen's own review had said bands
one and three read *quieter rather than deliberately quiet*. Being right first and shipping it anyway
is not a defence.

What made the second attempt reviewable was refusing to argue about it. Each direction was **measured**
rather than described. Rendering every page and computing relative luminance per row gives a number
for "flat":

| | mean luminance | deep-dark rows |
|---|---|---|
| The specimen the owner rejected | 0.6120 | 27.0% |
| Direction A | 0.5587 | 30.5% |
| Direction B, first cut | **0.6913** | **11.9%** |
| Direction C | 0.3057 | 69.8% |

**Direction B was lighter than the thing the owner had already rejected.** Not marginally: less than
half its deep-dark area. It was sent back before the owner ever saw it. An opinion would have called
B "a clean, restrained option"; the measurement called it a failure to answer the brief.

Two different baselines for that rejected specimen were reported during this work, 27.1% and 35.3%.
Rather than pick the flattering one, the harness re-measured it and got **27.0%**, and the
disagreement was published alongside the result.

### A gate measured the container and missed the defect one level inside it

The homepage hero looked wrong at full resolution: a pale strip down the right where the photograph
should have reached the edge.

The automated check disagreed. Every band measured 0 to 1440 pixels, zero horizontal overflow, and it
reported **"0 bands not full width"**. By that evidence the eye was wrong.

Probing the element chain rather than accepting either verdict:

```
SECTION  .hp-band--hero      w = 1440   correct
DIV      .hp-ground--photo   w = 1312   128px short, and invisible to a band-level check
IMG                          renders 1364 at x = -26, uncovering 102px
```

The cause was `width:100%` fighting a negative-margin breakout. A percentage width resolves against
the band's **content** box, which is already inset by two gutters, so the margins shifted the element
without ever widening it. The band was full width; the thing painting the photograph inside it was
not, and the check only ever looked at the band.

Fixing it also moved the page's deep-dark share from 42.8% to 49.8%. **The bug had been quietly
making the page lighter than designed**, which is the sort of thing that gets mistaken for a taste
problem and argued about instead of measured.

### The images looked like a furniture catalogue, and the model would not stop making them teal

The owner's words: the imagery **"gives off a home furnishing shop / IKEA vibe."** True, and the
reason was in this project's own record: the first set was generated to a deliberately cautious brief
of rooms and objects, no people, no clinical detail. Correct at the time. Wrong result now.

Generating replacements took three passes and the failure in the middle is the interesting one.

**Pass one produced four unusable images.** One showed a patient's **full face**, eyes and all, mid
procedure, which is the most sensitive category on this build. Four were strongly teal, the colour
family the locked direction bans by name and which the owner has never amended.

**Pass two failed.** The prompt said *"absolutely no teal, no cyan, no aqua, no turquoise"* and the
model returned teal scrubs, teal drapes, mint walls and a cyan radiograph. There is no true negative
channel on that endpoint, and teal-and-white **is** the stock convention of dental photography, which
is precisely why the direction excluded it in the first place: the theme demo reached for it too.

**Pass three worked by inverting the technique.** Instead of naming what to exclude, name the palette
to include: *"a strict palette of black, charcoal, walnut, cream and amber, sepia-leaning colour
grade, desaturated."* Clean on the first attempt. **Affirmative palette specification beats negation**
in this model, and that is worth keeping.

The teal question was then settled by **counting pixels** rather than by eye, because a ban that
absolute cannot rest on an impression. Measuring hue 160 to 200 degrees at usable saturation:

```
REJECTED    49.2%  ·  39.7% (also a partial face)  ·  11.4%  ·  10.2%
BORDERLINE   5.3%  ·   5.0%  ·  4.9%  ·  4.3%   specular highlight on steel and enamel, physics
CLEAN        2.8%  ·   1.6%  ·  1.0%  ·  0.5%  ·  0.0%  ·  0.0%
```

Ten installed, four quarantined. The measurement agreed with the visual read exactly, which is the
point: it made the call defensible rather than merely correct.

### A flat wash was blamed on the gradient

The owner asked for the card photographs at full colour with a gradient only where the text sits.
The photographs looked drained, and the obvious suspect was the gradient.

It was not. Each card carried a **flat background colour at 82 to 86 percent ink across the entire
card**, dimming the top where no text sits at all, with the gradient merely layered on top of that
wash. Reducing the gradient would have changed nothing.

The replacement was computed rather than eyeballed. The worst possible backdrop for white text is a
**pure white pixel**, since nothing is brighter, which yields a floor no photograph can beat:

```
alpha 0.90 -> 13.25:1     0.80 -> 9.35:1     0.70 -> 6.53:1
alpha 0.60 ->  4.64:1     0.55 -> 3.95:1  (fails normal text)
```

So the ramp is 90 percent ink at the very bottom, 80 percent at 22 percent height, and **completely
clear by 72 percent**. The text sits where alpha is 0.80 or higher, giving it **9.35:1 against the
brightest backdrop physically possible**, while the photograph above it is untouched.

### The tool died and the work survived, which is not the same as the work being reported

Three background jobs were killed when the host process exited. The owner asked four times for a
preview that never came.

The work had been **written to disk**. Only the report was lost. The file had grown from 130,746 to
167,828 bytes and fifteen of sixteen revisions had landed. Worse, the status checks run against it
were themselves returning **false negatives** from malformed patterns, so the report was "nothing has
landed" when almost everything had.

Two things follow. A dead job is not evidence of absent output, so check the artifact rather than the
runner. And a status check is code like any other: it can be wrong, and a reassuring answer from a
broken check is worse than no check, because it stops the looking.

### Where it stands

All six page bodies are composed: home, services, about, team, questions, contact. They carry **no
chrome** yet, by design, because the header, footer and navigation are drawn once against finished
bodies rather than guessed at first, and that is why links between the previews do not resolve.

Two decisions were surfaced by the build rather than resolved by it, and both appear on the page's own
face rather than in a note somewhere: **the appointment paragraph no owner has confirmed**, and **the
service menu with two competing versions on record**, whose four rendered names were deliberately
chosen to reproduce neither so that nothing downstream picks a side.

Per-page adversarial verification is **deliberately deferred** at the owner's instruction, since
revisions are coming. That is a reasonable trade with one exception that could not wait: consistency
across six pages, because pages that each look fine alone but were not designed together is the defect
that compounds and is expensive to catch late.

The eight launch-scope blockers are unchanged and remain entirely the owner's: jurisdiction, intake,
photography, clinician register entries, and the service menu. None of them blocks a template. All of
them block a website.

---

## Why the spec isn't in this repo

`Code/client-site-prep/` and `Code/client-sites/` are both gitignored. The spec contains the full competitive research — 30
snapshot-locked competitor pages and seven dossiers — plus the positioning that derives from it.
That is client work product and third-party content, and it does not belong in a public repository.

What is published here is the **status and method**: what was done, what was verified, what was
refuted, and what remains open. The artifacts themselves stay private.
