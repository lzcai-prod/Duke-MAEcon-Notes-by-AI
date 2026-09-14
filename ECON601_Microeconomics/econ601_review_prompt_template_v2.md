# Reusable prompt: ECON 601 lecture review builder (v2)

Paste the block below into a new session. Fill in the four bracketed fields at the top and attach the relevant PDFs to the project.

**What changed from v1.** The v1 template produced documents that were rigorous and unreadable: they restated the lecture in a different order without ever making a concept click. v2 fixes that. The main changes are a concrete scene at the head of every section instead of the formulaic "Why this is not trivial," one numerical worked consumer carried through the entire document, proofs demoted into skippable blocks, and the removal of the reference card and exercise sections, which duplicated material available elsewhere. Format changes: keep the lecture number in the title, use a two-level numbered table of contents.

---

## FILL IN FIRST

- **Focus lecture:** `[e.g. Lecture 4: Hicksian Demand]`
- **Supplies from earlier lectures:** `[e.g. Lectures 1-3]`
- **Destination lectures:** `[e.g. Lecture 5, Duality and Slutsky]`
- **Running example to carry through:** `[leave blank and let the model pick one, or specify]`

---

## THE PROMPT

You are helping me build a printable study document for a graduate microeconomics course. I have attached the lecture notes, review session solutions, and problem sets to this project. Read them before writing anything.

The document is for someone who has read the lecture notes and did **not** understand them. Restating the notes in a new order is a failure. If a reader could get the same thing from the notes, the section has not earned its place.

### Step 0: read the source material

Read every attached file in full before planning. Two mechanical notes:

- Project PDFs are sometimes zip archives containing per-page `.jpeg` and `.txt` files plus a `manifest.json`. If `pdfinfo` fails with a trailer-dictionary error, check `file` on it and unzip instead. Genuine PDFs read fine with `pdftotext -layout`. Both kinds may appear in the same project.
- Note every place the lecture says "Proof. Exercise.", "Try this.", "Easy.", "Omitted.", or "Later." Those are the highest-value items and must all appear in the finished document with full proofs.

### Step 1: find the logical spine, not the section list

Do **not** organize the document the way the lecture is organized.

Work out the **sequence of questions** the focus lecture is answering, and use those as the top-level sections. Usually each question costs one more assumption than the last. Say explicitly what each question costs.

Where the ladder is flat, say so and say why, because that is usually the most informative thing about the lecture. (Example from Lecture 3: homogeneity, monotonicity and quasi-convexity of the value function cost nothing about preferences at all, because they follow from the shape of the budget set. A reader who knows that will never again reach for a curvature assumption while proving them.)

Then state, up front, **why the material exists at all**, in terms of a problem in the world.

### Step 2: pick the running example before writing a word

Choose one concrete agent with **real numbers** and carry them through every section. Not a symbolic example. Actual dollars and actual quantities.

The example must be simple enough to compute in your head once set up, and rich enough that every property in the lecture can be tested on it. For consumer theory, a Cobb-Douglas consumer with two goods and round numbers works; keep a second, degenerate example (perfect substitutes, a bliss point) on hand for the counterexample sections.

**Verify every number with a script before writing it into the document.** Run the arithmetic, print it, and check it. A document full of concrete numbers is worthless if the numbers are wrong, and wrong numbers are worse than no numbers because they destroy trust in the parts that are right.

Introduce the example in Section 1 with a small table: symbol, her number, what it is in plain words.

### Step 3: structure the document like this

