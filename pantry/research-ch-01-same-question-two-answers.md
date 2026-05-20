# Research: Chapter 01 — The Same Question, Two Answers
## Bayesian Probability with LLMs

**Chapter one-line:** The medical testing problem reveals what frequentist statistics can and cannot say — and introduces the Bayesian alternative that answers the question the test actually asks.
**Research date:** 2026-05-13

---

## 1. Primary Sources

### Foundational papers and texts

- **Casscells, W., Schoenberger, A., and Graboys, T. B. (1978). "Interpretation by physicians of clinical laboratory results."** *New England Journal of Medicine*, 299(18), 999–1001. PubMed: [https://pubmed.ncbi.nlm.nih.gov/692627/](https://pubmed.ncbi.nlm.nih.gov/692627/); journal page: [https://www.nejm.org/doi/full/10.1056/nejm197811022991808](https://www.nejm.org/doi/full/10.1056/nejm197811022991808). The chapter's anchor study. Researchers at Harvard Medical School asked 60 medical professionals (20 house officers, 20 fourth-year medical students, 20 attending physicians) the medical-testing question: "If a test to detect a disease whose prevalence is 1/1000 has a false positive rate of 5%, what is the chance that a person found to have a positive result actually has the disease, assuming you know nothing about the person's symptoms or signs?" The modal answer was 95% (given by 27 of 60); the correct answer is about 2%. Only 11 of 60 produced a correct response. This single study is the strongest single piece of evidence for the chapter's claim that "most people say 99%" — because most *trained medical professionals* did.

- **Eddy, D. M. (1982). "Probabilistic reasoning in clinical medicine: Problems and opportunities."** In Kahneman, Slovic, & Tversky (eds.), *Judgment under Uncertainty: Heuristics and Biases*, Cambridge University Press, pp. 249–267. PhilPapers entry: [https://philpapers.org/rec/EDPRI](https://philpapers.org/rec/EDPRI) [verify — search result URL pattern; the canonical entry is in PhilPapers]; book front matter: [https://assets.cambridge.org/97805212/84141/frontmatter/9780521284141_frontmatter.pdf](https://assets.cambridge.org/97805212/84141/frontmatter/9780521284141_frontmatter.pdf). Eddy showed clinicians a description of a mammography result and asked them for the probability the patient had cancer. The modal estimate was 75%; the correct answer was about 7.5%. Eddy's contribution to the literature was naming the specific clinical reasoning error and showing it generalized beyond Casscells's vignette. This is the chapter's bridge from the "most people get it wrong" claim to the "the right answer is small" claim.

- **Gigerenzer, G. and Hoffrage, U. (1995). "How to improve Bayesian reasoning without instruction: Frequency formats."** *Psychological Review*, 102(4), 684–704. Open PDF: [https://pages.ucsd.edu/~scoulson/203/GG_How_1995.pdf](https://pages.ucsd.edu/~scoulson/203/GG_How_1995.pdf). The paper that broke the field. Same Bayesian problems that produced 10–20% correct response rates when framed in probabilities ("the prevalence is 0.1%, the false positive rate is 5%") produced ~50% correct when framed in natural frequencies ("10 out of 10,000 people have the disease; of the remaining 9,990, 500 will test positive..."). This matters for Ch 1 because it is the most defensible *pedagogical* finding in the entire base-rate-neglect literature, and it changes how the chapter should present the calculation.

- **Wasserstein, R. L. and Lazar, N. A. (2016). "The ASA Statement on p-Values: Context, Process, and Purpose."** *The American Statistician*, 70(2), 129–133. Open PDF: [https://www.tandfonline.com/doi/full/10.1080/00031305.2016.1154108](https://www.tandfonline.com/doi/full/10.1080/00031305.2016.1154108); ASA copy: [https://www.amstat.org/asa/files/pdfs/p-valuestatement.pdf](https://www.amstat.org/asa/files/pdfs/p-valuestatement.pdf). The American Statistical Association's first formal statement in its 177-year history on what p-values do and do not say. The six principles are written for working scientists and are quotable. Critical for Ch 1's frequentist-side claim that the p-value is widely misunderstood — this is the profession's own admission, not a Bayesian polemic.

- **Bar-Hillel, M. (1980). "The base-rate fallacy in probability judgments."** *Acta Psychologica*, 44(3), 211–233. Open PDF: [https://worthylab.org/wp-content/uploads/2020/12/bar-hillel_1980.pdf](https://worthylab.org/wp-content/uploads/2020/12/bar-hillel_1980.pdf). The first comprehensive theoretical treatment of why people ignore base rates. Bar-Hillel's explanation: people order information by perceived relevance, and individuating information ("this person tested positive") dominates statistical information ("the prevalence is 0.1%") regardless of how Bayes-theoretically diagnostic each piece is. Useful for the chapter as the *why* behind the empirical pattern Casscells documented.

### Key empirical cases

- **Casscells, Schoenberger, and Graboys (1978) — Harvard Medical School.** Documented above. 60 physicians, students, and house officers; 45% gave 95% as the answer, when the correct answer is ~2%. The chapter could open with this study directly. Fit for undergraduates because the numbers are simple, the answer is shocking, and the study's design is easy to explain. Strongly recommended as the chapter hook.

- **HIV ELISA testing in low-prevalence populations.** Documented in a large Chinese blood-donor study: HIV prevalence in the donor population was 0.0009%; the third ELISA's positive predictive value (proportion of positive tests that were true positives) was just 3.2% in the high-risk subgroup but the false-positive rate in donors was 222× higher than the prevalence. Source: [https://pubmed.ncbi.nlm.nih.gov/18573774/](https://pubmed.ncbi.nlm.nih.gov/18573774/). For prenatal HIV screening in a U.S. Hispanic population: positive predictive value of 9.8% at prevalence 0.05%, 82.6% at prevalence 2.43% — *same test, different population, same arithmetic*. Source: [https://pubmed.ncbi.nlm.nih.gov/15318249/](https://pubmed.ncbi.nlm.nih.gov/15318249/). The chapter could use this as the "real-world stakes" anchor after the textbook example. The numbers are documented, the math is the chapter's math, and the population variation makes the point that there is no test accuracy independent of prevalence.

- **Sally Clark prosecution (UK, 1999).** A British mother convicted of murdering her two infant sons, partly on testimony that the probability of two SIDS deaths in one family was 1 in 73 million. Conviction overturned 2003 after the "prosecutor's fallacy" was exposed: the testimony confused P(two SIDS deaths | innocent) with P(innocent | two SIDS deaths), the same inversion the chapter teaches. Documented at [https://forensicstats.org/blog/2018/02/16/misuse-statistics-courtroom-sally-clark-case/](https://forensicstats.org/blog/2018/02/16/misuse-statistics-courtroom-sally-clark-case/) and in the Royal Statistical Society's reporting: [https://rss.onlinelibrary.wiley.com/doi/full/10.1111/j.1740-9713.2005.00078.x](https://rss.onlinelibrary.wiley.com/doi/full/10.1111/j.1740-9713.2005.00078.x). Sally Clark died in 2007. Fit for Exercise 2 in TIKTOK.md ("DNA match argument") — the Clark case is the canonical worked example of what the exercise is asking the student to spot.

---

## 2. The Core Concept — State of the Field

### What is settled

The arithmetic of Bayes' theorem applied to diagnostic testing is not in dispute. Given prevalence P(D), sensitivity P(+|D), and specificity 1 − P(+|¬D), the positive predictive value P(D|+) is fully determined. The result that P(D|+) can be very small even when sensitivity and specificity are high *if the prevalence is low* is settled — it follows from the arithmetic and has been confirmed empirically in every diagnostic study that reports both sensitivity/specificity and PPV across populations. See [https://pmc.ncbi.nlm.nih.gov/articles/PMC8156826/](https://pmc.ncbi.nlm.nih.gov/articles/PMC8156826/) for a clean undergraduate-level treatment of the four quantities (sensitivity, specificity, PPV, NPV) as conditional probabilities.

That a p-value is not the probability the hypothesis is true is also settled — by the American Statistical Association's 2016 statement (Wasserstein & Lazar), which states this in Principle 2 unambiguously. The statement is the profession's consensus.

That trained medical professionals systematically commit the inversion error is settled empirically — Casscells (1978), Eddy (1982), and a half-century of replications since.

### What is disputed

1. **How much of the "physicians get it wrong" finding generalizes to current practice.** Critics have argued Casscells's vignette is unrealistic (the question explicitly says "assuming you know nothing about the person's symptoms or signs," which removes the clinical reasoning physicians actually use). Some replication studies have produced higher correctness rates with reformulated questions. The chapter should not present the 1978 finding as a fixed property of medical training; the finding is robust but the size of the effect depends on the framing. See [https://pmc.ncbi.nlm.nih.gov/articles/PMC4955674/](https://pmc.ncbi.nlm.nih.gov/articles/PMC4955674/) (Manrai et al. 2014, "Medicine's Uncomfortable Relationship With Math") for a measured 2014 update.

2. **Whether the failure is "people are bad at Bayes" or "people are bad at the probability format."** Gigerenzer's natural-frequency work argues for the second interpretation. The implication is that *the teaching is broken, not the people*. This is a real and live dispute in the cognitive psychology literature — Kahneman's and Gigerenzer's labs have argued it for thirty years. The chapter should pick a side or name the dispute; pretending it does not exist is fragile.

3. **Whether p-values are "fundamentally" misleading or merely "frequently misinterpreted."** The ASA statement carefully chose the second framing. More recent work (Wasserstein, Schirm, & Lazar 2019, "Moving to a World Beyond 'p < 0.05'") argues for the first. This dispute belongs more to Ch 4 (replication crisis) than Ch 1, but the chapter's framing of the frequentist solution should not assume the strong version of the critique.

4. **Whether the medical testing problem is the *right* opening example.** Some textbooks use it; others use a courtroom example (Sally Clark) or a security-screening example (TSA, airport). The medical example is the most common and the most cited. The reader will encounter it again in the wild. Stick with it.

### What has changed recently (last 5 years)

- **COVID-19 made every reader's intuition about diagnostic testing visible.** Rapid-antigen tests with 80% sensitivity and 99% specificity were ubiquitously deployed. In low-prevalence settings (asymptomatic screening in a community with 0.1% active infection), the PPV was below 10%. This was reported on by news outlets in 2020–2021 with varying accuracy. Many readers will have encountered the math at the kitchen table. The chapter can lean on this — but should not assume the reader resolved it correctly.

- **LLMs as diagnostic-reasoning partners.** GPT-4-class models, asked the Casscells vignette directly, produce the correct answer about 90% of the time in 2024 evaluations [verify — I do not have a specific cited evaluation paper to point to; this is my recall and should be checked]. Asked the same question through a sloppy clinical narrative, performance drops. This belongs in Ch 2's prompting discussion but should be flagged in Ch 1 as "you will be tempted to ask the LLM to do this for you; learn to do it yourself first because you will need to check."

- **The ASA's 2019 follow-up.** [https://www.tandfonline.com/doi/full/10.1080/00031305.2019.1583913](https://www.tandfonline.com/doi/full/10.1080/00031305.2019.1583913). "Moving to a World Beyond 'p < 0.05'." This editorial pushed the 2016 statement further: stop using statistical significance as a binary cutoff at all. The chapter could mention this as the frontier of the conversation, but Ch 4 is where it belongs.

---

## 3. Application Domain Examples

The chapter's named scenario domain is medical diagnostic testing. Application examples should be diagnostic-test cases with documented prevalence and accuracy figures.

1. **TIKTOK.md's stated example: rare disease, prevalence 0.001, sensitivity 0.99, specificity 0.99.** Compute: P(D|+) = (0.99 · 0.001) / (0.99 · 0.001 + 0.01 · 0.999) = 0.00099 / 0.01098 ≈ 0.090 ≈ 9%. This is the chapter's worked example. The numbers are clean and the answer is striking. Recommended as-is.

2. **HIV ELISA in a low-prevalence U.S. blood-donor population.** Prevalence ~0.01%; sensitivity ~99.7%; specificity ~99.0%. PPV ≈ (0.997 · 0.0001) / (0.997 · 0.0001 + 0.01 · 0.9999) ≈ 0.0001 / 0.0101 ≈ 1%. *A positive HIV ELISA from a blood-donor screen is wrong 99 times out of 100.* This is why all positive ELISAs go to confirmatory testing (Western blot or NAT). Documented at [https://www.cdc.gov/hiv/testing/laboratorytests.html](https://www.cdc.gov/hiv/testing/laboratorytests.html) [verify — CDC URL pattern; specific page not confirmed via WebSearch]. The arithmetic story is the test's protocol.

3. **Mammography screening.** Prevalence of breast cancer in women in their 40s ~0.8%; mammography sensitivity ~80%; specificity ~90%. PPV ≈ (0.80 · 0.008) / (0.80 · 0.008 + 0.10 · 0.992) ≈ 0.0064 / 0.1056 ≈ 6%. Eddy's 1982 calculation used similar numbers and produced the 7.5% figure he showed to clinicians. Documented at [https://www.stat.berkeley.edu/~aldous/157/Papers/health_stats.pdf](https://www.stat.berkeley.edu/~aldous/157/Papers/health_stats.pdf) (Gigerenzer et al. 2007, *Psychological Science in the Public Interest*). Fit for Exercise 3 in TIKTOK.md (public-health screening question).

4. **COVID-19 rapid antigen testing in low-prevalence asymptomatic screening.** Prevalence ~0.5% (community baseline during a low-transmission period); sensitivity ~80%; specificity ~99%. PPV ≈ (0.80 · 0.005) / (0.80 · 0.005 + 0.01 · 0.995) ≈ 0.004 / 0.014 ≈ 29%. Documented widely in 2020–2022; FDA EUA documents for specific tests give the underlying accuracy figures. The chapter could use this as the contemporary anchor — the reader was probably tested at some point.

5. **DNA evidence in a courtroom (Sally Clark variant).** A defendant matches DNA at a frequency of 1 in 1,000,000 in the general population. The city has 1,000,000 residents. P(match | innocent) = 1 in 1,000,000. Prior on the defendant being the source (before evidence): ≈ 1 in 1,000,000. Posterior P(source | match) is *not* 1 − 10⁻⁶; it is around 50% under uniform priors over the city's population, because the expected number of false matches in a million-person city is one. Exact computation depends on the prior population. Fit for TIKTOK.md Exercise 2 directly. The Clark case is the most-cited real failure; the Royal Statistical Society wrote an open letter about it in 2002.

---

## 4. The Book's Thesis Connection

The book's thesis is that statistical inference should be taught through explicit side-by-side comparison, and the reader should leave able to choose. Chapter 1 is the chapter that *introduces the choice itself*. Until Ch 1, the reader has been computing probabilities; from Ch 1 onward, they are choosing between inferential frameworks.

The medical-testing problem is the perfect first example because it lets both frameworks run on the same data and produce demonstrably different answers to different questions. The frequentist solution computes P(positive | no disease) — exactly what a hypothesis test computes — and the answer is 1%. The Bayesian solution computes P(disease | positive) — exactly what the clinician needs — and the answer is 9%. Both calculations are correct. They answer different questions. The reader sees that the two frameworks are not in a "who's right" competition; they are in a "what are you asking" conversation. This is the book's thesis, set in concrete on page one of the comparative content.

The chapter also establishes the book's framing for the rest of Act One: *the frequentist test is not wrong, it is incomplete.* It answers what it answers. The Bayesian framework answers a different question. The reader's job is to know which question the decision-maker is asking. This framing — fair to both sides, harsh toward neither — is the book's voice. Ch 1 sets it.

Finally, the chapter sets up Ch 2's LLM-implementation arc. The reader closes Ch 1 with the open problem of computing this posterior for different prevalence values. They will turn to an LLM in Ch 2. The chapter's last sentence is a handoff: "you will learn to ask the LLM the right question, so it does not make the same mistake the test makes." This is the book's other thesis — that LLMs amplify both clarity and confusion, and the antidote is knowing the math well enough to tell which.

---

## 5. Intellectual Lineage Notes

**Thomas Bayes (1701–1761).** Carried forward from Ch 0. In Ch 1, Bayes appears not as a historical figure but as the author of the rule the chapter is applying. The Royal Society essay (1763) states the inverse-probability problem in language that maps directly onto the medical-test problem: given observed effects, compute the probability of the unobserved cause. The chapter could note: the rule that resolves the medical-test paradox was written 215 years before Casscells documented physicians failing to use it. Source: [https://royalsocietypublishing.org/rstl/article/doi/10.1098/rstl.1763.0053/119736](https://royalsocietypublishing.org/rstl/article/doi/10.1098/rstl.1763.0053/119736). Useful as an epigraph or a closing sidebar contrasting "the math has been available for two centuries" with "the typical Harvard Medical School physician in 1978 still got it wrong."

**David M. Eddy (b. 1941).** American physician, mathematician, and policy analyst. His 1982 chapter in Kahneman/Slovic/Tversky brought the conditional-probability framework into clinical medicine in a way the field could not ignore. Eddy went on to develop "evidence-based medicine" as a formal practice. The connection to Ch 1: Eddy did not just observe the inverse fallacy; he argued it was *the* central pathology in clinical reasoning and that clinical training should be restructured around posterior probability. Sources: PhilPapers entry above; obituary record for Eddy (still active at time of writing) at [https://www.healthaffairs.org/](https://www.healthaffairs.org/) [verify — Eddy has published in Health Affairs extensively but a specific biographical page was not located]. Useful as a one-paragraph sidebar in the chapter's "what does the test actually answer" section: Eddy named the failure, gave it the language the chapter uses, and pointed the field toward Bayes.

**Casscells, Schoenberger, and Graboys.** Three Harvard-affiliated clinicians who designed the 1978 study and published it in NEJM. The study was small (n=60) but the design was clean, the question precise, and the result devastating. The chapter should name them. The study has been replicated dozens of times in different populations and the result has held — most recently in [https://pmc.ncbi.nlm.nih.gov/articles/PMC4955674/](https://pmc.ncbi.nlm.nih.gov/articles/PMC4955674/) (Manrai et al. 2014). Useful as the chapter's empirical hook — three real clinicians, real medical school, real question, real wrong answers. Not "people misunderstand probability." *Doctors at Harvard Medical School in 1978 misunderstood probability.* That sentence does work the abstract claim cannot.

Author could use Eddy as the chapter's intellectual anchor (the figure who *named* the problem the chapter solves) and Casscells et al. as the empirical anchor (the study that *demonstrated* the problem). Both are real, both are findable, both are quotable.

---

## 6. Pedagogical Delivery Research

### Prior knowledge required

The chapter assumes the reader has completed Ch 0 (conditional probability, Bayes as arithmetic). It also assumes basic familiarity with the idea of a hypothesis test — null, alternative, p-value — at the level a typical first-year statistics course provides. The chapter does *not* assume the reader can derive the t-test; it assumes only that they have heard of p-values.

### Common misconceptions in undergraduates

1. **The inverse fallacy.** Casscells et al. (1978) documented this in physicians; Bar-Hillel (1980) gave it theoretical structure. Undergraduates exhibit it at higher rates than physicians — typical experiments show 80–95% incorrect responses when the problem is in probability format. The chapter's worked example is designed to break this misconception. The chapter should do it in *both* formats: once with probabilities (the formula), once with natural frequencies (per Gigerenzer & Hoffrage 1995). Doing both teaches the math and provides the cognitive scaffold that makes the math intuitive.

2. **Conflating p-value with P(H₀ | data).** Documented in Wasserstein & Lazar (2016, Principle 2). Students leave their first stats course believing the p-value is the probability the null hypothesis is true. It is not; it is the probability of data at least this extreme *given* the null is true. This is the same inversion as the medical-test problem, dressed in different clothing. The chapter should name this explicitly — the failure modes are isomorphic.

3. **Treating sensitivity as the answer to "how likely is the disease?"** When a test is described as "99% accurate," the lay reading is "I have a 99% chance of being sick if I tested positive." Even after explanation, students drift back to this reading under time pressure. The chapter should give the student a calibration exercise: compute the same disease's PPV at three prevalences, write down what surprises them.

4. **Believing the math is "Bayesian" in some special sense.** Students sometimes treat Bayes' theorem as belonging to "the Bayesian camp" rather than as a theorem that follows from the definition of conditional probability. The theorem is not contested; only the *interpretation of probability* is. The chapter should make this distinction once, clearly, early.

### Instructional sequences shown to work

The natural-frequencies format (Gigerenzer & Hoffrage 1995, replicated many times) consistently outperforms the probability format in initial teaching. The sequence:
1. State the population frame: "Imagine 10,000 people."
2. State the prevalence as a count: "10 have the disease."
3. State the sensitivity as counts: "Of those 10, 9 test positive."
4. State the false positive rate as counts: "Of the 9,990 without the disease, 100 test positive."
5. Ask: "Of the 109 people who tested positive, how many have the disease?" Answer: 9. PPV = 9/109 ≈ 8%.

This is the same arithmetic as the formula, but undergraduate correctness rates are roughly 5–10× higher. The chapter should teach the formula and then *also* render the same problem in this form — both because it teaches the concept better and because it sets up Ch 2's prompting work (a good prompt for an LLM is closer to the natural-frequency framing than the formula).

The empirical evidence: Gigerenzer & Hoffrage (1995) report ~50% Bayesian responses with natural frequencies vs. ~20% with probabilities, n's of hundreds across multiple studies. [https://pages.ucsd.edu/~scoulson/203/GG_How_1995.pdf](https://pages.ucsd.edu/~scoulson/203/GG_How_1995.pdf).

### Known teaching failure modes

- **Stating the formula and applying it once.** This produces students who can recite Bayes' theorem and fail Casscells. The chapter needs three iterations of the problem at three different prevalence values (TIKTOK.md already does this — keep it).
- **Treating the frequentist solution as a strawman.** The chapter should give the frequentist test its due — it does answer a real question (how surprising is this data under the null), and that question has its own uses (multiple testing, regulatory contexts, signal detection). The chapter should not roll its eyes at the frequentist side. The book's thesis demands fairness.
- **Skipping the "why does this matter" connection.** A pure arithmetic example without HIV, mammography, or Clark feels academic. Anchor it.

### The difference between students who understand vs. memorize

Students who *understand* can predict what happens to PPV when prevalence changes without recomputing — they know PPV scales roughly with prevalence in the low-prevalence regime, and they know why. Students who *memorize* re-run the formula each time and are surprised every time. The chapter's three-prevalence exercise (0.001, 0.01, 0.1) is the diagnostic. If the student computes three numbers but cannot articulate the pattern, the teaching has not landed.

---

## 7. Representation and Display Research

TIKTOK.md (lines 130–137) sketches the chapter's side-by-side comparison table. Rendering it cleanly:

| | Frequentist | Bayesian |
|---|---|---|
| Question answered | How surprising is the data? | How likely is the hypothesis? |
| Operational quantity | P(positive \| no disease) = 1% | P(disease \| positive) = 9% |
| Uses prevalence? | No | Yes — required input |
| Output | Reject / fail to reject H₀ | Posterior probability |
| Clinician's decision | Ambiguous | Grounded |

**Additional row I would add:**

| | Frequentist | Bayesian |
|---|---|---|
| **What changes when the disease becomes more common?** | Nothing — the p-value is unchanged | Posterior rises sharply |

Rationale for the added row: the table as drafted shows the *static* difference between the frameworks at one prevalence. The added row shows the *dynamic* difference — what each approach does when the input that matters changes. The frequentist row produces 1% regardless of whether you are testing in a TB ward or a kindergarten. The Bayesian row produces 9% in a low-prevalence population, 50% in a moderate one, and 91% in a high one. This is the row that makes the chapter's title — "the same question, two answers" — visible at a glance, because the right-hand column is where the answer to the clinician's question actually lives. It also sets up Ch 3's confidence-vs-credible-interval comparison structurally: in both chapters, the Bayesian column is the one that responds to context.

The chapter should also include a natural-frequency display of the worked example (a 10,000-person frequency tree or 2×2 count table) alongside the formula calculation. Per Gigerenzer & Hoffrage, this is the representation that produces understanding, not just calculation.

---

## 8. Open Questions and Research Gaps

- **The exact "physicians get it wrong" rate in 2026.** Casscells is 1978. Manrai et al. (2014) found broadly similar results 36 years later, but neither is current. I could not locate a 2020s replication of the original Casscells vignette at scale. The chapter should cite the 1978 finding for its historical weight and the 2014 finding for its persistence — and not claim the rate is the same today without a current source.

- **LLM accuracy on the Casscells problem.** I asserted ~90% correctness for GPT-4-class models above but flagged it `[verify]`. I did not locate a peer-reviewed evaluation paper. There is informal benchmarking (Anthropic's own blog posts, Stanford CRFM evaluations) but no canonical citation. Flagged.

- **CDC URL for the HIV testing protocol.** I cited a CDC URL pattern but did not confirm the specific page in a WebSearch. The author should verify before linking. Flagged `[verify]`.

- **Eddy's biographical page.** Eddy is a real figure with a long publication record; I did not retrieve a single canonical biographical source. The Health Affairs publisher page exists but a specific Eddy bio page was not located. Flagged `[verify]`.

- **Sources likely to age within 3 years.** The ASA's 2016 statement is stable; the 2019 follow-up is current. Any LLM-accuracy figures will age in months, not years. The medical-prevalence figures (HIV, mammography) are stable to one decimal place over a decade. COVID prevalence figures are dated to specific time windows and should be cited with dates.

- **Cases not verifiable.** None of the cases in §1 are unverified. The Sally Clark case is well-documented; the Casscells study is on PubMed; the HIV ELISA studies are on PubMed. The chapter's empirical foundation is solid.

---

## 9. Sourcing Notes

- **Casscells, Schoenberger, & Graboys (1978).** NEJM. Paywalled for full text; PubMed abstract is open and contains the key numbers. The chapter can cite the abstract directly.
- **Eddy (1982).** Chapter in the Kahneman/Slovic/Tversky volume. The volume is in print; individual chapters are not separately downloadable. University library access required for the chapter's specifics beyond what's in the search-result summary.
- **Gigerenzer & Hoffrage (1995).** Open PDF via UCSD course materials. Fine to cite directly.
- **Wasserstein & Lazar (2016).** Open access via Taylor & Francis (the publisher released it open as part of the statement). ASA's own PDF is also open. Cleanly linkable.
- **Bar-Hillel (1980).** Open PDF via Worthy Lab. Original ScienceDirect version paywalled.
- **Manrai et al. (2014).** Open via PMC. The 2014 replication is the strongest current evidence for the chapter's "physicians get it wrong" claim.
- **Sally Clark case.** Multiple open sources: Center for Statistics and Applications in Forensic Evidence ([forensicstats.org](https://forensicstats.org/blog/2018/02/16/misuse-statistics-courtroom-sally-clark-case/)), Royal Statistical Society *Significance* magazine, Wikipedia. All free.
- **HIV ELISA studies.** PMC has open abstracts; full texts vary by journal.
- **Clayton (2021).** *Bernoulli's Fallacy*, Columbia University Press. Paywalled (the book is $30–40); reviews open at MAA and *Significance*. The book is a strong Bayesian-side reference for Ch 4's replication-crisis section, but Ch 1 does not depend on it.

No major fact-checking gaps. Two `[verify]` flags above (CDC URL, LLM-accuracy figure, Eddy biographical detail) should be confirmed before draft is finalized. The chapter's core claims — Casscells's numbers, the medical-test posterior arithmetic, the ASA statement's language, Gigerenzer's natural-frequency findings — are all primary-sourced and verified.
