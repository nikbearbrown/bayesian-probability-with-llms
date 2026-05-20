# Research: Chapter 10 — Time and Sequence
## Bayesian Probability with LLMs

**Chapter one-line:** Time series analysis and sequential updating — where the Bayesian approach is most intuitive, because the posterior from today is the prior for tomorrow.
**Research date:** 2026-05-13

---

## 1. Primary Sources

### Foundational papers and texts

- **Box, G. E. P. and Jenkins, G. M. (1970). *Time Series Analysis: Forecasting and Control*.** Holden-Day, San Francisco. Citation page: [https://www.scirp.org/reference/referencespapers?referenceid=2106713](https://www.scirp.org/reference/referencespapers?referenceid=2106713). Wikipedia overview of the Box–Jenkins method: [https://en.wikipedia.org/wiki/Box%E2%80%93Jenkins_method](https://en.wikipedia.org/wiki/Box%E2%80%93Jenkins_method). The book that gave ARIMA its name and its workflow — identify orders with ACF/PACF, estimate, diagnose residuals, forecast. Now in its 5th edition (Box, Jenkins, Reinsel, Ljung, 2015, Wiley); for Ch 10 it is the lineage anchor, not a free PDF. The chapter does not need to quote it directly — it needs to acknowledge that the frequentist ARIMA workflow students will see in `statsmodels` or `forecast::auto.arima` is this book's procedure with computational scaffolding bolted on.

- **Hyndman, R. J. and Athanasopoulos, G. (2021). *Forecasting: Principles and Practice* (3rd ed.).** OTexts. Free online: [https://otexts.com/fpp3/](https://otexts.com/fpp3/). Continuously updated; the 3rd edition's online version was last refreshed on 3 May 2026. The single best free undergraduate-accessible source for everything Ch 10 covers. Chapter 9 ("ARIMA models") is the canonical modern presentation of the Box–Jenkins workflow. Chapter 8 ("Exponential smoothing") is the structural-state-space alternative. The book uses R throughout; the LLM-implementation move of this textbook can have students prompt for both R and Python versions of the same fit. **Cite as both reading assignment and reference.**

- **Scott, S. L. and Varian, H. R. (2014). "Predicting the Present with Bayesian Structural Time Series."** *International Journal of Mathematical Modelling and Numerical Optimisation*, 5(1/2), 4–23. PDF (author copy): [https://people.ischool.berkeley.edu/~hal/Papers/2013/pred-present-with-bsts.pdf](https://people.ischool.berkeley.edu/~hal/Papers/2013/pred-present-with-bsts.pdf). SSRN: [https://papers.ssrn.com/sol3/papers.cfm?abstract_id=2304426](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=2304426). This is the paper that introduced the `bsts` R package and standardized "Bayesian structural time series" as a label for state-space models with MCMC posteriors and spike-and-slab regression components. The worked example — nowcasting U.S. initial unemployment claims using Google search trends — is the closest published demonstration to the inventory-demand example Ch 10 builds. The paper makes the sequential-updating point explicitly.

- **`bsts` R package (Scott).** CRAN manual: [https://cran.r-project.org/web/packages/bsts/bsts.pdf](https://cran.r-project.org/web/packages/bsts/bsts.pdf). The implementation companion to Scott & Varian. The package fits local-level, local-linear-trend, seasonal, and regression components; it returns posterior draws, not just point estimates. For Ch 10's LLM-prompting section, the right move is to have students ask the LLM to generate `bsts` code and explain each component.

- **Harvey, A. C. (1989). *Forecasting, Structural Time Series Models and the Kalman Filter*.** Cambridge University Press. ISBN 0-521-32196-4. Cambridge listing: [https://www.cambridge.org/core/books/forecasting-structural-time-series-models-and-the-kalman-filter/CE5E112570A56960601760E786A5E631](https://www.cambridge.org/core/books/forecasting-structural-time-series-models-and-the-kalman-filter/CE5E112570A56960601760E786A5E631). Internet Archive scan: [https://archive.org/details/forecastingstruc0000harv](https://archive.org/details/forecastingstruc0000harv). The book that established "structural time series" — explicit unobserved components (level, trend, seasonal) handled through the Kalman filter — as a coherent alternative to Box–Jenkins. Cite as the *frequentist* state-space predecessor that BSTS Bayesianizes. Reading Harvey makes clear that the structural decomposition is independent of the Bayesian/frequentist split; only the posterior distribution is Bayesian-specific.

- **West, M. and Harrison, J. (1997). *Bayesian Forecasting and Dynamic Models* (2nd ed.).** Springer Series in Statistics. ISBN 978-0-387-94725-9. Springer landing: [https://link.springer.com/book/10.1007/b98971](https://link.springer.com/book/10.1007/b98971). The canonical reference for Bayesian dynamic models — what Scott & Varian generalize. The book is more rigorous than Ch 10 needs and is paywalled. Cite as lineage, not as assigned reading. The phrase "the posterior from today is the prior for tomorrow" is in the spirit of West–Harrison's recursive Bayesian updating throughout.

- **Taylor, S. J. and Letham, B. (2018). "Forecasting at Scale."** *The American Statistician*, 72(1), 37–45. Open author PDF: [http://lethalletham.com/ForecastingAtScale.pdf](http://lethalletham.com/ForecastingAtScale.pdf). The Prophet paper. Prophet is a piecewise-linear-trend + seasonality + holiday additive model fit via Stan (Bayesian under the hood), exposed to users as a one-line forecast call. Useful for Ch 10 as the modern industrial Bayesian-structural alternative; FPP3 §12.2 treats it [https://otexts.com/fpp3/prophet.html](https://otexts.com/fpp3/prophet.html). Prophet is what an inventory manager actually reaches for in 2026 — and Ch 10 should name that.

- **Gelman, A., Carlin, J. B., Stern, H. S., Dunson, D. B., Vehtari, A., and Rubin, D. B. (2013). *Bayesian Data Analysis* (3rd ed.).** Chapman & Hall/CRC. Free PDF released by the authors: [https://sites.stat.columbia.edu/gelman/book/BDA3.pdf](https://sites.stat.columbia.edu/gelman/book/BDA3.pdf). Background reference for sequential-updating mechanics (Ch 1, Ch 7). Not the chapter's primary citation but should sit on the side desk.

### Key empirical cases

- **BLS Current Employment Statistics (CES, National).** Program page: [https://www.bls.gov/ces/](https://www.bls.gov/ces/). Bulk time-series flat files (the entire CES history): [https://download.bls.gov/pub/time.series/ce/](https://download.bls.gov/pub/time.series/ce/). The file `ce.data.0.AllCESSeries` carries every published series. CES is monthly establishment-survey data for industries (NAICS-coded), not occupations — important because TIKTOK.md Exercise 1 refers to "BLS employment data ... for an occupation category of your choice," which is closer to a different BLS program (see next). Monthly cadence, ~50 years of history for many series, seasonally adjusted and not-seasonally-adjusted versions both available. Fit for the chapter's 52-week-style exercise *if* the manager is forecasting industry employment rather than occupational employment.

- **BLS Occupational Employment and Wage Statistics (OEWS, formerly OES).** Program page: [https://www.bls.gov/oes/](https://www.bls.gov/oes/). Annual employment and wage estimates for ~830 SOC occupations at national, state, and MSA levels, May reference date. The cadence is *annual*, not monthly — so a "52-week" forecast on OEWS data is conceptually awkward. The author should choose:
  - **(a)** Use CES industry-level monthly data for the 52-week-style exercise (good fit for the inventory-style scenario), or
  - **(b)** Use OEWS annual occupation-level data and reframe the forecast as quarterly or annual horizon (better fit for the Ch 11 automation-exposure tie-in).

  Flagging as a `[design choice]` for Nik — TIKTOK.md's wording leaves it ambiguous, and the two choices teach slightly different things.

- **Inventory-demand benchmark datasets (public).** The closest publicly available analog to the chapter's inventory scenario is the **Walmart M5 Forecasting Accuracy** dataset (Makridakis competition 2020): hierarchical daily sales for 3,049 products across 10 Walmart stores, ~5 years of history. Kaggle archive: [https://www.kaggle.com/competitions/m5-forecasting-accuracy](https://www.kaggle.com/competitions/m5-forecasting-accuracy) [verify the dataset link is still accessible without a Kaggle account]. The M5 competition results are documented in Makridakis, Spiliotis, and Assimakopoulos's writeups in the *International Journal of Forecasting* in 2022. M5 is what students of this material will end up working on; mentioning it in the connections-forward section is honest.

- **Google Flu Trends and the Scott–Varian nowcasting example.** The original BSTS paper uses Google search trends to nowcast U.S. initial unemployment claims (a BLS weekly release). The "search trends + weekly economic indicator" pattern is exactly transferable to the inventory scenario: weekly demand for a product can be augmented with search interest for related queries. The Google Flu Trends cautionary tale — Lazer, Kennedy, King, Vespignani (2014), "The Parable of Google Flu," *Science* 343(6176): 1203–1205 [verify DOI 10.1126/science.1248506] — is the right limit case for Ch 10's "the Bayesian model is not magic" beat.

---

## 2. The Core Concept — State of the Field

### What is settled

Several things are not in dispute. **(1)** Sequential Bayesian updating is mathematically equivalent to one-shot updating on the full dataset for exchangeable observations — the order of operations does not change the posterior. This is the textbook fact behind "the posterior from today is the prior for tomorrow." Gelman BDA3 Ch 1 makes the point in three lines. **(2)** ARIMA(p,d,q) models, fit by maximum likelihood, produce identical point forecasts to their state-space representations fit via the Kalman filter, given the same data — see Hyndman–Athanasopoulos Ch 9 and Harvey 1989 Ch 4. **(3)** Bayesian and frequentist forecasts for stationary series with large samples and uninformative priors converge to the same point forecast; the meaningful difference lives in the prediction interval vs. predictive distribution. This is the asymmetry rule from TIKTOK.md showing up in this chapter: the Bayesian solution earns its complexity at the boundaries (short series, hierarchical structure, when the *decision* requires P(future value > threshold)).

The chapter can therefore say without controversy: ARIMA and BSTS give similar point forecasts when there is enough data and the series is well-behaved; they differ in what they hand the decision-maker downstream.

### What is disputed

A few real disputes lurk under the floor.

**(1) Model selection in ARIMA.** ACF/PACF inspection is the Box–Jenkins prescription; AICc-based search (`auto.arima` in `forecast`) is the modern default. The two procedures pick different models on the same data more often than students expect. Hyndman has written that automatic selection works well for most users — see his 2008 *Journal of Statistical Software* paper on the `forecast` package — but the practice still divides classical time-series econometricians from machine-learning practitioners.

**(2) When is a Bayesian time-series model worth the compute cost?** Scott–Varian argue: when you have leading indicators (search trends, sales data from related products) you want to include with sparsity, BSTS earns its keep. Hyndman has pushed back, in published reviews and his blog, that Prophet and BSTS are oversold for simple seasonal forecasting problems — that exponential smoothing or ETS state-space models match or beat them on the M4/M5 competition data at a fraction of the compute cost. The dispute is settled empirically by the Makridakis M4/M5 results: simple methods often win on aggregate accuracy, complex Bayesian methods win when the decision needs probabilistic statements about specific quantiles.

**(3) Whether "structural" decomposition (level + trend + seasonal) is the right inductive bias.** Harvey's structural-time-series program argues yes; the ARIMA tradition argues that differencing handles the same problems implicitly. For Ch 10 the answer is pedagogical: structural decompositions are easier to explain because the components have meanings. Differencing-based models are easier to fit but harder to interpret.

### What has changed recently (last 5 years)

- **Prophet and bsts are now industrial.** Both packages are installed in essentially every Python and R analytics environment by default in 2026. The Bayesian-vs-frequentist contrast Ch 10 draws will land on students who have already touched at least one of these libraries. The chapter should respect that.

- **Probabilistic forecasting has displaced point-forecast benchmarking in the M4/M5 competitions.** Makridakis, Spiliotis, Assimakopoulos and collaborators have published a series of competition results (M4 in 2018–2020; M5 in 2020–2022) showing that hybrid deep-learning + statistical methods now lead aggregate point-forecast accuracy, *but* that calibrated prediction intervals — which Bayesian methods produce naturally — remain hard for pure neural-net methods. This is the empirical wedge for the chapter's claim that the Bayesian framework wins when the decision needs a probability statement.

- **Stan and PyMC have matured.** Both libraries now handle the structural time-series models Ch 10 demonstrates with reasonable speed. The Stan reference manual ([https://mc-stan.org/docs/](https://mc-stan.org/docs/)) and PyMC docs ([https://www.pymc.io/](https://www.pymc.io/)) include worked time-series examples. LLM code-generation for these libraries is competent in 2026 in ways it was not in 2022.

- **Foundation models for forecasting.** Amazon's Chronos, Google's TimesFM, Salesforce's Moirai and others have appeared since 2023, claiming zero-shot forecasting performance competitive with model-specific fits. Whether this matters for Ch 10 depends on how the chapter wants to land — if the book's thesis is "frequentist vs. Bayesian, you choose," foundation models are a third path the chapter could mention in the connections-forward section as Ch 13 material. They will not be the primary contrast.

---

## 3. Application Domain Examples

Per TIKTOK.md, Ch 10's scenario is **inventory demand forecasting** over 52 weeks of weekly demand. Five anchor examples for the chapter:

1. **The TIKTOK.md inventory manager (primary worked example).** 52 weeks of weekly demand, upward trend, noise. Frequentist ARIMA → AIC selection picks ARIMA(1,1,1) with drift; point forecast plus 95% prediction interval for next 12 weeks. Bayesian BSTS → local-linear-trend component, weak prior on slope, MCMC posterior; 12-week predictive distribution with 90% credible interval AND P(weekly demand > reorder threshold) computable directly. The contrast is sharpest when the manager's question is "what is the probability we stock out in week 8?" — the frequentist prediction interval cannot answer this without extra distributional assumptions; the Bayesian posterior gives it as a quantile read-off.

2. **BLS CES industry employment, 52 weeks.** CES is monthly, not weekly, so the closest analog is 52 months of (e.g.) "Manufacturing, durable goods, employees" from CES series ID `CES3100000001`. The series is long (back to 1939), well-modeled by ARIMA with seasonal differencing, and a Bayesian state-space model with a level + cyclical + seasonal component gives a textbook-clean decomposition. Fit for Exercise 1 if the author reframes "52 weeks" as "52 months." Verify the precise series ID against [https://download.bls.gov/pub/time.series/ce/](https://download.bls.gov/pub/time.series/ce/) before publishing.

3. **BLS OEWS occupational employment, annual.** If the author wants to keep the Ch 11 connection foregrounded (occupational data here predicts occupational classification there), an annual occupation-level series like "Cashiers" (SOC 41-2011) or "Software developers" (SOC 15-1252) from OEWS gives ~25 annual data points for the 1999–2024 horizon. Too short for ARIMA-driven inference but a clean illustration of why Bayesian methods with priors dominate when the series is short. This is the right exercise if the author wants Ch 10 to set up Ch 11.

4. **Walmart M5 daily sales.** 1,941 days of unit sales for each of 3,049 products. The dataset's hierarchical structure (product → department → category → store → state) is what makes Bayesian hierarchical state-space models genuinely competitive against pure deep-learning approaches in the M5 results. Mention as a connections-forward example, not as a worked example — the dataset is too large for a chapter exercise.

5. **A retail seasonality demonstration.** Any product with strong yearly seasonality — ice cream sales, snow shovel sales, school-supply sales — gives the BSTS seasonal-component story its cleanest possible setup. The author can synthesize a clean 156-week series (3 years of weekly data) with known trend + seasonal + noise components, fit both ARIMA(p,d,q)(P,D,Q)[52] and BSTS with explicit seasonal component, and show the decomposition the Bayesian model returns. Synthetic data is *honest* here because the chapter's point is the mechanism, not a real-world claim about ice cream.

---

## 4. The Book's Thesis Connection

This book's thesis is that statistical inference should be taught through explicit side-by-side comparison, with the reader choosing. Ch 10 is where the choice gets sharpest because the two approaches diverge most visibly.

**The asymmetry rule from the chapter spec is doing real work here.** The frequentist ARIMA solution is one paragraph: identify orders, fit, forecast, report prediction interval. The Bayesian BSTS solution is several pages: prior choice on each component, MCMC posterior, posterior predictive distribution, downstream quantile and probability computations. The chapter spends more space on the Bayesian side because the Bayesian side does more work — and the chapter must name this explicitly rather than apologize for it.

**Sequential updating is the chapter where Bayesian inference feels *natural* rather than *foreign*.** A student who has resisted Bayesian methods through Chs 1–9 because the prior felt arbitrary will, in Ch 10, see priors as forecasts and posteriors as updated forecasts — exactly what every inventory manager does in their head every week. The chapter should lean into this. The "posterior from today is the prior for tomorrow" sentence is the chapter's spine.

**The decision-orientation is the bridge to Ch 11.** Both Ch 10 and Ch 11 are *decision-output* chapters: the calculation matters because it feeds a decision (reorder threshold in Ch 10; approve/decline in Ch 11). Ch 10 lays the groundwork for the explicit-decision-theoretic framing Ch 11 develops by showing that the Bayesian framework directly computes P(quantity > threshold), whereas the frequentist framework gives only the prediction interval and leaves the threshold-mapping implicit.

**Where the chapter must not overclaim.** For long, stable series with mild trend and seasonality, frequentist ARIMA forecasts are essentially indistinguishable from BSTS point forecasts and run in milliseconds where BSTS takes minutes. The chapter should say this. The Bayesian advantage is not "better forecasts on average." It is "the right output for decisions that need probability statements about specific events." That is the honest claim.

---

## 5. Intellectual Lineage Notes

**George E. P. Box and Gwilym M. Jenkins (1970).** *Time Series Analysis: Forecasting and Control*. The canonical text — ARIMA terminology, the identification-estimation-diagnostic-forecasting workflow, the use of ACF/PACF as diagnostic tools all originate (in their consolidated modern form) here. Box was a Bayesian by temperament (his 1973 book with Tiao, *Bayesian Inference in Statistical Analysis*, is itself influential) but his most-cited work in time series is operationally frequentist. Worth noting in a chapter sidebar.

**Andrew C. Harvey (1989).** *Forecasting, Structural Time Series Models and the Kalman Filter*. Cambridge UP. Harvey's program — explicit unobserved components, Kalman filtering for inference — is the structural-time-series tradition. Bayesian and frequentist versions of structural models both descend from this book. The Kalman filter is itself one of the cleanest examples of recursive estimation a student can see; the chapter could spend a paragraph on it as a "the Bayesian update rule running in real time" sidebar, but should not let it consume the deep-dive.

**Mike West and Jeff Harrison (1989, 2nd ed. 1997).** *Bayesian Forecasting and Dynamic Models*, Springer. The fully Bayesian state-space tradition. West–Harrison is where the technical apparatus for what Scott & Varian later made practical was developed. The student does not need to read it; the chapter should cite it once as the origin.

**Steven Scott and Hal Varian (2014).** "Predicting the Present with Bayesian Structural Time Series." The paper that took West–Harrison's apparatus and turned it into the `bsts` R package, popularized by Google's economics group. The phrase "Bayesian structural time series" as commonly used in 2026 means the Scott–Varian operationalization, not the West–Harrison theoretical framework. Worth being precise about.

**Sean Taylor and Ben Letham (2018).** "Forecasting at Scale" (Prophet). Facebook's contribution: a piecewise-linear-trend additive model fit through Stan, exposed as a one-call API. Prophet is Bayesian under the hood and frequentist-looking in the user interface — a useful pedagogical example of how the philosophical split can be invisible to the user when the implementation is good. The chapter could mention this in the prompting section.

**Sequential updating** as a concept goes back to Bayes (1763) and Laplace (1814) — the same lineage Ch 0 cited. What is new in Ch 10 is making the temporal structure of the updating *visible* in the forecast graph. Kalman (1960), "A New Approach to Linear Filtering and Prediction Problems" [verify DOI/link — original *Trans. ASME J. Basic Eng.* paper is sometimes paywalled] is the engineering version of the same recursive idea; it is fair to note in a sidebar.

---

## 6. Pedagogical Delivery Research

### Prior knowledge required

The chapter assumes the reader knows: linear regression (Chs 8–9 of this book), basic probability distributions (Ch 0 + Ch 3), prior/likelihood/posterior mechanics (Chs 4–6), and is comfortable with the side-by-side comparison move (Chs 1–9). New for Ch 10: the idea that *the same parameter has different values at different times* (state-space framing) is the only genuinely new mental move.

### Common misconceptions in undergraduates

**1. Correlation in time = causation.** The single most-named pedagogical hazard in introductory time-series teaching. Students see two trending series, compute a high correlation, and report a causal claim. The chapter should hit this explicitly: any two upward-trending series will correlate even if they share no causal connection (the standard spurious-correlation example: U.S. cheese consumption and deaths by bedsheet entanglement; see Tyler Vigen's spurious-correlations archive [https://tylervigen.com/spurious-correlations](https://tylervigen.com/spurious-correlations)). Differencing both series before correlating is the standard fix and the standard piece of advice the chapter should pass along.

**2. Autocorrelation treated as a nuisance, not as information.** Students reach for `arima()` without inspecting the ACF/PACF. They miss the autocorrelation structure that *is the model*. The chapter's deep-dive on Box–Jenkins identification should walk through this step on the page.

**3. Prediction interval = "there is a 95% chance the true value falls in this range."** It is not. A frequentist 95% prediction interval is constructed so that across many hypothetical replications, 95% of intervals will contain the realized future value. The Bayesian 95% credible interval *is* what students naively expect — "given everything we know, 95% probability the future value is in this range." This distinction is the chapter's cleanest single example of what the Bayesian framework gives the student that the frequentist framework does not. Hyndman–Athanasopoulos §1.7 makes this point but does not lean into it; Ch 10 should.

**4. ARIMA prediction intervals are well-calibrated.** Empirically, they are routinely overconfident — particularly at long horizons and especially when the series exhibits structural breaks the model did not capture. The M3 and M4 forecasting competition writeups document this. The chapter should be honest about it.

**5. "Bayesian = uses priors" rather than "Bayesian = treats parameters probabilistically."** The chapter should reinforce that what makes the BSTS forecast Bayesian is the posterior distribution over the trend and seasonal components, not the specific priors used. Defaults often dominate the prior choice in long series; the Bayesian-ness lives in the output.

### Instructional sequences that work

The standard pedagogical sequence: (1) visualize the series, (2) inspect ACF/PACF, (3) difference until stationary, (4) fit ARIMA, (5) diagnose residuals, (6) forecast. This is the Hyndman–Athanasopoulos progression and the Box–Jenkins original. For the Bayesian side: (1) decompose the series mentally into level + trend + seasonal + noise components, (2) specify priors on each component (default reasonable priors are fine for a first pass), (3) fit, (4) inspect posterior predictive samples, (5) compute decision-relevant probabilities from the posterior. The two sequences should be presented side by side, with the chapter naming where they overlap (visualize first; decompose mentally; diagnose) and where they diverge (the frequentist diagnostic checks residuals; the Bayesian diagnostic checks posterior predictive simulations against the data).

### Known teaching failure modes

- **Treating ARIMA as a black box.** `auto.arima` is so convenient that students fit it without ever inspecting the data. The chapter should require visualization and ACF inspection *before* any model fit, on the first worked example.
- **Skipping the seasonal component.** Weekly demand for retail products almost always has yearly seasonality (52-week period). A model fit without seasonal terms looks fine on the training data and fails immediately on the holdout. The chapter should demonstrate this failure explicitly.
- **Reporting point forecasts without intervals.** A point forecast is a number. A point forecast with no interval is a guess. The chapter should never present a point forecast without its interval — and should mark the interval's interpretation (prediction interval, credible interval) every time.

---

## 7. Representation and Display Research

### The side-by-side comparison table from TIKTOK.md

The TIKTOK.md spec does not include an explicit table for Ch 10; the standard side-by-side from §35 of the spec is the chapter template. Synthesizing from the chapter brief:

| **Dimension** | **Frequentist ARIMA** | **Bayesian Structural Time Series** |
|---|---|---|
| **Inputs** | Series; orders (p,d,q) chosen by ACF/PACF or AICc | Series; component specification (level, trend, seasonal, regression); priors |
| **Estimation** | Maximum likelihood (Kalman filter for state-space form) | MCMC sampling of posterior |
| **Output** | Point forecast + prediction interval | Posterior predictive distribution (full draws) |
| **Interpretation** | "95% of constructed intervals contain the future value over many replications" | "Given the data, 95% probability the future value lies in this interval" |
| **Cost** | Milliseconds | Seconds to minutes |
| **Decision support** | Manual: reader must map interval to decision rule | Direct: P(quantity > threshold) is a quantile read-off |
| **When it wins** | Long, stable series; computational budget tight; standardized reporting | Short series; hierarchical structure; threshold-decisions; informative priors available |
| **Failure mode** | Overconfident intervals at long horizons | Sensitive to prior choice on short series; compute cost on large data |

**One row I would add: Updateability.** This row sits at the heart of the chapter's "posterior from today is the prior for tomorrow" point.

| **Updateability** | Refit on the full series each time new data arrives; same compute cost as initial fit | Posterior from week *t* becomes prior for week *t+1*; updates are incremental and cheap |

The row matters because the chapter spends a section on sequential updating as the Bayesian core. If the comparison table omits the dimension where the Bayesian framework's advantage is structural rather than computational, the table is hiding the chapter's main beat.

### Visualizations the chapter should plan for

- **The training series + forecast plot.** Standard. Both frequentist and Bayesian versions side by side. The Bayesian plot should show multiple posterior predictive sample paths (50–100 lines, semi-transparent), not just an interval, to make the "distribution of futures" feel concrete.
- **The decomposition plot.** For the BSTS fit: level, trend, seasonal, and residual components on four stacked panels. This is what makes the structural model's transparency vivid.
- **The "forecast narrowing over time" animation/sequence.** Show the predictive distribution at week 1, then re-fit at week 13, week 26, week 39, week 52. The interval narrows; the chapter's narrative is that this is *the same operation* repeated.
- **A reorder-threshold visualization.** Mark the threshold horizontally; show the predictive distribution; shade the area above the threshold. The shaded area *is* P(reorder needed). One picture says what three paragraphs of frequentist explanation could not.

---

## 8. Open Questions and Research Gaps

- **The "52-week BLS occupation series" framing in TIKTOK.md is mildly inconsistent.** BLS CES is monthly industry data; BLS OEWS is annual occupation data. There is no 52-week occupational series on BLS. Flagged for Nik — the exercise either needs to switch to CES industry data (and keep "52 weeks" as "52 months") or to OEWS annual data (and reframe the horizon).

- **Whether to use `bsts` (R) or PyMC/Stan (Python) for the worked example.** The chapter's prompting section should probably show both. `bsts` is more compact and well-documented; PyMC is more flexible and Python-native. LLM code-generation is competent for both as of 2026. Author preference.

- **Foundation models for forecasting (Chronos, TimesFM, Moirai).** Will be more important by the book's publication date than they are now. The chapter could mention them in the connections-forward section. Aging risk: if the book has a 3-year shelf life, this section may need a refresh.

- **The Prophet vs. BSTS choice.** Both are Bayesian-under-the-hood structural time-series methods. Prophet is more popular; BSTS is more transparent. The chapter could profitably contrast them as two implementations of the same idea, but this risks blurring the frequentist-vs-Bayesian comparison the chapter is built around. My recommendation: cite Prophet once in the prompting section as "what students will reach for in practice" and use BSTS as the demonstrated method.

- **The M5 forecasting competition results are still being absorbed.** Aggregate findings (simple methods often win on point accuracy; hierarchical Bayesian methods do well on interval calibration) are published. The fine-grained per-method comparisons are still circulating in the literature. The chapter should cite Makridakis et al. on the aggregate findings and avoid leaning on specific per-method rankings.

- **Sources likely to age within 3 years.** Box–Jenkins (1970), Harvey (1989), West–Harrison (1997), Scott–Varian (2014), Hyndman–Athanasopoulos (3rd ed., continuously updated): not at risk. Foundation-model citations and the M5 commentary: high aging risk. Prophet's status (still widely used? superseded?): moderate aging risk. The chapter should structure citations so the swap-in points are obvious.

---

## 9. Sourcing Notes

- **Box & Jenkins (1970).** Paywalled book, no free PDF. Cite as lineage; do not lean on direct quotes. The 5th edition (2015) is the live reference.
- **Hyndman & Athanasopoulos (3rd ed.).** Open access via OTexts.com. The single best free undergraduate reference. Cite liberally.
- **Scott & Varian (2014).** Free author PDF at Berkeley iSchool. No paywall on the working version. The journal version is paywalled but the working PDF is the same content.
- **`bsts` R package documentation.** Free on CRAN.
- **Harvey (1989).** Paywalled book; Internet Archive scan exists for educational reading. Cite as lineage only.
- **West & Harrison (1997).** Paywalled. Cite as lineage only.
- **Taylor & Letham (2018), Prophet.** Free author PDF.
- **Gelman et al. BDA3.** Free PDF released by the authors. Cite for background.
- **BLS data.** Public domain, bulk downloads at `download.bls.gov`. No paywall, no API key required.
- **Walmart M5.** Kaggle dataset; free with Kaggle account. Cite the Makridakis et al. *International Journal of Forecasting* writeups (2022) as the canonical results.
- **Lazer et al. (2014), "The Parable of Google Flu."** *Science*, paywalled but widely quoted. The chapter can summarize the cautionary point without quoting; the citation is well-established.

No fact-checking gaps on the foundational mathematics. Two items flagged `[verify]` above: (a) the precise CES series ID the chapter ends up choosing for its worked example, and (b) the Kalman 1960 link, which is sometimes paywalled and sometimes available through engineering-society archives. Three items flagged `[design choice]` for Nik: (a) CES-monthly vs OEWS-annual for the BLS exercise, (b) `bsts` vs PyMC for the implementation, (c) whether to mention foundation models in the connections-forward section.