1. **Why any of this exists.** The motivating problem, stated as a situation rather than as mathematics. A small TikZ diagram showing the arc, with the focus lecture visibly the centre. Then the running example introduced with its numbers. Then a table of the questions the lecture answers, what each costs, and where each is answered. Then a **plain-words glossary**: every symbol in the lecture with a "say it like this" column. (`v(p,I)` is "her standard of living given these prices and this income," not "the indirect utility function.")
2. **What the earlier lectures hand over.** A "delivery manifest" table: earlier result → what it becomes here → which question uses it. Then the two or three earlier results that genuinely shape the answers, explained properly. Then an explicit line naming the earlier material that is **background you can leave alone**, so I know what not to re-read.
3. **One section per question.** See Step 4 for the internal shape, which is the heart of v2.
4. **Where this goes.** The destination lecture as the continuation: what carries over unchanged, what is new, and what looks similar but is not. The "looks similar but is not" list is the most valuable part; make it concrete. End with a short reading list with textbook section references.
**Do not include a reference card, an exercise section, or a standalone errata section.** All three were tried and all three were dead weight. Typos and gaps in the course materials still get flagged, but inline, in a boxed note at the point where the reader would otherwise be misled. Formula lists are available in the notes, exercise commentary is not what this document is for, and an errata list at the end is read by nobody; the same errata inline at the point of confusion are read by everybody.

### Step 4: the internal shape of a question section

This is the change that matters most. Every question section has five parts, in this order.

**(a) The scene.** Open with a specific, concrete, non-mathematical situation, with numbers, and make it the subsection heading. Never use a formulaic heading like "Why this is not trivial"; that phrasing signals a template and explains nothing.

Good scene headings from previous builds:
- *A number for how well off you are* — a city council choosing between a cash transfer and a price cap, with both options costed out for the running consumer.
- *Dropping three zeros from the currency* — Turkey's 2005 redenomination, for homogeneity of degree zero.
- *Two countries and the one in between* — three price regimes where the average regime is worse than both extremes, for quasi-convexity.
- *Coke, Pepsi, and a one-cent price change* — a two-cent move that shifts welfare 1% and flips the entire cart, for continuity of the value against discontinuity of the choice.
- *The suitcase that is already packed* — a raised weight allowance is worth the best item you left behind, for the envelope theorem.
- *Reading the shopping list off the pain* — a penny on coffee costs her thirty cents, and she buys thirty coffees, for Roy's identity.

The test: you should be able to reconstruct the whole lecture from the list of scene headings alone.

**(b) The claim in plain words.** One or two sentences, bolded, containing no symbols. If you cannot state the result without symbols, you do not understand it well enough to explain it.

**(c) The formal statement.** Definition, proposition, theorem, with its source tag.

**(d) The proof, in a skippable block.** Put every proof inside `\begin{leftbar}...\end{leftbar}` from the `framed` package, preceded by the line `Proof. Skippable on a first read.` Nothing later in the document may depend on having read a proof block. A reader must be able to go cover to cover ignoring all of them and lose nothing.

Still prove everything the lecture leaves open, in full. The proofs are the reason the document is trustworthy; they are just no longer the reason it is readable.

**(e) What breaks.** Weaken a hypothesis and show the failure **concretely**, on a named example with numbers, not as an abstract remark. Say which hypothesis was doing which job.

### Step 5: content rules

- Every claim gets a source tag in the small-sans style `(L2 p.6)` or `(RS3 Q1.2)`.
- Use inline `← L1:` and `→ L4:` flags in running prose and **inside proofs**, at the exact line where an earlier result is being spent. These are more useful than a front-loaded manifest table, which cannot tell you which step is consuming what. Keep the boxed forward-link notes at section ends as well.
- Where two results differ by a single word (strict versus weak), put them adjacent and say explicitly what the one character changes.
- Fold worked examples into the section whose machinery they demonstrate. No standalone examples section.
- For any fully worked example, finish with an **audit**: check the answer against each general property established earlier, with numbers. The audit is the lesson, not the algebra. Use audits repeatedly, not once.
- Where a result is invariant to relabeling (an ordinal object), demonstrate it by recomputing the example under a transformed utility function and showing every input changes while the answer does not. Tables comparing the two are very effective.
- Add a real-world grounding paragraph wherever a modelling assumption is doing silent work. (Example: homogeneity of degree zero is the formal statement that the consumer has no money illusion, which real people demonstrably do have; name the line of the proof that delivers the property so the reader knows where the model and the world part company.)

### Step 6: writing style

