# Research: Chapter 00 — Probability Foundations
## Bayesian Probability with LLMs

**Chapter one-line:** Everything you need before Chapter 1 — conditional probability, Bayes' theorem as arithmetic, nothing more.
**Research date:** 2026-05-13

---

## 1. Primary Sources

### Foundational papers and texts

- **Bayes, T. and Price, R. (1763). "An Essay towards solving a Problem in the Doctrine of Chances."** *Philosophical Transactions of the Royal Society of London*, 53, 370–418. Open-access Royal Society version: [https://royalsocietypublishing.org/rstl/article/doi/10.1098/rstl.1763.0053/119736](https://royalsocietypublishing.org/rstl/article/doi/10.1098/rstl.1763.0053/119736). A typeset modernized version is hosted at Washington University: [https://bayes.wustl.edu/Manual/an.essay.pdf](https://bayes.wustl.edu/Manual/an.essay.pdf). This is the founding document of the inference rule the chapter teaches as arithmetic. The pivotal passage states the problem in plain English: "Given the number of times in which an unknown event has happened and failed: Required the chance that the probability of its happening in a single trial lies somewhere between any two degrees of probability that can be named." Useful for the chapter as a historical sidebar — the reader is doing in five minutes what took the Royal Society sixty years to absorb.

- **Laplace, P.-S. (1814). *Essai philosophique sur les probabilités*.** Paris: Courcier. Open-access scan via Internet Archive: [https://archive.org/details/essaiphilosophiq00lapluoft](https://archive.org/details/essaiphilosophiq00lapluoft). Wikipedia overview: [https://en.wikipedia.org/wiki/A_Philosophical_Essay_on_Probabilities](https://en.wikipedia.org/wiki/A_Philosophical_Essay_on_Probabilities). Laplace independently rediscovered and fully developed inverse probability — what we now call Bayesian updating. He is the one who actually put the rule to work on real problems (e.g., the probability the sun will rise tomorrow given it has risen N times before). For Ch 0, Laplace is useful as the figure who treated the rule as practical arithmetic, not philosophical curiosity.

- **Grinstead, C. M. and Snell, J. L. (2006). *Introduction to Probability* (2nd revised ed.).** American Mathematical Society. Freely available as PDF: [https://math.dartmouth.edu/~prob/prob/prob.pdf](https://math.dartmouth.edu/~prob/prob/prob.pdf). Open Textbook Library record: [https://open.umn.edu/opentextbooks/textbooks/21](https://open.umn.edu/opentextbooks/textbooks/21). Chapter 4 is the canonical undergraduate treatment of conditional probability and Bayes' theorem — designed for sophomores in math, sciences, and engineering. The book runs Bayes through urn problems and the Monty Hall problem in exactly the register Ch 0 targets. Free to assign as a supplementary reading.

- **Ross, S. M. (2019). *A First Course in Probability* (10th ed.).** Pearson. Open preview: [https://www.cs.utexas.edu/~abdonm/SDS%20321/a_first_course_in_probability.pdf](https://www.cs.utexas.edu/~abdonm/SDS%20321/a_first_course_in_probability.pdf). The standard one-course-deep undergraduate text. §3.3 develops conditional probability from joint tables; §3.4 ("Bayes's Formula") is the cleanest derivation of the two-hypothesis form the chapter needs. The book is paywalled but earlier editions circulate; Ch 0 should point a serious student here for "if you want more practice."

- **Stigler, S. M. (1983). "Who Discovered Bayes's Theorem?"** *The American Statistician*, 37(4), 290–296. JSTOR-indexed; commonly cited entry point: [https://www.tandfonline.com/doi/abs/10.1080/00031305.1983.10483122](https://www.tandfonline.com/doi/abs/10.1080/00031305.1983.10483122) [verify — could not confirm the open landing page directly via WebSearch; the citation itself appears in Leonard 2014, *WIREs Computational Statistics*, [https://wires.onlinelibrary.wiley.com/doi/10.1002/wics.1293](https://wires.onlinelibrary.wiley.com/doi/10.1002/wics.1293)]. Useful as a sidebar source if the chapter wants to note that Bayes may not have been the first to state the rule (Stigler argues for Nicholas Saunderson). Optional flavor; do not lean on.

### Key empirical cases

- **The Monty Hall problem.** Documented effectiveness as an undergraduate teaching device for conditional probability in Roa-González et al. (2022), "Introducing conditional probability using the Monty Hall problem," *Journal of University Teaching and Learning Practice*: [https://files.eric.ed.gov/fulltext/EJ1348364.pdf](https://files.eric.ed.gov/fulltext/EJ1348364.pdf). A study of 20 non-mathematics undergraduates documented significant gains in conditional-probability understanding after a Monty Hall module. Fit for Ch 0 because the problem is solvable with the same arithmetic the chapter teaches, and it provides a third worked example beyond the urn.

- **The urn problem variations** in Grinstead & Snell Chapter 4 (link above). Multiple worked examples — drawing from urns of known composition, drawing without replacement, drawing from one of two urns chosen at random. Each maps cleanly to a 2-hypothesis Bayes calculation. The Ch 0 worked example in TIKTOK.md (3 red, 7 blue, "not blue" announced) is in this family.

- **[illustrative]** The "two children" problem (also called the "Boy or Girl" paradox). Statement: a family has two children; you are told at least one is a boy; what is the probability both are boys? Naive answer 1/2; conditional-probability answer 1/3 under standard assumptions. Documented teaching artifact at [https://en.wikipedia.org/wiki/Boy_or_Girl_paradox](https://en.wikipedia.org/wiki/Boy_or_Girl_paradox). Fit for Ch 0's "Identify where P(A|B) ≠ P(B|A) matters" exercise because the surprising answer comes precisely from the asymmetry.

---

## 2. The Core Concept — State of the Field

### What is settled

The arithmetic is not in dispute. P(A|B) = P(A∩B) / P(B), with P(B) > 0, is the definition; Bayes' theorem follows immediately. Every undergraduate probability textbook in print presents the rule the same way (Ross, Grinstead-Snell, DeGroot-Schervish, Pitman). The form most useful for two-hypothesis problems is P(H|D) = P(H)·P(D|H) / P(D), with P(D) expanded via the law of total probability as P(D|H)·P(H) + P(D|¬H)·P(¬H). Settled — see Ross §3.4 and Grinstead-Snell §4.

That P(A|B) ≠ P(B|A) in general is also settled. The asymmetry has a name in the medical literature ("the inverse fallacy") and a name in the legal literature ("the prosecutor's fallacy"). It is the same arithmetic mistake under both names.

### What is disputed

Nothing about the arithmetic. The dispute lives one level up — in *interpretation* of probability (frequentist vs. subjectivist) and in *which prior* to use when prior information is absent. Neither dispute belongs in Ch 0. The chapter teaches the calculation, not the philosophy. Ch 1 introduces the interpretive split; Ch 7 develops the prior-choice question.

One genuine pedagogical disagreement worth flagging: should Bayes' theorem be taught first via probability format (P(D|H) = 0.99 etc.) or via natural-frequency format ("of 1,000 patients, 1 has the disease...")? Gigerenzer & Hoffrage (1995) showed natural frequencies produce dramatically better student performance. That research belongs in Ch 1's pedagogical scaffolding, not Ch 0, but the author should be aware that the urn-style framing this chapter uses is closer to the probability format. The choice to teach formula-first is defensible (the formula is what the student will need going forward), but it is a choice.

### What has changed recently (last 5 years)

Almost nothing in the foundational arithmetic. Conditional probability has been taught the same way since Laplace. Two adjacent developments worth noting:

1. **LLM-mediated teaching.** Students now routinely ask ChatGPT or Claude to walk them through a Bayes calculation. The LLMs do this correctly for two-hypothesis problems with stated priors and likelihoods, but produce inverted answers (treating P(D|H) as P(H|D)) at non-trivial rates when the prompt is sloppy. This is a Ch 2 concern, not Ch 0, but it is the reason Ch 0 insists the student can compute the posterior by hand before opening Ch 1.

2. **Pandemic-era public exposure.** COVID-19 testing made conditional probability a kitchen-table topic from 2020–2022. The base-rate-neglect headlines that followed (rapid-test PPV in low-prevalence populations, etc.) live in Ch 1. For Ch 0, the takeaway is that the audience may now have *intuitive* (and sometimes wrong) priors about conditional probability before the chapter starts. The chapter should not assume a blank slate; it should assume a slate with a few smudges on it.

---

## 3. Application Domain Examples

Per TIKTOK.md, Ch 0's scenario domain is urn-style arithmetic only. Application examples should anchor the urn worked example and the three exercises.

1. **The TIKTOK.md urn (3 red, 7 blue, friend says "not blue").** Solved as: P(red | not blue) = P(red ∩ not blue) / P(not blue) = 0.3 / 0.3 = 1.0. The arithmetic is trivial *because "not blue" is equivalent to "red"* in this urn. A good chapter notes this and asks the reader why the answer is 1.0 — the exercise is recognizing that conditioning on the complement of "blue" forces "red" with certainty. Sharpens the move.

2. **Two-urn problem.** Urn 1 has 3 red, 7 blue. Urn 2 has 8 red, 2 blue. A friend flips a fair coin to choose an urn, then draws one ball and tells you it's red. Probability it came from Urn 2? P(U2 | red) = P(red | U2)·P(U2) / P(red) = (0.8 · 0.5) / (0.8·0.5 + 0.3·0.5) = 0.4 / 0.55 ≈ 0.727. This is the textbook two-hypothesis Bayes problem (Grinstead-Snell §4.1) and the cleanest version of what Ch 1 will do with disease prevalence. Fit for Exercise 2 directly.

3. **Drawing without replacement.** Urn has 5 red and 5 blue. Two balls drawn without replacement; you are told the first was red. P(second is red | first is red) = 4/9, not 5/10. Demonstrates P(A|B) ≠ P(A) — conditioning changes the sample space. Sets up the student for Ch 1's insight that conditioning is what makes the math interesting.

4. **2×2 joint probability table (Exercise 1).** Construct a 2×2 table over (Rain / No rain) × (Forecast rain / Forecast no rain). Give joint probabilities. Ask P(Rain | Forecast rain) vs. P(Forecast rain | Rain). The numbers are arbitrary, but the lesson is that the two conditionals are not the same number and not derivable from one another without the marginals. Forecast accuracy is one of the most common real-world places this matters.

5. **The Monty Hall problem.** Three doors; one hides a car; contestant picks Door 1; host opens Door 3, revealing a goat; should the contestant switch? Bayes gives P(car behind Door 2 | host opens Door 3) = 2/3 under standard assumptions. A famously counterintuitive result that the chapter's arithmetic resolves cleanly. Optional sidebar, not core exercise.

---

## 4. The Book's Thesis Connection

This book's thesis is that statistical inference should be taught through explicit side-by-side comparison of frequentist and Bayesian approaches, with the reader deciding. Chapter 0 is the prerequisite resolver — it does not advocate, it equips.

The book cannot deliver its thesis if the reader cannot compute a posterior by hand. The asymmetry P(A|B) ≠ P(B|A) is the foundation of every comparison the book will draw. The frequentist-Bayesian split that Ch 1 introduces — "the test reports P(positive | no disease); the clinician needs P(disease | positive)" — is unintelligible without the asymmetry from Ch 0. Bayes' theorem is the *bridge* the Bayesian approach uses to cross from the first quantity to the second. The frequentist approach does not have a bridge. Every chapter from 1 forward depends on the reader being able to compute the bridge.

The chapter is also the book's first commitment to the "show the work" rule. The urn example is solved step by step, formula on the page, arithmetic visible. This is the register the rest of the book will use. A reader who does not finish Ch 0 will not survive Ch 1's medical-test calculation — which is the same arithmetic with a story attached.

The author should resist the temptation to rush Ch 0. It is the shortest chapter for a reason: there is little to explain, and the explanation must be done well. The chapter is the contract.

---

## 5. Intellectual Lineage Notes

**Thomas Bayes (1701–1761).** English Presbyterian minister and amateur mathematician. The essay was published two years after his death. Richard Price found the manuscript in Bayes's papers, wrote about half of the published version himself, and submitted it to the Royal Society. Source: [Hooper (2013), *Significance*, "Richard Price, Bayes' theorem, and God"](https://rss.onlinelibrary.wiley.com/doi/full/10.1111/j.1740-9713.2013.00638.x); [Stigler (2018), "Richard Price, the First Bayesian," *Statistical Science*](https://projecteuclid.org/journals/statistical-science/volume-33/issue-1/Richard-Price-the-First-Bayesian/10.1214/17-STS635.pdf). Useful for the chapter as an epigraph or a one-paragraph sidebar: the rule's name comes from a man who never published it and who died before his work was understood. Price wrote in his transmission letter that the essay "has great merit, and well deserves to be preserved." That is the chapter's voice.

**Pierre-Simon Laplace (1749–1827).** French mathematician and astronomer. Independently developed inverse probability in the 1770s and 1780s, before he knew of Bayes's essay. *Théorie analytique des probabilités* (1812) and the more accessible *Essai philosophique sur les probabilités* (1814) made the rule a working tool of science. Laplace is who took Bayes' theorem from one essay in *Philosophical Transactions* to the default method for reasoning under uncertainty in nineteenth-century French science. Source: [Wikipedia, *A Philosophical Essay on Probabilities*](https://en.wikipedia.org/wiki/A_Philosophical_Essay_on_Probabilities); [Stigler (1986), *The History of Statistics*]. Useful for the chapter as a footnote: the rule the student will use was developed twice, independently, by a Presbyterian minister in Kent and the mathematician who calculated the perturbations of the planets. Same arithmetic. The arithmetic was findable.

Author could use either as an epigraph (Price's transmission letter is the strongest single sentence) or as a one-paragraph history at the chapter's end — the reader has just learned a rule that took European mathematics fifty years to absorb, and they did it in twenty minutes. That is the chapter's payoff move.

---

## 6. Pedagogical Delivery Research

### Prior knowledge required

The chapter assumes the reader knows: (a) what a probability is (a number between 0 and 1); (b) the addition and multiplication rules for independent events; (c) how to compute P(A) for simple events. TIKTOK.md confirms this in §49 ("knows arithmetic and basic probability"). No calculus required. No set theory beyond union and intersection notation.

### Common misconceptions in undergraduates

1. **The inverse fallacy.** Treating P(A|B) and P(B|A) as the same number. Documented in Eddy (1982) for medical contexts; addressed structurally in Bar-Hillel (1980) [https://worthylab.org/wp-content/uploads/2020/12/bar-hillel_1980.pdf](https://worthylab.org/wp-content/uploads/2020/12/bar-hillel_1980.pdf). This misconception is exactly what Ch 0 is designed to break. The chapter should hit it explicitly: ask the reader to compute both conditionals from a joint table and show they are different numbers.

2. **Forgetting to renormalize.** When students apply Bayes' theorem from memory, they often write P(H|D) = P(D|H)·P(H) without the denominator. Pedagogically, this means the chapter should derive Bayes from the definition of conditional probability *each time*, not present it as a memorized formula. Grinstead-Snell §4.1 does this well.

3. **Conflating "and" with "given."** Students compute P(A ∩ B) when asked for P(A | B). Diagnostic: ask the student to identify the sample space. P(A ∩ B) lives in the full sample space; P(A | B) lives in B.

4. **Treating prior probabilities as 50/50 when not given.** A reflex from coin-flip examples. The chapter should give a problem where the prior is *not* 50/50 (the two-urn problem with an unfair coin, for instance) to break the habit before Ch 1.

### Instructional sequences shown to work

The standard sequence in undergraduate probability texts: (1) joint probability from a 2×2 table, (2) marginal probability by summing rows/columns, (3) conditional probability as the ratio, (4) Bayes' theorem as a rearrangement of the same ratio. Roa-González et al. (2022) document that introducing conditional probability via the Monty Hall problem improves perception scores in a pre/post design with non-math-majors. Grinstead-Snell §4 is the canonical four-step sequence. Ross §3 is identical in structure with more exercises.

### Known teaching failure modes

- **Formula-first.** Presenting Bayes' theorem as a formula to memorize, without deriving it from the conditional-probability definition. Students pass the test, fail to apply the rule outside test conditions.
- **Skipping the joint table.** The 2×2 table is the most reliable scaffold for the inverse fallacy. Chapters that move directly to the formula lose the students whose intuitions are not yet calibrated.
- **All examples have prior = 0.5.** The most common pedagogical failure: every textbook example uses two equally likely hypotheses. The student leaves believing priors are 50/50 by default. Ch 1's medical example then breaks the student's brain. Fix in Ch 0: at least one worked example with an asymmetric prior.

### The difference between students who understand vs. memorize

Students who *understand* can compute the posterior from a joint table without knowing the formula. Students who *memorize* can apply the formula when prompted with P(D|H), P(H), and P(D), but cannot identify those quantities in a problem stated in plain English. Ch 0 should require both moves. The diagnostic exercise: give the student a story (with a stated prevalence and a stated test accuracy) and ask them to construct the 2×2 table themselves before applying the formula.

---

## 7. Representation and Display Research

No special display required for this chapter — Ch 0 is arithmetic only per TIKTOK.md. The chapter does not yet introduce the side-by-side frequentist/Bayesian comparison table; that arrives in Ch 1.

What Ch 0 should display:
- A 2×2 joint probability table for the worked exercise.
- Bayes' theorem written out as a single equation, with each term labeled in plain English.
- One worked calculation with every arithmetic step on the page.

That is all. The chapter's discipline is to do less than the reader expects and do it cleanly.

---

## 8. Open Questions and Research Gaps

- **Stigler (1983) "Who Discovered Bayes's Theorem?"** I could not confirm a freely available open-access version of this paper. The citation is well established (Leonard 2014, Stigler 2018) but the original is behind a JSTOR/Taylor-Francis paywall. If the chapter uses Stigler as a sidebar source, the author should pull the PDF from a university library before relying on its specific claims. Flagged `[verify]`.

- **Roa-González et al. (2022) on Monty Hall pedagogy.** The study has n=20, no control group, pre/post design only. The effect is real but the evidence is weak by itself. The chapter should cite it as suggestive, not authoritative.

- **The chapter's worked example trades clarity for a degenerate case.** "Not blue" in the 3-red-7-blue urn is equivalent to "red," so P(red | not blue) = 1. This is a calculation, but it does not exercise the renormalization the student needs. A better worked example would be: urn has 3 red, 7 blue. Two balls drawn without replacement; you are told the first was red. What is P(second is red | first is red)? Or: the two-urn problem from §3 above. The author should consider whether the TIKTOK.md example is the strongest pedagogical choice.

- **No undergraduate cognitive-psychology research located specifically on the urn-conditioning fallacy at scale.** Most base-rate-neglect literature uses medical or legal framings (Eddy, Casscells, Bar-Hillel). Whether undergraduates fail the urn version at the same rates is a real research gap. The chapter could acknowledge it.

- **Sources likely to age within 3 years.** None of the historical sources will age. The Monty Hall pedagogy paper is recent and could be superseded but the result is robust enough to cite for the foreseeable future.

---

## 9. Sourcing Notes

- **Bayes (1763).** Open access via Royal Society and Internet Archive. No paywall.
- **Laplace (1814).** Open access via Internet Archive (French original). An English translation by Truscott and Emory exists; available on Project Gutenberg and Internet Archive variants. No paywall.
- **Grinstead & Snell (2006).** Open access via Dartmouth (AMS license). No paywall. The author can assign this as a free companion text.
- **Ross (2019).** Pearson, paywalled. Earlier editions circulate in PDF; the cited UT Austin PDF (10th ed) is available but technically restricted to course use.
- **Stigler (1983).** Paywalled. Citation verified through secondary sources but original PDF not retrieved; flagged `[verify]` for direct claims.
- **Hooper (2013) and Stigler (2018).** Both open access through *Significance* and *Statistical Science* respectively. Strong, citable, freely linkable.
- **Bar-Hillel (1980).** Open PDF via Worthy Lab archive; original *Acta Psychologica* PDF behind a ScienceDirect paywall. The Worthy Lab version is fine to cite.
- **Roa-González et al. (2022).** Open access via ERIC.

No fact-checking gaps on the arithmetic (it is settled). One fact-checking gap on Stigler's specific historical claim that Saunderson may have predated Bayes — flagged above.
