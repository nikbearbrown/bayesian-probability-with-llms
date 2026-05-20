# Research: Chapter 05 — Regression, Both Ways
## Bayesian Probability with LLMs

**Chapter one-line:** Linear regression as a frequentist workhorse and as a Bayesian model — the solutions converge on the line, but diverge on everything else that matters for decision-making.

**Research date:** 2026-05-13

---

## 1. Primary Sources

### Foundational papers and texts

- **Adrien-Marie Legendre, 1805.** *Nouvelles méthodes pour la détermination des orbites des comètes*. First published exposition of the method of least squares. Historical overview at [Wikipedia "Least squares"](https://en.wikipedia.org/wiki/Least_squares) and the more careful [Plackett 1972 review (PDF)](https://hedibert.org/wp-content/uploads/2016/08/plackett1972-thediscoveryofthemethodofleastsquares.pdf). The chapter does not need to spend much time here, but the historical detail — least squares started as an astronomy and surveying technique for combining noisy measurements — is worth one sentence because it locates the method as practical first, theoretical second.

- **Carl Friedrich Gauss, 1809.** *Theoria motus corporum coelestium*. Connected least squares to the normal distribution and to a probability-of-error framework. Gauss claimed priority over Legendre, dating his use of the method to 1795. The priority dispute is famous (see [Stigler 1981, "Gauss and the Invention of Least Squares"](https://projecteuclid.org/journals/annals-of-statistics/volume-9/issue-3/Gauss-and-the-Invention-of-Least-Squares/10.1214/aos/1176345451.full)). For the chapter: Gauss's contribution is what made OLS *probabilistically* interpretable, which is what makes Bayesian regression possible at all.

- **Francis Galton, 1886.** "Regression Towards Mediocrity in Hereditary Stature." *Journal of the Anthropological Institute* 15: 246–263. UCLA hosts the [original (PDF)](http://www.stat.ucla.edu/~nchristo/statistics100C/history_regression.pdf). The word "regression" enters the statistical vocabulary here. Galton's observation — children of tall parents tend to be tall but less tall than their parents; children of short parents tend to be short but less short — is regression to the mean. The chapter should name that the modern "regression" of regression analysis carries the residue of Galton's specific finding, even though the technique applies far beyond inherited stature.

- **D. V. Lindley and A. F. M. Smith, 1972.** "Bayes Estimates for the Linear Model." *Journal of the Royal Statistical Society Series B* 34(1): 1–41. [JSTOR / Wiley](https://rss.onlinelibrary.wiley.com/doi/abs/10.1111/j.2517-6161.1972.tb00885.x). PDF at [Imperial College](https://www.ma.imperial.ac.uk/~das01/MyWeb/SCBI/Papers/LindleySmith.pdf). The paper that put Bayesian linear regression on its modern footing. Lindley & Smith derive the Bayes estimate as a closed-form expression under conjugate normal priors and show how the hierarchical structure (priors on the regression coefficients, hyperpriors on the prior parameters) emerges naturally from the principle of exchangeability. This is the source citation for the chapter's central technical claim: under flat priors, the Bayes posterior mean coincides with the OLS estimate.

- **Andrew Gelman, Jennifer Hill, Aki Vehtari, 2020.** *Regression and Other Stories*. Cambridge University Press. Companion site with code and examples at [avehtari.github.io/ROS-Examples/](https://avehtari.github.io/ROS-Examples/). Free PDF available at [users.aalto.fi/~ave/ROS.pdf](https://users.aalto.fi/~ave/ROS.pdf). Frontmatter: [Cambridge](https://assets.cambridge.org/97811070/23987/frontmatter/9781107023987_frontmatter.pdf). The modern reference for thinking about regression Bayesianly without ritualizing it. The book's central pedagogical move — fake-data simulation, careful plotting, treating regression as a tool for description before prediction — should set the tone for the chapter.

- **Andrew Gelman, Aki Vehtari, Daniel Simpson, Charles Margossian, Bob Carpenter, Yuling Yao, Lauren Kennedy, Jonah Gabry, Paul-Christian Bürkner, Martin Modrák, 2020.** "Bayesian Workflow." arXiv:2011.01808. [arxiv.org/abs/2011.01808](https://arxiv.org/abs/2011.01808). The current authoritative statement on how to actually do Bayesian inference. Prior predictive checks, posterior predictive checks, model comparison, validation. The chapter needs to introduce posterior predictive checks (PPC); this paper is the source.

- **Jonah Gabry, Daniel Simpson, Aki Vehtari, Michael Betancourt, Andrew Gelman, 2019.** "Visualization in Bayesian Workflow." *Journal of the Royal Statistical Society Series A* 182(2): 389–402. [Oxford Academic](https://academic.oup.com/jrsssa/article/182/2/389/7070184). arXiv: [1709.01449](https://arxiv.org/abs/1709.01449). The paper that gives the chapter its visual vocabulary. Posterior predictive distributions overlaid on observed data; trace plots; intervals on parameter posteriors. The `bayesplot` R package operationalizes this.

- **Francis J. Anscombe, 1973.** "Graphs in Statistical Analysis." *The American Statistician* 27(1): 17–21. The Anscombe quartet — four datasets with identical means, variances, correlations, and OLS regression lines but profoundly different scatterplots. Wikipedia summary: [Anscombe's quartet](https://en.wikipedia.org/wiki/Anscombe's_quartet). This is the most teachable piece of statistical pedagogy ever written. The chapter must use it. The quartet shows in two minutes what would take pages to argue: OLS coefficients are not the data; diagnostics matter; misspecification kills regression.

- **Richard McElreath, 2020.** *Statistical Rethinking: A Bayesian Course with Examples in R and Stan* (2nd edition). CRC Press. [Routledge page](https://www.routledge.com/Statistical-Rethinking-A-Bayesian-Course-with-Examples-in-R-and-STAN/McElreath/p/book/9780367139919). Won the 2024 De Groot Prize. The second edition emphasizes prior predictive simulation — running the prior forward to generate fake data and checking whether the fake data look reasonable. This is the right pedagogical move for an undergraduate chapter introducing Bayesian regression.

- **Cameron Davidson-Pilon, 2016.** *Bayesian Methods for Hackers*. Addison-Wesley. Open-source repository at [github.com/CamDavidsonPilon](https://github.com/CamDavidsonPilon/Probabilistic-Programming-and-Bayesian-Methods-for-Hackers). Computation-first, math-second pedagogy. Useful as a model for the prompting section: how to get an LLM to implement a Bayesian regression and how to verify the implementation.

### Key empirical cases / datasets

- **Marketing mix modeling (MMM).** The Google research paper [Jin, Wang, Sun, Chan, Koehler (2017) "Bayesian Methods for Media Mix Modeling with Carryover and Shape Effects"](https://research.google/pubs/bayesian-methods-for-media-mix-modeling-with-carryover-and-shape-effects/) is the canonical industry reference. Bayesian MMM is now a serious technology at Google, Meta, and most large consumer-goods companies. The chapter's retail/advertising scenario is not hypothetical; it is the modal Bayesian regression application in commerce.

- **PyMC Labs marketing mix modeling guide.** [pymc-labs.com](https://www.pymc-labs.com/blog-posts/marketing-mix-modeling-a-complete-guide). Useful for the prompting section — names adstock, saturation, and the carryover effect.

- **Retail/advertising public datasets.** Kaggle hosts several. The classic one is the "Advertising" dataset from James, Witten, Hastie, Tibshirani *Introduction to Statistical Learning* — 200 markets, three media (TV, radio, newspaper), one outcome (sales). Used in hundreds of tutorials. Small enough for a hand-fittable regression, large enough that OLS and Bayes agree on the point estimate.

---

## 2. The Core Concept — State of the Field

### What is settled

- **Under flat (uniform) priors and a normal likelihood, the Bayesian MAP estimate of the regression coefficients equals the OLS estimate.** This is a theorem, not an opinion. See [Wikipedia "Maximum a posteriori estimation"](https://en.wikipedia.org/wiki/Maximum_a_posteriori_estimation) and [Wikipedia "Bayesian linear regression"](https://en.wikipedia.org/wiki/Bayesian_linear_regression). For large samples or weakly informative priors, the posterior mean is also approximately equal to OLS. This is the chapter's central pedagogical anchor: the two approaches *agree on the line*. They disagree on what the line means, what uncertainty surrounds it, and what predictions can be made from it.

- **OLS makes assumptions.** Linear conditional expectation, homoscedastic errors, independent observations, no perfect multicollinearity. Anscombe's quartet shows what happens when any of these break — the OLS fit is unchanged but the data say something completely different. Modern frequentist practice handles this with residual diagnostics, robust standard errors, generalized least squares, or transformation. The diagnostics are well-developed.

- **Bayesian regression handles uncertainty in coefficients differently.** OLS produces a point estimate plus a standard error; Bayesian regression produces a full posterior distribution. For decision-theoretic uses — what is P(slope > 2)? what is P(forecast > threshold)? — the posterior is directly usable in a way the SE is not.

### What is disputed

- **Whether flat priors are "objective."** The convention of using flat priors when no information is available has a long defender lineage (Jeffreys, Bernardo's reference priors) and a long critic lineage (it depends on the parameterization; uniform on σ is different from uniform on log σ; there is no information-free prior). For an undergraduate chapter, the working answer is: flat priors recover OLS, weakly informative priors are usually better, sensitivity analysis is the discipline.

- **How much do priors matter in regression?** With large n and well-identified parameters, almost not at all — the likelihood dominates. With small n, multicollinear predictors, or weak signal, priors do real work. The chapter's retail/advertising example with n = 60 weeks is in the middle zone: priors will affect the tails of the slope posterior, but not the point estimate much.

- **Posterior predictive distribution vs. frequentist prediction interval.** Both produce intervals around future observations. Mathematically they are similar in the large-sample limit. Conceptually they differ: the posterior predictive distribution is a *probability* statement ("there is a 90% probability the next observation falls in this interval, given the data"); the prediction interval is a *coverage* statement ("if we repeated the experiment many times, 90% of constructed intervals would contain the next observation"). The chapter must teach this distinction without making it precious.

- **MCMC vs. variational vs. closed-form Bayesian inference.** For conjugate normal regression, closed-form posteriors exist (Lindley & Smith showed this in 1972). For more complex models, MCMC (Stan, PyMC) or variational methods (ADVI) are required. The chapter should use the closed-form result for the worked example and gesture toward MCMC for the prompting section.

### What has changed recently (last 5 years)

- **Bayesian workflow has been codified.** Gelman et al.'s 2020 arXiv paper, the 2019 Gabry et al. visualization paper, and the 2024 *Bayesian Workflow* book (Routledge) have produced a shared practice: prior predictive check → fit → posterior predictive check → model comparison via cross-validation (LOO-CV) or stacking. This is now graduate-textbook standard. The chapter does not need to teach the full workflow but should at minimum introduce posterior predictive checks.

- **Compute is no longer the barrier.** Stan, PyMC, brms, NumPyro make Bayesian regression accessible to undergraduates. An LLM can write a Stan model in seconds. The pedagogical question is no longer "can the student fit a Bayesian model" but "does the student understand what they fit."

- **LLMs as implementation partners.** A genuine shift. The prompting section in this chapter is not decoration — it is the chapter's leverage point. An undergraduate can produce a serious Bayesian regression analysis in an afternoon using Claude or ChatGPT to write the Stan/PyMC code, *if* they know how to specify the problem and verify the output. The book's thesis depends on this being true.

- **Marketing mix modeling has matured.** What was esoteric ten years ago is now standard practice at large advertisers, often with Bayesian implementations. The retail scenario in the chapter is genuinely a domain where Bayesian regression earns its keep over OLS.

---

## 3. Application Domain Examples

The chapter's scenario: a retail analyst with 60 weeks of sales and advertising spend, deciding whether to increase the budget. This is real.

- **Marketing mix modeling (MMM).** The Google paper cited above formalizes adstock (advertising's effect carries over for several weeks) and saturation (diminishing returns at high spend). For an undergraduate chapter, the chapter can present a simpler model — linear in current-week spend — and flag adstock/saturation as the extensions a working analyst would actually use.

- **The Anscombe quartet teaching gold.** The chapter's "common misconceptions" section must include the quartet. Same OLS regression line, four wildly different data structures. The pedagogical lesson: *fit a line, then plot the residuals*. A student who finishes Ch 5 without internalizing this has missed the chapter. The Bayesian version of the same lesson is the posterior predictive check: simulate from the fitted model, plot alongside observed data, see whether they look similar.

- **Public datasets for the chapter's worked example.** The ISLR "Advertising" dataset (TV, radio, newspaper → sales, n=200) is probably the cleanest. Alternative: the Kaggle "Sales and Advertising" datasets, or BLS retail sales × an advertising index. The companion website specification (TIKTOK.md) implies the book will use BLS/O*NET data for most chapters; a retail-sales BLS series cross-walked with advertising-spend data would be ideal. Worth flagging for the author.

- **Domain-specific failure modes the chapter should name:**
  - *Reverse causality.* If sales drive advertising budgets (high-revenue quarters fund higher ad spend the next quarter), the regression cannot identify the causal effect of ad spend on sales. Pearl's framework on causal vs. associational claims belongs here in a footnote or sidebar.
  - *Confounding.* Seasonality, holidays, competitor activity, weather. The 60-week sample is short enough that a single seasonal pattern can drive a "significant" effect.
  - *Multicollinearity.* If multiple ad channels run in the same weeks, their effects are not separately identifiable. The Bayesian approach is not magic against this; the posteriors on the affected coefficients just get wider.

- **The Bayesian advantage for the decision question.** "Should the company increase advertising spend?" requires a probability of payoff. The Bayesian posterior on the slope, combined with a cost-benefit model, gives P(ROI > 0). OLS gives a point estimate of the slope and a CI. The reader can compute roughly the same number from OLS by hand (point estimate ± 1.96·SE), but the operation is "frequentist with extra steps" — and it presumes the assumptions are met.

---

## 4. The Book's Thesis Connection

Chapter 5 is the Act Two opener — and per TIKTOK.md lines 42–45, this is where the *asymmetry rule* is named explicitly for the first time. The Bayesian solution starts getting longer than the frequentist solution because the Bayesian solution does more.

The chapter's central technical move — show that under flat priors, OLS and Bayesian MAP regression give identical point estimates — is the book's most important pedagogical claim about Bayesian methods. It says: Bayesian regression is not "different math." It is the same math, with explicit priors and full posterior distributions added. Once a student sees this, the question "frequentist or Bayesian?" stops being a tribal identification and becomes a question about what the analysis needs.

The chapter is also where the book's "decisions under uncertainty" thread starts to dominate. A point estimate of slope = 2.3 with SE = 0.4 is enough information to *test* a hypothesis. It is not enough information to *decide* whether to spend an extra $50,000 on advertising next quarter. For the decision, you need the distribution. The chapter should land this.

The connection to the Irreducibly Human series is indirect for this chapter but available: if a regression model is being used to predict labor-market outcomes from O*NET features, the same questions arise — is the slope different from zero (frequentist), or what is the distribution of plausible slopes given the data (Bayesian). Chapter 11 will revisit this in classification framing.

---

## 5. Intellectual Lineage Notes

**Galton (1886).** Coined "regression." The original phenomenon — tall parents have shorter-than-parents children — is *regression to the mean*, which is itself a frequent source of confusion in regression analysis. Naming this connection in a sentence in the chapter buys the student a permanent vaccination against the most common interpretive error in pre-post regression studies.

**Legendre / Gauss (1805 / 1809).** The least-squares method as a probability-of-error framework arrives with Gauss, not Legendre. The chapter does not need to wade into the priority dispute, but the conceptual leap — from "minimize sum of squared deviations" (mechanical) to "find the line that maximizes the likelihood under Gaussian errors" (probabilistic) — is the leap that makes Bayesian regression possible. The chapter should at least gesture at this.

**Lindley & Smith (1972).** The paper that established Bayesian linear regression in its modern hierarchical form. The chapter should cite it for two specific facts: (1) under conjugate normal priors, the Bayes posterior is closed-form; (2) the hierarchical structure (prior on coefficients, hyperprior on prior parameters) is not an ad hoc add-on but a natural consequence of exchangeability. This sets up Chapter 9 (Hierarchical Problems) and means the chapter is not orphaning a future concept.

**Gelman, Hill, Vehtari (2020).** The modern textbook. The chapter should pattern itself on *Regression and Other Stories*' approach — fake-data simulation, careful plotting, treating regression as description before prediction. This is also the place to cite for posterior predictive checks if the chapter wants a textbook reference rather than the arXiv workflow paper.

**Anscombe (1973).** Not Bayesian. Frequentist. Universally taught. The quartet is the most efficient pedagogy in regression. Use it.

---

## 6. Pedagogical Delivery Research

Common undergraduate misconceptions about regression, in rough order of frequency:

1. **"R² tells you whether the model is good."** No. R² tells you what fraction of variance is explained. A high R² with bad residual structure is a worse model than a low R² with clean residuals. The Anscombe quartet kills this misconception in one figure.

2. **"A significant coefficient means the predictor matters."** Significance is sensitive to sample size; meaningful effect size is what matters. With n = 60, the chapter's slope estimate of 2.3 with SE = 0.4 produces a t-statistic of 5.75 — overwhelmingly significant. But "is 2.3 a lot or a little?" requires domain knowledge, not a t-test.

3. **"The slope is the causal effect."** Not unless the design supports it. Observational regression identifies association, not causation. The retail/advertising scenario in the chapter is observational; reverse causality and confounding are live concerns. The chapter must at minimum flag this — Pearl's framework or Gelman's "the comparison the regression actually answers" framing both work.

4. **"The 95% CI means there's a 95% chance the slope is in there."** Same misconception as the t-test chapter, applied to regression. The Bayesian credible interval does mean this; the frequentist CI does not. The chapter is the right place to re-teach the distinction in a regression context.

5. **"OLS is unbiased so it's the best estimator."** Unbiased ≠ minimum-error. In small samples or with collinear predictors, OLS has high variance. Bayesian shrinkage (Chapter 8 will come back to this) or regularization (ridge, lasso) trade bias for variance and often produce better predictions.

The pedagogical model from Gelman/Hill/Vehtari (*Regression and Other Stories*) is to *simulate*. Generate fake data with known parameters; fit the model; check that the model recovers the parameters. This is the practice the chapter should teach. An LLM can generate the simulation code in seconds; the student's job is to read it critically.

McElreath's *Statistical Rethinking* uses *prior predictive simulation* — sample from the prior, propagate through the model, look at what the prior actually implies before seeing any data. For the chapter's retail example: if the prior on the slope is Normal(0, 100), the prior implies that a $1 increase in ad spend could swing sales by hundreds of dollars in either direction. Is that plausible? Usually no. Tightening to Normal(0, 5) is more honest. This move is pedagogically powerful and belongs in the chapter.

---

## 7. Representation and Display Research

The TIKTOK.md side-by-side table for Ch 5:

| | Frequentist | Bayesian |
|---|---|---|
| Slope estimate | 2.3 (SE = 0.4) | Posterior: mean 2.3, 95% CrI [1.5, 3.1] |
| Prediction | Interval [X, Y] | Full predictive distribution |
| P(ROI > 0)? | Not available | Directly computable |
| Computation | Closed form | MCMC or approximation |

The added row I would recommend:

| | Frequentist | Bayesian |
|---|---|---|
| **Diagnostic for model fit** | Residual plot, Q-Q plot, R² | Posterior predictive check (simulate, overlay, compare) |

This row matters because the chapter's central pedagogical move — Anscombe-quartet-style — is that *fit diagnostics are not optional*. The frequentist toolkit has well-developed diagnostics (residual plots, leverage, influence). The Bayesian toolkit has its own (posterior predictive checks, energy diagnostics, R-hat). The chapter should name them in parallel.

The full table I'd propose:

| | Frequentist | Bayesian |
|---|---|---|
| Slope estimate | 2.3 (SE = 0.4) | Posterior: mean 2.3, 95% CrI [1.5, 3.1] |
| Prediction | Interval [X, Y] | Full predictive distribution |
| P(ROI > 0)? | Not available | Directly computable |
| Diagnostic for model fit | Residual plot, Q-Q plot, R² | Posterior predictive check |
| Computation | Closed form | MCMC or approximation (closed form for conjugate normal) |
| When the answers agree | Large n, no informative prior | Flat priors, large n |

The last row is a load-bearing teaching move: *the two approaches give the same answer for most regression problems most practitioners will face*. The Bayesian approach earns its complexity in the cases the row names — small n, decision-theoretic questions, hierarchical structure (Ch 9), sequential updating (Ch 10). For a working analyst on a stable, large dataset, OLS is fine. The book's thesis depends on the reader believing this.

The Anscombe quartet figure is the chapter's single most important visual. Four scatterplots, identical OLS lines, profoundly different data. The chapter should reproduce it (it's public domain; the data are tiny).

---

## 8. Open Questions and Research Gaps

- **What's the right prior for the chapter's slope parameter?** The chapter says "weakly informative normal on slope and intercept, half-normal on σ." But the units matter. If sales are in thousands of dollars and ad spend is in thousands of dollars, a slope prior of Normal(0, 5) means "we think $1 of ad spend produces somewhere between -$10 and +$10 of sales with 95% probability." That is genuinely weak. If sales are in dollars and ad spend in thousands, the same prior implies hundreds-of-dollars-per-thousand-dollars effects, which is much stronger. The chapter should walk through the units check explicitly. Prior predictive simulation makes this concrete.

- **Should the chapter introduce posterior predictive checks (PPC) here or wait?** PPC is a chapter-9 concept in most Bayesian textbooks. But the *idea* of PPC — fit your model, simulate from it, see if the simulated data look like real data — is so pedagogically powerful that introducing it in Ch 5 might pay off. Anscombe is the frequentist parallel; PPC is the Bayesian parallel. The chapter could do both side by side.

- **Causal vs. associational regression.** The chapter's scenario is observational. The slope estimate of 2.3 is the association between ad spend and sales; it is not the causal effect of ad spend on sales unless additional assumptions hold (no confounding, no reverse causality, correct functional form). Pearl's causal framework lives in chapter 0 or in a separate book per TIKTOK.md, but the chapter should at minimum flag the distinction. Otherwise it teaches a confusion that will haunt the reader through every regression they ever read.

- **What does "weakly informative" mean precisely?** The Stan / brms community uses the term in a specific way — wide enough to not affect the posterior much, narrow enough to exclude implausible values. There is no formal definition. The chapter should give the working definition and acknowledge it is a craft skill, not a formula.

- **How to handle the LLM-implementation prompting section?** The standard Stan or PyMC code for Bayesian regression is short. An LLM can write it correctly on the first try in most cases. The harder skill the chapter must teach is *verifying* the output — checking that the prior makes sense, that the posterior looks sensible, that the predictive distribution covers the observed data. The prompting section should pattern-match: "ask the LLM to generate, then ask the LLM to diagnose, then verify a piece by hand."

- **The Type S / Type M issue (carried from Ch 4) applies to regression too.** If the slope is near zero and the sample is small, the published slope estimate is biased upward in magnitude conditional on significance. The chapter could plant this idea (a sentence) and let Ch 8 develop it.

- **What about non-linear effects?** Saturation and adstock in MMM are non-linear. The chapter introduces linear regression; non-linear regression and GAMs are not in the book's scope. The chapter should name the limit honestly: "linear regression is a strong model when the relationship really is linear; otherwise it is at best a useful local approximation."

---

## 9. Sourcing Notes

All sources verified to exist via web search 2026-05-13. Confirmations:

- Legendre 1805, *Nouvelles méthodes pour la détermination des orbites des comètes* — confirmed historical.
- Gauss 1809, *Theoria motus* — confirmed historical.
- Galton 1886, *Journal of the Anthropological Institute* 15: 246–263 — confirmed.
- Lindley & Smith 1972, *JRSS Series B* 34(1): 1–41 — confirmed via Wiley and Imperial PDF.
- Gelman, Hill, Vehtari 2020, *Regression and Other Stories*, Cambridge — confirmed; free PDF available.
- Gelman et al. 2020, "Bayesian Workflow," arXiv:2011.01808 — confirmed.
- Gabry et al. 2019, *JRSS Series A* 182(2): 389–402 — confirmed.
- Anscombe 1973, *The American Statistician* 27(1): 17–21 — confirmed.
- McElreath 2020, *Statistical Rethinking* 2nd ed — confirmed; won 2024 De Groot Prize.
- Davidson-Pilon 2016, *Bayesian Methods for Hackers* — confirmed; open-source.
- Jin, Wang, Sun, Chan, Koehler (Google), 2017, "Bayesian Methods for Media Mix Modeling" — confirmed via Google Research publications page.

`[verify]` flags:

- The Gauss 1795 priority claim is contested; Stigler's careful 1981 review is the authoritative source. The chapter can punt this entirely or relegate to a one-sentence footnote.
- The specific Anscombe quartet summary statistics (mean x = 9, mean y = 7.5, variance, correlation = 0.816, line y = 3 + 0.5x) — verified by Wikipedia; should be cross-checked against Anscombe's original paper before the draft cites them as exact values.
- The "60 weeks of sales / advertising" scenario is a stand-in; the chapter will need a specific dataset from the companion website. The ISLR Advertising dataset (200 observations) is a strong default; a BLS retail-sales × ad-spend cross-walk would tie the chapter to the rest of the book's data infrastructure.
- The slope estimate 2.3 (SE = 0.4) and 95% CrI [1.5, 3.1] in the side-by-side table are illustrative numbers. Real numbers will come from whatever dataset the companion site provides.

**Sources not yet exhausted:**
- Wasserman's *All of Statistics* on the OLS/Bayes equivalence — would tighten the central technical claim with a more rigorous statement.
- Hoff's *A First Course in Bayesian Statistical Methods* on conjugate normal-normal regression — closed-form derivations.
- Kruschke's *Doing Bayesian Data Analysis* — accessible undergraduate-level treatment of Bayesian regression with BUGS / JAGS examples.

**Strongest sources for this chapter:** Lindley & Smith 1972 (the foundational result), Gelman/Hill/Vehtari 2020 (the modern textbook), Anscombe 1973 (the pedagogical anvil), Gabry et al. 2019 (posterior predictive checks).

**Thinnest section:** The "Why anyone uses frequentist methods" justification — the chapter has the bullet points but needs a working example where OLS is genuinely the right call, not just a stopgap. A pre-registered confirmatory regulatory study or a high-n descriptive comparison would do it.

**Chapter 4 → Chapter 5 connection:** The replication-crisis concerns introduced in Ch 4 apply directly to regression in observational settings. A "significant slope" in a single observational study is subject to the same Ioannidis / Gelman-Carlin failure modes as a "significant t-test." The Bayesian regression's posterior predictive check is the analog of the Bayesian two-group posterior — it gives the analyst something to predict against. Ch 5 should explicitly carry the Ch 4 critique forward to non-experimental data.

---
