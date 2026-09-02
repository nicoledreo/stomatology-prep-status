# What we do

**Funnel role:** F2, evaluation.

**Primary CTA:** `contact`, from the S5 routing band, under the label `Find us`.

**Voice:** plainspoken and warm. Second person, addressed to a parent.

**Placeholder disclosure:** every value here is template content. No owner has confirmed any of it.

## S1 hero-category-outcome
<!-- facts: D-PAGE-002, D-IA-001, D-SEO-301-PAIR, D-PAGE-BRAND-HELD -->

### Heading
Dental services in Riverbend

### Body
What Alder Grove Dental does, listed by plain name.

### Microcopy
- Page title: `Dental services in Riverbend - Alder Grove Dental`

- Meta description: `Dental services at Alder Grove Dental in Riverbend, listed by plain name.`

- Image alt: `A corridor with doors on both sides and daylight at the end.`

- Markers: `<!-- swap:services-heading-1 -->` and `<!-- swap:city -->` on the h1.

- Markers: `<!-- swap:services-standfirst -->` and `<!-- swap:practice-name -->` on the standfirst.

- Markers: `<!-- swap:city -->` and `<!-- swap:practice-name -->` on the title and the meta.

- Marker: `<!-- swap:image-services-hero -->` on the image.

### Build note
Category and place. No benefit line, no claim of any kind.

One h1. The practice name stays out of it and carries in the title.

Title ceiling is 60 characters. Re-measure it once a real city and name land.

The standfirst is this page's only brand-name carrier in prose.

## S2 why-this-area-wedge
<!-- facts: D-POSITION-008, D-POSITION-002, D-POSITION-010, D-OFFER-013 -->

### Heading
How we work

### Body
We see people by appointment. You can make one by telephone or by email.

### Microcopy
- Marker: `<!-- swap:services-heading-2 -->` on the heading.

- Marker on the paragraph:

```
<!-- swap:services-wedge
     TEMPLATE CONDUCT, shortened on purpose. What is left says the practice
     works by appointment and names the two channels. No owner has confirmed
     either. Two unconditional conduct sentences were STRUCK here under
     content-bible H10, not softened. -->
```

### Build note
OWNER-CONFIRM. Two conduct sentences were struck here, not hedged.

`content-bible.md` section 0.3 H10 holds any unconditional promise about clinical conduct.

One of the two also implied a clinician. This site names none.

Both are specified at `briefs/services.md` section 2a and are not reprinted here.

Both return verbatim once an owner confirms them and names the protocol document.

What is left is thinner than the brief asks for. That is the honest size of it.

No comparative, no category framing, no service named, no count.

## S3 sub-area-blocks
<!-- facts: D-OFFER-017, D-OFFER-018, D-IA-011, D-OFFER-002 -->

### Heading
The work we do

### Body

#### Routine examinations
A booked appointment, where we look at your teeth and gums.

#### Hygiene appointments
Keeping your teeth and gums clean, here and at home.

#### Restorative work
Repairing a tooth that's damaged, worn or decayed.

#### Crowns and bridges
When a tooth is too damaged to repair, we rebuild it or replace it.

### Microcopy
- No control of any kind: no link, no button, no chevron, no arrow, no `Read more`.

- Marker: `<!-- swap:services-heading-3 -->` on the heading.

- Markers on the four names: `<!-- swap:service-1 -->`, `<!-- swap:service-2 -->`, `<!-- swap:service-3 -->`, `<!-- swap:service-4 -->`.

- Markers on the four lines: `<!-- swap:service-1-line -->`, `<!-- swap:service-2-line -->`, `<!-- swap:service-3-line -->`, `<!-- swap:service-4-line -->`.

### Build note
Each name is an h3 under this section's h2, with its line as body text.

The blocks are panels, not links: no anchor, no `role`, no `tabindex`, no click handler.

No pointer cursor, no hover lift, no hover border change. A border, a fill and padding are fine.

Four rows demonstrate the repeating block. They assert no number of services.

No line names equipment, a procedure, a material or a technique.

The owner's menu is unresolved. When it lands, these four strings are replaced whole.

The four lines are shared carriers. They render byte-identical on the homepage.

