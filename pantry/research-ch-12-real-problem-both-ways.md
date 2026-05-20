# Research: Chapter 12 — A Real Problem, Both Ways
## Bayesian Probability with LLMs

**Chapter one-line:** One real dataset, one real question, both frameworks deployed completely — the deliverable is not which approach won but a written comparison that demonstrates statistical judgment.
**Research date:** 2026-05-13

---

## 1. Primary Sources

### Foundational papers and texts

- **Gelman, Vehtari, Simpson, Margossian, Carpenter, Yao, Kennedy, Gabry, Bürkner, Modrák (2020).** "Bayesian Workflow." arXiv preprint [arXiv:2011.01808](https://arxiv.org/abs/2011.01808). The canonical statement of how a competent Bayesian analysis is actually constructed — iterative, model-checking-laden, with explicit attention to prior choice, posterior checks, and what to do when fit fails. It is the single closest published cousin to the six-question scaffold the chapter is asking students to follow, but it is one-sided (Bayesian only). The chapter needs to graft a frequentist twin onto its skeleton.
- **Box, G. E. P. (1976).** "Science and Statistics." *Journal of the American Statistical Association* 71(356): 791–799. [Taylor & Francis](https://www.tandfonline.com/doi/abs/10.1080/01621459.1976.10480949). The iterative-model-building tradition: theory confronts practice, practice confronts theory, "all models are wrong, some are useful." This is the deep ancestor of every workflow paper since.
- **Tukey, J. W. (1977).** *Exploratory Data Analysis.* Addison-Wesley. [Internet Archive scan](https://archive.org/details/exploratorydataa0000tuke_7616). "Look at the data first." The canon for the dataset-first posture the chapter takes. Look before you choose a framework.
- **Wasserstein, R. L., & Lazar, N. A. (2016).** "The ASA's Statement on p-Values: Context, Process, and Purpose." *The American Statistician* 70(2): 129–133. [DOI 10.1080/00031305.2016.1154108](https://www.tandfonline.com/doi/full/10.1080/00031305.2016.1154108). Establishes that no single number tells the story; reporting standards must include context, sample, assumptions. Strong precedent for the chapter's insistence on prose justification, not a verdict.

### Key empirical cases

- **Frey, C. B., & Osborne, M. A. (2017).** "The Future of Employment: How Susceptible Are Jobs to Computerisation?" *Technological Forecasting and Social Change* 114: 254–280. [ResearchGate preprint](https://www.researchgate.net/publication/271523899_The_Future_of_Employment_How_Susceptible_Are_Jobs_to_Computerisation). Used O*NET 2010 to score 702 occupations. A standing example of an O*NET-based analysis with extensively documented downstream criticism — a near-perfect Ch 12 worked-example candidate.
- **Melbourne Institute (Coelli & Borland, 2019), Working Paper No. 10/19.** "Why not to rely on Frey and Osborne's predictions of potential automation." [Melbourne Institute PDF](https://melbourneinstitute.unimelb.edu.au/__data/assets/pdf_file/0005/3197111/wp2019n10.pdf). Empirically tests Frey-Osborne against observed labour market exposure and finds weak correlation — exactly the kind of failure-after-success the chapter wants students to see.
- **BLS Monthly Labor Review (2022).** "Growth trends for selected occupations considered at risk from automation." [bls.gov/opub/mlr/2022/article/growth-trends-for-selected-occupations-considered-at-risk-from-automation.htm](https://www.bls.gov/opub/mlr/2022/article/growth-trends-for-selected-occupations-considered-at-risk-from-automation.htm). Official BLS treatment of automation-exposed occupations using their own data — primary source.
- **BLS Occupational Employment and Wage Statistics (OEWS), May 2024 release.** Press release: [bls.gov/news.release/pdf/ocwage.pdf](https://www.bls.gov/news.release/pdf/ocwage.pdf). Tables: [bls.gov/oes/tables.htm](https://www.bls.gov/oes/tables.htm). The current annual snapshot — released April 2, 2025, covering approximately 830 occupations at national, state, and metro levels.

---

## 2. The Core Concept — State of the Field

### What is settled

- A real comparative analysis requires explicit articulation of the data-generating process; both frameworks have something to say about it, and they say different things. (Gelman et al. 2020 makes this central for Bayesian work; Box 1976 makes it central for any work.)
- "Show your work" is no longer optional. Reporting standards across fields (CONSORT for clinical trials, [equator-network.org/reporting-guidelines/consort](https://www.equator-network.org/reporting-guidelines/consort/); APA JARS-Quant, [apastyle.apa.org/jars/quantitative](https://apastyle.apa.org/jars/quantitative)) all converge on this: methods documented, assumptions named, analytical choices justified.
- For comparative analyses specifically, the literature is sparse but converges on: (a) match the analytical question to the framework's natural claim, (b) make priors explicit if Bayesian, (c) report intervals not just points, (d) name the sensitivity check that would change the conclusion.

### What is disputed

- Whether the comparison should be done by the same analyst (consistency of judgment, conflict of method) or by two analysts (independence, framework loyalty). The literature does not settle this. The chapter takes the same-analyst position by default.
- Whether a "preferred approach" verdict is even appropriate, or whether the comparison is itself the deliverable. Wasserstein, Schirm, & Lazar (2019), "Moving to a World Beyond p < 0.05" [DOI 10.1080/00031305.2019.1583913](https://www.tandfonline.com/doi/full/10.1080/00031305.2019.1583913), pushes toward "no single decision rule" — a position friendly to the chapter's stance.
- What counts as a "defensible prior" for student work. The Gelman et al. (2020) workflow paper leans toward "weakly informative, sensitivity-tested." No competing standard is settled for pedagogy specifically.

### What has changed recently (last 5 years)

- The Bayesian workflow paper (Gelman et al. 2020) consolidated a decade of scattered methodological essays into a single citable framework. Before it, Bayesian comparative practice was inherited tacitly through advisors.
- The American Statistical Association's two-statement sequence — the 2016 statement on p-values and the 2019 "moving beyond p<0.05" editorial — has shifted what counts as a competent methods discussion. Methods sections now expected to defend choices, not just describe them.
- LLMs have changed the friction surface of a comparative analysis. A student can now request and inspect both a `scipy.stats` frequentist fit and a `PyMC` or `numpyro` Bayesian fit in one session, where before this was two separate skill investments. This is the book's bet.

---

## 3. Application Domain Examples

The TIKTOK dataset categories (BLS/O*NET) all appear live and downloadable as of May 2026:

- **Occupational wage distributions (BLS OEWS).** Tables at [bls.gov/oes/tables.htm](https://www.bls.gov/oes/tables.htm); May 2025 release scheduled May 15, 2026; May 2024 currently live. Frequentist question: mean wage differs across two metros? Bayesian question: posterior probability that occupation X pays > $Y in this metro, given prior from neighboring metros. Both supported.
- **Employment trend by occupation cluster (BLS CES).** [bls.gov/ces/](https://www.bls.gov/ces/) — monthly establishment survey. Time-series shape; the frequentist version runs OLS on logged employment, the Bayesian version is a state-space model with informative prior on trend. Both supported.
- **Automation exposure by occupation (O*NET).** Database at [onetcenter.org/database.html](https://www.onetcenter.org/database.html); CC-licensed, quarterly updates, next May 2026. Frequentist question: does automation-exposure score predict 2014–2024 employment change? Bayesian question: posterior on the slope, with prior informed by Frey-Osborne 2017 (with sensitivity analysis to a flat prior). Both supported, and the asymmetry is real teaching territory.
- **Educational attainment and earnings (BLS).** OEWS plus Current Population Survey tables ([bls.gov/cps/](https://www.bls.gov/cps/)). Standard inference questions; both frameworks land in classic regression territory.
- **Regional labor market variation (BLS QCEW).** Data files at [bls.gov/cew/downloadable-data-files.htm](https://www.bls.gov/cew/downloadable-data-files.htm); CSV downloads. Frequentist: county-level random effects ANOVA; Bayesian: partial-pooling hierarchical model — the asymmetry favors Bayes here.

The BLS API ([bls.gov/developers/api_signature_v2.htm](https://www.bls.gov/developers/api_signature_v2.htm)) supports 50 series, 20 years, 500 daily queries with free registration — easily enough for a student project. O*NET database is CC-licensed and downloadable in full ([onetcenter.org/db_releases.html](https://www.onetcenter.org/db_releases.html)). Both infrastructures are live, free, and stable. The book's data promise is honored.

---

## 4. The Book's Thesis Connection

The book's central thesis is that the choice between frequentist and Bayesian is a *reader's choice*, made on the basis of having worked both ways on actual problems. Chapter 12 is the first place where that promise is cashed. The reader stops being told that there's a choice and is forced to make one.

The chapter's deliverable form — a 4–6 page written argument about method, not a lab report of results — is the structural commitment to that thesis. A lab report would let the student hide behind numbers. A methodological essay forces the choice to surface. This is also where the book's pedagogical claim ("after reading this you can make a defensible choice") gets tested.

The chapter explicitly serves as Chapter 13's setup. Chapter 12 forces the choice. Chapter 13 systematizes the choosing. Without 12 the framework in 13 would be abstract; without 13 the choice in 12 would be unstructured.

---

## 5. Intellectual Lineage Notes

- **Tukey 1977** for the "look at the data first" prerequisite to any method choice. EDA is not Bayesian or frequentist — it precedes both. The chapter's dataset-selection step is Tukey-flavored.
- **Box 1976** for the iterative-modeling stance and the "all models are wrong" honesty. Box was a Bayesian who took frequentist tools seriously; the chapter inherits this disposition.
- **Gelman, Vehtari, et al. 2020 "Bayesian Workflow"** is the canonical close cousin. The chapter's six-question scaffold maps roughly to: (Q1 = "specify the model"; Q2 = "validate via simulation and posterior checks"; Q3 = "specify prior, run posterior"; Q4 = "compare models / compare to alternative analyses"; Q5 = "what does this inform"; Q6 = "what's the sensitivity"). The chapter's contribution is to require the same scaffold to be run for both frameworks side by side, which the Gelman paper does not do.
- **Reporting standards canon**: CONSORT 2010/2025 for clinical trials (EQUATOR Network); APA JARS-Quant 2018 update including Bayesian reporting standards ([apastyle.apa.org/jars/quantitative](https://apastyle.apa.org/jars/quantitative)). The six-question scaffold is closer in form to a *methodological essay* than to any reporting standard — note this explicitly. Standards tell you what to include; the scaffold asks you to argue.
- The ASA 2016 statement (Wasserstein & Lazar) and 2019 follow-up establish the field-wide invitation to argue rather than declare; the chapter takes that invitation literally.

---

## 6. Pedagogical Delivery Research

The literature on statistical capstone projects is small but useful. The most direct reference is the 2016 *Journal of Statistics Education* survey: Bailey, Spence, & Sinn (2016), "A Survey of Statistical Capstone Projects" [DOI 10.1080/10691898.2016.1257927](https://www.tandfonline.com/doi/full/10.1080/10691898.2016.1257927). It classifies four flavors — standalone, consultancy, embedded-in-methods-course, instruction-focused. Chapter 12 is closest to the *embedded* type but functions as a mini-standalone within a single week.

Recurring failure modes documented in the capstone literature:

- *Scope creep.* Students pick a dataset too large to analyze in the available time. The TIKTOK constraint ("tractable in a single work session") is the right response — but the chapter needs to enforce it, possibly by pre-curating dataset slices.
- *Question drift.* The student starts with one question and ends with another, often a less interesting one, because the data made the original question hard. Mitigation: pre-specified questions per dataset, which TIKTOK already commits to.
- *Method-loyalty.* Students pre-commit to a framework before seeing the data. The chapter's structure (do both, then argue) directly addresses this.
- *Verdict-seeking.* Students want to be told which approach is "right." The deliverable design (an argument, not a verdict) addresses this — but only if the grading rubric also rewards the argument over the conclusion.

What makes integrative projects in statistics succeed (from the survey and from related work, e.g., the *American Statistician*'s teaching-corner archive): (a) a tightly scoped dataset, (b) pre-specified questions, (c) a clear deliverable form, (d) explicit grading criteria, (e) a written component that forces synthesis, (f) early formative feedback. TIKTOK already commits to (a)–(e). The chapter should add (f): a midway checkpoint, even if informal.

Strategic LLM use is a new pedagogical variable. The book's Chapter 2 has already taught prompting for statistics. By Chapter 12, the student should be using the LLM as a paired analyst — generating both implementations, then arguing with them about prior choice, sensitivity, and interpretation. The chapter should model this explicitly in the worked partial example.

---

## 7. Representation and Display Research

Section 7 in this chapter is *not* a side-by-side comparison table — the student renders the table. The chapter renders the *scaffold for rendering it*.

**The deliverable described.** A 4–6 page written comparative analysis that answers the six questions, in prose, with embedded results. Not a lab report. Not a Methods/Results/Discussion structure. The reader of the deliverable is a methodologically literate skeptic who will accept a number only if it is justified.

Strong models for this kind of writing exist in:

- **Short methods papers in** *Statistics in Medicine* **and** *The American Statistician*. The methods discussions there are often 2–4 pages each, with the comparison between methods carried in prose and supported by one or two figures. This is the closest published genre to what students are being asked to produce.
- **Methodological appendices in the** *Journal of the American Statistical Association*'s *applications and case studies* section. These often contain the "alternative analyses" sub-section that maps closely to Q4–Q5 of the scaffold.
- **The Bayesian Workflow paper itself** (Gelman et al. 2020) as a master class in how to write about analytical choices with judgment rather than verdict.

What a strong deliverable looks like, concretely:

- *Opens with the question and the dataset*, not the method. The reader knows what is being asked and on what evidence before either framework appears.
- *Specifies the data-generating process* in plain language. Two paragraphs. What is the population? What is the sampling mechanism? What does each framework assume here?
- *Reports the frequentist analysis* with point estimate, interval, test result, and a sentence on what the result does *not* tell you. (Q2)
- *Reports the Bayesian analysis* with prior, posterior summary, credible interval, and an explicit statement of how the prior was chosen and what a flat prior would change. (Q3)
- *Compares* the two — where they agree numerically, where they diverge, and (this is the move that signals statistical judgment) *why* the divergence is what it is. (Q4)
- *Picks one* and *justifies* the pick in terms of what the decision actually needs. (Q5)
- *Names what would change the conclusion* — a sensitivity check, a different prior, a larger sample. (Q6)

The 4–6 page constraint is doing real work. It is long enough to force the prose moves and short enough to forbid filler.

---

## 8. Open Questions and Research Gaps

- **The pre-curated dataset slice problem.** TIKTOK promises tractable datasets. The chapter needs to deliver them. Companion website status is OWNED in the TIKTOK open-questions log but not yet live. Until live, the chapter risks pointing students at raw BLS downloads that exceed the session budget. Pre-cut CSVs are the right delivery; verify launch.
- **Grading rubric not specified.** The deliverable is a written argument; written-argument grading is hard. The chapter should at minimum suggest a 4-criterion rubric (specification quality, both-frameworks-complete, comparison quality, judgment quality). Without this the chapter is asking instructors to invent the rubric.
- **Worked partial example status.** TIKTOK promises one. The right candidate is the automation-exposure dataset, partly because the Frey-Osborne / Melbourne replication pair gives an existing methodological debate to scaffold against. But the example needs to be partial — leaving room for the student to finish — and that's a craft problem more than a research problem.
- **What happens when a student picks a question that admits a clear winner.** The chapter assumes the comparison will be informative. Some pairs of questions and datasets have a clear methodological winner (e.g., very large samples + no prior knowledge = frequentist by efficiency; very small samples + strong prior = Bayesian by stability). Students should not be punished for picking such a pair; the chapter should name this as an option and require them to explain *why* the answer is clear.
- **LLM in the deliverable.** The book commits to LLM-implemented analyses throughout. The deliverable should probably disclose LLM use — what was prompted, what was edited, what failed. This is a 2026 hygiene question the chapter has to take a position on.

---

## 9. Sourcing Notes

- All BLS data products verified live as of May 2026. OEWS, CES, CPS, QCEW all available via [bls.gov/data](https://www.bls.gov/data/) and the API ([bls.gov/developers](https://www.bls.gov/developers/)).
- O*NET database verified live at [onetcenter.org/database.html](https://www.onetcenter.org/database.html), CC-licensed, next quarterly update scheduled May 2026.
- Gelman et al. 2020 *Bayesian Workflow*: arXiv ID 2011.01808 confirmed; Routledge book version exists ([routledge.com/Bayesian-Workflow/...](https://www.routledge.com/Bayesian-Workflow/Gelman-Vehtari-McElreath-Simpson-Margossian-Yao-Kennedy-Gabry-Burkner-Modrak-Barajas/p/book/9780367490140)).
- Box 1976 JASA citation confirmed (vol 71, issue 356, pp. 791–799).
- Tukey 1977 EDA: Addison-Wesley, ISBN 0-201-07616-0 (confirmed via [archive.org](https://archive.org/details/exploratorydataa0000tuke_7616)).
- Frey & Osborne 2017 final journal version: *Technological Forecasting and Social Change*, vol. 114, pp. 254–280. The 2013 Oxford working paper preceded it; cite the 2017 journal version when possible.
- The 2016 *JSE* capstone survey by Bailey, Spence, & Sinn confirmed via Taylor & Francis and ERIC ([eric.ed.gov/?id=EJ1128173](https://eric.ed.gov/?id=EJ1128173)).
- Wasserstein & Lazar 2016 ASA statement and Wasserstein, Schirm, & Lazar 2019 editorial both confirmed in *The American Statistician*.
- `[verify]` items: precise wording of the May 2025 OEWS release once it lands May 15, 2026 — release date confirmed but content not yet inspected at time of research.
