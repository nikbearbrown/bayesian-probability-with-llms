# Research: Chapter 11 — Classification and Decision
## Bayesian Probability with LLMs

**Chapter one-line:** Classification as statistical inference — where the choice of threshold is a decision under a loss function, and making that loss function explicit is the difference between a model and a decision tool.
**Research date:** 2026-05-13

---

## 1. Primary Sources

### Foundational papers and texts

- **Cox, D. R. (1958). "The Regression Analysis of Binary Sequences (with Discussion)."** *Journal of the Royal Statistical Society, Series B*, 20(2), 215–242. DOI: 10.1111/j.2517-6161.1958.tb00292.x. Oxford Academic landing: [https://academic.oup.com/jrsssb/article/20/2/215/7027376](https://academic.oup.com/jrsssb/article/20/2/215/7027376). Wiley landing: [https://rss.onlinelibrary.wiley.com/doi/abs/10.1111/j.2517-6161.1958.tb00292.x](https://rss.onlinelibrary.wiley.com/doi/abs/10.1111/j.2517-6161.1958.tb00292.x). The paper that introduced logistic regression as a way to model binary outcomes with covariates. Cox treats the binary sequence as the observable and the log-odds as the linear modeling target — the same move every package implements today. The paper is short, technical, and remarkably modern; it does not feel like 1958 reading. Cite as the lineage anchor for "logistic regression has been around for two-thirds of a century, and the basic setup has not moved."

- **Wald, A. (1950). *Statistical Decision Functions*.** Wiley, New York. The foundational text for frequentist decision theory. Wald's machinery — a state space, a decision function mapping data to actions, a risk function (expected loss across replications), admissibility, minimax rules — is the apparatus the chapter's Bayesian decision theory will be compared against. Discussion at [https://psycnet.apa.org/record/1951-01400-000](https://psycnet.apa.org/record/1951-01400-000) and a useful modern overview in Manski (2019), CeMMAP working paper [https://www.cemmap.ac.uk/wp-content/uploads/2020/08/CWP0619.pdf](https://www.cemmap.ac.uk/wp-content/uploads/2020/08/CWP0619.pdf). The chapter does not need to teach Wald in detail — but it should name him once. Decision theory as a discipline starts here.

- **Berger, J. O. (1985). *Statistical Decision Theory and Bayesian Analysis* (2nd ed.).** Springer Series in Statistics. ISBN 978-0-387-96098-2. Springer landing: [https://link.springer.com/book/10.1007/978-1-4757-4286-2](https://link.springer.com/book/10.1007/978-1-4757-4286-2). The canonical Bayesian decision-theory text. Chapter 4 ("Bayesian Analysis") develops Bayes risk, posterior expected loss, and the optimal-decision rule (action minimizing posterior expected loss) — exactly the apparatus Ch 11 deploys for the threshold-choice problem. Paywalled book; the framework is teachable from the chapter without quoting Berger directly, but Berger is the source the chapter is leaning on. Cite as the rigorous reference.

- **Hand, D. J. and Henley, W. E. (1997). "Statistical Classification Methods in Consumer Credit Scoring: A Review."** *Journal of the Royal Statistical Society, Series A*, 160(3), 523–541. DOI: 10.1111/j.1467-985X.1997.00078.x. Open PDF: [https://www.sfu.ca/~rjones/bus864/readings/HandHenley1997JRSS.pdf](https://www.sfu.ca/~rjones/bus864/readings/HandHenley1997JRSS.pdf). Oxford Academic landing: [https://academic.oup.com/jrsssa/article/160/3/523/7102381](https://academic.oup.com/jrsssa/article/160/3/523/7102381). The canonical review of statistical methods for credit scoring. Hand's argument — that the choice of method matters less than the data and the threshold mapping — is exactly the chapter's point. The paper is 28 years old; the methods listed are dated; the diagnostic about *what credit scoring actually is* (a classification problem with asymmetric costs, a regulatory regime requiring explainability, and a threshold-mapping problem the model cannot solve internally) has not aged.

- **Hand, D. J. (2009). "Measuring Classifier Performance: A Coherent Alternative to the Area Under the ROC Curve."** *Machine Learning*, 77(1), 103–123. DOI: 10.1007/s10994-009-5119-5. Springer landing: [https://link.springer.com/article/10.1007/s10994-009-5119-5](https://link.springer.com/article/10.1007/s10994-009-5119-5). Open PDF (Case Western): [http://engr.case.edu/ray_soumya/mlrg/measuring_performance_hand.mlj09.pdf](http://engr.case.edu/ray_soumya/mlrg/measuring_performance_hand.mlj09.pdf). The paper that argues AUC is fundamentally incoherent as a single-number classifier metric because it implicitly uses different cost distributions for different classifiers. The H-measure Hand proposes makes the cost distribution explicit. Directly relevant to the chapter's theme that *making the loss function explicit is the move*. The chapter should cite this paper to puncture the standard "we report AUC" reflex.

- **Guo, C., Pleiss, G., Sun, Y., and Weinberger, K. Q. (2017). "On Calibration of Modern Neural Networks."** *Proceedings of the 34th International Conference on Machine Learning* (ICML), PMLR 70: 1321–1330. arXiv: [https://arxiv.org/abs/1706.04599](https://arxiv.org/abs/1706.04599). PMLR PDF: [https://proceedings.mlr.press/v70/guo17a/guo17a.pdf](https://proceedings.mlr.press/v70/guo17a/guo17a.pdf). The paper that documented modern deep networks are systematically *over*confident, and showed temperature scaling — a single-parameter post-hoc fix — calibrates them well. The chapter does not need to teach neural networks, but it needs to teach calibration: a probability output is only useful for decision-making if it is calibrated, and modern overparametrized models are not calibrated by default. This is the cleanest paper to cite for that fact.

- **Hardt, M., Price, E., and Srebro, N. (2016). "Equality of Opportunity in Supervised Learning."** *Advances in Neural Information Processing Systems 29* (NeurIPS 2016). arXiv: [https://arxiv.org/abs/1610.02413](https://arxiv.org/abs/1610.02413). NeurIPS PDF: [https://papers.neurips.cc/paper/6374-equality-of-opportunity-in-supervised-learning.pdf](https://papers.neurips.cc/paper/6374-equality-of-opportunity-in-supervised-learning.pdf). The paper that introduced the "equalized odds" fairness criterion — a constraint on threshold choice across protected groups. Relevant to the chapter because the threshold-choice problem is exactly where the fairness literature lives. Citing this paper signals to the student that "choose your threshold" is not a neutral act when the classifier's outputs map to consequential decisions about people. For the loan-default example, this is the natural turn to take in the synthesis section.

### Key empirical cases — automation exposure

- **Frey, C. B. and Osborne, M. A. (2017). "The Future of Employment: How Susceptible Are Jobs to Computerisation?"** *Technological Forecasting and Social Change*, 114, 254–280. DOI: 10.1016/j.techfore.2016.08.019. Open Oxford Martin PDF: [https://oms-www.files.svdcdn.com/production/downloads/academic/The_Future_of_Employment.pdf](https://oms-www.files.svdcdn.com/production/downloads/academic/The_Future_of_Employment.pdf). Oxford Martin program page: [https://www.oxfordmartin.ox.ac.uk/publications/the-future-of-employment](https://www.oxfordmartin.ox.ac.uk/publications/the-future-of-employment). The "47% of US jobs at risk" paper. The methodology: hand-label 70 occupations from the O*NET-SOC taxonomy as automatable or not, train a Gaussian process classifier on O*NET-derived features (manual dexterity, persuasion, originality, etc.), output a probability of computerization for each of 702 occupations, threshold at 0.7 to call an occupation "high risk." This *is* the classification problem the chapter's exercise asks the student to reproduce. The 47% figure comes from summing employment shares of all occupations above the threshold. **The threshold is the decision; the methodology is the model.** This is the chapter's single most pedagogically useful real-world example.

- **Arntz, M., Gregory, T., and Zierahn, U. (2016). "The Risk of Automation for Jobs in OECD Countries: A Comparative Analysis."** OECD Social, Employment and Migration Working Papers, No. 189. OECD landing: [https://www.oecd.org/en/publications/the-risk-of-automation-for-jobs-in-oecd-countries_5jlz9h56dvq7-en.html](https://www.oecd.org/en/publications/the-risk-of-automation-for-jobs-in-oecd-countries_5jlz9h56dvq7-en.html). Direct PDF: [https://www.oecd.org/content/dam/oecd/en/publications/reports/2016/05/the-risk-of-automation-for-jobs-in-oecd-countries_g17a27d8/5jlz9h56dvq7-en.pdf](https://www.oecd.org/content/dam/oecd/en/publications/reports/2016/05/the-risk-of-automation-for-jobs-in-oecd-countries_g17a27d8/5jlz9h56dvq7-en.pdf). The task-based response to Frey & Osborne. Same input data (O*NET); different unit of analysis (tasks within jobs, not whole jobs); dramatically different result (9% of jobs highly automatable, not 47%). The same probabilistic model can produce headline-grabbingly different numbers depending on what is being classified. This is gold for the chapter — it is *the* worked example of "your classification problem is your loss function is your reported number."

- **Brynjolfsson, E., Mitchell, T., and Rock, D. (2018). "What Can Machines Learn, and What Does It Mean for Occupations and the Economy?"** *AEA Papers and Proceedings*, 108, 43–47. DOI: 10.1257/pandp.20181019. AEA landing: [https://www.aeaweb.org/articles?id=10.1257/pandp.20181019](https://www.aeaweb.org/articles?id=10.1257/pandp.20181019). Open MIT PDF: [https://dspace.mit.edu/bitstream/handle/1721.1/120302/pandp.20181019.pdf](https://dspace.mit.edu/bitstream/handle/1721.1/120302/pandp.20181019.pdf). The paper that built the "Suitability for Machine Learning" (SML) score across 18,156 tasks in O*NET. The Brynjolfsson–Mitchell rubric is different from Frey–Osborne's classifier: it asks 23 expert-rated questions per task to score how learnable-by-ML the task is. The aggregate result — most occupations have *some* automatable tasks, very few are fully automatable — is the third leg of the chapter's automation-exposure triangle (Frey-Osborne / Arntz-Gregory-Zierahn / Brynjolfsson-Mitchell-Rock). Three respected analyses, same underlying O*NET data, three different headline conclusions, all driven by classification-problem choices.

- **Acemoglu, D. and Restrepo, P. (2020). "Robots and Jobs: Evidence from U.S. Labor Markets."** *Journal of Political Economy*, 128(6), 2188–2244. JPE listing: [https://ideas.repec.org/a/ucp/jpolec/doi10.1086-705716.html](https://ideas.repec.org/a/ucp/jpolec/doi10.1086-705716.html). NBER WP23285: [https://www.nber.org/papers/w23285](https://www.nber.org/papers/w23285); open WP PDF: [https://www.nber.org/system/files/working_papers/w23285/w23285.pdf](https://www.nber.org/system/files/working_papers/w23285/w23285.pdf). Empirical rather than classification-based: links industrial robot adoption to local labor market outcomes. Headline: one new robot per thousand workers reduces the employment-to-population ratio by about 0.2 percentage points. Useful for the chapter as a "this is what actually happened" counterweight to the Frey-Osborne / Arntz / Brynjolfsson predictions — those are forecasts; this is post-hoc measurement. Tone of the chapter should be: predictions about automation exposure differ wildly; the post-hoc empirical evidence is narrower in scope and shows real but smaller-than-forecast effects.

- **Acemoglu, D. and Restrepo, P. (2022). "Tasks, Automation, and the Rise in U.S. Wage Inequality."** *Econometrica*, 90(5), 1973–2016. DOI: 10.3982/ECTA19815. Wiley landing: [https://onlinelibrary.wiley.com/doi/full/10.3982/ECTA19815](https://onlinelibrary.wiley.com/doi/full/10.3982/ECTA19815). Open MIT PDF: [https://economics.mit.edu/sites/default/files/2022-10/Tasks%20Automation%20and%20the%20Rise%20in%20US%20Wage%20Inequality.pdf](https://economics.mit.edu/sites/default/files/2022-10/Tasks%20Automation%20and%20the%20Rise%20in%20US%20Wage%20Inequality.pdf). The follow-up paper that estimates 50–70% of changes in U.S. wage structure 1980–2016 are accounted for by task displacement in rapidly automating industries. Most directly useful for the chapter's "what does the loss function mean?" beat — calling an occupation "high automation exposure" is a classification claim; the wage-inequality effects are the consequences the classification implicitly weights.

### Key empirical cases — credit decisions

- **The LendingClub loan dataset.** Public lending data for ~2.9 million loans issued 2007–2018 by the LendingClub peer-to-peer platform; 140 variables per loan; "loan_status" target (fully paid / charged off / current / late / in grace period). Widely used in credit-scoring tutorials and benchmark studies — a recent re-analysis appears in Gilani and Kleer Kliimand at Belmont University [https://repository.belmont.edu/spark_presentations/280/](https://repository.belmont.edu/spark_presentations/280/), and a benchmark dataset version is archived at Zenodo: [https://zenodo.org/records/11295916](https://zenodo.org/records/11295916). LendingClub itself ceased peer-to-peer lending operations at the end of 2020, so the dataset is a closed historical archive — useful for teaching, less so for live decisions. Fit for Exercise 1 in TIKTOK.md. **The author should pin a specific dataset snapshot in the companion-website materials** rather than asking students to source it themselves; the Kaggle-hosted version moves around.

- **The German Credit dataset.** Smaller (1,000 cases), more pedagogically tractable, hosted in the UCI Machine Learning Repository as `statlog/german`. URL: [https://archive.ics.uci.edu/dataset/144/statlog+german+credit+data](https://archive.ics.uci.edu/dataset/144/statlog+german+credit+data) [verify URL is current — UCI restructured its site in recent years]. Includes a pre-specified asymmetric cost matrix (5× cost of approving a bad credit relative to declining a good one) baked into the dataset documentation. This is *exactly* the loss function the TIKTOK.md exercise references — and the chapter could note that the 5× number is not an estimate by the author, it is the cost matrix the German Credit dataset documentation explicitly specifies. Useful sidebar.

### O*NET data products

- **O*NET Database (current version) at O*NET Resource Center.** Landing: [https://www.onetcenter.org/database.html](https://www.onetcenter.org/database.html). The Database is downloadable as tab-delimited files, SQL dumps, Excel, MySQL, and Oracle exports. Quarterly updates; primary update in Q3 of each year. Files relevant to automation-exposure classification:
  - **Abilities.txt** — content-model ratings (1–5 importance, 1–7 level) for 52 abilities per O*NET-SOC occupation. Frey & Osborne pulled their "manual dexterity," "finger dexterity," and "originality" features from this file.
  - **Work_Activities.txt** — content-model ratings for 41 generalized work activities. Brynjolfsson-Mitchell-Rock's SML score is built across detailed work activities. File reference: [https://www.onetcenter.org/dictionary/25.0/excel/work_activities.html](https://www.onetcenter.org/dictionary/25.0/excel/work_activities.html).
  - **Work_Context.txt** — content-model ratings for 57 work context elements (work-setting features, like physical work conditions and interpersonal relationships). Used in the task-based Arntz-Gregory-Zierahn analysis.
  - **Skills.txt, Knowledge.txt, Tasks.txt** — additional content-model files. The full content-model documentation is at [https://www.onetcenter.org/content.html](https://www.onetcenter.org/content.html) [verify the deep-link is current].
  - **Occupation Data.txt** — the occupation list with SOC codes and titles, the master key for joining content-model files.

- **O*NET-SOC Taxonomy.** [https://www.onetcenter.org/taxonomy.html](https://www.onetcenter.org/taxonomy.html). The current taxonomy is O*NET-SOC 2019, built on the 2018 SOC. 1,016 occupational titles, 923 with O*NET data, mapping to 867 SOC codes, grouped into 459 Broad, 98 Minor, 23 Major occupational groups. The taxonomy update document is [https://www.onetcenter.org/dl_files/Taxonomy2019_Summary.pdf](https://www.onetcenter.org/dl_files/Taxonomy2019_Summary.pdf). The student's exercise will work in O*NET-SOC codes, not raw SOC; the chapter should be precise about that.

- **BLS OEWS occupational employment data.** [https://www.bls.gov/oes/](https://www.bls.gov/oes/). The "weight" in any employment-share calculation (like the Frey-Osborne 47%) comes from OEWS employment counts per occupation. Annual; May reference; ~830 SOC occupations. The student computing "what fraction of U.S. employment is above the threshold" needs OEWS to do the weighting.

---

## 2. The Core Concept — State of the Field

### What is settled

**Logistic regression as the canonical binary classifier with probabilistic output.** Cox (1958) gave the model; the maximum-likelihood estimator with iteratively reweighted least squares is settled procedure; Wald-type standard errors are settled procedure; the Bayesian version with normal or Cauchy priors on coefficients is settled procedure (Gelman et al. 2008, "A Weakly Informative Default Prior Distribution for Logistic and Other Regression Models," *Annals of Applied Statistics* [verify DOI 10.1214/08-AOAS191]). For large datasets with small parameter uncertainty, frequentist and Bayesian posterior means are numerically indistinguishable. Settled.

**The threshold choice is not a statistical question.** The model outputs a probability. Mapping that probability to a decision (approve/decline, flag/don't-flag, predict-class-A/predict-class-B) requires a loss function — a statement of the relative costs of false positives and false negatives — and the optimal threshold falls out of standard Bayesian decision theory (Berger 1985, Ch 4). When false positives and false negatives are equally costly, the threshold is 0.5. When the costs are asymmetric, the threshold moves. This is settled mathematics. What is not settled is whether anyone actually *does* this in practice — see "what is disputed" below.

**Modern overparametrized classifiers are typically not well-calibrated.** Guo et al. (2017) demonstrated this for deep neural networks; subsequent work (Ovadia et al. 2019, Minderer et al. 2021) extended the finding to broader model classes and distribution-shift settings. Post-hoc calibration (temperature scaling, Platt scaling, isotonic regression) generally helps. Settled.

**Bayesian and frequentist logistic regression converge for large *n* with flat priors.** The likelihood dominates; the posterior is approximately Gaussian around the MLE. The Bayesian framework's advantages live at small *n*, where priors matter, and in the downstream decision-theoretic apparatus, where the posterior gives quantities the MLE+SE pair does not.

### What is disputed

**Whether anyone actually specifies a loss function in practice.** Hand (2009) argues that operational practice in credit scoring, fraud detection, and medical diagnosis is to report AUC (or a related summary metric) and not to specify the cost matrix. Threshold choice happens — but it is justified post-hoc by appeals to operational throughput or regulatory comfort, not by an explicit loss-function calculation. The chapter's "make the loss function explicit" prescription is therefore an *argument*, not a description of standard practice. The literature agrees the prescription is correct; the literature also documents that it is widely ignored.

**Whether logistic regression is enough.** Industrial practice now reaches for gradient-boosted trees (XGBoost, LightGBM, CatBoost) for credit scoring and similar classification problems, often with substantial AUC improvements. The interpretability cost is real and matters for credit-scoring regulatory regimes (Fair Credit Reporting Act in the U.S.; GDPR's "right to explanation" in the EU). Whether the AUC gain is worth the interpretability cost is genuinely disputed. The chapter should name this but not dive in — it is a complete chapter of its own.

**Whether fairness criteria are compatible.** Chouldechova (2017), Kleinberg, Mullainathan, Raghavan (2017) showed that several reasonable fairness criteria — predictive parity, equalized odds, calibration within groups — cannot all be satisfied simultaneously when base rates differ across groups. The chapter need not solve this; it should be honest that "fair classification" is a genuine open problem and the threshold choice is where the impossibility lives.

**Automation-exposure classifications.** This is the most contested area the chapter touches. Frey & Osborne 47%; Arntz-Gregory-Zierahn 9%; Brynjolfsson-Mitchell-Rock "few occupations fully automatable, most have some automatable tasks." Each used O*NET data; each is published in a peer-reviewed venue; each headline number is wildly different. The dispute is not "who is right" — the dispute is what classification *unit* (whole occupations vs. tasks) and what *threshold* are appropriate. This is the chapter's most teachable contest.

### What has changed recently (last 5 years)

- **Large language models as classifiers.** LLMs prompted with zero-shot or few-shot classification instructions now match or exceed fine-tuned baselines for many text-classification problems. This changes what a "classifier" is in 2026 in ways the chapter should mention. It does not change the decision-theoretic framing, but it changes the pipeline.

- **Calibration of LLM outputs is poor.** When LLMs are asked to output probabilities, the numbers are systematically miscalibrated — typically overconfident, and sometimes badly so. This is a 2024–2026 finding in active research [verify primary citations: Kadavath et al. 2022 "Language Models (Mostly) Know What They Know" is foundational; Tian et al. 2023 "Just Ask for Calibration" is a representative follow-up — confirm DOIs before relying on specific claims]. Worth one paragraph in the prompting section: when the student asks an LLM "what is the probability this applicant defaults," the number returned is not a calibrated probability and should not be used as one.

- **Frey & Osborne 47% has not aged well.** The seven years since publication have *not* produced the predicted occupational apocalypse. Some occupations Frey-Osborne flagged as high risk (truck drivers, telemarketers) have grown in employment, not shrunk. The Acemoglu-Restrepo 2020 empirical work suggests automation effects are real but ~1–2 orders of magnitude smaller than Frey-Osborne's worst-case forecasts. The chapter should be honest that the 47% number is the most-cited figure in the literature and also the least-vindicated.

- **The Coelli & Borland critique.** Coelli and Borland (2024), "Behind the Headline Number: Why Not to Rely on Frey and Osborne's Predictions of Potential Job Loss from Automation," SSRN [https://papers.ssrn.com/sol3/papers.cfm?abstract_id=3472764](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=3472764) [verify the date — SSRN papers can have revision histories; the working paper appears to predate 2024]. Methodologically careful pushback on the Frey-Osborne classifier — specifically about training-data labeling, feature selection, and the Gaussian process classifier's uncertainty handling.

- **Generative AI shifted the exposure conversation.** Eloundou, Manning, Mishkin, Rock (2023), "GPTs are GPTs" [arXiv:2303.10130, [https://arxiv.org/abs/2303.10130](https://arxiv.org/abs/2303.10130) — verify], applied an LLM-and-human rubric to O*NET task data and concluded ~80% of U.S. workers could have ≥10% of their work tasks affected by GPT-style models, ~19% could have ≥50%. The pattern of "use O*NET, define exposure, get a headline number" repeats itself. The 2023 paper is on a different generation of automation technology than Frey-Osborne — and produces, predictably, different numbers.

---

## 3. Application Domain Examples

Per TIKTOK.md, Ch 11's domains are **loan-default classification** (primary worked example) and **occupational automation-exposure classification** (the Irreducibly Human series tie-in). Anchor examples:

1. **The TIKTOK.md loan-officer scenario (primary worked example).** Logistic regression on loan-application features (income, credit score, debt-to-income, loan amount). Output: P(default). Threshold choice: 0.5 (default), 0.3 (lenient), 0.7 (strict). Frequentist: report ROC curve and AUC; threshold imported from regulatory or operational convention. Bayesian: posterior over coefficients; posterior predictive probability per applicant; explicit loss function specifying cost of false positive (declined good loan = lost interest income) vs. false negative (approved bad loan = principal loss). Optimal threshold = (cost of false positive) / (cost of false positive + cost of false negative). At 5× cost asymmetry (TIKTOK.md Exercise 2), optimal threshold = 1/6 ≈ 0.167. **Note the size of this gap from the default 0.5.** This is the chapter's "the threshold choice is the decision, and the default is a particular implicit loss function" beat made vivid.

2. **The German Credit dataset with its 5× cost matrix.** UCI's documentation specifies the asymmetric cost — and at that asymmetry, the optimal threshold is ~0.167, not 0.5. This is the worked example to deploy if the author wants to ground Exercise 2 in a real dataset with a published cost matrix rather than a synthesized one.

3. **The LendingClub portfolio.** Larger and noisier than German Credit; behaves like real industrial data. Charge-off rates (the realized default rate) are documented in LendingClub's own quarterly reports through 2020. Fit for the primary worked example if the author wants scale.

4. **Frey-Osborne automation-exposure replication (TIKTOK.md Exercise 3).** Student downloads the O*NET database, selects content-model features (Manual Dexterity, Finger Dexterity, Originality, Persuasion, Social Perceptiveness, Negotiation, Assisting and Caring for Others — the seven "bottleneck" features Frey-Osborne identified), fits a logistic regression to predict above/below median automation exposure (the median is the threshold; the chapter could ask the student to vary it). Compare to Frey-Osborne's Gaussian process classifier results. Discussion: at what threshold is this exercise's answer stable? Where does the loss function live in this exercise — what cost is the student implicitly minimizing?

5. **A medical-diagnosis sidebar.** Cancer screening with a known asymmetric cost (false negative = missed cancer, very high cost; false positive = unnecessary biopsy, lower cost). Eddy (1982) — the classic "doctors-can't-do-Bayes" paper — sets up the same kind of arithmetic at a different scale. Not the chapter's core example but a useful one-paragraph callback to Chapter 0/1's medical-test material.

6. **A fraud-detection sidebar.** Credit-card fraud detection runs at thresholds far below 0.5 — most banks flag transactions at posterior probabilities in the 0.05–0.10 range because the cost of a missed fraud is much higher than the cost of an inconvenienced cardholder. The threshold *is* the operational decision; the model just sorts the cases.

---

## 4. The Book's Thesis Connection

The book's thesis is that statistical inference should be taught through side-by-side comparison with the reader choosing. Ch 11 is where the Bayesian framework's structural advantage becomes operationally visible — not because the parameter estimates differ from the frequentist version (they typically don't, for credit-scoring datasets with thousands of cases), but because the *decision-theoretic apparatus* is built in.

**The asymmetry rule named in §35 of the book spec is doing real work here, and the chapter should name it explicitly (as the spec requires).** The frequentist solution is one paragraph: fit, get AUC, pick a threshold from operational convention. The Bayesian solution is several pages: fit, get posterior, define loss function, derive optimal threshold, propagate parameter uncertainty into threshold uncertainty. The chapter spends more space on the Bayesian side because the Bayesian side does more. The chapter is honest about this.

**This is the chapter where the implicit-loss-function move becomes a teaching weapon.** A threshold of 0.5 is *not* neutral. It is the threshold optimal under the assumption that false positives and false negatives are equally costly. For loan decisions, they aren't. For medical diagnoses, they aren't. For automation-exposure flagging, they aren't. The chapter's central pedagogical move is: a student who reads "the model predicts above-median automation exposure when P > 0.5" should now reflexively ask "above-median by what loss function?" before reading the next sentence. That is the capability the chapter installs.

**The connection to the Irreducibly Human series (TIKTOK.md lines 981–986) is structural, not decorative.** The Irreducibly Human series is built around questions about what work humans will still do as AI capabilities expand. Every paper in that conversation — Frey-Osborne, Arntz-Gregory-Zierahn, Brynjolfsson-Mitchell-Rock, Eloundou et al. — is, formally, a classification problem with a threshold. Different thresholds produce different headlines. Different loss functions produce different policy recommendations. The series cannot be read intelligently without Ch 11's apparatus, and Ch 11 cannot land its synthesis without the series's stakes. They depend on each other.

**Where the chapter must not overclaim.** Logistic regression's parameter estimates are essentially identical between frequentist and Bayesian framings for the loan-default datasets students will see. The chapter should say this. The Bayesian advantage is not "more accurate." It is "you get parameter uncertainty propagated into decision uncertainty without extra work." That is the honest claim.

---

## 5. Intellectual Lineage Notes

**David R. Cox (1924–2022).** The Cox of logistic regression and of Cox proportional-hazards. *The Regression Analysis of Binary Sequences* (1958) is the source paper. Cox was, by reputation, a frequentist with strong taste for likelihood-based methods. The chapter can note that the model itself is framework-neutral — the Bayesian version of logistic regression uses the same likelihood Cox specified, with a prior on the coefficients. Cox's 2006 *Principles of Statistical Inference* (Cambridge UP, ISBN 978-0-521-68567-2) discusses Bayesian and non-Bayesian inference together with characteristic clarity; cite as background.

**Abraham Wald (1902–1950).** *Statistical Decision Functions* (1950). The frequentist decision-theory framework — state space, decision function, risk function, admissibility, minimax — that Berger's Bayesian version is positioned against. Wald died young (plane crash) before fully developing the framework; the apparatus has carried his name for 75 years. The chapter can mention him once. Decision theory's intellectual scaffold begins with him.

**James O. Berger (b. 1950).** *Statistical Decision Theory and Bayesian Analysis* (2nd ed., 1985). The canonical Bayesian decision-theory text. Berger's framing — Bayes risk = E_θ[loss(decision(data), θ)], with the optimal decision minimizing posterior expected loss — is the chapter's mechanism. Berger is at Duke; his text has been the graduate Bayesian decision-theory reference since the 1980s.

**Frey & Osborne and the automation-exposure literature.** Carl Benedikt Frey (Oxford Martin School) and Michael Osborne (Oxford Engineering Science). The 2013 working paper version of "Future of Employment" went viral before the 2017 journal version appeared; the methodology was the same. The Arntz-Gregory-Zierahn 2016 OECD response is the methodologically careful pushback. Brynjolfsson-Mitchell-Rock 2018 is the alternative rubric. Acemoglu-Restrepo 2020/2022 are the empirical follow-up. Eloundou-Manning-Mishkin-Rock 2023 (the OpenAI/U Penn "GPTs are GPTs" paper) is the LLM-era version of the same classification exercise.

**For classification fairness/threshold lineage.** Hardt-Price-Srebro 2016 (NeurIPS) introduced "equalized odds." Chouldechova 2017 (FATML; arXiv:1610.07524 [verify]) and Kleinberg-Mullainathan-Raghavan 2017 (ITCS; arXiv:1609.05807 [verify]) proved the incompatibility theorems. This is a 2016–2018 burst of foundational work; the chapter does not need to teach it in depth but should cite Hardt-Price-Srebro once in the synthesis.

---

## 6. Pedagogical Delivery Research

### Prior knowledge required

The chapter assumes the reader knows: linear regression and likelihood-based estimation (Chs 5–9 of this book), prior/posterior mechanics (Chs 4–6), the comparison move (Chs 1–10), and basic decision-theoretic vocabulary (action, state, loss — likely introduced in Ch 7 of this book). New: the idea that *the threshold is part of the system, not separate from it*; the explicit loss-function framing; the calibration concept.

### Common misconceptions in undergraduates

**1. Leaving the threshold choice implicit.** The dominant pedagogical failure in undergraduate classification teaching. Students report "the model achieves 87% accuracy" without noting that accuracy *depends on* the threshold (almost always 0.5 by software default), and that 0.5 is the optimal threshold only under the implicit assumption that false positives and false negatives are equally costly. The chapter's central teaching task is to make this implicit choice visible. Hand 2009 documents this failure mode in the credit-scoring literature; the same failure shows up in every undergraduate classification assignment with no cost-matrix specification.

**2. Treating "accuracy" as the metric.** Accuracy is a meaningful number only when the class proportions are roughly balanced *and* the costs of the two error types are roughly symmetric. For loan defaults (typical default rate 5–15%), accuracy is dominated by the majority class. A model predicting "no default" for every loan achieves 85–95% accuracy and is useless. The chapter should hit this on page 1 of the loan example.

**3. Treating AUC as the metric.** Better than accuracy because it is threshold-independent; still problematic because it implicitly weights all parts of the ROC curve equally, including regions of the threshold space the operational system would never visit. Hand 2009's H-measure is the response. The chapter can note this without teaching H-measure in detail — the point is that "we report AUC" is not a complete classifier evaluation.

**4. Confusing P(default | features) with P(features | default).** The Ch 0 inverse fallacy returns. A logistic regression outputs the former. A naive Bayes classifier computes the latter and inverts it. Students sometimes mix these up. The chapter should re-anchor this once.

**5. Treating coefficient signs as causal.** A positive coefficient on "debt-to-income ratio" means *predictive of default*, not *causes default*. The Pearl framing (Chs 3, 8 of this book) belongs in the misconception list explicitly — the loan example is the canonical place to remind the student that classification models predict, they do not explain.

**6. Forgetting that the LLM's stated probability is not calibrated.** Specific to this book's LLM-implementation thesis. When a student prompts Claude or GPT-5 with "what is the probability this loan defaults" and gets back "0.32," the 0.32 is not a calibrated probability. The chapter must teach this explicitly.

### Instructional sequences that work

The standard sequence in undergraduate classification teaching: (1) frame the binary outcome, (2) fit logistic regression, (3) inspect coefficients, (4) compute predicted probabilities, (5) choose a threshold, (6) build a confusion matrix, (7) compute metrics, (8) plot ROC. This is the workflow in Hyndman & Athanasopoulos (regression chapter), James-Witten-Hastie-Tibshirani *Introduction to Statistical Learning*, and every introductory statistics curriculum.

What Ch 11 should *add* to this sequence: between step 4 and step 5, **define the loss function explicitly**. The threshold is derived from the loss function and the posterior, not chosen by intuition. This single insertion is the chapter's core pedagogical move.

For the Bayesian sequence: (1) frame the binary outcome, (2) specify weakly informative priors on coefficients (Gelman et al. 2008's Cauchy prior is the standard default; cite explicitly), (3) fit (Stan, PyMC, or `brms` for R), (4) inspect posterior distributions on coefficients, (5) compute posterior predictive probability per applicant, (6) define loss function, (7) derive optimal threshold, (8) propagate parameter uncertainty into threshold uncertainty (the posterior on the optimal threshold given the posterior on the parameters).

### Known teaching failure modes

- **Demanding cost matrices students can't justify.** If the chapter requires students to specify dollar costs of false positives and false negatives without giving them any data to anchor the numbers, the exercise becomes "what number sounds reasonable." Worse than useless. The German Credit dataset's published 5× cost matrix and the LendingClub charge-off rate / loan principal data are the anchors. The exercise should provide them.
- **Confusing classification probability with calibration.** A model can output probabilities that are *discriminative* (high P for actual positives, low for actual negatives) but *miscalibrated* (the actual frequency of positives among predictions of P=0.7 is 0.5). Calibration plots are the diagnostic. The chapter should include one.
- **Treating Bayesian = automatic fairness.** Bayesian classifiers are not automatically fair across groups. Adding a prior on group-specific parameters can help or hurt depending on the data. The chapter should mention this honestly.

### The Hand 2009 connection

Hand's paper is worth more than a citation — it is a complete pedagogical model for what the chapter wants to teach. Hand's argument: AUC is incoherent because it integrates cost distributions over a range no actual decision-maker faces; the H-measure fixes this by making the cost distribution explicit. The chapter could profitably mirror Hand's structure: "the standard practice [reporting AUC, using threshold 0.5] is incoherent; the fix is to make the loss function explicit." Hand wrote it for machine-learning researchers; Ch 11 writes it for undergraduates.

---

## 7. Representation and Display Research

### The side-by-side comparison table from TIKTOK.md

TIKTOK.md does not include an explicit table for Ch 11; the §35 chapter-anatomy template is the source. Synthesizing from the chapter brief:

| **Dimension** | **Frequentist Logistic Regression** | **Bayesian Logistic Regression** |
|---|---|---|
| **Inputs** | Features X, binary outcome Y | Features X, binary outcome Y, priors on coefficients |
| **Estimation** | Maximum likelihood (IRLS) | MCMC sampling of posterior |
| **Output: coefficients** | Point estimates with Wald standard errors | Full posterior distributions |
| **Output: probability per case** | Point estimate of P(Y=1 \| X) | Posterior distribution of P(Y=1 \| X) |
| **Threshold choice** | Imported from outside (default 0.5; sometimes operationally tuned) | Derived from explicit loss function and posterior |
| **Threshold uncertainty** | Not handled | Posterior on the optimal threshold given parameter uncertainty |
| **Standard metrics** | Accuracy, precision, recall, AUC | Same metrics + posterior-predictive checks + Bayes risk |
| **Regulatory acceptance (credit, medical)** | Long-established, well-understood | Less standard but increasing |
| **Cost** | Milliseconds | Seconds to minutes |
| **When it wins** | Large *n*, low parameter uncertainty, standardized reporting | Small *n*, asymmetric costs, decision-theoretic framing needed |

**One row I would add: Calibration.**

| **Calibration** | Not assessed by default; logistic regression is reasonably well-calibrated at large *n* | Posterior predictive checks built into the workflow; miscalibration visible in posterior predictive plots |

This row matters because the chapter's central pedagogical move — making the loss function explicit — is only sound if the model's output is a calibrated probability. A miscalibrated probability fed into an explicit loss-function calculation produces a confidently-wrong threshold. The standard side-by-side table omits this dimension; including it makes the chapter's argument honest.

### Visualizations the chapter should plan for

- **ROC curve with threshold markers.** Standard. Mark the 0.5, 0.3, 0.7 thresholds from Exercise 1 directly on the curve. The student sees that threshold choice is a *position* on the curve, not a parameter of the curve.
- **Cost curves / cost-benefit plots.** For different cost ratios (1:1, 1:5, 1:10), plot total expected cost as a function of threshold. The minimum of each curve is the optimal threshold for that cost ratio. One picture shows the entire chapter's argument.
- **Calibration plot.** Predicted probability bins on the x-axis, observed frequency on the y-axis, 45° line for perfect calibration. Use this to demonstrate miscalibration in a deep-learning baseline if the chapter takes that detour.
- **Posterior plots for coefficients.** Standard Bayesian diagnostic. Density curves with credible interval markers. Show the student what "we have parameter uncertainty" looks like as a picture, not just a number.
- **The automation-exposure scatter.** O*NET occupations plotted on (manual dexterity, originality) axes, colored by Frey-Osborne classification, with the decision boundary drawn at multiple thresholds. The student sees the threshold sweep through the occupational map.

---

## 8. Open Questions and Research Gaps

- **The "above-median automation exposure" framing in TIKTOK.md Exercise 3 is underspecified.** "Median" of what? Of the Frey-Osborne probability scores? Of an O*NET-derived composite the student constructs? The author should pin this in the exercise — my recommendation is to have the student compute a Frey-Osborne-style score from O*NET features and then ask which threshold (median of the score? top quartile? 0.7 like Frey-Osborne?) makes sense and why.

- **The 5× cost ratio in TIKTOK.md Exercise 2 is plausible but not sourced.** The German Credit dataset uses 5× explicitly. Real bank cost ratios are not public; they are estimated from charge-off rates and lost-interest income, which vary by loan grade. The author can either ground the 5× in the German Credit documentation or note that it is a teaching simplification.

- **Whether to teach calibration explicitly or leave it for Ch 12.** Calibration is essential for the chapter's loss-function argument to land cleanly. It is also conceptually new for the student. My recommendation: include a one-page calibration sidebar inside Section 3 (deep-dive) rather than letting the topic drift to Ch 12.

- **The automation-exposure literature is moving fast.** Eloundou et al. 2023 (GPT exposure), the Acemoglu-Restrepo follow-ups, and 2025–2026 LLM-impact studies will continue to appear. The chapter's safest move is to use Frey-Osborne 2017, Arntz-Gregory-Zierahn 2016, and Brynjolfsson-Mitchell-Rock 2018 as the three-cornered foundational comparison and treat the newer LLM-exposure studies as "the same classification problem on different technology," not as primary citations. This insulates the chapter from rapid obsolescence.

- **Sources likely to age within 3 years.** Cox 1958, Wald 1950, Berger 1985, Hand & Henley 1997, Hand 2009, Guo et al. 2017, Hardt et al. 2016: not at risk. Frey-Osborne 2017 and the rest of the automation-exposure cluster: high aging risk in their *headline numbers* (the 47% in particular looks worse every year), low aging risk in the *methodological point* the chapter uses them for. The chapter should cite Frey-Osborne for the *method* (build a classifier from O*NET features, pick a threshold, report an employment-weighted share) and be explicit that the headline number has not been borne out by subsequent evidence.

- **LLM calibration research.** Most claims here are 2022–2026 and changing rapidly. The chapter should keep the prompting-section discussion of LLM calibration tight and date-stamped rather than presenting any specific result as durable.

- **The fairness literature.** The 2016–2018 impossibility results are stable. The 2020–2026 work on contextual fairness, individual fairness, and procedural fairness is still moving. The chapter should cite Hardt-Price-Srebro once and not try to summarize the broader fairness literature.

---

## 9. Sourcing Notes

- **Cox 1958.** Paywalled at Wiley/Oxford. Citation well-established; do not need to quote directly. Open landing page describes the contents adequately.
- **Wald 1950.** Out of print as a primary book; widely cited from secondary sources. Citation only.
- **Berger 1985.** Paywalled Springer book. Free Internet Archive scans circulate. Cite as lineage; do not quote directly.
- **Hand & Henley 1997.** Open PDF at SFU mirror, paywalled at Oxford Academic. The SFU PDF is fine for the chapter's purposes.
- **Hand 2009.** Open PDF at Case Western mirror; paywalled at Springer. The Case Western PDF is fine.
- **Guo et al. 2017.** Open on arXiv and on the PMLR proceedings site. Free.
- **Hardt-Price-Srebro 2016.** Open on arXiv and NeurIPS proceedings. Free.
- **Frey & Osborne 2017.** Open at Oxford Martin School and elsewhere; the *Tech Forecasting & Social Change* version is paywalled but the working PDF is the same content. Cite the open PDF.
- **Arntz-Gregory-Zierahn 2016.** Open at OECD. Free.
- **Brynjolfsson-Mitchell-Rock 2018.** Open at MIT DSpace; AEA landing free for the abstract. Cite the MIT mirror.
- **Acemoglu & Restrepo 2020.** NBER WP open; JPE version paywalled. Cite the NBER PDF.
- **Acemoglu & Restrepo 2022.** Open at MIT economics; *Econometrica* paywalled. Cite the MIT mirror.
- **LendingClub data.** Free with Kaggle account. Pin a specific version in the companion-website materials.
- **German Credit data.** Free at UCI Machine Learning Repository. Verify the URL is current before publication.
- **O*NET database files.** Public domain, free download at onetcenter.org. Quarterly-updated; pin a specific version (e.g., O*NET 28.0 or whatever is current at publication) for reproducibility.
- **BLS OEWS.** Public domain, free download at bls.gov.

Fact-checking gaps flagged `[verify]` above: (a) Gelman et al. 2008 Annals of Applied Statistics DOI for the weakly-informative-prior paper, (b) Ovadia et al. 2019 and Minderer et al. 2021 specifics for the calibration follow-ups, (c) Tian et al. 2023 "Just Ask for Calibration" specifics, (d) Kadavath et al. 2022 "Language Models (Mostly) Know What They Know" specifics, (e) Eloundou et al. 2023 "GPTs are GPTs" arXiv link, (f) Chouldechova 2017 and Kleinberg-Mullainathan-Raghavan 2017 arXiv specifics, (g) Coelli & Borland date (SSRN paper has revision history; the 2024 dating is approximate). These flags do not block the chapter — the foundational sources are well-pinned — but the LLM-calibration and fairness-impossibility citations should be confirmed by Nik or a research assistant before publication.
