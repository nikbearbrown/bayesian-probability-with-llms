# Research: Chapter 08 — When Data Is Sparse
## Bayesian Probability with LLMs

**Chapter one-line:** Small samples, rare events, and underpowered studies — where frequentist methods break down, produce inflated estimates, or simply refuse to run, and where Bayesian priors do their most important work.
**Research date:** 2026-05-13

---

## 1. Primary Sources

### Foundational papers and texts

- **Stein, C. (1956). "Inadmissibility of the Usual Estimator for the Mean of a Multivariate Normal Distribution."** *Proceedings of the Third Berkeley Symposium on Mathematical Statistics and Probability*, Vol. 1, 197–206. University of California Press. Open-access via Project Euclid: [https://projecteuclid.org/ebooks/berkeley-symposium-on-mathematical-statistics-and-probability/Proceedings-of-the-Third-Berkeley-Symposium-on-Mathematical-Statistics-and/chapter/Inadmissibility-of-the-Usual-Estimator-for-the-Mean-of-a/bsmsp/1200501656](https://projecteuclid.org/ebooks/berkeley-symposium-on-mathematical-statistics-and-probability/Proceedings-of-the-Third-Berkeley-Symposium-on-Mathematical-Statistics-and/chapter/Inadmissibility-of-the-Usual-Estimator-for-the-Mean-of-a/bsmsp/1200501656). PDF mirror at Yale: [http://www.stat.yale.edu/~hz68/619/Stein-1956.pdf](http://www.stat.yale.edu/~hz68/619/Stein-1956.pdf). The original proof that, in three or more dimensions, the sample mean is *inadmissible* under squared-error loss — there is always an estimator that dominates it. The estimator that does the dominating shrinks the sample means toward a common point. This is the mathematical bedrock under "shrinkage as regularization." For Ch 8 the citation is a sidebar, not the main argument; the chapter teaches shrinkage by example, not by inadmissibility theorem.

- **James, W. and Stein, C. (1961). "Estimation with quadratic loss."** *Proceedings of the Fourth Berkeley Symposium on Mathematical Statistics and Probability*, Vol. 1, 361–379. The James-Stein estimator made explicit. The closed-form shrinkage factor (1 − (k−2)σ²/‖x‖²) is what the chapter can show in one line and trace to the original paper. [verify exact pages — citation widely reproduced; primary scan less consistently online].

- **Efron, B. and Morris, C. (1975). "Data Analysis Using Stein's Estimator and Its Generalizations."** *Journal of the American Statistical Association*, 70(350), 311–319. DOI: [https://doi.org/10.1080/01621459.1975.10479864](https://doi.org/10.1080/01621459.1975.10479864). Tandfonline landing: [https://www.tandfonline.com/doi/abs/10.1080/01621459.1975.10479864](https://www.tandfonline.com/doi/abs/10.1080/01621459.1975.10479864). The 18-baseball-players-1970 dataset enters the canon here: midseason batting averages predict end-of-season batting averages better when shrunk toward the league mean than when used raw. The dataset is reproduced in R (`pscl::EfronMorris`): [https://vincentarelbundock.github.io/Rdatasets/doc/pscl/EfronMorris.html](https://vincentarelbundock.github.io/Rdatasets/doc/pscl/EfronMorris.html). For Ch 8: this is the *teaching* citation. Numbers concrete, mechanism visible.

- **Efron, B. and Morris, C. (1977). "Stein's Paradox in Statistics."** *Scientific American*, 236(5), 119–127. Author-hosted PDF: [https://efron.ckirby.su.domains/other/Article1977.pdf](https://efron.ckirby.su.domains/other/Article1977.pdf). The popular-audience version of the 1975 paper. Useful as the introductory pointer in Ch 8 for a student who wants the historical and conceptual story before the math. Written exactly at the register Ch 8 is aiming for.

- **Capen, E. C., Clapp, R. V. and Campbell, W. M. (1971). "Competitive Bidding in High-Risk Situations."** *Journal of Petroleum Technology*, 23(6), 641–653. DOI: [https://doi.org/10.2118/2993-PA](https://doi.org/10.2118/2993-PA). [verify DOI — paper is widely cited but primary SPE landing is paywalled; secondary descriptions confirm publication venue and dates]. Three petroleum engineers at ARCO noticed that the firms winning offshore drilling leases in the Gulf of Mexico were systematically losing money. They named the mechanism: when n bidders estimate the value of an uncertain asset, the highest bid is, in expectation, an overestimate. The winner *is the one who most overestimated*. This is the deepest historical root of what statisticians later called the winner's curse and what Gelman now calls Type M error. For Ch 8: the origin-story footnote that grounds the chapter's signature claim.

- **Button, K. S., Ioannidis, J. P. A., Mokrysz, C., Nosek, B. A., Flint, J., Robinson, E. S. J. and Munafò, M. R. (2013). "Power failure: why small sample size undermines the reliability of neuroscience."** *Nature Reviews Neuroscience*, 14, 365–376. DOI: [https://doi.org/10.1038/nrn3475](https://doi.org/10.1038/nrn3475). PubMed: [https://pubmed.ncbi.nlm.nih.gov/23571845/](https://pubmed.ncbi.nlm.nih.gov/23571845/). Erratum: [https://www.nature.com/articles/nrn3502](https://www.nature.com/articles/nrn3502). The empirical headline number: median statistical power across neuroscience subfields was estimated at 8–31%. Three consequences are spelled out: low probability of detecting true effects, low probability that a significant result is a true positive (positive predictive value), and — directly — *inflation of effect sizes that do reach significance*. This is the canonical source for Ch 8's winner's-curse-in-research-publication claim. Required citation.

- **Ioannidis, J. P. A. (2008). "Why Most Discovered True Associations Are Inflated."** *Epidemiology*, 19(5), 640–648. DOI: [https://doi.org/10.1097/EDE.0b013e31818131e7](https://doi.org/10.1097/EDE.0b013e31818131e7). [verify access — Epidemiology paper is at LWW, often paywalled; PubMed PMID 18633328]. The cleanest single-paper statement of the winner's curse in observational epidemiology: among studies that report significant associations, the magnitudes are systematically larger than the true magnitudes, by an amount that depends on the study's power. Useful for Ch 8 because the language ("inflation") is the language the chapter wants.

- **Trikalinos, T. A. and Ioannidis, J. P. A. (2005). "Effect sizes in cumulative meta-analyses of mental health randomized trials evolved over time."** *Journal of Clinical Epidemiology*, 58(11), 1124–1130. The "decline effect" paper: across cumulative meta-analyses, the first published studies on a given association tend to report larger effects than the body of later, larger studies that follow. Mechanism is identical to the winner's curse: small early studies that reach significance do so partly because of an unusually large observed effect. [verify exact volume/issue/pages — citation appears in multiple downstream reviews but the primary landing was not directly opened in this research session].

- **Gelman, A. and Carlin, J. (2014). "Beyond Power Calculations: Assessing Type S (Sign) and Type M (Magnitude) Errors."** *Perspectives on Psychological Science*, 9(6), 641–651. DOI: [https://doi.org/10.1177/1745691614551642](https://doi.org/10.1177/1745691614551642). PubMed: [https://pubmed.ncbi.nlm.nih.gov/26186114/](https://pubmed.ncbi.nlm.nih.gov/26186114/). Author PDF: [https://sites.stat.columbia.edu/gelman/research/published/retropower_final.pdf](https://sites.stat.columbia.edu/gelman/research/published/retropower_final.pdf). Two new error types named: **Type S** (the probability the significant estimate has the wrong sign) and **Type M** (the *exaggeration ratio* — the expected magnitude of a significant estimate divided by the true magnitude). For Ch 8, Type M is the operational definition of "winner's curse." This was likely cited in the Ch 4 research notes as well; cross-reference.

- **Hanley, J. A. and Lippman-Hand, A. (1983). "If nothing goes wrong, is everything all right? Interpreting zero numerators."** *JAMA*, 249(13), 1743–1745. PDF via McGill: [http://www.medicine.mcgill.ca/epidemiology/hanley/reprints/If_Nothing_Goes_1983.pdf](http://www.medicine.mcgill.ca/epidemiology/hanley/reprints/If_Nothing_Goes_1983.pdf). The "rule of three" — if zero events occur in n independent trials, the 95% upper bound for the event rate is approximately 3/n. This is the cleanest frequentist answer to "what should the hospital say when they had zero complications?", and it is exactly the question Ch 8's hospital scenario abuts. Useful as a contrast to the Bayesian posterior: 3/n is a confidence bound; the Bayesian gives you the full posterior distribution over rates.

- **Gelman, A. and Tuerlinckx, F. (2000). "Type S error rates for classical and Bayesian single and multiple comparison procedures."** *Computational Statistics*, 15(3), 373–390. The Type S concept first appears here. [verify access — Springer link likely paywalled]. Optional historical pointer for the Type S/M lineage.

### Key empirical cases

- **The Efron-Morris baseball data (1970, 18 players, first 45 at-bats).** Reproducible in R via the `pscl` package; documentation at [https://vincentarelbundock.github.io/Rdatasets/doc/pscl/EfronMorris.html](https://vincentarelbundock.github.io/Rdatasets/doc/pscl/EfronMorris.html). The chapter can run the James-Stein vs. raw-average vs. shrink-to-mean comparison live on the page in 20 lines of code, then ask the reader to do the same thing with a Beta(α, β) prior. Ideal worked example because the "true" values (end-of-season averages) are known.

- **ACS National Surgical Quality Improvement Program (NSQIP).** Program overview: [https://www.facs.org/quality-programs/data-and-registries/acs-nsqip/](https://www.facs.org/quality-programs/data-and-registries/acs-nsqip/). NSQIP collects 135 preoperative-through-30-day-postoperative variables across 700+ hospitals and is the source for the kinds of complication-rate numbers Ch 8's hospital scenario invokes. The published evaluations — e.g., the meta-analysis of NSQIP risk calculator predictive accuracy at [https://www.sciencedirect.com/science/article/pii/S2666262024000056](https://www.sciencedirect.com/science/article/pii/S2666262024000056) — give realistic baseline rates the chapter can use to construct a Beta prior with named provenance (rather than the TIKTOK.md placeholder Beta(3, 200)). Worth a 2-sentence footnote on why NSQIP exists and why the 30-day window matters.

- **The Bayesian rare-events meta-analysis literature.** Günhan et al. (2020) "Random-effects meta-analysis of few studies involving rare events" and Pateras et al. (2018) on Bayesian beta-binomial models for rare-event meta-analysis ([https://pubmed.ncbi.nlm.nih.gov/37607885/](https://pubmed.ncbi.nlm.nih.gov/37607885/)). The medical-statistics community has converged on Bayesian beta-binomial as the standard rare-event tool. For Ch 8 this is the "this is not a toy example, the field actually does this" footnote.

---

## 2. The Core Concept — State of the Field

### What is settled

Three propositions are not in serious dispute. **First**, with binomial counts and small n, the normal approximation to the proportion test fails. The exact (Clopper-Pearson) and Wilson intervals exist and are widely available, but they remain wide; a 3/200 observation gives a 95% CI of roughly [0.003, 0.043], which is mathematically correct and operationally useless. The frequentist sparsity problem is real and not a Bayesian invention.

**Second**, the winner's curse exists as a mathematical fact, not a sociological claim. If true effect size is θ and observed effect size from a single study is θ̂ = θ + ε with noise ε, then conditional on |θ̂| > threshold, E[θ̂] > θ. The selection on significance produces inflation. This is provable, has been demonstrated in simulation across statistical methods, and is reproduced empirically every time large-scale replications are run (Open Science Collaboration 2015 *Science*; Camerer et al. 2018 *Nature Human Behaviour* — verify, both are real but DOIs need checking).

**Third**, Bayesian inference with an informative prior produces tighter intervals than the corresponding frequentist procedure with the same likelihood. The cost is that the prior is now part of the answer. Whether the cost is worth the tighter interval depends on whether the prior is defensible — which is where the disagreement lives.

### What is disputed

Two real disagreements.

**Where do priors come from?** In the surgical-complication case, "use the published literature on this procedure type" sounds reasonable until you ask whose literature, weighted how, and whether the literature itself suffers from publication bias (in which case the prior may encode the same winner's curse the Bayesian analysis is supposed to correct for). The Bayesian view: explicit priors are always better than implicit ones, and you can do sensitivity analysis. The frequentist view: an explicit defensible prior is rarely available; calling the data sparse is honest, calling the data sparse-but-here-is-our-guess is hand-waving. Both views have force.

**Is sparse-data shrinkage bias or regularization?** The frequentist usage of "biased estimator" treats any departure from unbiasedness as a defect. Stein's result (1956) is the technical refutation: unbiased estimators of a multivariate normal mean are dominated by biased ones in dimensions ≥3. The Bayesian view recasts the trade: a small amount of bias in exchange for a large reduction in variance is regularization, not error. Modern frequentist practice (penalized regression, ridge, lasso) has adopted the same machinery without using the word "Bayesian." But the philosophical disagreement persists at the level of "what is the estimator *for*?"

### What has changed recently (last 5 years)

The replication crisis has moved the winner's curse from a statistical curiosity into the operational vocabulary of meta-science. As of 2024 the term "Type M error" is standard in psychology and clinical research methods courses (Gelman & Carlin 2014 above). The Open Science Framework and the registered-report format are direct institutional responses: preregistration neutralizes selection on significance, which is what produces the inflation.

Computationally, Bayesian rare-event analysis has become reproducible-by-default. `brms` and `Stan` produce posterior distributions over Beta(α, β) parameters in seconds; the bottleneck used to be code, and the bottleneck is now choosing the prior. This shifts the pedagogical center of Ch 8 from "how to compute" to "how to defend the prior."

---

## 3. Application Domain Examples

The chapter's anchor case — 3 complications in 200 procedures — sits inside a real domain. Three points to make concrete:

**Hospital accreditation thresholds are typically stated as fixed numbers.** The Joint Commission, CMS Hospital Compare, and state-level surgical quality programs frequently use complication-rate thresholds of the form "your rate must be below X%." A 95% CI of [0.3%, 4.3%] crossing a 2% threshold is operationally ambiguous in a way the frequentist framework cannot resolve. The Bayesian posterior, given a defensible prior, returns *the probability* the true rate is below 2% — which is exactly the input an accreditation committee needs. This is the strongest pedagogical case for Bayesian methods in the chapter.

**Rare-event meta-analysis is now standard in surgical research.** The Cochrane Collaboration's *Handbook* §16.9.4 explicitly addresses zero-event studies ([https://handbook-5-1.cochrane.org/chapter_16/16_9_4_confidence_intervals_when_no_events_are_observed.htm](https://handbook-5-1.cochrane.org/chapter_16/16_9_4_confidence_intervals_when_no_events_are_observed.htm)). The recommended approach is either continuity correction (frequentist) or Bayesian beta-binomial with an informative or weakly informative prior. The fact that the gold-standard evidence synthesis institution recommends Bayesian methods for this problem is worth a sentence.

**Pharmacovigilance is the other obvious example.** Adverse-event detection in post-market drug surveillance is a sparse-data problem by construction: a 1-in-10,000 adverse event will not appear in a 3,000-person trial. FDA Sentinel and the WHO VigiBase both use Bayesian shrinkage estimators (the IC and GPS algorithms) for adverse-event signal detection. [verify — FDA and WHO documentation on these methods is publicly available; landing pages need direct checking].

---

## 4. The Book's Thesis Connection

The book's central claim is that the two frameworks are tools and the reader should pick. Chapter 8 is the chapter where the Bayesian tool earns the asymmetry the book has been advertising. Three threads converge here.

**The winner's curse is a frequentist failure mode that the Bayesian framework partially fixes — but only partially.** Bayesian shrinkage toward a sensible prior reduces the inflation, but it does not eliminate selection on significance, and it does not protect against bad priors. The honest comparison is not "Bayesian wins"; it is "frequentist methods report inflated estimates as if they were unbiased; Bayesian methods report shrunk estimates and require you to defend the shrinkage target." The chapter should pose the trade in those terms.

**This is the first chapter where the prior does serious work the data cannot do alone.** In chapters 1–7 the prior either was uniform (and the posterior was close to the likelihood) or could be defended on first principles. Here, with three events in 200 procedures, the prior is doing roughly half of the inferential work. The student needs to *see* that.

**This is the chapter where the LLM tool earns a specific kind of use.** Translating a published reported "mean and 95% CI" into Beta(α, β) parameters is moment-matching arithmetic; an LLM does it competently. Verifying that the resulting Beta has the right shape against the source claim is a check the student can do by hand. This is the chapter where the LLM is most clearly *implementing*, not *deciding*.

---

## 5. Intellectual Lineage Notes

**Winner's curse lineage.** Capen, Clapp & Campbell 1971 in the oil-bidding context → Thaler 1988 (*Journal of Economic Perspectives*, "Anomalies: The Winner's Curse"; open at [https://pubs.aeaweb.org/doi/pdf/10.1257/jep.2.1.191](https://pubs.aeaweb.org/doi/pdf/10.1257/jep.2.1.191)) → Ioannidis & Trikalinos 2005 and Ioannidis 2008 (the medical-research framing) → Button et al. 2013 (the neuroscience headline) → Gelman & Carlin 2014 (Type M as the operational name). The chapter can run this lineage in a single paragraph: same mathematical structure under five different names, applied to oil leases, baseball, drug trials, and brain-imaging studies.

**Shrinkage lineage.** Stein 1956 (the inadmissibility result) → James & Stein 1961 (the closed-form estimator) → Efron & Morris 1975 (the baseball application that made it concrete) → Efron & Morris 1977 *Scientific American* (the popular exposition) → Lindley & Smith 1972 and forward (the explicit Bayesian re-derivation as a hierarchical model). Ch 8 stops at the first half of this chain; Ch 9 picks up the second half. The intellectual continuity is the book's strongest single argument that frequentist regularization and Bayesian hierarchy are different vocabularies for the same machinery.

**Reflexive note.** Both lineages are tools, not authorities. Stein's theorem doesn't apply to one-dimensional problems; the chapter should note that the 3/200 surgical example is one-dimensional, so the dominating-estimator argument doesn't formally apply. What does apply — and is what the chapter is really teaching — is the Bayesian re-derivation: a Beta prior on a single probability produces shrinkage by the same mechanism, even in one dimension. Be clean about what Stein 1956 does and does not buy.

---

## 6. Pedagogical Delivery Research

**Base-rate neglect is the most documented obstacle.** Kahneman & Tversky's representativeness-heuristic research (1972, 1973) established that undergraduates systematically ignore base rates when a vivid case description is available. The mammography problem (Eddy 1982) — even physicians solve it correctly at roughly 10–15% — is the canonical evidence. Gigerenzer & Hoffrage 1995 showed natural-frequency framing ("10 out of 1,000") dramatically improves performance over probability framing ("1%"). For Ch 8, this matters because the chapter's prior is a base rate, and student resistance to using base rates is the obstacle the chapter has to overcome. Suggested move: present the prior as "out of every 1,000 similar surgeries reported in the literature, about 15 had complications" before showing it as Beta(15, 985).

**Underpowered-study illiteracy is the second documented obstacle.** Most undergraduates have never been taught what statistical power is, let alone how to estimate it. A study by Hoekstra et al. (2014) — "Robust misinterpretation of confidence intervals" ([https://link.springer.com/article/10.3758/s13423-013-0572-3](https://link.springer.com/article/10.3758/s13423-013-0572-3); verify) — found even researchers with statistical training systematically misinterpret confidence intervals. The chapter should not assume the reader knows what "power = 0.20" means; it should *show* the consequence (Type M ratio of ~3) and let the consequence motivate the concept.

**Suggested pedagogical move: run the simulation on the page.** Generate 10,000 simulated studies of n=20 with true effect d=0.2 (small, plausible). Apply p<0.05 filter. Report the average effect size among "significant" studies. The student sees, in their own code, that the average is much larger than 0.2 — typically d ≈ 0.5 or larger. This is the winner's curse in one screenful. Gelman's blog has versions of this simulation; the chapter can reuse the move and credit it.

---

## 7. Representation and Display Research

The chapter's side-by-side comparison table from TIKTOK.md is reconstructed here. Ch 8 doesn't have an explicit table in TIKTOK.md (the table lives in Ch 9), but the chapter's "Frequentist solution" and "Bayesian solution" sections compose into an implicit comparison. Rendered:

| | Frequentist proportion test | Bayesian Beta-binomial |
|---|---|---|
| Estimate (3/200) | 0.015 | 0.015 (likelihood mean) → shrunk by prior |
| 95% interval | [0.003, 0.043] (Clopper-Pearson) | Beta(3+3, 197+200) → [0.55%, 3.18%] |
| What the interval means | Long-run coverage frequency | Posterior probability that rate is in range |
| Comparison to last year | p = 0.71, "not significant" | Posterior probability rate improved = X% |
| Behavior with zero events | Rule of three: upper bound = 3/n | Posterior pulled toward prior mean |
| What you need to defend | The test assumptions, the threshold | The prior |

**Recommended row to add:** "Behavior at the accreditation decision boundary." The frequentist test, applied at the standard 2% threshold, tells you whether to reject the null *that the rate equals 2%* — and with this sample size it cannot reject either direction. The Bayesian posterior tells you the probability the true rate is below 2%, which can be reported as a single number (e.g., "78%"). The decision-relevance of the two outputs is fundamentally different, and the new row would make this explicit. This is the most teachable column for an undergraduate.

A second recommended display: a small-multiple plot. Six panels showing the same calculation under six different priors (Beta(1,1), Beta(3,200), Beta(15,985), Beta(1.5,98.5), Beta(0.5, 0.5), and a literature-based prior). The visual point is that the prior matters most when the data are sparse, which is exactly when the chapter says the prior is doing the most work. The plot is the chapter's prior-defense honesty in graphical form.

---

## 8. Open Questions and Research Gaps

**The chapter's biggest unresolved tension.** "Use a prior from the literature" assumes a literature uncorrupted by selection effects. If the literature itself reports inflated effect sizes (the winner's curse), the prior built from the literature will be biased upward. The fix — shrink the literature-based prior toward null before using it — is theoretically sound but rarely done in practice. The chapter should *name* this tension rather than smooth past it. I do not have a clean undergraduate-level resolution.

**When is sparse data actually too sparse for a Bayesian fix?** The chapter's exercise 3 ("when could shrinkage lead you astray?") asks this without giving a clean answer. The honest answer: when the prior is wrong and the data are too weak to overpower it, the Bayesian estimate is worse than the frequentist one. Numerical demonstration would be useful but the cleanest reference I am aware of is BDA3 §5.5 ("Hierarchical models for the binomial distribution"), which is at the right register for the chapter but requires a citation check. [verify].

**A genuine domain-knowledge gap.** I am not a surgeon or a hospital quality officer. The chapter's hospital scenario should be reviewed by someone who knows how accreditation actually works in 2026 — the specific thresholds, the specific review cycles, the specific consequences of a borderline complication rate. Without that review, the chapter risks pedagogical truth at the cost of operational misrepresentation. Flag for Nik.

---

## 9. Sourcing Notes

Primary sources verified by direct WebSearch this session:
- Button et al. 2013 *Nat Rev Neurosci* — DOI 10.1038/nrn3475 confirmed.
- Stein 1956 Berkeley Symposium — Project Euclid and Yale PDFs confirmed accessible.
- Efron & Morris 1975 JASA — Tandfonline DOI confirmed; 1977 *Scientific American* PDF confirmed at efron.ckirby.su.domains.
- Gelman & Carlin 2014 — DOI 10.1177/1745691614551642 confirmed; author PDF at Columbia confirmed.
- Hanley & Lippman-Hand 1983 — JAMA citation widely reproduced; McGill-hosted PDF confirmed accessible.
- Capen, Clapp & Campbell 1971 — publication venue (*Journal of Petroleum Technology*) and pagination confirmed via multiple secondary citations including the Kagel encyclopedia entry ([https://www.asc.ohio-state.edu/kagel.4/Encyclopedia_SS.pdf](https://www.asc.ohio-state.edu/kagel.4/Encyclopedia_SS.pdf)); SPE primary landing not directly opened — DOI 10.2118/2993-PA flagged `[verify]`.

Items flagged `[verify]` in this file: Capen et al. 1971 DOI; James & Stein 1961 exact pagination; Trikalinos & Ioannidis 2005 *J Clin Epidemiol* exact pagination; Ioannidis 2008 *Epidemiology* access; Hoekstra et al. 2014 access; FDA Sentinel and WHO VigiBase Bayesian methodology landing pages; BDA3 §5.5 page citation. None of these flagged items are load-bearing — the chapter's core argument is supported by the items that did verify.

Cross-references to other chapter research files: Gelman & Carlin 2014 may already appear in the Ch 4 research notes (see TIKTOK.md instructions). Cross-link rather than duplicate when assembling the chapter draft.
