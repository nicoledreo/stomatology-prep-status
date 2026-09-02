# Find us

**Page:** `contact` | type `T-CONTACT` | nav-6 | `funnel_role: F3` | `terminal: true`

> **NOT RENDERED.** Nothing before `## S1` reaches a visitor.

**NOT RENDERED. Placeholder disclosure.** The practice name, city, street address, telephone number,
email address and opening hours are TEMPLATE VALUES. They are stand-ins, not this practice's data,
each carrying its own `<!-- swap:... -->` marker.

**NOT RENDERED. Action.** Both routes end on this page, so no onward CTA pair. Primary action is the
telephone or the email; secondary is the five-page route list.

**NOT RENDERED. Not carried.** No form, map or place card. No directions, parking, transport,
reply-time, availability, capacity or fee. No named clinician, rating, review, award, testimonial or
count.

**NOT RENDERED. Voice ceiling.** The brief fixes every rendered string as a literal. Warmth cannot be
added from inside the copy. A warmer page needs one or two more sentences authorised at S2 and S4.

**NOT RENDERED. This pass.** Copy cut to the owner's limits: headings and notes shortened, held claims
and rationale removed. No fact, value, marker or section moved.

---

## S1 contact-hero
<!-- facts: D-PAGE-006, D-IA-001, D-PAGE-BRAND-HELD -->

### Heading

<!-- swap:contact-heading-1 -->
<!-- swap:practice-name -->
<!-- swap:city -->

Reach Alder Grove Dental in Riverbend

### Body

<!-- swap:contact-subline -->
<!-- swap:address -->
<!-- swap:street -->
<!-- swap:city -->
<!-- swap:phone -->
<!-- swap:email -->

114 Alder Street, Riverbend. Call (555) 555-0142 or email hello@aldergrovedental.example.

### Microcopy

- Telephone control: `tel:5555550142`. No country code.

- Email control: `mailto:hello@aldergrovedental.example`. No prefilled subject or body.

- Head-block image alt, under `<!-- swap:image-contact-hero -->`:
  `A dental practice frontage seen from the opposite side of a street.`

- Build note. Renders the heading, the one line, and the head-block image. No card, no panel, no
  further prose.

- Build note. The photograph is generic: no readable street name, house number, signage or
  identifiable passer-by. Rewrite this alt when a real photograph arrives.

- Build note. In the line, the telephone and email are live controls: `tel:5555550142` and
  `mailto:hello@aldergrovedental.example`. The address is not a link.

- FLAG. `_preview-site/contact.html` uses a different alt and mints
  `<!-- swap:image-contact-closing -->` at S4. This deck carries the alt the brief owes.

---

## S2 contact-details
<!-- facts: D-IA-011, D-PAGE-PLACEHOLDERS-IN-FORCE, D-PAGE-DEADLOCK-CONTACT, D-PAGE-JURISDICTION-WORKING -->

### Heading

<!-- swap:contact-heading-2 -->

Reach us, and when we're open

### Body

<!-- swap:field-label-address -->

**Address**

<!-- swap:address
     Template value, not this practice's data.
     Swap for the page-inventory.md section 2.3 "full address line" row when the owner supplies it. -->
<!-- swap:street -->
<!-- swap:city -->

114 Alder Street
Riverbend

<!-- swap:field-label-phone -->

**Telephone**

<!-- swap:phone
     Template value, not this practice's data.
     Swap for the page-inventory.md section 2.3 "telephone" row when the owner supplies it. -->

(555) 555-0142

<!-- swap:field-label-email -->

**Email**

<!-- swap:email
     Template value, not this practice's data.
     Swap for the page-inventory.md section 2.3 "email" row when the owner supplies it. -->

hello@aldergrovedental.example

<!-- swap:field-label-hours -->

**Opening hours**

<!-- swap:hours
     Template value, not this practice's data.
     Swap for the page-inventory.md section 2.3 "opening hours" row when the owner supplies it. -->

Mon-Thu 8:00-17:00
Fri 8:00-14:00

### Microcopy

- Field labels, in order: `Address`, `Telephone`, `Email`, `Opening hours`.

