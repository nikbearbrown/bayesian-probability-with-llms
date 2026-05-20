# Research: Chapter 03 — Counting and Estimating
## Bayesian Probability with LLMs

**Chapter one-line:** The binomial problem — estimating a proportion — run both ways, producing the book's first full side-by-side comparison and the clearest possible illustration of the difference between a confidence interval and a credible interval.

**Research date:** 2026-05-13

---

## 1. Primary Sources

### Foundational papers and texts

1. **Hoekstra, R., Morey, R. D., Rouder, J. N., & Wagenmakers, E.-J. (2014).** "Robust misinterpretation of confidence intervals." *Psychonomic Bulletin & Review,* 21(5), 1157–1164. [Springer link](https://link.springer.com/article/10.3758/s13423-013-0572-3). 120 researchers and 442 psychology students were asked to evaluate six false statements about a 95% confidence interval. Both groups endorsed, on average, more than three of the six falsehoods. Self-declared statistical experience did not predict performance. This is the load-bearing empirical citation for "the CI is famously misinterpreted, even by experts."

2. **Morey, R. D., Hoekstra, R., Rouder, J. N., Lee, M. D., & Wagenmakers, E.-J. (2016).** "The fallacy of placing confidence in confidence intervals." *Psychonomic Bulletin & Review,* 23(1), 103–123. [PMC open access](https://pmc.ncbi.nlm.nih.gov/articles/PMC4742505/). The companion theoretical paper. Demonstrates with worked examples that confidence intervals can fail to support the inferences they are routinely used to support — specifically, they do not justify post-data probability statements. The chapter's pedagogical position rests on this paper being correct.

3. **Greenland, S., Senn, S. J., Rothman, K. J., Carlin, J. B., Poole, C., Goodman, S. N., & Altman, D. G. (2016).** "Statistical tests, P values, confidence intervals, and power: a guide to misinterpretations." *European Journal of Epidemiology,* 31(4), 337–350. [PMC open access](https://pmc.ncbi.nlm.nih.gov/articles/PMC4877414/). 25 enumerated misinterpretations of frequentist concepts. The strongest single-source list for the chapter's "what the CI does *not* say" subsection. Useful precisely because the authors are not Bayesian partisans — they argue for correct frequentist interpretation.

4. **Bayes, T. (1763).** "An Essay towards solving a Problem in the Doctrine of Chances." *Philosophical Transactions of the Royal Society of London,* 53, 370–418. [Royal Society Publishing](https://royalsocietypublishing.org/doi/10.1098/rstl.1763.0053). The original paper. Bayes specifically solves the binomial inverse probability problem — given observed successes and failures, what is the distribution over the underlying success rate? Cite for the historical primacy: the chapter's worked problem is *the original problem* Bayes addressed.

5. **Clopper, C. J., & Pearson, E. S. (1934).** "The Use of Confidence or Fiducial Limits Illustrated in the Case of the Binomial." *Biometrika,* 26(4), 404–413. The canonical exact frequentist interval for a binomial proportion. Cite for the classical frequentist solution; flag that the chapter uses the normal-approximation interval (Wald) for pedagogical clarity but should at least note Clopper-Pearson exists.

6. **Wilson, E. B. (1927).** "Probable inference, the law of succession, and statistical inference." *Journal of the American Statistical Association,* 22(158), 209–212. The Wilson score interval — the modern default recommendation for small-sample binomial proportions ([Brown, Cai, & DasGupta, 2001](https://projecteuclid.org/journals/statistical-science/volume-16/issue-2/Interval-estimation-for-a-binomial-proportion/10.1214/ss/1009213286.full)). The chapter should note that the Wald interval used in TIKTOK.md's worked numbers is the *taught* interval, not the *recommended* interval.

7. **Gelman, A., Carlin, J. B., Stern, H. S., Dunson, D. B., Vehtari, A., & Rubin, D. B. (2013).** *Bayesian Data Analysis,* 3rd edition. CRC Press. [Free PDF from author](http://www.stat.columbia.edu/~gelman/book/BDA3.pdf). Chapter 2 gives the Beta-Binomial conjugate derivation in full. The chapter's canonical reference for the Bayesian construction; cite the section, not just the book.

### Key empirical cases

1. **Hoekstra et al. (2014) headline number.** Researchers endorsed an average of 3.51 false statements out of 6 about CIs; students endorsed 3.45. The student/researcher gap was not statistically meaningful. Cite this in the chapter as the empirical hook for "even people who are paid to know this get it wrong."

2. **The 2014–2016 statistical literature wave.** Greenland et al. (2016), Morey et al. (2016), Hoekstra et al. (2014), and the ASA's 2016 statement on p-values are part of a coordinated push by frequentists and Bayesians alike to correct widespread misinterpretation. The chapter's argument is *not* that the Bayesian is right and the frequentist is wrong — it is that the CI is widely misread *as if it were* a credible interval, and that the Bayesian gives directly what people were trying to extract from the CI.

3. **ISO 2859-1 acceptance sampling.** [ISO 2859-1:1999](https://www.iso.org/obp/ui/#iso:std:iso:2859:-1:ed-2:v1:en). Real, in-use manufacturing standard built around binomial defect rates and Acceptable Quality Limits (AQL). The chapter's scenario is not synthetic — exactly this calculation drives accept/reject decisions on real production batches.

---

## 2. The Core Concept — State of the Field

### What is settled
- **The Beta-Binomial conjugate update.** Beta(α, β) prior + Binomial(n, k) likelihood gives Beta(α+k, β+n−k) posterior. Closed form, derivable in two pages, in every Bayesian intro text. ([Gelman et al. 2013, Ch. 2](http://www.stat.columbia.edu/~gelman/book/BDA3.pdf).)
- **The CI is not a probability statement about the parameter.** A 95% CI is a procedure that produces intervals; 95% of such intervals over hypothetical repetitions contain the true parameter. For any given interval, the true parameter is either in it or not — there is no probability statement attached. ([Morey et al. 2016.](https://pmc.ncbi.nlm.nih.gov/articles/PMC4742505/))
- **For large samples with flat priors, frequentist and Bayesian intervals nearly coincide.** This is why both approaches can produce defensible results most of the time and why the difference matters most at small n.
- **The credible interval *is* a probability statement about the parameter** — conditional on the prior and model. ([Gelman et al. 2013.](http://www.stat.columbia.edu/~gelman/book/BDA3.pdf))

### What is disputed
- **Whether the CI misinterpretation problem is fixable by better teaching or whether the concept is structurally unteachable.** Morey et al. (2016) argue the latter — that the standard interpretations are wrong and there is no simple correct interpretation. The teaching community pushes back. The chapter should land on Morey's side without making it a polemic.
- **Which prior is "uninformative."** Beta(1,1) is the uniform prior on the proportion. Jeffreys's prior is Beta(0.5, 0.5). Haldane's prior is Beta(0, 0). All are defended as "objective." The chapter can sidestep by using Beta(1,1) and noting briefly that "uninformative" is itself a choice.
- **Whether the Wald interval should be taught at all.** [Brown, Cai, & DasGupta (2001)](https://projecteuclid.org/journals/statistical-science/volume-16/issue-2/Interval-estimation-for-a-binomial-proportion/10.1214/ss/1009213286.full) argue Wald has bad coverage for small samples and recommend Wilson, Agresti-Coull, or Jeffreys. The chapter uses Wald for transparency; it should acknowledge this is a pedagogical choice, not best practice.

### What has changed recently (last 5 years)
- **Replication crisis aftermath.** The 2014–2016 wave of misinterpretation papers (Hoekstra, Morey, Greenland) has filtered into intro-stats curricula slowly. Bayesian methods are now standard in some intro sequences and absent from others; convergence has not happened.
- **Computational accessibility.** Beta-Binomial inference no longer requires a textbook table — it requires three lines of Python. This shifts the pedagogical center of gravity: students can run the analysis, but explaining what it *means* is harder than ever because the computation hides the inference.

---

## 3. Application Domain Examples — Manufacturing QC and Binomial Estimation

1. **ISO 2859-1 / ANSI Z1.4 acceptance sampling.** [ISO standard](https://www.iso.org/obp/ui/#iso:std:iso:2859:-1:ed-2:v1:en). The international standard governing how manufacturers decide whether to accept a production lot. Built on binomial OC (operating characteristic) curves. Real engineers in real factories use exactly this calculation. The chapter's "50 boards, 8 defective" scenario is structurally identical to a real AQL lot inspection.

2. **Semiconductor defect rates.** Yield loss in chip manufacturing is modeled as binomial / Poisson at the die level. Reference: standard fabs report defect density (defects per cm²) which feeds into wafer-level yield via Poisson-binomial. The chapter need not go this deep but should signal that the toy 50-board problem scales to billion-dollar yield decisions.

3. **Pharmaceutical batch release testing.** Tablet content uniformity, dissolution testing — binomial pass/fail counts feeding into batch accept/reject decisions. Regulated environments use Clopper-Pearson exact intervals or sequential testing (Wald). FDA guidance documents on batch release sampling are good primary sources; [FDA's Guidance for Industry on Process Validation](https://www.fda.gov/media/71021/download) is the umbrella document.

4. **Software defect estimation.** Number of bugs found in n test cases — exactly the binomial inference problem in a different domain. Capture-recapture variants extend this. Mentioned briefly to signal that the chapter's method is not domain-locked.

5. **[illustrative]** A new supplier sends 30 boards, 3 defective. The exercise (TIKTOK.md line 311) walks the student through the calculation. The didactic point: at n=30 with k=3, the frequentist and Bayesian intervals diverge enough that the accept/reject decision can flip depending on which one is consulted — and that's the moment the methodological difference becomes a business decision.

---

## 4. The Book's Thesis Connection

This chapter is structurally critical: it is the **first full deployment of the side-by-side comparison anatomy** the book promised in Chapter 1 and deferred through Chapter 2's methods detour.

Three thesis-level claims this chapter must land:

1. **The two approaches answer different questions.** The CI's question is "if I repeated this procedure, how often would the interval contain the truth?" The credible interval's question is "given what I observed, where is the truth likely to be?" The engineer wants the second. The frequentist procedure cannot give the second. This is the same structural point Chapter 1 made for diagnosis; Chapter 3 generalizes it.

2. **For decisions, posterior probabilities are first-class outputs.** P(rate < 0.20 | data) is a number the Bayesian computes directly and the frequentist cannot produce without leaving the frequentist framework. When the decision criterion is a threshold probability, this is the difference between an answer and a non-answer.

3. **Conjugacy is a gift, not the general case.** The Beta-Binomial works cleanly because the prior and likelihood are mathematically matched. Chapter 4 will start to lose that gift; later chapters lose it entirely. The chapter should celebrate the conjugate trick honestly — Feynman's "look at this, it's beautiful" — while signaling that the general Bayesian case is messier.

The chapter also connects to the book's LLM/prompting backbone: the prompting section (line 305) takes the same skill from Chapter 2 and applies it to a problem where the student can verify the answer by hand against the closed form. Verification is cheap here. That's the point of starting the comparison machinery with this problem.

---

## 5. Intellectual Lineage Notes

The history is unusually rich for an undergraduate chapter because the binomial problem is *the original problem* of statistical inference.

1. **Jakob Bernoulli, *Ars Conjectandi* (posthumously published 1713).** Bernoulli's "golden theorem" — the law of large numbers for the binomial — was the first rigorous proof that observed frequencies converge to underlying probabilities. [MAA Convergence article](https://old.maa.org/press/periodicals/convergence/jacob-bernoullis-ars-conjectandi). The forward direction (given p, predict the relative frequency) was solved here. The chapter's problem is the *inverse* — given the frequency, infer p — which Bernoulli posed but did not solve.

2. **Thomas Bayes, "An Essay towards solving a Problem in the Doctrine of Chances" (1763).** [Philosophical Transactions](https://royalsocietypublishing.org/doi/10.1098/rstl.1763.0053). Solved the inverse problem for the binomial: given observed successes and failures, what is the probability distribution over the underlying rate? *This is the chapter's problem.* The chapter can legitimately open with the historical claim that the modern engineering scenario is the same problem Bayes wrote up 263 years ago.

3. **Pierre-Simon Laplace, *Essai philosophique sur les probabilités* (1814).** [Internet Archive](https://archive.org/details/essaiphilosophiq00lapluoft). Laplace independently rediscovered and substantially generalized Bayes's work. The rule of succession — (k+1)/(n+2) — is Laplace's, and it is exactly the posterior mean under a Beta(1,1) prior on a binomial proportion. The chapter's "posterior mean 9/52" is Laplace's formula applied to the engineering scenario.

4. **Karl Pearson, chi-square paper (1900).** [Pearson's 1900 paper](https://www.tandfonline.com/doi/abs/10.1080/14786440009463897). Pearson's chi-square test connects to the binomial through the normal approximation: in the two-category case, the chi-square reduces to the squared z-statistic on the proportion. Cite for the frequentist methodology lineage — Pearson is the bridge from Bernoulli's combinatorics to modern hypothesis testing.

5. **C. J. Clopper and E. S. Pearson (1934).** "The Use of Confidence or Fiducial Limits Illustrated in the Case of the Binomial." *Biometrika,* 26, 404–413. Egon Pearson (Karl's son) and Clopper give the exact frequentist interval for a binomial proportion. The chapter should at least name Clopper-Pearson as the rigorous frequentist counterpart to the Wald approximation it teaches.

6. **E. B. Wilson (1927).** "Probable inference, the law of succession, and statistical inference." *JASA,* 22, 209–212. The score interval. Notable for being a 1927 paper whose title explicitly invokes Laplace's "law of succession" — the same Bayesian formula Laplace derived, here being borrowed back into frequentist territory. Worth a footnote.

**The lineage move the chapter can make:** Bernoulli stated the problem. Bayes solved it Bayesian. Laplace generalized it. Pearson's school re-solved it frequentist. The two-track history isn't a 21st-century rivalry — it's three centuries old. The chapter teaches both because both are still in use, both are correct given their assumptions, and both have answers to questions the other cannot answer.

---

## 6. Pedagogical Delivery Research — Teaching CI vs. Credible Interval

This is documented terrain. The CI misinterpretation literature is the largest body of evidence in any domain this book addresses.

- **[Hoekstra et al. (2014)](https://link.springer.com/article/10.3758/s13423-013-0572-3)** is *the* citation. Specifically: when 442 psychology students and 120 researchers were given six interpretations of "the 95% CI is [0.1, 0.4]," both groups endorsed on average 3+ of the false interpretations. The misinterpretations that students endorsed most often are *exactly the Bayesian credible interval interpretation* — they read the CI as "95% probability the true value is in this interval." Pedagogically, this means students don't fail to understand the CI; they understand it as something else (a credible interval).

- **[Morey et al. (2016)](https://pmc.ncbi.nlm.nih.gov/articles/PMC4742505/)** offers the theoretical case that the CI is structurally a procedure, not an inference. Their pedagogical implication: trying to teach the CI as "the probability the parameter is in this interval, but only loosely" is not a workable middle ground. The honest teaching is: the CI is a frequency property of the procedure. If you want a probability about the parameter, you want a credible interval.

- **[Greenland et al. (2016)](https://pmc.ncbi.nlm.nih.gov/articles/PMC4877414/)** addresses 25 misinterpretations — useful as a teacher's reference even though it's longer than what the chapter can quote.

**The teaching strategy the evidence supports:**
1. Show students *both* intervals on the same data (the chapter already plans this).
2. State the CI interpretation correctly and *flag explicitly that the natural intuition is wrong*. Don't soft-pedal — name the misinterpretation, then name why it's wrong.
3. Give the credible interval as the interval that does what students wanted the CI to do.
4. Make the practical implication concrete: when the decision requires P(rate < threshold), only the Bayesian framework can produce it directly.

**The pedagogical trap to avoid:** Framing this as "the CI is wrong" or "frequentists are confused." The CI is correct *as a statement about the procedure*. The misinterpretation is users wanting it to be something it isn't. The chapter's voice should be sympathetic — most readers will themselves have held the wrong interpretation. The lesson is "here is what you were trying to get; here is the tool that actually delivers it."

---

## 7. Representation and Display Research — The Side-by-Side Table

TIKTOK.md (lines 289–297) sketches this table:

| | Frequentist | Bayesian |
|---|---|---|
| Point estimate | 0.16 | 0.173 (posterior mean) |
| Interval | 95% CI [0.065, 0.255] | 95% CrI [0.081, 0.295] |
| Interval meaning | Procedure guarantee | Probability statement |
| P(rate < 0.20)? | Not available | Directly computable |
| Prior required? | No | Yes — uniform here |

**One additional row I would recommend the author add — placed as the new top row to make the chapter's structural claim first:**

| | Frequentist | Bayesian |
|---|---|---|
| **Question answered** | **"How often would intervals built this way contain the true rate?"** | **"Given this data, where is the true rate likely to be?"** |

Rationale: the entire pedagogical move of the chapter is that the two frameworks answer different questions about the same data. Putting that row first makes the table teach the lesson before the numbers do. Every subsequent row is a consequence of the first. Without it, the table reads as a comparison of outputs; with it, the table reads as a comparison of *questions* — which is what the book is actually about.

A second optional row worth considering, placed near the bottom:

| | Frequentist | Bayesian |
|---|---|---|
| **What changes if you collect more data** | **Interval narrows; interpretation unchanged** | **Posterior narrows; converges to the data as prior influence fades** |

This previews Chapters 7 and 8 — the prior's role and what happens with sparse data — without spending chapter words on the preview.

**Worked-example display recommendations:**
- Show the Beta(1,1) prior, the Binomial likelihood, and the Beta(9, 43) posterior as three plots stacked on the same axis. This is the closed-form update visualized. Companion website D3 visualization is the obvious home for the interactive version.
- For the frequentist side, show the sampling distribution of p̂ under the null and the CI construction. Students need to *see* the procedure to understand why it doesn't answer their question.
- The CI vs. CrI overlay on a single axis should be the chapter's hero figure. The intervals are nearly the same; the interpretive content is completely different. That visual contradiction is the chapter's whole argument in one picture.

---

## 8. Open Questions and Research Gaps

### Aging risk — moderate
Less than Chapter 2, but real:
- LLM-generated Bayesian code (the prompting section) inherits the prompting chapter's aging risk. Specific model names should not appear in body text.
- The Wald interval may eventually be replaced by Wilson in intro curricula. The chapter teaches Wald because the algebra is transparent; future editions may want to switch.

### Genuinely open / unsettled
- **The "right" uninformative prior for the binomial proportion.** Beta(1,1) is conventional but Jeffreys's Beta(0.5, 0.5) has better frequency properties. The chapter sidesteps this; a more advanced book would not.
- **What to do when the prior matters for the decision.** Chapter 7 will address this — but Chapter 3 should flag that the choice of Beta(1,1) is itself a choice, even though it looks "neutral."
- **Whether students can transfer the lesson.** The CI literature suggests that even after explicit instruction, students often revert to the misinterpretation. Whether side-by-side teaching (this chapter's approach) helps with retention is not strongly established. Chapter is taking a pedagogical bet.

### Mechanism gaps
- The Bayesian credible interval depends on the posterior, which depends on the prior. For Beta(1,1), the dependence is minimal in this problem; for sparse data and asymmetric priors, it can dominate. The chapter touches this only by saying "uniform here" — Chapter 7 will earn it properly.

---

## 9. Sourcing Notes

- **All seven foundational sources are accessible.** Hoekstra (2014), Morey (2016), and Greenland (2016) are all open-access in PMC or on Springer with free PDFs. Gelman BDA3 is freely available from the author's site. Bayes (1763) is on Royal Society Publishing. Clopper-Pearson (1934) and Wilson (1927) are older and in JSTOR/paywalled journals but are textbook-standard enough to cite without re-reading the original.
- **The Bayes (1763) original is hard to read.** Eighteenth-century notation, idiosyncratic vocabulary. Cite it for the historical claim but don't ask students to read it. The [Barnard (1958) transcription](https://www.york.ac.uk/depts/maths/histstat/bayesbarnard.pdf) is more readable.
- **The Laplace *Essai* (1814)** is on Internet Archive in French. An English translation exists (Truscott & Emory, 1902) and is also on Archive.org.
- **ISO 2859-1** is paywalled at iso.org. The chapter can cite it without quoting it; summaries of the AQL system are widely available open-access ([ANSI blog overview](https://blog.ansi.org/ansi/iso-2859-1-2026-aql-sampling/)).
- **No source on this chapter requires institutional access** to be used at the level the chapter needs. This is a comparatively clean sourcing landscape.
- **Strongest single citation** if the chapter can only have one: Hoekstra et al. (2014) for the empirical claim that CI misinterpretation is robust and widespread. The chapter's entire pedagogical premise rests on that finding.
