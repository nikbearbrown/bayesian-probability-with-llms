# Research: Chapter 7 — Priors: Where Does Your Assumption Come From?
## Bayesian Probability with LLMs

**Chapter one-line:** Every statistical analysis has prior assumptions. Frequentist methods hide theirs in the machinery. Bayesian methods name theirs explicitly. This chapter makes both visible — and shows what changes when you change them.

**Research date:** 2026-05-13

---

## 1. Primary Sources

### Foundational papers and texts

- **Laplace, P.-S. (1814).** *Essai philosophique sur les probabilités.* The "principle of insufficient reason" — assigning equal probability to indistinguishable outcomes — and its extension to continuous parameters as a uniform prior. Later renamed the "principle of indifference" by Keynes (1921). Useful historical context that the chapter's "flat prior" is older than statistics-as-a-discipline. ([Wikipedia: Principle of indifference](https://en.wikipedia.org/wiki/Principle_of_indifference).)
- **Jeffreys, H. (1946).** "An invariant form for the prior probability in estimation problems." *Proc. Roy. Soc. London A* 186: 453–461. The Jeffreys prior — a reparametrization-invariant default. Important because it shows "uninformative" is not a single well-defined thing; you have to choose an invariance principle to get a unique answer.
- **de Finetti, B. (1937/1974).** "La prévision: ses lois logiques, ses sources subjectives" / *Theory of Probability*. The foundational subjectivist text: probability *is* degree of belief, period. De Finetti's exchangeability theorem (1937) shows that an exchangeable sequence is equivalent to conditioning on a parameter with a prior. This is why subjectivists say all inference is implicitly Bayesian: "there is no prior" is a position, not an escape from priors. ([Wikipedia summary of de Finetti's theorem](https://en.wikipedia.org/wiki/De_Finetti%27s_theorem); 1937 paper introduction at [Springer](https://link.springer.com/chapter/10.1007/978-1-4612-0919-5_9).)
- **Bernardo, J. M. & Smith, A. F. M. (1994/2000).** *Bayesian Theory.* Wiley. The standard advanced reference; reference priors (Bernardo's information-theoretic construction) and a careful treatment of the distinction between subjective, objective, and reference Bayesian programs. [PDF copy hosted at WordPress mirror](https://statisticalsupportandresearch.wordpress.com/wp-content/uploads/2019/03/josc3a9-m.-bernardo-adrian-f.-m.-smith-bayesian-theory-wiley-1994.pdf).
- **Gelman, A. et al. (2017–present).** "Prior Choice Recommendations" wiki on `stan-dev/stan`. The living document for weakly informative default priors. ([GitHub](https://github.com/stan-dev/stan/wiki/prior-choice-recommendations).) Refresh date matters: cite as accessed 2026-05.
- **Gelman, A., Simpson, D. & Betancourt, M. (2017).** "The Prior Can Often Only Be Understood in the Context of the Likelihood." *Entropy* 19: 555. Argues against the idea of a "prior in isolation": priors are calibrated by what likelihood they meet.

### The frequentist defense (the "fairness test" set)

- **Efron, B. (1986).** "Why Isn't Everyone a Bayesian?" *The American Statistician* 40 (1): 1–5. Foundational, still cited. Argues that frequentist methods are practical, objective, and that the *theoretical* superiority of Bayes does not translate to applied superiority once one tries to construct genuine priors. [PDF](https://www2.isye.gatech.edu/isyebayes/bank/efronwhy1986.pdf); [journal page](https://www.tandfonline.com/doi/abs/10.1080/00031305.1986.10475342).
- **Mayo, D. G. (2018).** *Statistical Inference as Severe Testing: How to Get Beyond the Statistics Wars.* Cambridge University Press. The most rigorous contemporary defense of frequentist (error-statistical) inference. Mayo argues that the question inference should answer is "has this hypothesis passed a severe test?" — and Bayesian posterior probability is not, in general, an answer to that question. ([Cambridge book page](https://www.cambridge.org/core/books/statistical-inference-as-severe-testing/D9DF409EF568090F3F60407FF2B973B2); [NDPR review](https://ndpr.nd.edu/reviews/statistical-inference-as-severe-testing-how-to-get-beyond-the-statistics-wars/).) Required reading for the chapter's "fairness test" commitment.
- **Senn, S. (2011).** "You May Believe You Are a Bayesian But You Are Probably Wrong." *Rationality, Markets and Morals* 2: 48–66. The cleanest pharma-statistician critique of subjective Bayesianism: in real clinical trials, statisticians can't write down priors that they genuinely believe; the doctrine is incoherent in practice. ([Discussion at Mayo's blog](https://errorstatistics.com/2012/01/14/you-may-believe-you-are-a-bayesian-but-you-are-probably-wrong/).)
- **Senn, S. (various).** Senn's blog and clinical-trials papers consistently push the point that priors used in practice are not the priors statisticians could honestly report under examination. ([Berry Consultants podcast episode 55](https://www.berryconsultants.com/resource/55-a-visit-with-stephen-senn-time-concurrent-controls-and-the-bayesian-guidance) is a more accessible introduction.)

### The Bayesian responses

- **Gelman, A. (2008).** "Objections to Bayesian Statistics." *Bayesian Analysis* 3 (3): 445–449. Gelman writes the anti-Bayesian case in the voice of a hypothetical critic, then answers it. The discussion (Bernardo, Kadane, Senn) is at least as valuable as the article. ([Project Euclid](https://projecteuclid.org/journals/bayesian-analysis/volume-3/issue-3/Objections-to-Bayesian-statistics/10.1214/08-BA318.full); [PDF](https://sites.stat.columbia.edu/gelman/research/published/badbayesmain.pdf); [rejoinder PDF](https://sites.stat.columbia.edu/gelman/research/published/badbayesresponsemain.pdf).)
- **Gelman, A. & Hennig, C. (2017).** "Beyond Subjective and Objective in Statistics." *J. Roy. Stat. Soc. A* 180 (4): 967–1033. Read paper with extensive discussion. Argues that "objective" and "subjective" are unhelpful labels and proposes replacing each with a cluster of operational virtues — transparency, consensus, impartiality, correspondence to observable reality on one side; awareness of multiple perspectives, context dependence on the other. ([Wiley](https://rss.onlinelibrary.wiley.com/doi/abs/10.1111/rssa.12276); [arXiv preprint](https://arxiv.org/abs/1508.05453); [full discussion PDF](https://sites.stat.columbia.edu/gelman/research/published/gelman_hennig_full_discussion.pdf).) This is the single most important paper for the chapter to engage with.

### Regulatory and applied perspectives

- **ICH E9 (1998).** "Statistical Principles for Clinical Trials." The original ICH guideline; explicitly frequentist in default framing.
- **ICH E9(R1) (2019, adopted by FDA 2021).** "Addendum on Estimands and Sensitivity Analysis in Clinical Trials." Establishes the estimands framework — defining "what is to be estimated" independent of method. Allows for Bayesian analyses but requires sensitivity analyses. ([FDA page](https://www.fda.gov/regulatory-information/search-fda-guidance-documents/e9r1-statistical-principles-clinical-trials-addendum-estimands-and-sensitivity-analysis-clinical); [ICH PDF](https://database.ich.org/sites/default/files/E9-R1_Step4_Guideline_2019_1203.pdf); [Federal Register notice](https://www.federalregister.gov/documents/2021/05/12/2021-10066/e9r1-statistical-principles-for-clinical-trials-addendum-estimands-and-sensitivity-analysis-in).)
- **FDA (2010).** "Guidance for the Use of Bayesian Statistics in Medical Device Clinical Trials." The landmark — FDA's first explicit acceptance of Bayesian designs in regulated submissions. ([FDA page](https://www.fda.gov/regulatory-information/search-fda-guidance-documents/guidance-use-bayesian-statistics-medical-device-clinical-trials-pdf-version); [Federal Register 2010 notice](https://www.federalregister.gov/documents/2010/02/08/2010-2596/guidance-for-industry-and-food-and-drug-administration-guidance-for-the-use-of-bayesian-statistics).) Establishes the regulatory rules around prior justification.
- **FDA (2026 draft).** "Use of Bayesian Methodology in Clinical Trials of Drug and Biological Products," draft guidance, Federal Register Jan 12 2026. ([Federal Register notice](https://www.federalregister.gov/documents/2026/01/12/2026-00325/use-of-bayesian-methodology-in-clinical-trials-of-drug-and-biological-products-draft-guidance-for); [JAMA viewpoint](https://jamanetwork.com/journals/jama/fullarticle/2847011); [JAMA research methods piece](https://jamanetwork.com/journals/jama/fullarticle/2847012); [Berry Consultants guide](https://www.berryconsultants.com/resource/guide-to-the-draft-fda-bayesian-guidance-2026).) Explicit on the requirement that priors be justified, pre-specified, and accompanied by sensitivity analyses. Chapter 7's "fairness test" rationale is in the bones of this document.
- **Campbell, G. (2023).** "Bayesian Statistics for Medical Devices: Progress Since 2010." [PMC link](https://pmc.ncbi.nlm.nih.gov/articles/PMC9984131/). Historical review of how device approvals have actually used Bayesian methods. Useful real-world numbers.

### Pedagogy

- **van Erp, S., Mulder, J. & Oberski, D. L. (2020).** "The Importance of Prior Sensitivity Analysis in Bayesian Statistics: Demonstrations Using an Interactive Shiny App." *Frontiers in Psychology* 11: 608045. ([Frontiers](https://www.frontiersin.org/journals/psychology/articles/10.3389/fpsyg.2020.608045/full); [PMC](https://pmc.ncbi.nlm.nih.gov/articles/PMC7721677/).) The classroom-ready resource on prior sensitivity.
- **Kallioinen, N., Paananen, T., Bürkner, P.-C. & Vehtari, A. (2024).** "Detecting and diagnosing prior and likelihood sensitivity with power-scaling." *Stat. Comput.* 34: 57. ([arXiv 2107.14054](https://arxiv.org/pdf/2107.14054).) The automated diagnostic for prior sensitivity now built into `posterior` and `priorsense`.

---

## 2. The Core Concept — State of the Field

### What is settled

- **A prior is always present.** A frequentist t-test, run honestly, gives results equivalent to a Bayesian analysis with an *improper uniform* prior on the mean. The flat prior is itself a prior. Whether or not this counts as "the same prior" in some technical sense is debated; that there is no analysis without distributional assumptions is not.
- **Different priors produce different posteriors, especially in low-data regimes.** This is arithmetic, not philosophy. The contested question is what to do about it.
- **Sensitivity analysis — running the same model under multiple reasonable priors — is the standard professional move.** Required by ICH E9(R1) for Bayesian submissions. Recommended by Stan/Gelman/Vehtari documentation. Not optional.
- **"Improper" priors (e.g., uniform on the real line) can yield proper posteriors when the data are informative.** They are mathematically legitimate but require justification each time.

### What is disputed

- **Whether priors are subjective.** The classical position (de Finetti, Lindley, Savage) is yes, irreducibly. The objective Bayesian position (Jeffreys, Bernardo, Berger) is that for many problems a unique principled "non-informative" prior exists (Jeffreys prior, reference prior). The Gelman-Hennig position is that the subjective/objective dichotomy is the wrong question; transparency and sensitivity analysis are what actually matter.
- **Whether the prior is the *prior on a parameter*, or the *prior on a model*.** Subjective priors on continuous nuisance parameters are different in kind from priors on which-model-is-true. The latter is dramatically more sensitive (this is the Lindley-paradox machinery from Ch 6).
- **Whether frequentist methods really hide a prior.** Mayo argues no — that error-statistical methods do not require a prior because they are answering a different question (long-run error control, severity), not "what should I believe?" Bayesians counter that any *interpretation* of frequentist output as a degree of belief secretly requires a prior. Both are right depending on what you take inference to be *for*.
- **Whether elicited priors are honest.** Senn's central charge: practicing statisticians cannot write down priors they genuinely hold. They write down priors that produce defensible analyses. This is a serious objection. Gelman & Hennig's response: prior elicitation is a transparency tool, not a window into the analyst's soul.

### What has changed recently (last 5 years)

- **Weakly informative priors are the new default.** Flat priors have fallen out of favor in the Stan/`brms` ecosystem. Weakly informative priors (e.g., normal(0, 5) on regression coefficients on standardized predictors, half-normal(0, 1) on scale parameters) are the recommended starting point. ([Stan prior choice wiki](https://github.com/stan-dev/stan/wiki/prior-choice-recommendations).)
- **The 2026 FDA draft Bayesian guidance** (Federal Register Jan 12 2026) formalizes prior sensitivity analyses and external-information-borrowing safeguards as regulatory requirements. This is the chapter's real-world hook for "priors are contestable in regulated settings."
- **Power-scaling diagnostics** (Kallioinen et al. 2024; `priorsense` R package) make prior sensitivity quantifiable rather than narrative. This is a methodological maturation worth flagging.
- **Reference-prior debates have quieted.** The 1990s-2000s flurry of Berger-Bernardo work on objective priors has been overtaken in practice by weakly informative defaults. Important historical move; not the live frontier.

---

## 3. Application Domain Examples

The chapter's central scenario is a clinical-trial reanalysis under three priors. Real material to draw on:

- **Pharma examples of priors that change conclusions.** Subgroup analyses are the cleanest case: with a strong prior toward "no subgroup effect," you find none; with a weak prior, you find an apparent effect. This is precisely why FDA reviewers scrutinize priors.
- **Specific contested-priors examples.** FDA medical-device submissions have had priors challenged on grounds that they overweighted the sponsor's prior internal data. The 2010 FDA medical-device guidance explicitly warns that priors based on expert opinion (rather than data) can delay or block approval if FDA panel members disagree. ([2010 FDA guidance](https://www.fda.gov/regulatory-information/search-fda-guidance-documents/guidance-use-bayesian-statistics-medical-device-clinical-trials-pdf-version).) The chapter can quote this guidance directly.
- **A worked clinical-trial example.** The chapter says "previous Phase II trials showed small or null effects" as the informative prior. A concrete published case: meta-analytic priors built from historical control arms have been used in oncology trials with FDA approval. The MAP (Meta-Analytic-Predictive) prior approach (Neuenschwander et al., *Clinical Trials* 2010) is the standard tool. [verify exact citation before printing.]
- **The COVID vaccine trials as a teaching parallel.** The mRNA vaccine trials used Bayesian designs with informative priors for accelerated approval decisions. Public documents from Pfizer's BNT162b2 trial and Moderna's mRNA-1273 trial describe the priors used. [verify specific design documents and primary citations before using.]

---

## 4. The Book's Thesis Connection

This is the philosophical hinge of the book. If a reader is going to switch from frequentist defaults to Bayesian methods, they are going to do it (or refuse to do it) because of the priors question. So the chapter is doing two things at once:

1. **Defending frequentist methods on the strongest available grounds.** Mayo, Efron, Senn. Not as straw to knock down, but as a fair description of the cost of going Bayesian. The chapter's "fairness test" commitment (TIKTOK lines 594–602) makes this explicit.
2. **Defending Bayesian methods on their strongest grounds.** Gelman, Hennig, Bernardo. The prior is not a weakness to be hidden — it is a place where domain knowledge enters the analysis explicitly. Sensitivity analysis converts the prior from a vulnerability into an auditable artifact.

The book's stance, consistent with its thesis, is *not* to declare a winner. The chapter shows the reader the cost of each side and hands them the choice. The thesis-aligned move is the side-by-side demonstration: same data, three priors, three posteriors, none of them "right" — and then asking the reader what they would do.

The Ch 6 → Ch 7 link is structural: Bayes factors (Ch 6) are *defined* as ratios of marginal likelihoods, which are *integrals of likelihoods against priors*. So the prior-sensitivity of Bayes factors flagged in Ch 6 is exactly what Ch 7 unpacks. The reader who finished Ch 6 wondering "but where did the prior come from in the BF?" gets the answer here. The whole of Ch 7 is implicitly a continuation of Ch 6's last paragraph.

---

## 5. Intellectual Lineage Notes

- **Laplace's principle of insufficient reason (1814)** — the original move: in the absence of distinguishing information, assign equal probability. Generalizes to uniform priors on continuous parameters. Famously breaks under reparametrization (a uniform prior on θ is not uniform on θ²), which is the failure that motivates Jeffreys.
- **Jeffreys priors (1946)** — invariant under reparametrization. The first principled "objective" prior. Works cleanly for one-parameter problems; complications for multi-parameter problems lead to the reference-prior program (Bernardo 1979; Berger & Bernardo 1992c).
- **Bernardo & Smith *Bayesian Theory* (1994)** — the encyclopedic exposition of reference priors as the "objective Bayesian" canon. Important because it shows there *is* a principled objective Bayesian position, distinct from subjective Bayes and from frequentism. ([Bernardo's monograph on reference analysis](https://www.uv.es/~bernardo/Monograph.pdf).)
- **The de Finetti / Lindley / Savage subjectivist tradition** — probability is degree of belief, full stop. De Finetti's theorem (1937) provides the deepest argument: exchangeability *forces* a representation as conditioning on a parameter with a prior. There is no escape from priors, only honest or dishonest priors.
- **Efron 1986** — the practitioner's frequentist counter: even granted the philosophical case for Bayes, the operational case is harder than Bayesians admit. Required reading; under-cited in modern Bayesian textbooks.
- **Mayo 2018** — the philosophical frequentist counter: severity, not posterior probability, is the epistemically right thing to compute. The serious version of "p-values measure something real and meaningful."
- **Gelman & Hennig 2017** — the move past the dichotomy. The chapter's most usable contemporary framing.
- **Stan prior choice wiki (2017–present)** — the working-Bayesian consensus. Weakly informative defaults; sensitivity analysis as standard practice; priors and likelihoods understood together, not in isolation.

---

## 6. Pedagogical Delivery Research

Student confusions specific to this chapter:

- **"The prior is the conclusion."** Students new to Bayes often think that if you start with a prior favoring H₁, you'll end with a posterior favoring H₁ — i.e., that Bayesian inference is circular. The teaching move: show, with one calculation, that strong data overrides a wrong prior. A normal(0, 1) prior on a treatment effect, faced with data strongly suggestive of effect size 2.0, produces a posterior near 2.0, not near 0. The prior is updated, not preserved.
- **"The prior is arbitrary."** Subtle inverse of the first confusion. The fix: walk through how a domain expert would actually construct a weakly informative prior. Half-normal(0, σ) where σ is set so that 95% prior mass falls within "physically plausible" range. This is not arbitrary; it is a quantification of background knowledge. The chapter should explicitly compare a defensible prior with a transparently silly one (e.g., normal(50, 0.1) for a coin's bias toward heads) so students see the difference.
- **"Flat priors are objective."** Trap. A flat prior is a strong prior on certain quantities (e.g., flat on σ implies a particular curved prior on σ², which implies an even more curved prior on log σ). Demonstrate with one reparametrization on the board.
- **The sensitivity-analysis pedagogy.** The van Erp et al. 2020 Shiny app is the right reference. Students learn faster by *moving* the prior and watching the posterior shift than by being told sensitivity matters. If the book has a companion site, a similar interactive widget is the chapter's natural complement.
- **Robust vs. fragile conclusions.** Frame the takeaway as: "*If the same conclusion survives reasonable variation in the prior, report it. If it doesn't, get more data or pick the prior you can defend, and report the sensitivity.*" This converts the prior from a methodological weakness into a methodological discipline.

LLM-specific pedagogy for this chapter:

- Have students prompt an LLM to write Stan or PyMC code for the trial reanalysis under all three priors. Inspect the prior specifications. Catch the LLM if it silently substitutes a different prior (a common LLM failure mode is reverting to default flat priors when asked for "weakly informative").
- The chapter's prompting section should explicitly teach the student to *check the rendered priors*, not just accept LLM output. This is a methodological skill the book can claim uniquely.

---

## 7. Representation and Display Research

TIKTOK.md does not give Ch 7 a side-by-side comparison table. The chapter would benefit from one. Recommended construction:

| | Frequentist | Bayesian (informative) | Bayesian (weakly informative) | Bayesian (flat) |
|---|---|---|---|---|
| Prior on treatment effect | Implicit uniform | Normal(0, 0.5) — "small effects expected" | Normal(0, 2) — "anything within reason" | Uniform(−∞, +∞) |
| Output | p = 0.04, reject H₀ | P(effect > 0 | data) = 0.78 | P(effect > 0 | data) = 0.94 | P(effect > 0 | data) = 0.95 |
| Point estimate | β̂ = 0.6 | Posterior mean = 0.3 | Posterior mean = 0.55 | Posterior mean = 0.6 |
| 95% interval | (0.05, 1.15) CI | (−0.05, 0.65) credible | (0.10, 1.00) credible | (0.05, 1.15) credible |
| Decision (α=0.05 / 95% threshold) | Reject H₀ | Don't act | Act | Act |
| What's hidden | Uniform prior; α=0.05 convention | Informative prior — needs justification | Weakly informative — defensible | Improper prior — equivalent to frequentist |

(*Numbers above are constructed for the table's pedagogical shape; the chapter should populate them from a real worked example. [verify against a chosen dataset before printing.]*)

**Recommended additional row to flag for Nik:**

| | Frequentist | Bayesian (informative) | Bayesian (weakly informative) | Bayesian (flat) |
|---|---|---|---|---|
| Regulatorily acceptable? | Default; rarely contested | Contested unless prior is justified by external data | Generally acceptable with sensitivity analysis | Acceptable; equivalent to frequentist |

Rationale: makes the regulatory politics visible in the table. The "fairness test" claim (frequentist analyses are "harder to game with convenient priors") gets concrete teeth this way.

**Visual:** the canonical chart is three posteriors overlaid on the same axes, with the prior shown as a dashed curve behind each. The eye learns immediately that "the point estimate barely moves; the tails change" — which is exactly the claim TIKTOK.md makes in the Bayesian-solution section.

---

## 8. Open Questions and Research Gaps

- **The chapter must avoid sliding into Bayesian advocacy.** The TIKTOK "fairness test" language is well-intentioned but the actual chapter will tilt unless Mayo, Senn, and Efron are quoted *at their strongest*, not paraphrased toward easy refutation. Recommend that the chapter literally quote one paragraph each from Mayo 2018 and Senn 2011 before responding.
- **The "regulators require frequentist" claim in TIKTOK needs nuance.** It's true historically and partly true currently, but the 2010 FDA medical-device guidance and especially the 2026 FDA draft Bayesian-drugs guidance show the regulatory landscape moving. The chapter should describe this as "currently in transition" rather than as a settled state.
- **Where to put the "no analysis is prior-free" demonstration.** Two options: (a) early, as a setup move ("watch — even the t-test has a prior"); (b) late, as the synthesis ("having seen what priors do, you can now see one in the t-test"). Option (b) is the Feynman move — make the student do the work, then reveal the trick.
- **The interaction with Ch 8 (sparse data).** Ch 7 says "prior sensitivity matters most when data is sparse." Ch 8 picks that up. The bridge sentence at the end of Ch 7 is doing important work; recommend writing it tight.
- **Domain gap to flag for Nik:** the clinical-trial example requires being right about what a real Phase III analysis looks like. If domain expertise is thin, recommend either (a) anchoring to a published reanalysis (e.g., one of the published examples in Spiegelhalter, Abrams & Myles 2004 *Bayesian Approaches to Clinical Trials*) or (b) staying with a simpler stylized example and naming the simplification.
- **The Gelman & Hennig 2017 framing should be central, not peripheral.** It's the most defensible contemporary position and dissolves a lot of the "subjective vs. objective" cargo. Recommend devoting a substantial subsection to it.
- **The chapter does not currently mention prior predictive checks.** These are the practical companion to sensitivity analysis: simulating data from the prior, checking whether it produces "physically plausible" datasets. Worth a paragraph. ([Gabry, Simpson, Vehtari, Betancourt & Gelman 2019 *JRSSA*.](https://rss.onlinelibrary.wiley.com/doi/abs/10.1111/rssa.12378) [verify exact citation.])

---

## 9. Sourcing Notes

Tier-1 (primary, accessible, verified):
- Gelman 2008 *Bayesian Analysis* — open PDF and Project Euclid.
- Gelman & Hennig 2017 *JRSS A* — Wiley, arXiv preprint, full discussion PDF.
- Efron 1986 *American Statistician* — open PDFs at Georgia Tech and Duke.
- Mayo 2018 Cambridge book — published, available, multiple review essays.
- Stan prior choice wiki — live document, cite as accessed 2026-05-13.
- FDA 2010 medical-device Bayesian guidance — official FDA page.
- FDA 2026 Bayesian-drugs draft — Federal Register notice, JAMA viewpoints.
- ICH E9(R1) — official ICH PDF and FDA page.
- van Erp, Mulder & Oberski 2020 — open access, Frontiers.

Tier-2 (foundational, cited via secondary sources for this research file):
- Laplace 1814 — historical context via Wikipedia and standard references.
- Jeffreys 1946 *Proc. Roy. Soc.* — referenced via Kass & Raftery 1995 discussion.
- de Finetti 1937 — referenced via Bayesian Spectacles and Wikipedia.
- Bernardo & Smith 1994 *Bayesian Theory* — referenced via Bernardo's online monograph and the Wiley PDF mirror.

Tier-3 ([verify] before printing in the chapter):
- The specific MAP-prior pharma reanalysis examples — Neuenschwander et al. 2010 needs page-level confirmation.
- The COVID vaccine trial design documents — Pfizer and Moderna trial protocols should be sourced directly rather than from journalistic summaries.
- Spiegelhalter, Abrams & Myles 2004 *Bayesian Approaches to Clinical Trials and Health-Care Evaluation*, Wiley — chapter on prior elicitation in clinical trials is canonical; [verify direct quotes against the book itself].
- The Senn 2011 paper appears in *Rationality, Markets and Morals* — open-access journal but verify final pagination before quoting.

**Voice-anchoring:** the root `style/` and per-book `style/` folders were not inspected for this research file. The draft chapter that uses this research should flag `voice-unanchored` if those folders are still empty when drafting begins.

**Chapter-level honesty caveat:** this is the most philosophically loaded chapter in the book. The temptation to settle the frequentist-vs-Bayesian question is high. The book's thesis depends on not settling it. The research above is deliberately balanced; the chapter should be too.
