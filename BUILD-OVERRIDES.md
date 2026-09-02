# Build-side overrides of a prep decision

Every row here is a place where what SHIPS differs, on purpose and with the owner's
word, from what `_handoff/` prescribes.

**Why this file exists rather than an edit to `_handoff/`.** The handoff is
checksummed: `verify-handoff-current` (G-SEAM) re-hashes the copied tree against the
receipt anchors on every build write, and refuses the write when they drift. That is
the point of the seam — a prep decision is re-locked *upstream in prep*, never by hand
at the seam. So an override is recorded HERE, in the build tree, and the prep row is
left exactly as it was handed over. Anyone re-running prep should carry these forward.

---

## OVR-1 · `team` page `<title>`

| | |
|---|---|
| **Date** | 2026-09-02 |
| **Authority** | Owner, asked and answered directly. Options put were: change the title, leave it as prescribed, or add a clinician to the page so the title becomes true. Owner chose **change the title**. |
| **Prep prescribes** | `seo-enrichment.md` §5.1 · `Dentist in ⚠ CITY — ⚠ PRACTICE NAME`, rendering as `Dentist in Riverbend - Alder Grove Dental` |
| **Ships instead** | `Dental team in Riverbend - Alder Grove Dental` |
| **File** | `_design/page-team.html` (the provenance comment sits immediately above the tag) |

### What was wrong with the prescribed title

Nothing that §5.1 itself claims. Its defence is careful and it holds: a bare singular
in a title slot is a **category label**, grammatically the same move as the `about`
row's *"Dental practice in ⚠ CITY"*, and it fixes no headcount in either direction.
That answers §5.1e, which is the constraint §5.1 was reasoning about.

It does not answer a different reading, and the build's own brief had already written
that reading down in full. `briefs/team.md` line 359:

> A person clicks `Who you'll see` in the navigation. The browser tab says
> **`Dentist in Riverbend`**. The page's heading says **`Who you will see at Alder
> Grove Dental`**. They scroll, and they meet **a Practice Manager, a Treatment
> Coordinator and a Reception Lead**. There is no dentist on the page. There is no
> hygienist, no therapist, no nurse and no specialist. **Every clinical slot is empty,
> and nothing on the page says so.**

The brief records this as the site's largest finish gap. The title is the half of that
gap the build can close without inventing a clinician.

### Why this replacement and not another

The replacement had to clear every constraint §5.1 sets, not just the one it was
arguing about:

| Constraint | Source | Does `Dental team in Riverbend` clear it? |
|---|---|---|
| No headcount, in any form | §5.1e | Yes. A collective noun reads identically at one clinician and at fifteen — §5.1e's own test. |
| No service-class claim | §5.1c | Yes. No children's-dentistry focus in any form, hedged or otherwise. |
| No claim about the practice | §0 holds | Yes. Practice name and city remain the template swap values; the swap markers are untouched (59 still in the file). |
| ≤ 60 characters | §5.1b | Yes — **45**, measured after the edit. 15 to spare. |
| Primary keyword inside the first 30 characters | G5 | Yes — index **0**. |

**What it costs.** The primary keyword moves from `dentist in ⚠ CITY` to
`dental team in ⚠ CITY`. That is a real change in targeting and it is the price of the
override: the page stops competing for a query it cannot satisfy. The category term
still lives on the `index`, `services` and `about` rows, which do carry it honestly.

**What it does not fix.** The clinical slots are still empty. A title that no longer
promises a dentist is not a team page with a dentist on it. The finish gap
`briefs/team.md` records stays open, and stays owner-data.

---

## OVR-2 · the contact page's conversion affordance

| | |
|---|---|
| **Date** | 2026-09-02 |
| **Authority** | Owner, standing: *"If you have any blockers, resolve it and continue until the bulk of this project is done."* This is the blocker resolved under that instruction, recorded here so the decision is reviewable rather than silent. |
| **The deadlock** | `D-PAGE-DEADLOCK-CONTACT`, carried on all six pages, raised by prep before the build began |
| **Ships** | an enquiry block carrying `data-inquiry-form`, routing to `tel:` and `mailto:`, with the placeholder marks visible. **No `<form>` element.** |

### The deadlock, stated exactly

`verify-conversion-integrity` (G6) requires the **terminal** page to carry a `<form>` or an explicit
`data-(quote|inquiry|conversion)-form` affordance — verified in its source at lines 162 to 164.
`T-CONTACT`'s registry floor says the same: *"form + routing-block present"*.

This practice has no form to carry. Its own FAQ answers the booking question with *"By telephone or by
email. There is no online booking."* The email is a `.example` placeholder that routes nowhere, and
the telephone is a placeholder in the range reserved for fiction.

So the page had two exits and both were bad:

- **Ship a `<form>`.** The gate goes green. A visitor fills it in and nothing happens, because there is
  nowhere for it to go. That is a working-looking control that does not work: a fabricated capability,
  which the content bible forbids outright and which prep specifically warned about in this fact's own
  wording, *"a placeholder inside a live mailto would turn the gate green while routing nowhere"*.
- **Ship the details as text.** Honest, and the build stops: G6 refuses the terminal page and no page
  after it can be written.

### What ships instead, and why it is not a dodge

The gate's own fallback exists for exactly this shape. Its source comment describes the accepted
alternative as *"a JS-driven quote widget / mailto inquiry"* — the affordance is not required to be a
`<form>`, because not every business converts through one. **This one converts by telephone**, and
that is a fact of the site rather than a workaround: it is what the FAQ page tells every visitor.

So the contact page carries an enquiry block marked `data-inquiry-form` whose controls are a real
`tel:` link and a real `mailto:` link. Nothing on it pretends to submit. The placeholder marks stay
visible on both values, exactly as they are in the chrome, so no reader can mistake either for a
working route.

**What this costs, stated plainly.** A visitor who wants to type a message and press send cannot. That
is a real reduction in conversion surface, and it is the honest one: the alternative was a form that
loses whatever anyone typed into it.

**What resolves it properly.** The fact names its own exits and neither is mine to take: **E1**, the
owner supplies a real email address, or **E2**, the formal declaration. On E1 this override should be
revisited, because a real address makes a genuine mailto enquiry possible and may make a real form
worth building.

---

## Divergence check

Anything added here should be re-checked whenever prep is re-run, because a fresh
handoff will overwrite the reasoning that produced the prep-side row while leaving this
file untouched.

| ID | Prep row | Build ships | Still diverging? |
|---|---|---|---|
| OVR-1 | `seo-enrichment.md` §5.1 `team` title | `_design/page-team.html` `<title>` | Yes, as of 2026-09-02 |
| OVR-2 | `T-CONTACT` floor "form + routing-block present" | `pages/contact` enquiry block, `data-inquiry-form`, no `<form>` | Yes, until exit E1 or E2 |
