# One change, all six steps

**The ask:** "Customers keep booking the wrong service. Can we make the service picker clearer?"

**Level:** Open. It is visual, and "clearer" could mean several things.

## 1. Understand

- Read the booking form. Services are a plain dropdown of 14 names with no prices or durations.
- Touches: the booking form only. The services list comes from one data file. Confirmation emails
  read the same names, so names must not change.
- Open questions: show prices? group by type? does phone matter most?

## 2. Show

`previews/2026-11-17-service-picker.html`, from the template:

- **What and why:** People pick the wrong service because 14 similar names sit in one dropdown.
  This makes each service a card with its length and price, grouped by type.
- **Before and after:** the real dropdown, recreated, beside the proposed cards.
- **Try it:** working cards in the site's own colours, with a long service name, the phone width,
  and the "no services available" state.
- **Options:** A. Grouped cards (recommended: fewest wrong picks, more scrolling). B. Keep the
  dropdown, add price and length to each line (smallest change, still cramped). C. Two steps:
  pick a type, then a service (clearest, one more tap).
- **Decisions:** Show prices on the cards? (Yes, recommended: stops price questions at the desk /
  No.) Which type goes first? (Most booked, recommended / Alphabetical.)
- **Not changing:** service names, the rest of the form, confirmation emails.

## 3. Wait

"The preview is at previews/2026-11-17-service-picker.html. Open it in your browser. I'd go with
option A. Pick an option, answer the two questions, press Copy my answers and paste them here."

Answers come back: option A, prices yes, most booked first, comment "make the price smaller than
the name".

## 4. Spec and plan

- **Spec:** grouped service cards replace the dropdown. Each card shows name, length, price (price
  in smaller type). Groups ordered by bookings in the last 90 days. Acceptance checks: every
  service appears once; choosing a card sets the same form value the dropdown did; works by
  keyboard; readable at 390px wide.
- **Not shown in the preview:** group order needs a booking count, so the build adds one read of
  booking history. Nothing is written or deleted.
- **Plan:** 1) card component, check it renders all 14. 2) wire it to the form value, check a
  booking still submits. 3) ordering, check against a hand count. 4) phone layout, check at 390px.

The "not shown" item only reads data, so carry on.

## 5. Build

Four steps in order, each checked before the next. Noticed the form's error message is vague:
mentioned it, did not change it.

## 6. Prove

Opened the real page in a browser at desktop and phone widths, booked one of each type, compared
with the preview.

```
Built: grouped service cards on the booking form, replacing the dropdown.
Matches the preview: yes, except card spacing is 4px tighter on phone so two cards fit above the fold.
Acceptance checks: 4 of 4 pass.
Still open: the form's error message is vague. Not part of this change.
```
