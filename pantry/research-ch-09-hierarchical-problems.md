# Research: Chapter 09 — Hierarchical Problems
## Bayesian Probability with LLMs

**Chapter one-line:** Data with natural grouping structure — students in schools, patients in hospitals, users in cities — requires models that share information across groups. This is where the frequentist and Bayesian approaches diverge most sharply, and where the Bayesian asymmetry is most pronounced.
**Research date:** 2026-05-13

---

## 1. Primary Sources

### Foundational papers and texts

- **Lindley, D. V. and Smith, A. F. M. (1972). "Bayes Estimates for the Linear Model."** *Journal of the Royal Statistical Society, Series B (Methodological)*, 34(1), 1–41. Wiley landing: [https://rss.onlinelibrary.wiley.com/doi/abs/10.1111/j.2517-6161.1972.tb00885.x](https://rss.onlinelibrary.wiley.com/doi/abs/10.1111/j.2517-6161.1972.tb00885.x). PDFs: [https://www.ma.imperial.ac.uk/~das01/MyWeb/SCBI/Papers/LindleySmith.pdf](https://www.ma.imperial.ac.uk/~das01/MyWeb/SCBI/Papers/LindleySmith.pdf) and [https://faculty.ucmerced.edu/jvevea/classes/290_21/readings/week%204/Lindley%20and%20Smith.pdf](https://faculty.ucmerced.edu/jvevea/classes/290_21/readings/week%204/Lindley%20and%20Smith.pdf). The foundational paper that derives Bayesian estimators for the linear model using exchangeability and a hierarchical prior. This is *the* paper that connects James-Stein shrinkage to a fully Bayesian hierarchical model. Described in the literature as a "breakthrough" — the technical bridge between Stein 1956 and modern multilevel Bayesian practice. For Ch 9: the deep historical citation, the one the chapter can point to and say *this is where the hierarchy formally entered the picture*.

- **Efron, B. and Morris, C. (1975). "Data Analysis Using Stein's Estimator and Its Generalizations."** *Journal of the American Statistical Association*, 70(350), 311–319. DOI: [https://doi.org/10.1080/01621459.1975.10479864](https://doi.org/10.1080/01621459.1975.10479864). The baseball example. Same citation as Ch 8 — this paper does double duty. In Ch 8 it teaches shrinkage as a phenomenon; in Ch 9 it teaches partial pooling as a hierarchical mechanism. The 18-player dataset is the cleanest possible undergraduate demonstration of the chapter's core claim: borrowing strength across groups (here: 18 batters) gives better predictions than treating each group separately. R dataset: [https://vincentarelbundock.github.io/Rdatasets/doc/pscl/EfronMorris.html](https://vincentarelbundock.github.io/Rdatasets/doc/pscl/EfronMorris.html).

- **Rubin, D. B. (1981). "Estimation in Parallel Randomized Experiments."** *Journal of Educational Statistics*, 6(4), 377–401. SAGE landing: [https://journals.sagepub.com/doi/abs/10.3102/10769986006004377](https://journals.sagepub.com/doi/abs/10.3102/10769986006004377). The original eight-schools paper. SAT-V coaching programs run in eight schools; observed effects ranged from −3 to +28 points; the natural method-of-moments estimate of the between-school variance is zero. Rubin shows that a full Bayesian analysis recovers a sensible posterior even when the variance-component point estimate collapses. This is the world's most-cited Bayesian hierarchical example and almost certainly belongs in Ch 9 as a worked sidebar, even though the chapter's main case is a 30-school math-performance study. The data are reproduced in the R package `bayesmeta` ([https://rdrr.io/cran/bayesmeta/man/Rubin1981.html](https://rdrr.io/cran/bayesmeta/man/Rubin1981.html)) and form the canonical Stan example: [https://www.tensorflow.org/probability/examples/Eight_Schools](https://www.tensorflow.org/probability/examples/Eight_Schools).

- **Gelman, A. and Hill, J. (2007). *Data Analysis Using Regression and Multilevel/Hierarchical Models*.** Cambridge University Press. Book home: [https://sites.stat.columbia.edu/gelman/arm/](https://sites.stat.columbia.edu/gelman/arm/). Cambridge listing: [https://www.cambridge.org/9780521686891](https://www.cambridge.org/9780521686891). Full text PDF (university repository copy): [http://www.nicksun.fun/assets/misc_papers/Regression_and_Multilevel_Models.pdf](http://www.nicksun.fun/assets/misc_papers/Regression_and_Multilevel_Models.pdf). The textbook every applied multilevel-modeling course in the world is built on. Chapter 12 ("Multilevel linear models: the basics") is the canonical pedagogical treatment of the no-pooling / complete-pooling / partial-pooling trichotomy that Ch 9 inherits directly. For Ch 9 this is the primary text the chapter should cite — and the place the chapter takes its three-way comparison from. Note the publication year: the book is widely cited as "2006" because the paperback launched in late 2006, but the formal publication date is 2007.

- **Gelman, A., Carlin, J. B., Stern, H. S., Dunson, D. B., Vehtari, A. and Rubin, D. B. (2013). *Bayesian Data Analysis*, 3rd ed.** Chapman & Hall/CRC. Author-hosted PDF (corrected printing): [https://sites.stat.columbia.edu/gelman/book/BDA3.pdf](https://sites.stat.columbia.edu/gelman/book/BDA3.pdf). Chapter 5 ("Hierarchical models") is the authoritative graduate-level treatment of hierarchical Bayesian inference. The eight-schools example is worked end-to-end in §5.5 with the half-Cauchy / half-normal prior recommendation on the variance component τ (§5.7, p. 128). For Ch 9 the BDA3 citation is the "where to go next" reference — the chapter is built at the level of Gelman & Hill 2007, and a serious student goes from there to BDA3 §5.

- **Bates, D., Mächler, M., Bolker, B. and Walker, S. (2015). "Fitting Linear Mixed-Effects Models Using lme4."** *Journal of Statistical Software*, 67(1), 1–48. DOI: [https://doi.org/10.18637/jss.v067.i01](https://doi.org/10.18637/jss.v067.i01). arXiv preprint: [https://arxiv.org/abs/1406.5823](https://arxiv.org/abs/1406.5823). CRAN citation: [https://cran.r-project.org/web/packages/lme4/citation.html](https://cran.r-project.org/web/packages/lme4/citation.html). The implementation citation for the frequentist side. `lme4` is the de facto standard frequentist mixed-effects fitter in R; the JSS paper is what the chapter cites when it says "the frequentist solution runs `lmer(score ~ 1 + (1|school), data=schools)`."

- **Pinheiro, J. C. and Bates, D. M. (2000). *Mixed-Effects Models in S and S-PLUS*.** Springer, New York. Springer landing: [https://link.springer.com/book/10.1007/b98882](https://link.springer.com/book/10.1007/b98882). The frequentist canon. Predates `lme4`; the methods are in `nlme`. For Ch 9 this is the "frequentist mixed-effects models, as a self-contained subject" reference — useful for the student who wants the frequentist machinery developed fully without Bayesian framing.

- **Raudenbush, S. W. and Bryk, A. S. (2002). *Hierarchical Linear Models: Applications and Data Analysis Methods*, 2nd ed.** SAGE Publications. Publisher landing: [https://us.sagepub.com/en-us/nam/hierarchical-linear-models/book9230](https://us.sagepub.com/en-us/nam/hierarchical-linear-models/book9230). The education-research canon. The acronym HLM has been used in education-research vocabulary for forty years primarily because of this text and its predecessor. The book uses examples like students-within-schools growth modeling extensively — directly relevant to Ch 9's 30-school scenario. The 1988 Raudenbush paper ([https://journals.sagepub.com/doi/10.3102/10769986013002085](https://journals.sagepub.com/doi/10.3102/10769986013002085)) is also worth citing as the entry point.

- **Goldstein, H. (2010). *Multilevel Statistical Models*, 4th ed.** Wiley. The UK / European canon. Bristol-hosted PDF of an earlier edition: [https://www.bristol.ac.uk/media-library/sites/cmm/migrated/documents/multbook1995.pdf](https://www.bristol.ac.uk/media-library/sites/cmm/migrated/documents/multbook1995.pdf). Parallel to Raudenbush & Bryk, with a slightly different notational tradition (and a longer history with the MLwiN software). Useful as the second source on hierarchical models in education when the chapter wants a non-US perspective.

- **Spiegelhalter, D. J. (2005). "Funnel plots for comparing institutional performance."** *Statistics in Medicine*, 24(8), 1185–1202. Wiley: [https://onlinelibrary.wiley.com/doi/10.1002/sim.1970](https://onlinelibrary.wiley.com/doi/10.1002/sim.1970). The argument that institutions (hospitals, schools) should not be ranked in league tables and that funnel plots are the principled display. Directly relevant to Ch 9's Exercise 3 (the district official who wants to publish rankings of 30 schools). The Goldstein, Spiegelhalter, et al. (1996) *JRSSA* paper "League tables and their limitations" ([verify] DOI 10.2307/2983252) makes the same argument at length. The Annual Reviews chapter "League Tables for Hospital Comparisons" ([https://www.annualreviews.org/content/journals/10.1146/annurev-statistics-022513-115617](https://www.annualreviews.org/content/journals/10.1146/annurev-statistics-022513-115617)) is the modern synthesis.

### Key empirical cases

- **The 1981 eight-schools data (Rubin).** Eight SAT-V coaching programs, observed effects (SE) of 28(15), 8(10), −3(16), 7(11), −1(9), 1(11), 18(10), 12(18). Reproducible from `bayesmeta::Rubin1981`. The data are tiny, the answer is interesting, the lesson is that a hierarchical model both *shrinks the individual estimates* and *quantifies the between-school variability*. For Ch 9: the worked sidebar. Suggested move: do the eight schools first, in 40 lines, then scale up to the 30-school district case.

- **The 1970 Efron-Morris 18-batters data.** Same data as Ch 8. In Ch 9 use the data to demonstrate the *hierarchical re-derivation* of the James-Stein shrinkage: assume θᵢ ~ Normal(μ, τ²), with each batter's observed average distributed Normal(θᵢ, σᵢ²), and fit the full Bayesian model. The result matches the James-Stein estimator in the limit. This is the moment the book has been pointing at since the introduction: frequentist regularization and Bayesian hierarchy are the same machinery in different vocabularies.

- **The NYC teacher data release (February 2012).** Coverage: [https://hechingerreport.org/how-new-york-citys-value-added-model-compares-to-what-other-districts-states-are-doing/](https://hechingerreport.org/how-new-york-citys-value-added-model-compares-to-what-other-districts-states-are-doing/); critical assessment: [https://www.classsizematters.org/wp-content/uploads/2011/05/Statement_on_NYC_Teacher_Value_Added_Model_Final.pdf](https://www.classsizematters.org/wp-content/uploads/2011/05/Statement_on_NYC_Teacher_Value_Added_Model_Final.pdf). The NYC Department of Education released value-added rankings for ~18,000 teachers; the city itself cautioned that the rankings had large margins of error; the underlying year-to-year score correlations were ~0.2–0.3 in English and 0.4–0.6 in math, indicating the rankings were heavily noise. The Wikipedia overview ([https://en.wikipedia.org/wiki/Value-added_modeling](https://en.wikipedia.org/wiki/Value-added_modeling)) summarizes the methodological dispute. For Ch 9 Exercise 3: this is the worked real-world example of what happens when you publish rankings without taking the hierarchical uncertainty seriously. Cite as the cautionary tale.

- **DC IMPACT teacher evaluation (2009–present).** Air Institutes program description: [https://www.air.org/sites/default/files/publications/IMPACT_Report_RELEASE.pdf](https://www.air.org/sites/default/files/publications/IMPACT_Report_RELEASE.pdf). National Academies review: [https://sites.nationalacademies.org/cs/groups/dbassesite/documents/webpage/dbasse_160397.pdf](https://sites.nationalacademies.org/cs/groups/dbassesite/documents/webpage/dbasse_160397.pdf). 2013 calculation-error coverage: [https://www.washingtonpost.com/local/education/dc-school-officials-44-teachers-were-given-mistaken-performance-evaluations/2013/12/23/c5cb9f26-6c0c-11e3-a523-fe73f0ff6b8d_story.html](https://www.washingtonpost.com/local/education/dc-school-officials-44-teachers-were-given-mistaken-performance-evaluations/2013/12/23/c5cb9f26-6c0c-11e3-a523-fe73f0ff6b8d_story.html). 2021 racial-bias study coverage: [https://www.washingtonpost.com/local/education/dc-teacher-evaluation-system-impact-study/2021/08/13/d24066e2-fbb0-11eb-9c0e-97e29906a970_story.html](https://www.washingtonpost.com/local/education/dc-teacher-evaluation-system-impact-study/2021/08/13/d24066e2-fbb0-11eb-9c0e-97e29906a970_story.html). DCPS launched IMPACT in 2009–10 with high-stakes value-added scores tied to pay and retention. A 2013 incident corrected 44 teachers' ratings after calculation errors; one had been fired. A 2021 study found systematic racial disparities in scores. Second case study for Exercise 3 — what the chapter should show is that the hierarchical-model uncertainty was real, ignoring it had consequences, and the consequences fell unevenly. The chapter need not litigate value-added modeling as a policy; it should show what the math demands the reader say about it.

---

## 2. The Core Concept — State of the Field

### What is settled

Three propositions are not in serious dispute.

**First**, when data have nested structure (students within schools, patients within hospitals, repeated measurements within subjects), ignoring the structure produces incorrect standard errors. Complete pooling treats independent observations as exchangeable when they are not. No pooling treats clusters as independent estimation problems and ignores the regularizing information available from neighboring clusters. Both are dominated, in mean-square-error sense, by partial pooling.

**Second**, frequentist mixed-effects models and Bayesian hierarchical models give numerically very similar point estimates when the dataset is large and balanced. On the 1970 baseball data, on most balanced multilevel datasets, the lmer point estimates and the posterior means from a corresponding Bayesian model agree to two or three decimal places. This is settled and is the source of the "why use the harder method?" pushback the chapter needs to address.

**Third**, the methods diverge when group sizes are very unequal (the chapter's case: some schools have 200 students, some have 8), when the variance component τ is poorly identified (as in the eight-schools data, where the method-of-moments point estimate is zero), or when the question being asked requires a full posterior distribution rather than a point estimate plus standard error. In these cases the Bayesian framework produces calibrated answers that the frequentist mixed model approximates only.

### What is disputed

The dispute is operational, not foundational.

**Are frequentist mixed-model standard errors trustworthy for cluster-level inference?** When a school has 8 students, the no-pooling estimate of that school's mean has a standard error roughly proportional to 1/√8. The mixed model shrinks the estimate toward the district mean and shrinks the standard error along with it — but how the standard error of the shrunken estimate is computed depends on whether the between-school variance τ is treated as known (it isn't) or estimated (the uncertainty in τ̂ is not propagated forward in standard `lme4` output). Bates et al. argue this is a feature of the design philosophy of `lme4`. Critics (including Gelman) argue it produces under-stated uncertainty for cluster-level claims. The disagreement is real.

**Is partial pooling appropriate in adversarial settings?** When small-school estimates are *shrunk toward the district mean*, a school whose true performance is genuinely far from the district mean has its estimate biased toward the center. For accountability purposes — ranking schools, identifying outlier schools for intervention — this is exactly the *wrong* property. The chapter should name this explicitly: shrinkage is appropriate when the goal is to *estimate each school's true performance*; it is questionable when the goal is to *identify the most unusual schools*. This is the substantive critique of value-added modeling, and it has force.

### What has changed recently (last 5 years)

Three developments since 2020.

**Stan / brms have made hierarchical Bayesian modeling routine.** A two-level Bayesian hierarchical model can be specified in `brms` with the same syntax as `lmer` and fit in roughly the same wall-clock time for medium datasets. The historical cost asymmetry (Bayesian = hours of MCMC; frequentist = seconds of REML) has narrowed substantially. This changes the chapter's "computational cost" row in the side-by-side table.

**Default-prior conventions have stabilized.** The recommendation for variance components has moved from inverse-gamma (problematic; the BUGS-era default that BDA3 §5.7 critiques) to half-Cauchy (Gelman 2006) to half-normal (current BDA3 recommendation for cases where high values are not expected). Ch 9 should use half-normal as the default and note the lineage.

**The value-added modeling literature has become more critical.** The 2010s saw a wave of policy implementations (NYC, DC, Tennessee); the early 2020s have seen retrospective evaluations finding both lasting student-achievement effects (Education Next, *A Lasting Impact*) and systematic racial bias in evaluation outcomes (the 2021 DC IMPACT study). The chapter's Exercise 3 can land in this conversation honestly.

---

## 3. Application Domain Examples

**Education is the canonical application domain for hierarchical models.** Students within classrooms within schools within districts within states is a four-level hierarchy; Raudenbush & Bryk and Goldstein built their textbook traditions on it. The chapter's 30-school district case sits squarely in this lineage. The companion-website dataset should encode the realistic feature that group sizes vary by ~25× (8 students to 200 students). This is what makes partial pooling necessary rather than merely defensible.

**Hospital quality measurement is the parallel application.** Spiegelhalter (2005) on funnel plots and the Annual Reviews league-tables chapter are the right references. The mathematical structure is identical: hospitals = schools, patient outcomes = student scores, with the additional complication that complication rates are rare events (so a beta-binomial hierarchy is more appropriate than a normal one). For a chapter sidebar: the same hierarchical mechanism applied to a different domain. Useful because it ties Ch 9 back to Ch 8.

**Sports analytics is the easy-to-explain application.** Batting averages (Efron-Morris 1975), basketball shooting percentages, NHL goalies' save percentages — every domain where you have repeated trials nested within players gives the same partial-pooling story with the same shrinkage answer. A.S. Kurz's blog post "Stein's Paradox and What Partial Pooling Can Do For You" ([https://solomonkurz.netlify.app/blog/2019-02-23-stein-s-paradox-and-what-partial-pooling-can-do-for-you/](https://solomonkurz.netlify.app/blog/2019-02-23-stein-s-paradox-and-what-partial-pooling-can-do-for-you/)) is a worked re-creation of the baseball example in `brms`, suitable as an undergraduate auxiliary reading.

---

## 4. The Book's Thesis Connection

This is the chapter where the book's asymmetry claim is made explicit. TIKTOK.md lines 755–763 instruct the chapter to *open with* the asymmetry notice: "This chapter spends more space on the Bayesian solution than any prior chapter. That asymmetry is the lesson." The research connection is this: that statement is *defensible* because the methodological literature actually says so. Gelman & Hill 2007 spends most of its 600 pages on multilevel models that they describe as *easier to think about Bayesianly even when fit frequentistly*; BDA3 Chapter 5 is twice the length of the corresponding chapters in the Pinheiro-Bates or Raudenbush-Bryk frequentist canons. The asymmetry is not a stylistic choice; it is a property of the subject.

**Three threads converge here.**

The book's running comparison reaches its sharpest divergence. Chapters 1–7 had frequentist and Bayesian methods producing nearly identical answers from nearly identical machinery. Chapter 8 introduced shrinkage. Chapter 9 makes shrinkage the central mechanism, *under the name hierarchy*, and shows that the Bayesian framework gets it cleanly while the frequentist mixed-effects framework gets it approximately. This is the strongest case the book makes for Bayesian methods, and it is also the most honest case — because the chapter also names where mixed models are perfectly fine (large balanced data, π = standard inference on fixed effects).

The chapter's exercises (TIKTOK.md lines 833–844) press exactly the book's thesis. Exercise 1 fits both models and compares small-school estimates — the empirical test of whether the methods differ where the theory says they should. Exercise 2 forces the no-pooling / complete-pooling / partial-pooling comparison on a specific case (6 students, 95% average). Exercise 3 brings the methodological choice into operational consequence (publishing rankings of 30 schools) — and the right answer is informed by Spiegelhalter on funnel plots and the value-added-modeling literature.

The chapter is also where the book's "asymmetry rule" (TIKTOK.md lines 42–46) gets its second invocation. The rule is named at Chapter 5; Chapter 9 cashes it in. The book's promise has been: the asymmetry is evidence, not apology. Chapter 9 is the chapter that has to *make that promise visible* by showing precisely what the extra Bayesian complexity buys.

---

## 5. Intellectual Lineage Notes

**Hierarchical Bayes lineage.** Stein 1956 (inadmissibility) → James & Stein 1961 (closed-form estimator) → Lindley & Smith 1972 (the explicit Bayesian re-derivation as a hierarchical linear model — the *transformation* of the technical result into a modeling framework) → Efron & Morris 1975 (the empirical demonstration on the baseball data) → Rubin 1981 (the eight-schools example, which becomes the canonical pedagogical case) → Gelman & Hill 2007 / BDA3 (the modern teaching synthesis). This is a 50-year line of intellectual descent and Ch 9 should run it explicitly. The student should *see* that the chapter's content has a history.

**Frequentist mixed-models lineage.** Henderson 1950s (best linear unbiased predictor / BLUP) → the LMER algorithms of the 1980s (Laird-Ware; Harville) → Pinheiro & Bates 2000 (the `nlme` book) → Bates et al. 2015 (`lme4`). The frequentist tradition is older in some respects and developed largely independently of the Bayesian one. They converge at the point of "BLUPs are shrinkage estimators that approximate hierarchical Bayesian posterior means." The convergence is itself part of the lesson.

**Education-research lineage.** Burstein 1980 and Cronbach 1976 (the "units of analysis" problem in educational measurement) → Aitkin & Longford 1986 (the first applied multilevel analysis of school effects) → Raudenbush & Bryk 1986, 1988 → the textbook tradition (HLM software, *Hierarchical Linear Models* 1992 / 2002). This is the lineage Ch 9 is operating *inside* when it picks a school-district scenario; the textbook tradition has trained the audience the chapter is writing for.

**Reflexive note.** The chapter invokes hierarchy and partial pooling as tools. They are not universally appropriate. When clusters are *not* exchangeable — for example when one school is structurally different in a way that the data cannot reveal — the hierarchy is mis-specified and the partial pooling pulls the estimate in a wrong direction. The chapter should name this. The honest sentence is something like: *Partial pooling assumes the schools are similar enough to learn from each other; when that assumption fails, the method fails.* Show the tool doing work; name the conditions under which it doesn't.

---

## 6. Pedagogical Delivery Research

**Partial pooling is famously hard to teach.** Gelman has written multiple times on his blog ([https://statmodeling.stat.columbia.edu/](https://statmodeling.stat.columbia.edu/)) and in the Gelman-Hill text that students take time to internalize the trichotomy of complete / no / partial pooling. The textbook itself (Chapter 12, "Multilevel linear models: the basics") devotes most of its first ten pages to the trichotomy specifically because of this difficulty. A. Solomon Kurz writes that the trichotomy "gives students an 'aha' moment after sometimes years of confusion about fixed and random effects" — meaning that the trichotomy is *what the chapter should teach to*, not from. The student should leave the chapter able to say which kind of pooling each method does.

**The fixed-vs-random-effects vocabulary is a known obstacle.** Gelman (2005, *Annals of Statistics*, "Analysis of variance — why it is more important than ever"; verify) argues the fixed/random distinction is more confusing than illuminating and recommends replacing it with the more transparent "varying intercept, varying slope" language. Ch 9 should follow that recommendation. The traditional vocabulary makes the chapter harder to read and is not load-bearing.

**Suggested pedagogical move: visualize the shrinkage.** A scatter plot with no-pooling estimates on the x-axis and partial-pooling estimates on the y-axis shows shrinkage as a line steeper-than-y=x near the cluster boundary and shallower in the middle. The plot is in Gelman & Hill 2007 Chapter 12 and reproduced in dozens of teaching materials. Ch 9 should reproduce it on the page with the chapter's own 30-school data.

**Second pedagogical move: lead with the eight schools, end with the 30 schools.** The eight-schools dataset is small enough to write out by hand. The student can see all 8 numbers, fit the hierarchical model, and watch the shrinkage. Then scale up to the 30-school district case where the same machinery handles unequal group sizes and where the small-school behavior is the interesting feature. The pedagogical pattern is "demonstrate on toy, apply on real."

**Third pedagogical move: have the LLM do the model specification.** TIKTOK.md notes the prompting section is longer in this chapter than previous chapters because hierarchical model specification requires more precision. This is the chapter where an LLM earns its keep as a *translator* between the conceptual hierarchy ("two levels: schools, students") and the brms / Stan / PyMC syntax. The exercise should have the student verify the LLM-produced model code by checking that the prior, likelihood, and hyperprior all appear and are correctly addressed.

---

## 7. Representation and Display Research

The chapter's side-by-side comparison table appears verbatim in TIKTOK.md (lines 809–815). Rendered:

| | Frequentist mixed model | Bayesian hierarchical |
|---|---|---|
| Small school estimates | Shrunk, unstable SE | Full posterior, calibrated |
| Uncertainty in shrinkage | Not propagated | Fully propagated |
| District-level inference | Fixed effect | Posterior on hyperparameter |
| Computation | Fast (REML) | Slow (MCMC) |
| Interpretability | Standard in social science | Requires explanation |

**Recommended row to add: "Behavior when the variance component τ is poorly identified."** This is the eight-schools situation: the method-of-moments point estimate of τ is zero, which under REML produces a degenerate or near-degenerate fit with the random-effect term collapsing to the complete-pooling answer. The Bayesian model, with a half-normal prior on τ, returns a sensible posterior over τ that reflects the data's genuine ambiguity about whether the schools differ at all. This is the row that most cleanly distinguishes the two methods on the kind of data the chapter is built around. Suggested cell contents: Frequentist — "may collapse to complete pooling"; Bayesian — "posterior over τ remains informative."

**Two recommended displays beyond the table.**

A caterpillar plot of the 30 schools, showing posterior medians and 95% credible intervals, ordered by point estimate. The visual point is that *the intervals overlap heavily for most schools*, which is exactly Spiegelhalter's argument against league tables. The plot is the chapter's most efficient way to make the case behind Exercise 3.

A funnel plot of school complication-rate-or-test-score estimates against precision (1/SE). Schools inside the funnel are statistically indistinguishable from the district mean; schools outside are worth investigating. This is the principled alternative to ranking, recommended by Spiegelhalter 2005 and used in NHS hospital performance reporting in the UK. Ch 9 should show it and recommend it as the chapter's preferred display for this kind of data.

---

## 8. Open Questions and Research Gaps

**The chapter has a real philosophical tension to name.** Partial pooling improves average estimation accuracy across schools but worsens estimation accuracy for any particular school whose true value is far from the district mean. If the policy question is "is this specific school underperforming?", the hierarchical model's shrinkage is biasing the answer toward "no" exactly when the answer should be "yes." The chapter's mention of this in the "Why anyone uses frequentist mixed models" section gestures at the issue. A clean resolution requires deciding what the estimate is *for* — which is a policy question, not a statistical one. The chapter should name this without resolving it.

**A pedagogical gap.** I do not have a clean undergraduate-level explanation for *why* the half-normal prior on τ is the current default. The graduate-level answer is in BDA3 §5.7 and Gelman 2006 ("Prior distributions for variance parameters in hierarchical models," *Bayesian Analysis* 1(3), 515–533; verify). The undergraduate-level answer is roughly "it puts most of its mass on small values of τ but allows large values when the data demand them." The chapter should *show* this with a plot of the prior, rather than asserting it.

**A domain-knowledge gap.** I know the methodological literature on value-added modeling but I do not have current operational knowledge of how a US school district's accountability office actually computes and publishes school rankings in 2026. The chapter's Exercise 3 (a district official wants to publish rankings) needs to be plausibly grounded in current practice. Flag for Nik or for a domain reviewer.

**A genuine research gap in the field.** When is the additional complexity of full Bayesian hierarchical modeling worth it, *measured by decision quality rather than statistical fit*? The methodological literature has not produced a clean answer at the level the chapter's Learning Outcome 5 demands ("Evaluate when the additional complexity is worth the cost"). The chapter should be honest that the answer is partly subjective and depends on what the analysis is for. Do not pretend there is a rule.

---

## 9. Sourcing Notes

Primary sources verified by direct WebSearch this session:
- Lindley & Smith 1972 *JRSS-B* — Wiley DOI and PDF mirrors confirmed.
- Rubin 1981 *J Educ Stat* — SAGE landing confirmed; `bayesmeta` data documentation confirmed.
- Gelman & Hill 2007 — Cambridge listing and Stat-Columbia book home confirmed; full text PDF via repository confirmed.
- BDA3 — author-hosted PDF at sites.stat.columbia.edu/gelman/book/BDA3.pdf confirmed.
- Bates et al. 2015 *JSS* — DOI 10.18637/jss.v067.i01 confirmed; arXiv preprint 1406.5823 confirmed; CRAN citation confirmed.
- Pinheiro & Bates 2000 — Springer landing confirmed.
- Raudenbush & Bryk 2002 — SAGE listing confirmed.
- Spiegelhalter 2005 funnel plots — Wiley listing confirmed; Annual Reviews league-tables chapter confirmed.
- NYC 2012 teacher data release — multiple primary sources (Hechinger Report, Class Size Matters) confirmed.
- DC IMPACT — AIR Institutes report, National Academies review, Washington Post 2013 and 2021 coverage all confirmed.

Items flagged `[verify]` in this file: Goldstein/Spiegelhalter 1996 *JRSSA* "League tables and their limitations" DOI; Gelman 2005 *Ann Stat* "ANOVA — why it is more important than ever" exact citation; Gelman 2006 *Bayesian Analysis* "Prior distributions for variance parameters" exact pagination. None of these flagged items are load-bearing — the chapter's core argument is supported by the items that did verify.

Cross-references to other chapter research files: the Efron-Morris 1975 baseball citation and the Stein 1956 reference also appear in `research-ch-08-when-data-is-sparse.md`. Cross-link rather than duplicate when assembling the chapter draft. The two chapters share intellectual lineage but use the references for different teaching purposes — Ch 8 uses Efron-Morris to introduce shrinkage as a phenomenon, Ch 9 uses the same paper to demonstrate hierarchical re-derivation.
