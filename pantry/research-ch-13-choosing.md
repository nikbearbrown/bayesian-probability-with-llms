# Research: Chapter 13 — Choosing
## Bayesian Probability with LLMs

**Chapter one-line:** Not a verdict — a framework for choosing between statistical approaches based on what the problem actually requires, what the decision maker actually needs, and what the data can actually support.
**Research date:** 2026-05-13

---

## 1. Primary Sources

### Foundational papers and texts

- **Efron, B. (1986).** "Why Isn't Everyone a Bayesian?" *The American Statistician* 40(1): 1–5. [Taylor & Francis abstract](https://www.tandfonline.com/doi/abs/10.1080/00031305.1986.10475342); [author PDF (Stanford)](https://www2.isye.gatech.edu/isyebayes/bank/efronwhy1986.pdf). The canonical short statement of the tradeoffs. Efron — a Bayesian-sympathetic frequentist — lists practical reasons most working statisticians pick frequentist methods most of the time. Reads as a list of decision factors avant la lettre. The closest existing thing to what Chapter 13 is trying to be.
- **Senn, S. (2011).** "You May Believe You Are a Bayesian But You Are Probably Wrong." *Rationality, Markets and Morals* 2: 48–66. [EconPapers](https://econpapers.repec.org/article/rmmjournl/v_3a2_3ay_3a2011_3ai_3a42.htm). A specific operational argument: if a hypothetical result would cause you to revise your prior, the prior wasn't actually yours; pure subjective Bayesianism is impossible to honor in practice. Sharpens the question of *whose prior* a Bayesian analysis really uses.
- **Gelman, A., & Hennig, C. (2017).** "Beyond Subjective and Objective in Statistics." *Journal of the Royal Statistical Society: Series A* 180(4): 967–1033. [Wiley](https://rss.onlinelibrary.wiley.com/doi/abs/10.1111/rssa.12276); [full discussion PDF](https://sites.stat.columbia.edu/gelman/research/published/gelman_hennig_full_discussion.pdf). Replaces "objective" with transparency, consensus, impartiality, correspondence to reality; replaces "subjective" with awareness of multiple perspectives and context dependence. Dissolves the dichotomy the choice is sometimes framed as.
- **Wasserstein, R. L., & Lazar, N. A. (2016).** "The ASA's Statement on p-Values: Context, Process, and Purpose." *The American Statistician* 70(2): 129–133. [Taylor & Francis full text](https://www.tandfonline.com/doi/full/10.1080/00031305.2016.1154108). Six principles that bound what a p-value can and cannot say. Sets the field's modern frame for how a frequentist tool ought to be interpreted.
- **Wasserstein, R. L., Schirm, A. L., & Lazar, N. A. (2019).** "Moving to a World Beyond 'p < 0.05'." *The American Statistician* 73(sup1): 1–19. [DOI 10.1080/00031305.2019.1583913](https://www.tandfonline.com/doi/full/10.1080/00031305.2019.1583913). Editorial introducing the post-significance special issue. Argues against "statistically significant" as a phrase. Friendly to Chapter 13's "no single decision rule" stance.
- **Mayo, D. G. (2018).** *Statistical Inference as Severe Testing: How to Get Beyond the Statistics Wars.* Cambridge University Press. [Cambridge Core](https://www.cambridge.org/core/books/statistical-inference-as-severe-testing/D9DF409EF568090F3F60407FF2B973B2). The modern frequentist defense, grounded in error-statistical philosophy descended from Popper. Required reading for any chapter that claims to give a frequentist defense fairly.
- **Box, G. E. P., & Tiao, G. C. (1973).** *Bayesian Inference in Statistical Analysis.* Addison-Wesley; reprinted Wiley Classics 1992. [Wiley](https://onlinelibrary.wiley.com/doi/book/10.1002/9781118033197). The early canon on choice of prior, especially noninformative priors and when each makes sense. Useful as a reminder that the Bayesian camp is not monolithic on prior choice.
- **Bernardo, J. M., & Smith, A. F. M. (1994).** *Bayesian Theory.* Wiley. [Wiley](https://onlinelibrary.wiley.com/doi/book/10.1002/9780470316870). The decision-theoretic Bayesian foundation. Relevant for Block 2's "decisions requiring P(outcome > threshold)" — the framework Bernardo and Smith treat as the natural Bayesian object of inference.
- **Lindley, D. V. (2006).** *Understanding Uncertainty.* Wiley. [Wiley](https://onlinelibrary.wiley.com/en-us/Understanding+Uncertainty,+Revised+Edition-p-9781118650127). A dogmatic Bayesian's plain-language account of why probability is the only coherent calculus of uncertainty. Useful contrast to the "horses for courses" pragmatic position Chapter 13 takes.

### Key empirical cases

- **The 2015 reproducibility crisis in psychology** (Open Science Collaboration, *Science*, 2015) is the empirical event behind the ASA 2016 statement. Cite when discussing why "audiences need p-values" has gotten more complicated.
- **FDA Bayesian guidance for medical devices** (FDA, 2010, [verify current version]) — operational example of a regulated environment where Bayesian methods *are* explicitly accepted, complicating the TIKTOK Block 1 claim that regulation always favors frequentism. The chapter should engage rather than dodge this.

---

## 2. The Core Concept — State of the Field

### What is settled

- Neither framework is universally correct. The "statistics wars" position (Mayo 2018) explicitly seeks to move past the question. The Bayesian workflow position (Gelman et al. 2020, arXiv:2011.01808) explicitly endorses mixed practice. The field has stopped litigating "which is right" and started litigating "which when."
- p-values are widely misinterpreted. The ASA 2016 statement establishes six principles that bound interpretation; the 2019 follow-up argues for dropping "statistically significant" as a term.
- Bayesian methods require computational and prior-elicitation costs that frequentist methods do not. This is settled even among Bayesians (Efron 1986; Gelman & Hennig 2017).
- For decision problems that natively ask for P(outcome > threshold), Bayesian methods give the right *kind* of answer; frequentist methods give a related but not equivalent answer. This is settled.

### What is disputed

- Whether a "subjective" prior is a feature or a bug. Bernardo & Smith (1994) and Lindley (2006) take the feature position; Senn (2011) takes the bug position; Gelman & Hennig (2017) dissolve the dichotomy.
- Whether Bayesian methods are appropriate in regulated environments. The TIKTOK draft of Block 1 puts clinical trials in the frequentist column. This is mostly true but the FDA medical-device guidance shows it is not absolutely true. The chapter should be specific.
- Whether small samples *favor* Bayes. The standard claim — small n + good prior = stabilized estimate — is largely accepted, but Senn (2011) sharpens the question of *which* prior, and Mayo (2018) argues that small-sample frequentist methods (exact tests, profile likelihoods) are often underestimated.
- Whether "communicate probability, not significance" is a clean win for Bayes. Wasserstein, Schirm, & Lazar (2019) push the field toward better communication generally; the Bayesian framing is one of several proposals, not the consensus winner.

### What has changed recently (last 5 years)

- The post-2019 ASA editorial era has shifted the question from "p-value vs. posterior" to "what does the audience need to decide." This is the framing Chapter 13 inherits.
- LLM-implementable Bayesian analysis (via PyMC, numpyro, brms) has eroded one of Efron's 1986 practical objections: that Bayes is computationally costly. The cost is now elicitation and validation, not implementation.
- The reproducibility crisis (2011–2015) pushed reporting standards toward pre-registration, sensitivity analysis, and effect-size focus — moves that are neutral between frameworks but require more explicit method-justification regardless of choice.

---

## 3. Application Domain Examples

Chapter 13 is the framework chapter — no single scenario carries it. The chapter works by example types. The clearest examples for each block in TIKTOK:

**Block 1 (frequentist is right):**
- *Phase III drug trial with 20,000 patients.* Sample is huge; regulator demands prior-free analysis; audience is FDA reviewers. Frequentist wins on every dimension. [FDA guidance though: medical device Bayesian carve-out exists; name the asymmetry.]
- *Exploratory genomics with 30,000 hypotheses.* False-discovery-rate methods (Benjamini & Hochberg, 1995, [JRSS B](https://rss.onlinelibrary.wiley.com/doi/10.1111/j.2517-6161.1995.tb02031.x)) are explicitly frequentist and the dominant approach.
- *Manufacturing quality control.* Control charts, process capability indices — frequentist by construction and by regulation (ISO).

**Block 2 (Bayes earns its complexity):**
- *Small clinical trial with strong prior evidence from past trials.* Stabilizing inference matters; meta-analytic priors are well established.
- *Sales forecasting with sequential updating.* New data arrives weekly; you want yesterday's posterior to be today's prior. This is the natural Bayesian update structure.
- *Hierarchical school-effects data* (Rubin 1981; Gelman & Hill 2007). Partial pooling has no clean frequentist analog at the same level of expressivity.
- *Decision under uncertainty in business* — "what's the probability our profit exceeds $X next quarter?" This is a posterior tail probability; the frequentist version (e.g., confidence intervals on a forecast) is awkward and easily misread.

**Block 3 (the framework as questions):**
1. What does the decision maker need? Point estimate, probability statement, or significance?
2. Is prior information available, defensible, and worth its cost?
3. How large is n relative to the effect being estimated?
4. What audience receives the result, and what vocabulary do they already accept?
5. What are the computational and time constraints?

---

## 4. The Book's Thesis Connection

The book's thesis is that the choice is the reader's. Chapter 13 is the chapter that makes good on the choice — *and refuses to make it for them*. The metacognitive close ("statistics can inform judgments; it cannot replace them") is the thesis in its final form.

This is also the chapter where the book's "not always Bayesian" commitment lives or dies. If the chapter argues that Bayesian methods are always preferred when computationally feasible (a position McElreath comes close to), the book's apparent neutrality collapses into a Bayesian advocacy text. The decision framework structure is the structural commitment to genuine neutrality. The chapter has to make the frequentist case strongly enough to be believed — Efron 1986 and Mayo 2018 are the load-bearing references for that.

The chapter's connection to Chapter 12 is structural and pedagogical: 12 forces the choice; 13 systematizes it. The exercise that asks students to write a methodological justification for their Chapter 12 work is the integration move. By the time they're done with 13, they should be able to *justify* what they did in 12 in a way they couldn't immediately after finishing it.

---

## 5. Intellectual Lineage Notes

- **Box & Tiao 1973** for the foundational treatment of when each Bayesian framework choice is appropriate, including noninformative priors.
- **Lindley 2006** for the strict-Bayesian position — coherence requires probabilities everywhere. Useful contrast.
- **Mayo 2018** for the strongest current frequentist defense, grounded in severe-testing / error-statistical philosophy.
- **Efron 1986** is the canonical short statement of the tradeoffs and the closest published cousin to Chapter 13's enterprise. Cite as the chapter's intellectual ancestor.
- **Gelman & Hennig 2017** is the canonical recent statement that the framing of the debate itself is wrong. The chapter should use this to refuse the false binary.
- **Bernardo-Smith 1994** for the canonical decision-theoretic Bayesian position.
- **Wasserstein, Schirm, & Lazar 2019** for the ASA's invitation to move past p-value culture, which Chapter 13 takes literally.

The lineage move: the chapter does not invoke any of these as authority. It uses them as instruments — Efron's list, Mayo's defense, Gelman & Hennig's reframe — and shows them doing work in specific cases.

---

## 6. Pedagogical Delivery Research

Chapter 13 is a metacognitive chapter. It asks students to develop method-selection judgment — a skill that the empirical literature on metacognition in statistics identifies as late-developing.

Key pedagogy points from the metacognition literature ([CBE Life Sciences Education review](https://www.lifescied.org/doi/10.1187/cbe.20-12-0289); [PMC review on metacognitive judgment](https://pmc.ncbi.nlm.nih.gov/articles/PMC2742428/)):

- Students reliably overestimate their own statistical-method knowledge — the gap between "I know what a p-value is" and "I can tell you when not to use one" is large and self-invisible.
- Method-selection judgment develops through *contrasting cases*, not through abstract lecture. A student who has worked one analysis both ways (Chapter 12) is positioned to make the choice; a student who has only read about both is not.
- Worked-example fading (Sweller and successors) is the right pedagogy: full justifications early, then progressively more student-generated justification. Chapter 13 should follow this — show fully worked justifications in the chapter, then ask students to produce one in the exercises.
- The "five problem descriptions" exercise (TIKTOK Ch 13 Ex. 1) is a textbook application of the *transfer task* form recommended in the metacognition-in-stats literature.
- Self-explanation is the highest-leverage metacognitive activity available; Exercise 2 (justify your Chapter 12 choice) is exactly this.

A risk worth naming: the chapter could easily produce students who feel they have a *decision procedure* but actually have a vocabulary for post-hoc justification. The remedy is to require the justification to be falsifiable in some way — "name the alternative you considered and rejected, and why."

---

## 7. Representation and Display Research

The chapter's likely display — per TIKTOK Block 3 — is a *question-set*, not a flowchart. This matters.

A flowchart implies an algorithm: enter at the top, follow arrows, arrive at the answer. The TIKTOK explicitly rejects this. The chapter is committed to the position that *which approach to use when* is a judgment, not a function.

What the question-set form does:

- It surfaces the dimensions of the choice without pre-collapsing them into a verdict.
- It invites the student to weigh, not compute.
- It models the actual reasoning a working statistician does when faced with a new problem — which is closer to "what are my priorities here?" than to "what does the algorithm say?"

The five-question form (TIKTOK Block 3) is the right grain. Each question gets a paragraph in the chapter that:
1. States the question plainly.
2. Names what each answer implies — favors frequentist, favors Bayes, neutral.
3. Gives one specific case where the question's answer was decisive.
4. Acknowledges the case where the question's answer was *not* decisive — when other questions overrode it.

The chapter could include a single one-page reference card (the *printable decision guide* in TIKTOK open question #4). If used, the card should be the question-set in its bare form — no recommendations, just the questions. The student reads the chapter, then uses the card.

What the chapter should *not* include:
- A scoring rubric (e.g., "+1 for each Bayesian indicator") — this is decision-procedure thinking dressed up.
- A flowchart with terminal nodes labeled "frequentist" or "Bayesian."
- A table that maps problem features to method recommendations — same failure mode, harder to argue with.

Models for this kind of teaching artifact exist in clinical decision-making literature (e.g., signal-symptom checklists rather than diagnostic algorithms) and in the medical reasoning literature on "scripts" vs. "algorithms." Worth naming as the right comparison genre.

---

## 8. Open Questions and Research Gaps

- **The companion volume on causal inference does not yet exist.** TIKTOK line 1139 points readers to `causal-inference-with-case-studies`. As of May 2026 this book is not in `/Users/bear/Documents/CoWork/bear-textbooks/books/`. The pointer needs to be either removed, softened to "forthcoming," or repointed to an existing primary source (Pearl, Hernán & Robins, Imbens & Rubin) until the companion exists.
- **The FDA Bayesian-acceptance carve-out** for medical devices complicates Block 1's clinical-trials claim. The chapter should engage rather than ignore this.
- **The "always Bayesian" colleague exercise** (Ex. 3) is good but risks producing a strawman if the imagined colleague is too weak. Strongest version of the claim: Lindley 2006 and McElreath 2020. The exercise should require students to engage with the strongest form.
- **What about likelihood-ist methods?** The chapter binarizes the choice (frequentist vs. Bayesian). The likelihoodist position (Royall 1997, *Statistical Evidence*) is a third option that some philosophers of statistics consider distinct. Probably out of scope for this book but worth a footnote.
- **What about machine-learning approaches that defy both frameworks?** Cross-validated prediction-accuracy methods are neither frequentist nor Bayesian in the classical sense. The chapter should at minimum acknowledge this — probably in Block 4 (beyond scope).
- **Block 4 pointers need verification.** McElreath's *Statistical Rethinking* 2nd edition (Routledge 2020, 2024 De Groot Prize): primary source confirmed at [routledge.com/Statistical-Rethinking](https://www.routledge.com/Statistical-Rethinking-A-Bayesian-Course-with-Examples-in-R-and-STAN/McElreath/p/book/9780367139919). Ghosal & van der Vaart, *Fundamentals of Nonparametric Bayesian Inference* (Cambridge 2017): [cambridge.org/core/books/fundamentals-of-nonparametric-bayesian-inference](https://www.cambridge.org/core/books/fundamentals-of-nonparametric-bayesian-inference/C96325101025D308C9F31F4470DEA2E8). Benjamini & Hochberg 1995 FDR paper: [JRSS B link](https://rss.onlinelibrary.wiley.com/doi/10.1111/j.2517-6161.1995.tb02031.x). Huber & Ronchetti, *Robust Statistics* 2nd ed., Wiley 2009: [Wiley link](https://onlinelibrary.wiley.com/doi/book/10.1002/9780470434697). All verified.

---

## 9. Sourcing Notes

- Efron 1986: confirmed in *The American Statistician* 40(1): 1–5. Author PDF available; DOI 10.1080/00031305.1986.10475342.
- Senn 2011: confirmed in *Rationality, Markets and Morals* 2: 48–66. Open access via [JLUpub](https://jlupub.ub.uni-giessen.de/items/90c15235-a8ca-4f53-9f52-72f856427f9d).
- Gelman & Hennig 2017: confirmed in *JRSS Series A* 180(4): 967–1033, DOI 10.1111/rssa.12276; Read Paper at RSS April 12, 2017.
- Wasserstein & Lazar 2016: confirmed in *The American Statistician* 70(2): 129–133; DOI 10.1080/00031305.2016.1154108.
- Wasserstein, Schirm, & Lazar 2019: confirmed in *The American Statistician* 73(sup1); DOI 10.1080/00031305.2019.1583913.
- Mayo 2018: *Statistical Inference as Severe Testing*, Cambridge University Press; ISBN 978-1-107-66464-7.
- Box & Tiao 1973: Addison-Wesley original; Wiley Classics 1992 reprint.
- Bernardo & Smith 1994: *Bayesian Theory*, Wiley; ISBN 0-471-92416-4.
- Lindley 2006: *Understanding Uncertainty*, Wiley; revised edition 2014.
- Benjamini & Hochberg 1995: *JRSS B* 57(1): 289–300.
- McElreath 2020: *Statistical Rethinking*, 2nd ed., Chapman & Hall/CRC.
- Ghosal & van der Vaart 2017: *Fundamentals of Nonparametric Bayesian Inference*, Cambridge.
- Huber & Ronchetti 2009: *Robust Statistics*, 2nd ed., Wiley.
- **`[verify]` items:** FDA Bayesian medical-device guidance — confirmed to exist, exact current version and citation form to be inserted at draft time. The chapter should not cite if the current guidance number cannot be verified.
- **Missing:** the `causal-inference-with-case-studies` companion volume in `/Users/bear/Documents/CoWork/bear-textbooks/books/`. TIKTOK line 1139 currently points to a non-existent target. Flag for Nik before draft.