- Telephone control: `tel:5555550142`. Email control: `mailto:hello@aldergrovedental.example`.

- Build note. Four labelled rows, no sentence.

- Build note. Each label is a real visible element, beside its value and outside the link. Never an
  icon alone, never a placement convention, never an `aria-label` alone.

- Build note. The address renders as an `<address>` place block: `114 Alder Street` with
  `<!-- swap:street -->`, then `Riverbend` with `<!-- swap:city -->`. It is not a link.

- Build note. The hours are two labelled rows, not one run-on string.

- Build note, GW. `section_seq` name `contact-details` ships as a class token: emit
  `class="contact-details"` and no `form` class. There is no form on this page.

- **HEADING CHANGED.** The brief fixes `How to reach us, and when we are open`. Cut to
  `Reach us, and when we're open` for the six-word heading limit. No fact moved.

---

## S3 routing-block
<!-- facts: D-IA-009, D-POSITION-001, D-POSITION-002, D-MARKET-MOUNTAINKIDS-POS -->

### Heading

<!-- swap:contact-heading-3 -->

More about us

### Body

<!-- swap:contact-route-1 -->
<!-- swap:contact-route-2 -->
<!-- swap:contact-route-3 -->
<!-- swap:contact-route-4 -->
<!-- swap:contact-route-5 -->

Home
What we do
About us
Who you'll see
Questions and answers

### Microcopy

- `Home` routes to `index`, under `<!-- swap:contact-route-1 -->`

- `What we do` routes to `services`, under `<!-- swap:contact-route-2 -->`

- `About us` routes to `about`, under `<!-- swap:contact-route-3 -->`

- `Who you'll see` routes to `team`, under `<!-- swap:contact-route-4 -->`

- `Questions and answers` routes to `faq`, under `<!-- swap:contact-route-5 -->`

- **HEADING CHANGED.** `More about us` replaces the brief's `More about the practice`. The same
  component heads the rails on `services`, `faq` and `team`: all four land together or revert together.

- Build note. Five link labels, no sentence. Each label is the name the navigation gives that page.

- Build note. No label characterises what a visitor will find. No label offers to field a question.

- Build note, G-CTA1 RULE 1. No class token on this `<section>` may contain `cta`. Also banned:
  `precta`, `pre-cta`, `prefooter`, `pre-footer`, `cta-band`, `cta-section`, `closing-cta`,
  `final-cta`, `closer`, `end-cta`, `conversion-band`, `cta-banner`. Executed: `cta-band` blocked,
  exit 2.

- Build note, G-CTA1 RULE 2. No `btn`, `button` or `cta` class token on the five route controls, and
  no conversion verb as a label. Executed: a verb label blocked, exit 2.

- Build note. No supporting line under any label. The content floor is not available and must not be
  manufactured.

---

## S4 booking-intent
<!-- facts: D-IA-006, D-IA-007, D-IA-008, D-POSITION-009 -->

### Heading

<!-- swap:contact-heading-4 -->

Making an appointment

### Body

<!-- swap:booking-line -->

Call or email us to make an appointment.

<!-- swap:phone -->

(555) 555-0142

<!-- swap:email -->

hello@aldergrovedental.example

### Microcopy

- Telephone control: `tel:5555550142`. Email control: `mailto:hello@aldergrovedental.example`.

- **LINE CHANGED.** The line replaces the brief's `Appointments are arranged by telephone or by
  email`. `swap:booking-line` is shared: `about` and `services` land the identical string, or all
  three revert.

- Build note. Four elements: the heading, the line, and the two channels as live controls.

- Build note. The channels carry the same marker names as S2.

- Build note. No form, submit control or field labels.

- Build note. This page adds no legal, privacy or data-handling text.

- Build note, GW. `section_seq` name `booking-intent`, so emit `class="booking-intent"`. The retired
  name `no-booking-note` must not ship.

- Build note, G-CTA1 RULE 1. No class token in this band may contain `cta`. Executed: `cta-band`
  blocked, exit 2. Do not collapse the four elements into two.
