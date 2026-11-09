# Design notes: Dhiandra Pradika portfolio

Every rule below is written as **decision → reason**, so a later change can be argued with instead of guessed at.

## 1. Palette (Elaina: cream paper, indigo ink, lilac ground, gold accent)

| Token | Value | Used for | Contrast measured |
|---|---|---|---|
| `--cream` | `#f9f6ef` | page ground | — |
| `--card` | `#fffdf8` | card surfaces | — |
| `--lilac` | `#efe9f8` | the Mobile band | — |
| `--ink` | `#221a3c` | headings and body | 16.4:1 on cream |
| `--muted` | `#4f4767` | secondary copy | 9.4:1 on cream, 8.6:1 on lilac |
| `--gold` | `#7d5f1a` | eyebrows, counters, arrows | 5.5:1 on cream, 5.0:1 on lilac |
| `--indigo` | `#251c42` | the closing band | — |
| cream on indigo | `#f7f1e6` | closing band text | 13.9:1 |
| stack line | `#5f4a10` | tech list under a card | 7.9:1 on cream, 7.2:1 on lilac |

Every number above is computed with the WCAG formula, not eyeballed. The one colour that failed at first was the stack line at `#6f5516` (5.9:1 on lilac): it was darkened to `#5f4a10` to clear 7:1, which is the bar this page holds itself to for small text.

## 2. Type

- **Fraunces** for the h1, the section numbers' neighbours and card titles. A serif with a little swash is what makes the page feel written rather than generated; it also carries the storybook tone of the palette.
- **Schibsted Grotesk** for everything else. Neutral, narrow, and it holds 15–17px body copy without looking like a system font.
- One h1 at `clamp(36px,4.8vw,60px)`, section h2 at `clamp(32px,4vw,50px)`, card h3 fixed at 18px. Sizes are set by level, never by section.

## 3. Structure, top to bottom

1. **Hero, exactly one screen.** `grid-template-rows: 1fr auto` inside `min-height: calc(100svh - 68px)`. Row one is two top-aligned columns: text left (eyebrow, h1, lead, two buttons, six chips) and a 320px column right (portrait 5:6, then a hairline and two fact rows). The text column stretches to the right column's height with `justify-content: space-between`, so both columns end on the same line and no corner is left dead. Row two is the evidence rail pinned to the bottom edge: `08 web apps`, `02 Android apps`, and a link to the source. Numbers and rail exist because the first version left the lower third of the hero empty; the face stays small on purpose, the work is the subject.
2. **Web, nine cells.** The section head carries a chapter number (`01 — Web apps`, `02 — Mobile apps`, `03 — Say hello`) so the page reads as three parts, not one long list. Eight projects as cards with a real preview, plus a ninth cell that says the source is public. The ninth cell exists because eight cards in a three column grid leave one hole; a hole reads as unfinished, a statement reads as designed.
3. **Mobile, a lilac band.** Two Android projects, two columns, same card anatomy. The band's ground change is the category break: no heading decoration needed when the background already says "different kind of thing".
4. **Contact, an indigo band.** Text and buttons left, the address as a large tappable line right, then one footer row. The dark ground closes the page so the last thing on screen is a door, not a fade-out.

## 4. Rules that were broken on purpose, and why

- **One hairline per boundary, not per heading.** The hero ends with a full bleed 1px rule and the lilac band carries `border-block`; headings themselves get no rule. Sections are otherwise separated by ground (cream → lilac → indigo) and air.
- **Nothing is highlighted while the hero owns the screen.** The nav's current state is computed geometrically against a line at 28% of the viewport; before the first section the state is empty. Marking "Web" as current on load was wrong: the reader had not reached it yet.
- **No captions under pictures.** The one caption that existed (the degree line under the portrait) was moved into the text column, where it belongs to the sentence rather than to the photograph.
- **Two button styles, page wide.** A filled gold pill for the one action that matters, an outlined pill for the second. The closing band reuses both, with the outline lightened so it survives the dark ground.
- **Cards share one anatomy.** Preview, name, one sentence, stack. Nine cards that differ in size would make the reader compare layouts instead of projects.
- **Window chrome on every preview.** A 23px bar with three dots above each screenshot. Ten screenshots taken at different zooms and different brightness otherwise read as ten unrelated rectangles; the chrome turns them into one series of screens.
- **Motion is one gesture, twice.** On load the hero arrives in reading order (eyebrow, headline, lead, buttons, availability, chips, portrait, rail) with a 70ms stagger, 18px rise and 0.74s ease-out. On scroll each section head, card and closing block does the same once, then never again. Nothing parallaxes, nothing bounces, nothing loops.
- **Motion never hides content.** The hidden state only exists while JS is running (`.js` on the root), the observer reveals anything already in view as a fallback, a failed script reveals everything, and `prefers-reduced-motion: reduce` turns the whole layer off. A visitor with a slow connection reads the page, not a blank screen.

## 5. Copy rules (written for a recruiter, not for a designer)

- **Every claim carries a number or a mechanism.** "Ten projects in ten months", "throttled to 5 tries a minute", "signed R2 links cached by TTL". No adjective does the work that a fact can do.
- **The lead answers four questions in three lines:** what role, what was built, what part of it he owns, and how much of it exists. It is the only paragraph most recruiters will read.
- **A card sentence names a constraint, not a feature list.** "Refuses negative stock" and "audit trail that stores the old and new value" tell a reviewer what was hard; "product management" tells them nothing.
- **Availability is stated once, plainly.** Open to internship or junior roles, Jakarta or remote, next to a CV link, because hiring managers look for both in the first ten seconds.
- **Nothing is invented.** Every card sentence is traceable to that repo's README. Where a README states a mechanism (login throttling, WorkManager, sharp, PHPUnit), the sentence uses that exact mechanism.
- **No buzzwords.** No "passionate", "seamless", "leverage", "robust". The reader is paid to spot them.

## 6. Widths tested

1440, 1024, 820, 768, 390. No horizontal scroll at any of them. The hero is one screen at all five; the Mobile band stacks at 600px; the card grid goes 3 → 2 → 1 column.

## 7. Where the taste-skill checker and this design disagree

The checker's rhythm family (SR-1 to SR-8) wants every section to be exactly one or two screens tall, sections to start on whole screens, and no more than two cards of one layout per page. With eight preview cards that must be visible at 390px, the Web section is 4.3 screens on a phone and 1.6 on a desktop: those two goals cannot both hold. The card grid was kept because "every project has a card and a preview" was an explicit requirement, and the section-height rules were not chased. Everything outside that family — contrast, alignment, container edges, button count, heading names, split lines — was fixed.
