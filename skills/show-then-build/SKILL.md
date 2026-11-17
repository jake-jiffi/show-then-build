---
name: show-then-build
description: >-
  Show a change before building it. For any feature, change, redesign or fix to something that
  already exists: understand the problem, make a preview page the person can open (before and
  after, a clickable prototype for visual changes, two or three options when the direction is
  open, and a decisions form for open questions), wait for a yes, then write a short spec and
  plan, build it, and check the result against the approved preview. Use this whenever someone
  asks to add, change, improve, redesign or fix something in an existing app, site, dashboard or
  tool, even if they only say "add X" or "can we change Y", and especially when the change is
  visual or they are not sure what they want. Tiny edits skip the preview. Pairs with
  build-then-break.
license: MIT
---

# Show, then build

The expensive mistake is building the wrong thing well. A preview takes minutes to judge. Rework
takes hours. So show the change first, in a form a person can judge at a glance, then build only
what they approved.

The person reading may not be a developer. Write everything they will see in plain language.

This skill decides what gets built. Its partner, build-then-break, governs how it is built and
checked. Every build that comes out of this skill goes through build-then-break when it is
installed. Changes that need no preview skip this skill and go straight there.

## Pick the level

Effort scales with how much there is to see and decide.

| Level | When | What to do |
|---|---|---|
| Small | Typo, wording, a config value, or a bug with one obvious fix and nothing new to look at | Say the plan in one line, then build and check. No preview. Report in three lines at most. |
| Standard | A feature or change with one sensible direction | Understand, show, wait, build, prove. |
| Open | A redesign, anything visual with real choices, "I'm not sure how this should work", or something hard to undo | Standard, plus two or three options and a decisions form. |

Unsure between Small and Standard? Ask whether the person would want to see it before it exists.
If yes, Standard.

## 1. Understand

No code yet.

- Restate the problem in a sentence or two, in their words.
- Read the real current state: the actual files, screens and data. The "before" you show must be
  the real before, not a guess.
- Note what else this touches: who uses it, what depends on it, what must not break, and the
  existing look and conventions.
- Collect open questions. Don't fire them off one at a time in chat, where they get missed. They
  go in the decisions form in the preview. Ask in chat first only if you can't start the preview
  without the answer.

## 2. Show

Make one preview page. Start from `assets/preview-template.html`: copy it, fill it in, and save it
in the project as `previews/YYYY-MM-DD-short-name.html`. It is one self-contained file that opens
in any browser. If you are somewhere that publishes artifacts instead of files, publish it as an
artifact with the same contents.

Put in it, in this order:

1. **What and why.** Three sentences at most.
2. **Before and after.** Side by side. For a visual change, recreate the real before faithfully
   and put the proposed after next to it. For a change you can't see, use concrete examples: what
   goes in, what happens now, what will happen.
3. **Try it.** For anything visual or interactive, a working prototype of the after, in the
   project's own colours, type and components, so it reads as their product and not a mock-up.
   Make the states that matter reachable: empty, error, long text, phone width. Use sample data
   and label it as sample. The Phone width button narrows the prototype's box, not the browser
   window, so write the narrow layout with `@container`, not `@media`. Press the button and
   check the layout changes before you hand the preview over.
4. **Options** (Open level). Two or three directions that are really different, not three shades
   of one idea. For each: what it is and what it costs. Mark one as recommended and say why.
5. **Decisions.** Every open question as a form item: the question, the choices, which one you
   recommend, what each choice changes, and a comment box. Only questions whose answer changes
   what gets built.
6. **Not changing.** What stays as it is, so silence isn't read as scope.

Rules for the preview: no network calls or CDN links, no real customer data, no passwords or
keys. Prototype only what is needed to judge the change. It is a sketch, not a second product.

## 3. Wait

Stop here. Don't touch the project's real files yet.

Tell the person, in a few lines: where the preview is and how to open it, what you recommend, and
what you need from them (pick an option, answer the decisions, press **Copy my answers**, paste
them back). The preview does the explaining, so don't repeat its contents in chat. Then wait.

When the answers come back, read all of them before acting. Anything marked NOT ANSWERED is
still open: list each one with the choice you recommend and get a yes before you build. Don't
fill it in for them. If the feedback changes the design more than slightly,
update the preview and get a yes on the new version. The approved preview is the contract for the
build.

## 4. Spec and plan

Write both from the approved preview and the answers. Keep them short. Save them beside the
preview (`previews/<same-name>-spec.md`).

- **Spec:** what will be built, each decision and the choice made, and acceptance checks that a
  person or a test can verify.
- **Not shown in the preview:** anything the spec decides that the person hasn't seen. Data
  changes, edge cases, things being removed. Most people won't read a spec that matches what they
  approved, so this list is how surprises get seen. If there is nothing, write "Nothing".
- **Plan:** ordered steps, each with its own check.

Show the person the "Not shown in the preview" list and the plan in a few lines. If that list is
empty or minor, carry on. If it touches data, money, access or deletes anything, wait for a yes.

## 5. Build

- Follow the plan in order and run each step's check before the next step.
- Independent pieces can go to subagents when they are available. Otherwise do them one at a time.
- Stay inside what was approved. If you notice something else worth fixing, mention it. Don't
  build it.
- Build with the build-then-break skill when it is installed: its build rules while you write,
  its break drill before you call a step done. Without it, still try to break each step yourself
  (empty, huge and odd input, the unhappy path) before moving on.

## 6. Prove

Look at the real thing, not just the code.

- Open the built result in a browser tool (Playwright or similar) if you have one. Walk through
  the same flows as the preview at desktop and phone widths, and take screenshots.
- With no browser tool, run every check you can, then give the person a short list of what to
  click and what they should see.
- Compare against the approved preview point by point.

Then report, in this shape. The report is the reply: add only what the person must act on, and
leave the rest (how you checked, what held, small differences) in the spec file where they can
find it. A long reply buries the answer.

```
Built: <what, in a sentence>
Matches the preview: yes | no, with each difference and why
Acceptance checks: <n> of <n> pass (list any that fail)
Still open: <anything undecided or deferred, or "nothing">
```

## Keep it light

- One preview per change. Update it rather than making a new one.
- Don't narrate these steps or restate this skill in replies.
- A preview that takes longer than the change itself means the level was wrong. Drop to Small.

`references/worked-example.md` walks one change through all six steps. Read it only if stuck.
