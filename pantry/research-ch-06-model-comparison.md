# Research: Chapter 6 — Model Comparison
## Bayesian Probability with LLMs

**Chapter one-line:** How do you choose between two models? Frequentist model comparison requires choosing a test; Bayesian model comparison produces a probability — and the difference matters most when the models are close.

**Research date:** 2026-05-13

---

## 1. Primary Sources

### Foundational papers and texts

- **Akaike, H. (1973).** "Information theory and an extension of the maximum likelihood principle." In B. N. Petrov & F. Csáki (Eds.), *2nd International Symposium on Information Theory*, pp. 267–281. Akadémia Kiadó, Budapest. The first English presentation of what becomes AIC; conference proceedings, sometimes hard to access.
- **Akaike, H. (1974).** "A new look at the statistical model identification." *IEEE Transactions on Automatic Control*, AC-19, 716–723. The formal AIC paper. By 2014 it had >14,000 Web of Science citations, among the 100 most-cited papers of all time. ([Wikipedia summary of citation count](https://en.wikipedia.org/wiki/Akaike_information_criterion))
- **Schwarz, G. (1978).** "Estimating the Dimension of a Model." *Annals of Statistics* 6, 461–464. The original BIC paper. Derives BIC as an asymptotic approximation to a transformation of the Bayesian posterior probability of a candidate model. ([Reference entry](https://www.scirp.org/reference/referencespapers?referenceid=1741009))
- **Jeffreys, H. (1961).** *Theory of Probability*, 3rd ed., Oxford University Press. Source of the Bayes factor as a formal device and of the original evidence-strength classification table that Ch 6 leans on.
- **Kass, R. E. & Raftery, A. E. (1995).** "Bayes Factors." *Journal of the American Statistical Association* 90 (430): 773–795. The modern canonical reference — defines BF, gives computational approaches (Laplace approximation, BIC as approximation), revises Jeffreys's strength categories, and works five applied examples (genetics, sports, ecology, sociology, psychology). PDF copies hosted at [stat.washington.edu](https://www.stat.washington.edu/raftery/Research/PDF/kass1995.pdf) and [CMU](https://www.andrew.cmu.edu/user/kk3n/simplicity/KassRaftery1995.pdf); journal page at [Taylor & Francis](https://www.tandfonline.com/doi/abs/10.1080/01621459.1995.10476572).
- **Burnham, K. P. & Anderson, D. R. (2002).** *Model Selection and Multimodel Inference: A Practical Information-Theoretic Approach*, 2nd ed., Springer. The standard reference defending AIC in applied (especially ecological) work. ([Springer book page](https://link.springer.com/book/10.1007/b97636))
- **Burnham, K. P. & Anderson, D. R. (2004).** "Multimodel Inference: Understanding AIC and BIC in Model Selection." *Sociological Methods & Research* 33 (2): 261–304. The article-length version most readers actually cite. Argues that the AIC-vs-BIC choice cannot be framed as Bayes-vs-frequentist; both can be derived under either philosophy with different assumptions about reality. ([PDF](https://sites.warnercnr.colostate.edu/wp-content/uploads/sites/73/2017/05/Burnham-and-Anderson-2004-SMR.pdf))
- **Vehtari, A., Gelman, A. & Gabry, J. (2017).** "Practical Bayesian model evaluation using leave-one-out cross-validation and WAIC." *Statistics and Computing* 27 (5): 1413–1432. Introduces PSIS-LOO (Pareto-smoothed importance sampling LOO) as the practical replacement for both AIC and Bayes factors in most working-Bayesian model comparisons. ([Springer](https://link.springer.com/article/10.1007/s11222-016-9696-4), [arXiv preprint](https://arxiv.org/abs/1507.04544), and tooling at [mc-stan.org/loo](http://mc-stan.org/loo/).)
- **Lindley, D. V. (1957).** "A Statistical Paradox." *Biometrika* 44: 187–192. The original Lindley paradox paper, building on Jeffreys's 1939 discussion. Wikipedia's [Lindley's paradox page](https://en.wikipedia.org/wiki/Lindley%27s_paradox) is a usable secondary survey.
- **Spanos, A. (2013).** "Who Should Be Afraid of the Jeffreys-Lindley Paradox?" *Philosophy of Science* 80 (1): 73–93. Useful philosophical exposition of the disagreement.

### Key empirical cases

- **COVID-19 growth-curve modeling.** Several published studies compare exponential, logistic, Gompertz, SIR, SEIR, and ARIMA models on COVID case data using AIC and related criteria.
  - Roosa et al., "Real-time forecasts of the COVID-19 epidemic in China from February 5th to February 24th, 2020," *Infectious Disease Modelling* 5 (2020): 256–263.
  - Mahanty et al. (2022), "Prediction of COVID-19 active cases using exponential and non-linear growth models." [Wiley link](https://onlinelibrary.wiley.com/doi/10.1111/exsy.12648).
  - "On the use of growth models to understand epidemic outbreaks with application to COVID-19 data." *PLOS ONE* (2020). [Link](https://journals.plos.org/plosone/article?id=10.1371/journal.pone.0240578).
  These are real examples the chapter can mine for its disease-spread scenario without invention. [verify] whether any of them publish AIC-vs-BF on the *same* dataset; if not, the side-by-side becomes a chapter-built worked example with synthetic-but-realistic data.

---

## 2. The Core Concept — State of the Field

### What is settled

- The mathematical definitions: AIC = −2·log(L̂) + 2·k; BIC = −2·log(L̂) + k·log(n); Bayes factor BF₁₀ = P(D|M₁) / P(D|M₀) = ∫p(D|θ,M₁)p(θ|M₁)dθ / ∫p(D|θ,M₀)p(θ|M₀)dθ. These are uncontested.
- AIC is an estimator of out-of-sample predictive deviance (Kullback-Leibler discrepancy). BIC is an asymptotic approximation to the log marginal likelihood under specific conditions. They answer different questions, and most pedagogical confusion comes from pretending they answer the same one. (Burnham & Anderson 2004; Kass & Raftery 1995.)
- Jeffreys's classification — values around 1 are anecdotal, 3–10 moderate, 10–30 strong, 30–100 very strong, >100 extreme — is a heuristic, not a theorem. Kass & Raftery (1995) lightly revised it (3, 20, 150 as thresholds).
- The likelihood ratio test (Neyman-Pearson lemma) is uncontestedly the most powerful test for nested simple-vs-simple hypotheses. Wilks's theorem gives the χ² asymptotic null distribution for nested LR statistics.

### What is disputed

- **AIC vs. BIC.** A long-running and partly tedious literature. BIC is consistent (probability of selecting the true model → 1 as n → ∞ *if* the true model is in the candidate set); AIC is efficient (chooses the model that minimizes expected prediction error in the realistic case where no candidate is true). Burnham & Anderson (2004) argue this is a difference of stance toward "is there a true model?" not a difference of philosophy.
- **Bayes factors are highly sensitive to priors on parameters** — far more sensitive than posterior estimates within a single model. This is the cleanest illustration of why Ch 6 implicitly requires Ch 7. ([Liu & Aitkin 2008, *J. Math. Psychol.*](https://www.sciencedirect.com/science/article/abs/pii/S002224960800028X); Sinharay & Stern 2002.) When the prior on a parameter under M₁ is widened, the marginal likelihood under M₁ shrinks roughly proportionally, and the BF can be moved by orders of magnitude with no change to the data.
- **The Lindley paradox.** With a large enough sample, a frequentist p-value can be very small (reject H₀ at α = 0.05) while the Bayes factor strongly favors H₀ (BF >> 1). The disagreement is not bug or arithmetic error — it is the consequence of fixing α as n grows, which p-values do but BFs don't. See [Wikipedia summary](https://en.wikipedia.org/wiki/Lindley%27s_paradox) and Spanos (2013).
- **Whether marginal likelihoods (and therefore Bayes factors) are even the right object.** Gelman, Vehtari and collaborators argue for predictive checks (LOO, WAIC, posterior predictive distributions) over Bayes factors for most practical Bayesian model comparison. The Bayes factor answers "given that exactly one of these models generated the data, what odds should I update to?" — almost never the question a working modeler is actually asking. Vehtari et al. (2017) is the now-standard alternative.

### What has changed recently (last 5 years)

- **PSIS-LOO has eaten the practical-Bayesian model-comparison market.** The `loo` R package and Stan integration make leave-one-out cross-validation computationally cheap. Most contemporary applied Bayesian papers report `elpd_loo` differences rather than Bayes factors. This is the single biggest thing missing from TIKTOK's Ch 6 brief.
- **Power-scaling sensitivity diagnostics** (Kallioinen, Paananen, Bürkner, Vehtari, *Stat. Comput.* 2024; [arXiv 2107.14054](https://arxiv.org/pdf/2107.14054)) — automated diagnostics that quantify how much the posterior moves when the prior is scaled. Becoming default in the Stan/`brms` workflow.
- **Bridge sampling and nested sampling** have made Bayes factor computation tractable in moderate-dimensional problems — the `bridgesampling` R package (Gronau et al., 2020) is now the standard. Bayes factors are no longer infeasible to compute; they are just often the wrong tool.
- **The 2026 FDA draft guidance** on Bayesian methods in drug trials (Federal Register, Jan 12 2026) explicitly requires sensitivity analyses for any Bayesian submission. ([JAMA viewpoint](https://jamanetwork.com/journals/jama/fullarticle/2847012); [Big Molecule Watch summary](https://www.bigmoleculewatch.com/2026/02/04/fda-issues-guidance-on-modernizing-statistical-methods-for-clinical-trials/).) Reinforces the chapter's point that Bayes factor sensitivity is a feature, not a bug, if you also report the sensitivity.

---

## 3. Application Domain Examples

The chapter scenario is an epidemiologist deciding between a linear-trend and exponential-growth model for early disease-spread data. Real material the chapter can draw on:

- **Roosa et al. 2020** — exponential vs. logistic on Chinese provincial COVID data, early 2020. The exponential won early and lost late as containment kicked in. Good teaching point: "model comparison gives you the right model *for the regime you're in*."
- **Pell, Kuang, Viboud, Chowell 2018, *Epidemics*** — generalized growth models on Ebola, Zika, foot-and-mouth. AIC weights, not raw AIC differences, are the field-standard reporting unit. [verify exact citation details before printing.]
- **Smith et al. (2002) ICES Journal,** fisheries stock assessment — Burnham & Anderson's own go-to multimodel inference case. The "ΔAIC < 4" rule the chapter cites traces directly to their guidance ("models with Δ ≤ 2 have substantial support; 4–7, considerably less; > 10, essentially none").
- **Lindley paradox concrete numbers.** A textbook construction: n = 100,000 coin flips, observed proportion 0.50098. p-value against H₀: p = 0.5 is ≈ 0.05 (just significant). Bayes factor under a Uniform(0,1) prior on p under H₁ favors H₀ by ≈ 10:1. Lays the paradox bare in two lines.

---

## 4. The Book's Thesis Connection

The book's thesis is that frequentist and Bayesian methods answer different questions and the reader should choose which question they want answered. Model comparison is the cleanest place that distinction lands.

- **AIC answers:** "Of these candidate models, which would have the lowest expected out-of-sample deviance?"
- **Bayes factor answers:** "Given the data, by what factor should I update the relative odds of these two models?"
- **PSIS-LOO answers (Bayesian):** "Which model would predict best on data I haven't seen yet, integrating over my parameter uncertainty?"

These are not the same question, and the side-by-side chapter format clarifies that *the choice of method is the choice of question*. The book's recurring move — "both methods are correct, they're answering different things" — is on full display.

This is also the chapter where the asymmetry rule (Ch 5 onward, Bayesian gets more space) earns its rent. AIC is a one-liner. Bayes factors require explaining marginal likelihoods, priors on parameters, and what happens when the prior gets wider. The space is honest, not advocacy.

---

## 5. Intellectual Lineage Notes

- **Akaike 1973/1974** — AIC originates in time-series identification, not classical inference. The Kullback-Leibler distance framing came later (Akaike 1981). Worth telling: AIC was invented to choose autoregressive orders, not to settle hypothesis tests.
- **Schwarz 1978** — BIC's "Bayesian" label comes from its derivation as a Laplace approximation to the log marginal likelihood under a unit-information prior. Schwarz himself was careful that the prior assumption is what makes it Bayesian.
- **Jeffreys, *Theory of Probability* (1939, revised 1961)** — Bayes factors are not Jeffreys's invention but his systematization. The evidence-strength table (Appendix B of the 1961 edition) is the cultural artifact; the actual numerical thresholds are post-hoc.
- **Kass & Raftery 1995** — the synthesis paper that made Bayes factors usable in applied work. Crucial because it openly discusses prior sensitivity and the use of BIC as an approximation when integration is hard.
- **Vehtari, Gelman & Gabry 2017** — the present consensus position in the Stan/Gelman wing of applied Bayes. PSIS-LOO as the default; Bayes factors reserved for problems where the marginal likelihood is the actual quantity of interest (e.g., Bayesian model averaging weighting, formal hypothesis testing in fields that demand it).
- **Burnham & Anderson** — defenders of information-theoretic model comparison against both naïve hypothesis testing and Bayes factor enthusiasm. Their key move: "all models are wrong; the question is which approximates best for the use you have in mind."

---

## 6. Pedagogical Delivery Research

Student-facing difficulties documented in the stats-education literature:

- **Confusing evidence strength with effect size.** A Bayes factor of 8 does not mean the exponential model fits "eight times better" — it means the data are eight times more likely under M₁ than under M₀ marginalized over the priors. Worked example with two near-overlapping fits gets this across better than any verbal definition.
- **The Bayes factor as odds-update intuition.** Posterior odds = BF × prior odds. Students who already know Bayes' theorem can be taught BF as "the multiplicative factor by which evidence updates your odds." This is the chapter's strongest analogical move.
- **The Jeffreys thresholds are heuristics, not laws.** A 2.9 vs. 3.1 BF should not be reported as "anecdotal" vs. "moderate." Encourage students to report the BF itself, plus a sensitivity analysis, not the verbal category alone. The interactive Shiny app of [van Erp, Mulder & Oberski (2020, *Frontiers in Psychology*)](https://www.frontiersin.org/journals/psychology/articles/10.3389/fpsyg.2020.608045/full) is a usable classroom artifact.
- **Why the close-call case is the interesting one.** When ΔAIC > 10 or BF > 100, both methods agree and the comparison is uninteresting. The teaching value of the chapter lies entirely in the ΔAIC ≈ 2, BF ≈ 5 zone where good decisions require thought, not formula.
- **AIC weights as the missing reporting unit.** Many students stop at "ΔAIC = 4.2, exponential wins." Akaike weights — w_i = exp(−Δ_i/2) / Σ exp(−Δ_j/2) — convert AIC differences into a probability-like quantity over the model set. The notation invites direct comparison with posterior model probabilities, which is exactly the pedagogical move the chapter needs.

LLM-specific pedagogy: the chapter's prompting section should ask the student to compute AIC, BIC, BF, and (the recommended addition) elpd_loo on the same dataset with one prompt. The LLM exposes the working code; the student inspects it to verify the BF uses the priors they intended.

---

## 7. Representation and Display Research

The chapter's side-by-side comparison table from TIKTOK.md:

| | Frequentist | Bayesian |
|---|---|---|
| Output | ΔAIC = 4.2, exponential preferred | BF = 8.3, moderate evidence for exponential |
| Communicable? | "Fits better" | "8× more likely given the data" |
| Model averaging | Not standard | Natural — weight by posterior probability |
| Prior required? | No | Yes — on model parameters |

**Recommended additional row:**

| | Frequentist | Bayesian |
|---|---|---|
| Sensitivity to assumptions | Sensitivity to model form; little prior to vary | Sensitivity to parameter priors — sometimes by orders of magnitude. Reportable as a sensitivity analysis. |

Rationale: the chapter brief is honest that Bayesian requires priors, but does not yet name *prior sensitivity of BF specifically* — which is precisely the thing Ch 7 then unpacks. Adding this row makes the Ch 6 → Ch 7 bridge visible inside the comparison table.

**Recommended second additional row (optional):**

| | Frequentist | Bayesian |
|---|---|---|
| Modern alternative | Cross-validation (k-fold, LOO-CV) | PSIS-LOO (Vehtari et al. 2017) |

This signals to the student that the AIC-vs-BF face-off is partly a historical staging, and that working analysts today often use cross-validation flavors that don't pick a side.

**Visual:** the canonical chart for model comparison is two fitted curves over the data with their AIC and BF in the legend. Recommend an additional panel: the same comparison run with three different priors on the exponential rate parameter, showing how the BF shifts while the AIC stays put. That single side-by-side does more pedagogical work than three paragraphs of explanation.

---

## 8. Open Questions and Research Gaps

- **TIKTOK.md does not mention PSIS-LOO.** This is the single most important addition to flag for Nik. Most working Bayesians have moved on from Bayes factors for model comparison; teaching BF as the canonical Bayesian answer is teaching a slightly dated frame. Recommendation: keep BF as the chapter's pedagogical centerpiece (it is what the side-by-side with AIC was built for) but add a closing subsection — "What working Bayesians actually do now" — that names elpd_loo and points the reader at the `loo` package.
- **The Lindley paradox deserves more than the one sentence TIKTOK seems to plan.** It is the cleanest demonstration in the book of "frequentist and Bayesian answer different questions" and would justify a half-page worked example with explicit numbers.
- **Marginal-likelihood computation is hard.** The chapter's BF = 8.3 example glosses how that number is computed in practice. Bridge sampling, harmonic mean (avoid!), Laplace approximation, nested sampling. A one-paragraph "and here's why this is hard to compute" honesty footnote is worth the space.
- **The "model averaging" row in the table is true but glib.** Bayesian model averaging weights models by posterior probability, which inherits all the prior sensitivity issues. Pseudo-BMA and stacking (Yao et al. 2018) are the modern alternatives, also based on LOO. Worth a paragraph.
- **Domain gap to flag for Nik:** if Nik does not have epidemiological-modeling experience, the COVID-era literature on growth curves is rich enough that the chapter can lean on published examples. Roosa et al. 2020 is a good anchor.

---

## 9. Sourcing Notes

Tier-1 (primary, well-anchored, verified URLs):
- Kass & Raftery 1995 — multiple PDF mirrors, JASA published.
- Vehtari, Gelman & Gabry 2017 — *Statistics and Computing*, arXiv preprint, Stan tooling all confirm.
- Burnham & Anderson 2004 *SMR* — open PDF available.
- FDA medical-device Bayesian guidance 2010 — official FDA page.

Tier-2 (foundational, cited everywhere, but where I rely on secondary descriptions of the original):
- Akaike 1973, 1974 — citation details from Wikipedia and survey papers (Cavanaugh & Neath 2019). Did not personally verify the 1973 conference-proceedings pagination.
- Schwarz 1978 — *Annals of Statistics* citation verified via secondary references; did not access the original four-page paper directly.
- Jeffreys *Theory of Probability* 1961 — referenced through Kass & Raftery's discussion and the [Statlect Jeffreys-scale page](https://www.statlect.com/fundamentals-of-statistics/Jeffreys-scale).

Tier-3 ([verify] before printing):
- Pell, Kuang, Viboud, Chowell 2018 — citation should be checked.
- The specific Roosa et al. 2020 numbers (AIC values, sample sizes) need verification from the paper itself before being quoted in the chapter.
- The "ΔAIC = 4.2, BF = 8.3" numbers in TIKTOK.md are illustrative — they should be reproduced from a real dataset (or named as constructed) in the final chapter, not implied to be from a specific study.

Notes on the 2026 FDA Bayesian draft guidance: cited via Federal Register notice (Jan 12 2026) and secondary coverage in JAMA and Big Molecule Watch. The full draft text is available at the federal register link. If the chapter cites it, cite the federal register entry directly.

**Voice-anchoring:** the root `style/` and per-book `style/` folders were not inspected for this research file. The draft chapter that uses this research should flag `voice-unanchored` if those folders are still empty when drafting begins.