`briefs/services.md` section 3 prints older wording. Where the two differ, the warmed string wins.

## S4 cross-link-rail
<!-- facts: D-IA-003, D-PAGE-003, D-PAGE-004, D-PAGE-005 -->

### Heading
More about the practice

### Body

**About us.** How a visit here runs, and why it runs that way.

**Who you'll see.** The people at reception and on the telephone, and what each of them does.

**Questions and answers.** Where we are, when we are open, and how an appointment is made.

### Microcopy
- Link labels: `About us` to `about`, `Who you'll see` to `team`, `Questions and answers` to `faq`.

- Marker: `<!-- swap:services-heading-4 -->` on the heading.

- Markers on the three labels: `<!-- swap:services-rail-1 -->`, `<!-- swap:services-rail-2 -->`, `<!-- swap:services-rail-3 -->`.

- Markers on the three clauses: `<!-- swap:services-rail-1-line -->`, `<!-- swap:services-rail-2-line -->`, `<!-- swap:services-rail-3-line -->`.

### Build note
`contact` is absent here on purpose. It belongs to S5.

Each clause says what is on the page it points at, and stops there.

No clause promises a qualification, a founding story or a reassurance.

Each clause renders as its own element. It may not be folded into its label.

No `btn`, `button` or `cta` class token on the three controls.

All six strings are byte-identical with the built page.

## S5 routing-band
<!-- facts: D-IA-009, D-PAGE-006, D-PAGE-DEADLOCK-CONTACT, D-OFFER-006 -->

### Heading
Arranging an appointment

### Body
Appointments are arranged by telephone or by email.

(555) 555-0142

hello@aldergrovedental.example

Find us

### Microcopy
- Telephone renders as a live link: `<a href="tel:5555550142">(555) 555-0142</a>`, no country code.

- Email renders as a live link: `<a href="mailto:hello@aldergrovedental.example">hello@aldergrovedental.example</a>`, no subject parameter.

- Route label: `Find us`, to `contact`. Same word the navigation uses.

- Sentence case, no terminal punctuation.

- Markers: `<!-- swap:services-heading-5 -->` on the heading, `<!-- swap:booking-line -->` on the line.

- Markers: `<!-- swap:phone -->`, `<!-- swap:email -->`, `<!-- swap:services-route-contact -->`.

### Build note
Four paragraph-level elements: the line, the telephone, the email and the route.

No `btn`, `button` or `cta` class token. The route label stays `Find us`.

The band says how an appointment is arranged and where to go next.

It does not say that anyone picks up, or how soon.

Both channel values are placeholders that reach nobody. A real practice email is still owed.

`swap:booking-line` is a shared carrier and stays unchanged.

## S6 where-the-work-happens
<!-- facts: D-BRAND-RAILS-009, D-IA-010, D-PAGE-FLOOR-COLLISION, D-PAGE-PLACEHOLDERS-IN-FORCE, D-POSITION-001, D-POSITION-011 -->

### Heading
Where the work happens

### Body
The work we do happens in the treatment room.

Reception keeps the appointment book, so that is where your appointment is written down.

You arrive at reception first, whatever the appointment is for.

### Microcopy
- No link, no button, no closing ask. The contact verb is carried once, in the chrome band.

- Image alt: `The treatment room seen from the doorway, with nobody in it.`

- Marker: `<!-- swap:services-heading-6 -->` on the heading.

- Marker: `<!-- swap:services-closing -->` on the three lines, which swap as one unit.

- Marker: `<!-- swap:image-services-where -->` on the image.

### Build note
The nouns are fixed: `the treatment room`, `the appointment book`, `reception` in lower case.

Not the room, not the chair, not the diary, not the desk.

No line fixes a number of rooms. None adds a service to S3.

No equipment, no materials, no technique. No `cta` class token on the section.

Two of the three lines were rewritten and no fact moved.

Line 1 now names the work, not the page. Line 2 puts a person in the subject position.

`_spec/CANONICAL-LINK-LABELS.md` section 8.1 fixes `the appointment book` as the canonical noun.

`_copy/team.md` renders reception keeping it. Two pages, one fact.
