# Research: Chapter 04 — Comparing Two Groups
## Bayesian Probability with LLMs

**Chapter one-line:** The t-test and its Bayesian analog — same data, different questions, and a first encounter with why statistically significant results don't always replicate.

**Research date:** 2026-05-13

---

## 1. Primary Sources

### Foundational papers and texts

- **William Sealy Gosset ("Student"), 1908.** "The Probable Error of a Mean." *Biometrika* 6(1): 1–25. The paper that invented the t-distribution. Gosset was a brewer at Guinness working on small-sample beer quality control; "Student" was a pseudonym Guinness imposed for trade-secret reasons. The historical detail matters for the book: the t-test was born for industrial small-sample inference, not for sweeping causal claims about psychological interventions. Original paper at York's history-of-stats archive: [PDF](https://www.york.ac.uk/depts/maths/histstat/student.pdf). Historical commentary by Zabell: [PDF](https://personal.morris.umn.edu/~jongmink/Stat2611/s1.pdf).

- **R. A. Fisher, 1925.** *Statistical Methods for Research Workers* (Oliver & Boyd, Edinburgh). The book that institutionalized significance testing for working scientists and pushed p < 0.05 into the canon. The phrase "null hypothesis" arrives in Fisher's 1935 *Design of Experiments*, not the 1925 book — useful to be precise about. CUNY's overview: [Introduction to NHST](https://academicworks.cuny.edu/cgi/viewcontent.cgi?article=1111&context=qb_oers). PMC essay tracing the history: ["Before p < 0.05 to Beyond p < 0.05"](https://pmc.ncbi.nlm.nih.gov/articles/PMC6693672/).

- **John P. A. Ioannidis, 2005.** "Why Most Published Research Findings Are False." *PLoS Medicine* 2(8): e124. DOI: [10.1371/journal.pmed.0020124](https://journals.plos.org/plosmedicine/article?id=10.1371%2Fjournal.pmed.0020124). The most-cited paper in the replication-crisis canon. Ioannidis's argument is Bayesian in shape: positive predictive value (PPV) of a finding depends jointly on power, α, and the pre-study probability the hypothesis is true. When pre-study probability is low and power is moderate, the post-test probability that a "significant" result is true can fall below 50% — which is the chapter's central technical claim.

- **Andrew Gelman & John Carlin, 2014.** "Beyond Power Calculations: Assessing Type S (Sign) and Type M (Magnitude) Errors." *Perspectives on Psychological Science* 9(6): 641–651. PubMed: [26186114](https://pubmed.ncbi.nlm.nih.gov/26186114/). Author's PDF: [Columbia](https://sites.stat.columbia.edu/gelman/research/published/retropower_final.pdf). Two concepts the chapter must teach. Type S = probability a significant estimate has the wrong sign. Type M = exaggeration ratio, the factor by which a significant estimate's magnitude exceeds the true effect. Gelman & Carlin show that in low-power studies, conditional on significance, the published effect can be 2x–10x the true effect — and sometimes opposite in sign. This is "winner's curse" formalized.

- **Open Science Collaboration (Brian Nosek et al.), 2015.** "Estimating the Reproducibility of Psychological Science." *Science* 349(6251): aac4716. DOI: [10.1126/science.aac4716](https://www.science.org/doi/10.1126/science.aac4716). 100 replications of psychology papers. 97% of originals reported a significant effect; only 36% of replications did. Replication effect sizes were on average half the originals'. The empirical anchor for the chapter's claim — but the OSC's methods were themselves contested (see §2 below).

- **Jacob Cohen, 1994.** "The Earth Is Round (p < .05)." *American Psychologist* 49(12): 997–1003. SJSU mirror: [PDF](https://www.sjsu.edu/faculty/gerstman/misc/Cohen1994.pdf). The canonical critique of NHST written for working psychologists. Cohen names the central confusion: researchers want P(H | data); the test gives P(data | H₀). The piece is 30 years old and reads like it was written yesterday — which is itself a lesson the chapter should make explicit.

- **Steven N. Goodman, 2008.** "A Dirty Dozen: Twelve P-Value Misconceptions." *Seminars in Hematology* 45(3): 135–140. DOI: [10.1053/j.seminhematol.2008.04.003](https://www.sciencedirect.com/science/article/abs/pii/S0037196308000620). PubMed: [18582619](https://pubmed.ncbi.nlm.nih.gov/18582619/). PDF mirror: [Six Sigma DSI](https://sixsigmadsi.com/wp-content/uploads/2020/10/A-Dirty-Dozen-Twelve-P-Value-Misconceptions.pdf). Twelve named misconceptions, each refuted in a paragraph. Use it as the chapter's misconceptions inventory.

- **Sander Greenland, Stephen J. Senn, Kenneth J. Rothman, John B. Carlin, Charles Poole, Steven N. Goodman, Douglas G. Altman, 2016.** "Statistical Tests, P Values, Confidence Intervals, and Power: A Guide to Misinterpretations." *European Journal of Epidemiology* 31(4): 337–350. PMC: [PMC4877414](https://pmc.ncbi.nlm.nih.gov/articles/PMC4877414/). 25 misinterpretations, each with technical correction. More thorough than Goodman 2008; written as a community-of-authority statement after the ASA's 2016 p-value statement.

### Key empirical cases

- **OSC 2015 reproducibility project.** Three psychology journals, 100 studies, prereg'd direct replications. Headline number: 36% replicated by significance test. Half-magnitude replication effects.

- **Begley & Ellis, 2012.** "Drug Development: Raise Standards for Preclinical Cancer Research." *Nature* 483(7391): 531–533. DOI: [10.1038/483531a](https://www.nature.com/articles/483531a). Amgen tried to replicate 53 landmark preclinical cancer papers; 6 replicated. Not a peer-reviewed replication study — a methods commentary — and the underlying data were not released, which the chapter should name. But the 11% number gets cited everywhere and the reader will encounter it.

- **Verhagen & Wagenmakers replication Bayes factor work.** "Bayesian Tests to Quantify the Result of a Replication Attempt." Author's PDF: [ejwagenmakers.com](https://www.ejwagenmakers.com/2014/VerhagenWagenmakers2014.pdf). Proposes computing a Bayes factor comparing the replication data under (a) the original effect size and (b) the null. Better-calibrated than asking "did the replication achieve p < 0.05" because it doesn't impose an arbitrary threshold.

---

## 2. The Core Concept — State of the Field

### What is settled

- A p-value is P(data at least this extreme | null hypothesis), not P(null hypothesis | data). Every working statistician and every careful methods textbook agrees on this. The misuse is downstream of the math, not in it.
- Confidence intervals are procedure guarantees, not probability statements about the parameter on this trial. This is the same conceptual move; the same misinterpretation pattern.
- Statistical significance and practical importance are different. A trivially small effect can be highly significant with a large enough sample; a meaningful effect can fail to reach significance in an underpowered study.
- Selective reporting, p-hacking, garden-of-forking-paths analyses inflate apparent discovery rates. The empirical pattern is documented across psychology, medicine, economics, and education.

### What is disputed

- **How bad is the replication crisis, really?** Daniel Gilbert and colleagues argued the OSC 2015 estimate was too pessimistic — that infidelities in the replications (different stimuli, different cultural contexts, different lab conditions) account for much of the apparent failure. The OSC team responded that their fidelity protocols were strong and the alternative explanation doesn't survive scrutiny. The debate is live. The chapter should not pretend it's resolved.

- **Is NHST itself the problem?** Gerd Gigerenzer's ["Mindless Statistics"](https://sciences.ucf.edu/biology/d4lab/wp-content/uploads/sites/23/2023/01/Gigerenzer-2004-Mindless-Statistics.pdf) (*Journal of Socio-Economics*, 2004) argues the problem is not NHST but the "null ritual" — the mechanical version Fisher, Neyman, and Pearson would all have rejected. Gigerenzer's defense of statistics-done-right is the strongest counter-argument the chapter has to engage. He is not defending p < 0.05 as decision rule; he is defending the underlying logic when applied with judgment, alternative hypotheses specified, and power considered.

- **Deborah Mayo's severe-testing philosophy.** *Statistical Inference as Severe Testing: How to Get Beyond the Statistics Wars* (Cambridge, 2018). Cambridge page: [book overview](https://www.cambridge.org/core/books/statistical-inference-as-severe-testing/D9DF409EF568090F3F60407FF2B973B2). Mayo argues frequentist error-statistical methods are not just defensible but superior in many contexts because they directly control the probability of being wrong in ways Bayesian methods don't. Her severity criterion — a hypothesis passes when a test that probably would have detected its flaws fails to — is a genuine philosophical alternative to Bayesian updating, not a confused holdover from Fisher. The book treats her as a serious opponent of Bayesian-as-default; this is the position the chapter must steelman.

- **Bayes factors as a remedy: how strong?** Wagenmakers and collaborators argue Bayes factors fix what's broken in NHST: they quantify evidence for the null as well as against it; they don't depend on stopping rules; they're calibrated by Jeffreys's interpretive thresholds. Critics (including some in the Replicability-Index community) argue default Bayes factor priors (Cauchy) make assumptions about effect size distributions that don't match the empirical record in psychology. See [Replicability-Index critique](https://replicationindex.com/2016/06/30/wagenmakers-default-prior-is-inconsistent-with-the-observed-results-in-psychologial-research/). The chapter's claim that Bayesian methods "fix" the problem must be hedged.

### What has changed recently (last 5 years)

- Preregistration is now standard practice in psychology and increasingly in medicine. Registered reports — where the journal accepts the methodology before the data are collected — solve the garden-of-forking-paths problem at the source.
- The ASA's 2016 statement on p-values, followed by the 2019 special issue of *The American Statistician* on "moving beyond p < 0.05," moved the official consensus toward more skeptical use of NHST.
- Bayesian methods have become accessible. Stan, PyMC, brms make it possible for a competent undergraduate to fit a Bayesian two-group model in 20 lines of code. The compute cost is no longer the barrier.
- The replication-crisis literature has matured. The 2015 OSC paper is no longer the only data point; later projects in social-behavioral economics, cancer biology, and political science have produced consistent qualitative results — replication rates well below the implied 95% of "p < 0.05 → finding is real."

---

## 3. Application Domain Examples

The chapter's scenario is education: two versions of a statistics tutorial, A and B, with post-test scores. This is the right domain for the replication-crisis sidebar because education research has its own well-documented replication problems and the reader can ground every claim in something they have lived through (a classroom).

- **What Works Clearinghouse** ([ies.ed.gov/ncee/wwc](https://ies.ed.gov/ncee/wwc/)) is the U.S. Department of Education's effort to rate educational interventions by evidence quality. The fact that this exists at all is a tell: a federal agency had to step in because the published literature could not be taken at face value. The WWC's "Meets Standards Without Reservations" rating requires random assignment, low attrition, valid outcome measures — and even with all that, intervention reports often conclude "evidence is mixed."

- **John Hattie's *Visible Learning* (2008).** [Routledge page](https://www.routledge.com/) and effect size list at [visible-learning.org](https://visible-learning.org/hattie-ranking-influences-effect-sizes-learning-achievement/). Hattie aggregated ~800 meta-analyses to rank 138 influences on learning. The "average effect" is d = 0.40 and Hattie's "hinge point" is d > 0.40 as the threshold for "worth doing." The methodological critique is extensive: unweighted averaging of heterogeneous meta-analyses, problematic correlation-to-d conversions, an arbitrary threshold. Critique from [Didau (Substack)](https://daviddidau.substack.com/p/visible-learning-invisible-errors); a thoughtful piece is also at [School Matters Foundation](https://www.schoolmattersfoundation.org/john-hattie-is-wrong). Hattie's 2023 update walks back some of the framing. Useful as a worked example of "famous statistical claim that does not survive close reading."

- **Education replication mapping review (2011–2020).** Tackett, Brown, Tay, et al. and others have done bibliometric work showing only ~0.2% of education-journal papers between 2011 and 2020 were replication studies. [Tandfonline overview](https://www.tandfonline.com/doi/full/10.1080/13803611.2021.2022315). The base rate of replication in education is low enough that the field cannot identify which findings replicate.

- **AERA / APA replication initiatives.** Both organizations have published replication guidance for educational research. The community knows the problem; the structural fix is harder.

---

## 4. The Book's Thesis Connection

The book's thesis is: side-by-side comparison, reader chooses. Chapter 4 is the chapter where the comparison stops being a polite exercise and starts mattering.

For the t-test versus the Bayesian two-group model, the side-by-side is not about which one is "right." Both can be done correctly. The chapter's pedagogical move is:

1. The t-test answers a question. State the question precisely: "If there were no difference between groups, how surprising is this data?"
2. The clinician/teacher/policy-maker has a different question. State that question precisely: "Given this data, how likely is it that B is better than A — and by how much?"
3. The frequentist toolkit cannot answer question 2 directly. This is not a flaw in the toolkit; it is the toolkit doing what it does.
4. The Bayesian toolkit answers question 2 directly, at the cost of requiring an explicit prior. This is not magic; it is the trade-off named.

Chapter 4 is also the Act One closer — the last chapter before Exam 1 — which means it has to consolidate everything the reader has built so far: Bayes' theorem (Ch 0–1), LLM prompting (Ch 2), the beta-binomial (Ch 3). The replication-crisis sidebar is the chapter's emotional payoff: "now you know enough to read the methods section of an education paper and tell whether to trust the conclusion."

The asymmetry rule (TIKTOK.md lines 42–45) lands in Chapter 5, not Chapter 4. But Chapter 4 plants it: the Bayesian solution is not yet markedly longer than the frequentist one here. By Ch 5, it will be. The reader should be ready for that shift.

---

## 5. Intellectual Lineage Notes

**Gosset / "Student" (1908).** The t-test was a quality-control instrument for a brewery. The mismatch between its origin (small-sample industrial measurement) and its modern use (definitive claims about human psychology) is itself part of the lineage. The Physiological Society piece on Gosset's strange origins is good: [physoc.org](https://www.physoc.org/magazine-articles/the-strange-origins-of-the-students-t-test/).

**Fisher (1925).** Statistical Methods for Research Workers turned significance testing into a tool every working agronomist, biologist, and psychologist could pick up. The 5% threshold was a working heuristic, not a metaphysical line. Fisher never argued it was a probability of the hypothesis being true. The institutional ossification of "p < 0.05 = real" is downstream of him, not from him.

**Ioannidis (2005).** The single most important paper for this chapter. Ioannidis's PPV framework is mathematically Bayesian: post-study odds = pre-study odds × Bayes factor of the test. The chapter's strongest formulation is to walk through Ioannidis's argument with numbers. If the pre-study probability of a hypothesis is 10% (which is generous for most exploratory psychology), power is 50%, α is 5%, then PPV ≈ 0.53. With pre-study probability 1% (reasonable for some genomics or drug-screening contexts), PPV drops to ~10%. Most "significant" findings are false. Worth showing the calculation on the page.

**Gelman & Carlin (2014).** The Type S / Type M extension is what makes the argument concrete for individual studies. The reader can compute Type S and Type M errors for a paper they've read. This is a teachable skill.

**OSC 2015.** The empirical confirmation. Worth noting that Gilbert et al. (2016) pushed back in *Science* with a comment; OSC responded; the debate is live. The chapter must hold both: the numbers are striking *and* the methods of measuring replication failure are themselves contested. Calibrated uncertainty, not crisis evangelism.

---

## 6. Pedagogical Delivery Research

The pedagogical literature on teaching NHST critique is small but consistent: students cannot reliably distinguish p-value from posterior probability after one course; even instructors get the question wrong on surveys. Cohen 1994 makes this point explicitly. Greenland et al. 2016 documents 25 distinct misinterpretations — each one is a place a student goes wrong if not specifically inoculated against.

The chapter's pedagogical move should be:

- **Lead with the wrong answer most students will give.** "p = 0.03 means there's a 97% chance the new tutorial is better." Then dismantle it. Do not start with the correct definition of p-value; start with the misconception and unwind it.

- **Translate every claim from p-value language to probability language and back.** "If there really were no difference, we'd see data this extreme 3% of the time" → "p = 0.03." "There's a 91% chance B is better than A given this data" → "P(δ > 0 | data) = 0.91." Make the translation visible.

- **Run the Ioannidis calculation on the page.** Pre-study probability × likelihood ratio = post-study odds. Three values of pre-study probability (1%, 10%, 50%). Watch the PPV swing.

- **Show one published abstract.** Pick a real education or psychology paper with p < 0.05, walk through what it actually establishes and what it does not. (For the published draft, pick a paper where the author has discussed limitations openly so the chapter is not a cheap shot.)

- **The replication sidebar must include the counter-argument.** Gigerenzer and Mayo are not strawmen. NHST done with judgment, with alternative hypotheses, with power considered, with preregistration — works. The crisis is about institutional incentives and ritual application, not about the math.

---

## 7. Representation and Display Research

The TIKTOK.md side-by-side table for Ch 4:

| | Frequentist | Bayesian |
|---|---|---|
| Result | p = 0.03, significant | P(B better) = 0.91 |
| Effect size | Cohen's d = 0.31 | Posterior median δ = 4.1 points |
| Replication? | No prediction available | Posterior predictive check possible |
| Prior required? | No (hidden uniform) | Yes — named explicitly |

The added row I would recommend:

| | Frequentist | Bayesian |
|---|---|---|
| **What the output answers** | "How surprising is the data if H₀ is true?" | "How likely is B better than A, given the data?" |

This row should go *first*. The whole chapter hinges on the question-mismatch. Naming it at the top of the table tells the reader why the rest of the rows differ.

The full table I'd propose:

| | Frequentist | Bayesian |
|---|---|---|
| What the output answers | "How surprising is the data if H₀ is true?" | "How likely is B better than A, given the data?" |
| Result | p = 0.03, significant | P(B better) = 0.91 |
| Effect size | Cohen's d = 0.31 | Posterior median δ = 4.1 points |
| Replication? | No prediction available | Posterior predictive check possible |
| Prior required? | No (hidden uniform) | Yes — named explicitly |
| Risk if misread | "97% chance B is better" (Cohen 1994) | "P(B better) = 1" (overconfidence in tails) |

The bottom row is also new and worth defending: the chapter should be honest that the Bayesian output has its own misreading failure modes. P(B better) = 0.91 is not "B is definitely better." A 9% probability of being wrong is not nothing. The Feynman move is to name both ways the reader can go wrong, not just the frequentist one.

---

## 8. Open Questions and Research Gaps

- **What is the right pre-study probability for an educational intervention?** Ioannidis's PPV depends on it. The honest answer is "we don't know precisely, but it's not high." For pedagogical interventions where the literature suggests most A/B comparisons show no effect or trivially small effects, a pre-study probability of 10–20% for "meaningfully better" might be defensible. The chapter should flag that this number is itself a judgment, not a measurement.

- **Is the t-test even the right frequentist comparison for the chapter's scenario?** The tutorial data are likely not normal, group sizes differ, variances may differ. Welch's t-test is more appropriate than Student's. Modern practice would lean on permutation tests or bootstrap. The chapter should at minimum name that Student's t is being used for pedagogical reasons; it is not the only or even the best frequentist option.

- **How should the Bayesian posterior predictive check be displayed?** Gabry et al. 2019 visualize PPC distributions overlaid on observed data. For two-group comparison, the natural display is two posterior densities for μ_A and μ_B and one posterior density for δ. A density-plot literacy assumption is required.

- **The Gilbert et al. (2016) critique of OSC.** Should the chapter cite both sides? My reading: yes. The chapter should name OSC 2015's headline number, name Gilbert et al.'s response, and conclude that even under the most generous re-reading, replication rates are far below the implicit 95% promise of "p < 0.05 = real finding."

- **Bayesian priors in education research are themselves contested.** What prior should the analyst use for an effect size in a tutorial comparison? Half-normal with scale 0.3? Centered at 0 with wide variance? Cohen's "small effect" of d = 0.2? The choice is not innocuous. Chapter 7 will handle this directly, but Chapter 4 must at least acknowledge it.

- **Type S error rates for the chapter's example.** With n_A = 40, n_B = 38, and a true effect of d = 0.1 (small), what is Type S? Worth computing for the chapter as a worked example. The retropower R package handles this.

---

## 9. Sourcing Notes

All sources verified to exist via web search 2026-05-13. Specific DOIs and journal volumes confirmed:

- Ioannidis 2005, PLOS Medicine 2(8): e124, DOI 10.1371/journal.pmed.0020124 — confirmed.
- OSC 2015, Science 349(6251), DOI 10.1126/science.aac4716 — confirmed, published August 28, 2015.
- Gelman & Carlin 2014, *Perspectives on Psychological Science* 9(6): 641–651 — confirmed.
- Cohen 1994, *American Psychologist* 49(12): 997–1003 — confirmed.
- Goodman 2008, *Seminars in Hematology* 45(3): 135–140, DOI 10.1053/j.seminhematol.2008.04.003 — confirmed.
- Greenland et al. 2016, *European Journal of Epidemiology* 31(4): 337–350 — confirmed.
- Gosset 1908, *Biometrika* 6(1): 1–25 — confirmed.
- Fisher 1925, *Statistical Methods for Research Workers* (Oliver & Boyd) — confirmed.
- Begley & Ellis 2012, *Nature* 483: 531–533, DOI 10.1038/483531a — confirmed. Note: this is a methods commentary, not a peer-reviewed replication study, and the underlying data were never released. The chapter should cite carefully.
- Gigerenzer 2004, *Journal of Socio-Economics* 33(5): 587–606 — confirmed. Note: title is "Mindless Statistics"; it's a critique of ritual NHST, not a blanket defense of NHST. Use precisely.
- Mayo 2018, *Statistical Inference as Severe Testing* (Cambridge) — confirmed.
- Verhagen & Wagenmakers, 2014, replication Bayes factor — confirmed via author site.
- Hattie *Visible Learning* (2008/2023) — confirmed.
- What Works Clearinghouse — confirmed.
- Anscombe 1973, "Graphs in Statistical Analysis" — confirmed (for Ch 5 reference).

`[verify]` flags:

- The OSC 2015 specific number "97% of originals, 36% of replications" — verified by multiple sources but reader should check the *Science* paper's Table 1 directly before citing in the draft.
- Begley & Ellis "6 of 53" replication number — widely cited but the original *Nature* commentary doesn't include the protocols. Treat as a community estimate, not a measured rate.
- Hattie's d = 0.40 hinge point: confirmed as Hattie's claim; the methodological critique that this threshold is arbitrary is also confirmed. Chapter should present both.

**Sources not yet exhausted:**
- Senn's *Statistical Issues in Drug Development* on regulatory perspectives — would strengthen the "why anyone uses frequentist methods" section but probably too narrow for an Act One chapter.
- Wasserstein & Lazar 2016, the ASA p-value statement — official institutional position, worth a citation.
- Benjamin et al. 2018, "Redefine Statistical Significance" — proposed p < 0.005 as new default; relevant to the "is the math broken or the threshold" question.

**Strongest sources for this chapter:** Ioannidis 2005 (the argument), Gelman & Carlin 2014 (the mechanics), OSC 2015 (the empirical anchor), Cohen 1994 (the misconception inventory).

**Counter-argument sources:** Gigerenzer 2004 (NHST done right), Mayo 2018 (severe testing as alternative), Gilbert et al. 2016 (OSC overstated).

---