- No em dashes anywhere.
- Never use the phrase "rather than."
- Explanation or example **before** the formula, never after.
- Formulas are displayed, never inlined in a sentence.
- Plain declarative sentences. No "it's worth noting," no "not X but Y" constructions, no colon-then-reveal.
- Assume I am competent and short on time. Do not pad.
- Analogies are welcome and should carry real structural weight. A good analogy explains *why* the result is true, not merely what it feels like.

### Step 7: figures

Draw figures in TikZ. Three to five for a document of this size. **Make them concrete**: plot the running example's actual budget lines and actual numbers with axis ticks, not a generic schematic. A figure showing three budget lines at $2/$6, $6/$2 and $4/$4 crossing at (15,15) teaches more than the same figure labelled $p^1$, $p^2$, $p^t$.

Label them so a caption is unnecessary.

### Step 8: build it as a PDF

Use `pdflatex`. Environment gotchas learned the hard way:

- `lmodern` is **not installed**. Use `\usepackage[T1]{fontenc}` with `\usepackage{mathptmx}`.
- If you use `\textsf` anywhere (the source-tag style does), you must also load `\usepackage[scaled=0.90]{helvet}`, or `microtype` dies with a font-expansion error on the non-scalable `cmss`.
- Available and tested: `geometry`, `amsmath`, `amssymb`, `amsthm`, `booktabs`, `array`, `tikz` (with `arrows.meta`, `positioning`, `calc`), `enumitem`, `titlesec`, `fancyhdr`, `framed`, `xcolor`, `hyperref`.
- `snugshade` from `framed` for boxed notes; `leftbar` from the same package for skippable proof blocks. Using two visually distinct devices matters: the reader must be able to tell a flag from a proof at a glance.
- Title keeps the lecture number and topic: `Lecture 3: Indirect Utility`.
- Two-level numbered table of contents: use `\subsection`, not `\subsection*`, and set `\setcounter{tocdepth}{2}`.
- Letter paper, 1 inch margins, 11pt, running header.
- Compile twice. Check `grep -c "Overfull \\hbox"` is zero and `grep -c undefined` is zero.

**Figure debugging, which always takes more passes than expected.** Rasterize every figure page with `pdftoppm` and actually look at it. Recurring failures, all of which happened:
- Node labels colliding with each other or with a plotted curve. Fix by moving the label into empty space and adding a short leader arrow.
- Arrow labels placed on short arrows in a node chain; put the text inside the boxes instead.
- Fills rendering invisible because the shade colour is too light. Use `black!11`, not a 0.93 grey.
- Axis ticks colliding when values are close together. Drop the redundant ones.
- Annotation text overrunning the axis line. Move it to the emptiest quadrant of the plot.

Write the final PDF and the `.tex` source to the outputs directory and call `present_files`.

### Step 9: before you deliver

- Could a reader reconstruct the lecture's argument from the section headings alone? If any heading is formulaic or is the lecture's own section name, rewrite it.
- Does every question section open with a concrete scene containing numbers?
- Is every proof inside a skippable block, and does the document still make sense if you delete them all?
- Was every number in the document verified by running the arithmetic?
- Is every "what breaks" illustrated on a named example rather than asserted?
- Are all formulas displayed and all explanations ahead of their formulas?
- Zero overfull boxes, zero undefined references, all figure pages visually inspected?

---

## Notes on reusing this

- One document per lecture, not one covering several. The `←` and `→` flags are what connect them.
- The hypothesis-family classification (regularity, curvature, monotonicity, smoothness, constraint geometry) is specific to consumer theory, and even within it the right list changes: Lecture 3 needed a fifth family, constraint geometry, that Lectures 1 and 2 did not. Derive the classification from the material rather than importing it.
- If the focus lecture has no natural question sequence, the fallback spine is: what object are we building, what must be true for it to exist, what is true of it always, how do we compute it, what do we do with it.
- Expect roughly 18 to 20 pages. If it is running past 23, the proofs have probably crept back out of their blocks and into the main line of the argument.
- Documents already built with earlier versions of this template can be brought into line cheaply: the TOC depth is a one-line change, the scene headings are a rewrite of one paragraph per section, and moving proofs into `leftbar` is mechanical. The running numerical example is the only expensive retrofit, and it is also the one that does the most work.
