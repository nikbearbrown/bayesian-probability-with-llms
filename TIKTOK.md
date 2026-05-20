# Full TOC Specification
## Bayesian Probability with LLMs — Bear Brown LLC
*Tic TOC /g1 output — complete chapter brief for content generation*
*Version 1.0 — built from intake, arc, and design decisions confirmed in session*

---

## Book Concept Summary

A hands-on undergraduate textbook teaching statistical inference through
explicit comparison — every problem solved frequentist-first, then
Bayesian, side by side. Implementation via LLM-generated code throughout.
Reader decides which approach serves their problems. $1 / Kindle Unlimited.
Companion website: BLS/O*NET datasets, D3 animated visualizations, dataset
selection tool, data preparation reference.

**The book succeeds if:** after completing it, a reader can take a real
dataset, implement both a frequentist and Bayesian analysis of the same
problem, articulate what each approach assumes and where each fails, and
make a defensible choice between them.

**Series context:** Part of the Irreducibly Human / Bear Brown LLC
publishing program. Methods foundation for readers who need to reason
carefully about human and AI capability claims.

---

## Standard Chapter Anatomy

Every primary chapter (1–13) follows this structure:

1. **The Problem** — one concrete situation, stated before any theory
2. **Frequentist Solution** — built and interpreted completely
3. **Where Frequentist Strains** — specific failure mode for this problem
4. **Bayesian Solution** — built and interpreted completely
5. **Side-by-Side Comparison** — assumptions, capabilities, limits of each
6. **Prompting for Implementation** — how to prompt an LLM for this
   chapter's analysis (assumes skill from Chapter 2)
7. **Exercises** — minimum 3, at least one requiring production,
   at least one at Apply level or above under both frameworks

**Asymmetry rule:** Later chapters (Act Two onward) spend more space
on the Bayesian solution because the frequentist analog is simpler.
This asymmetry is named explicitly when it first appears (Chapter 5)
and treated as evidence, not apology.

---

## CHAPTER 0 — Probability Foundations

**Type:** Prerequisite resolver — not part of the semester chapter budget.
Assigned as Week 0 reading or diagnostic exercise.

**One-line:** Everything you need before Chapter 1 — conditional
probability, Bayes' theorem as arithmetic, nothing more.

**The problem it solves:** A reader who knows P(A) but not P(A|B) cannot
follow Chapter 1's Bayesian solution. This chapter closes that gap in
the minimum space required.

**Learning outcomes:**
1. (Remember) State the definition of conditional probability P(A|B)
2. (Apply) Compute P(A|B) from a joint probability table
3. (Apply) Apply Bayes' theorem to a two-hypothesis problem by hand
4. (Understand) Explain why P(A|B) ≠ P(B|A)

**Content blocks:**
- Joint probability and the multiplication rule
- Conditional probability: P(A|B) = P(A∩B) / P(B)
- The asymmetry: P(A|B) vs. P(B|A)
- Bayes' theorem as arithmetic: P(H|D) = P(H)·P(D|H) / P(D)
- Two worked calculations by hand

**Worked example:** An urn contains 3 red and 7 blue balls. You draw
one ball without looking and a friend tells you it's not blue. What is
the probability it's red? Solved step by step using the formula.

**No prompting section** — this chapter is arithmetic only.

**Exercises:**
1. Compute P(A|B) from a 2×2 joint probability table
2. Apply Bayes' theorem to a two-hypothesis urn problem
3. Identify where P(A|B) ≠ P(B|A) matters in a real-world scenario

**Exit condition:** Reader can compute posteriors for two-hypothesis
problems by hand before opening Chapter 1.

---

## CHAPTER 1 — The Same Question, Two Answers

**One-line:** The medical testing problem reveals what frequentist
statistics can and cannot say — and introduces the Bayesian alternative
that answers the question the test actually asks.

**The problem:** A patient tests positive for a rare disease. The test
is 99% accurate. What is the probability the patient actually has
the disease? Most people say 99%. The answer is not 99%.

**Learning outcomes:**
1. (Understand) Explain what a p-value does and does not say
2. (Analyze) Identify the specific question frequentist hypothesis
   testing cannot answer about a single patient's diagnosis
3. (Apply) Compute a posterior probability using Bayes' theorem
   for a two-hypothesis diagnostic problem
4. (Evaluate) Compare what each approach tells the clinician
   and what each leaves unanswered

**Frequentist solution:**
- Null hypothesis: patient does not have the disease
- Test statistic: positive result
- p-value calculation: P(positive test | no disease) = 0.01
- Decision: reject null at α = 0.01
- The wall: this says nothing about P(disease | positive test)
- What the clinician actually needs vs. what the test provides

**Where frequentist strains:**
The p-value answers "how surprising is this result if the patient
is healthy?" The clinician needs "how likely is this patient to be
sick?" These are not the same question. NHST has no mechanism to
answer the second question.

**Bayesian solution:**
- Prior: disease prevalence = 0.001 (1 in 1,000)
- Likelihood: P(positive | disease) = 0.99, P(positive | no disease) = 0.01
- Posterior via Bayes' theorem: P(disease | positive) ≈ 9%
- The answer: a positive result from a rare-disease test still means
  the patient probably doesn't have the disease

**Side-by-side comparison:**
| | Frequentist | Bayesian |
|---|---|---|
| Question answered | How surprising is the data? | How likely is the hypothesis? |
| Uses prevalence? | No | Yes — required |
| Output | Reject / fail to reject | Probability of disease |
| Clinician's decision | Ambiguous | Grounded |

**Prompting for implementation:**
Chapter 2 will teach the full prompting skill. This chapter closes
with the implementation problem left open: "In the next chapter,
you'll learn to prompt an LLM to run this calculation for any
disease prevalence and test accuracy. For now, do it by hand
for three different prevalence values: 0.001, 0.01, and 0.1.
What changes? What does this tell you?"

**Exercises:**
1. (Apply) Recompute the posterior for disease prevalence = 0.01
   and 0.1. What happens to the answer?
2. (Analyze) A lawyer argues that a DNA match (1 in 1,000,000 false
   positive rate) proves guilt. What is missing from this argument?
3. (Evaluate) A public health official wants to screen an entire
   city for a rare condition. Using what you know from this chapter,
   what would you tell them about interpreting positive results?

**Chapter bridge:** "You've seen that the Bayesian calculation requires
one thing the frequentist test ignores: the prior probability. In
Chapter 2, you'll learn to use an LLM to implement this calculation —
and to ask it the right questions so it doesn't make the same mistake
the frequentist test makes."

---

## CHAPTER 2 — Prompting for Statistics

**One-line:** Learn to use an LLM as a statistical implementation
partner — describing problems precisely, verifying outputs critically,
and iterating toward solutions that match what the math actually requires.

**The problem:** You can follow the Bayesian calculation from Chapter 1
by hand for simple cases. For anything more complex — different
distributions, multiple parameters, real datasets — you need
implementation help. This chapter teaches you how to get it reliably.

**Learning outcomes:**
1. (Apply) Prompt an LLM to implement a two-hypothesis Bayesian
   inference problem and verify the result matches hand calculation
2. (Analyze) Identify when an LLM's statistical output is wrong
   by checking it against the problem's structure
3. (Apply) Prompt for both frequentist and Bayesian solutions
   to the same problem and compare the outputs
4. (Create) Write a statistical problem description precise enough
   that an LLM produces correct, verifiable code on the first attempt

**Content blocks:**

*Block 1: Why prompting for statistics is different*
LLMs can produce plausible-looking wrong answers. Statistical code
that runs without errors can still compute the wrong thing. The
verification skill is as important as the generation skill.

*Block 2: The anatomy of a good statistical prompt*
- State the data generating process, not just the data
- Name the quantity you want, not just the analysis
- Specify both frameworks explicitly when you want comparison
- Ask for the mathematical steps, not just the code
- Request a plain-language interpretation alongside the output

*Block 3: Finishing Chapter 1's open problem*
Walk through prompting an LLM to compute P(disease | positive test)
for a range of prevalence values. Show what a good prompt looks like,
what the output should contain, and how to verify it against the
hand calculation from Chapter 1.

*Block 4: Prompting for comparison*
Template prompt structure for the book's standard comparative analysis:
"Solve [PROBLEM] using both a frequentist hypothesis test and a
Bayesian posterior calculation. Show the mathematical steps for each,
implement both in [language of your choice], and explain in plain
language what each result means and what each approach cannot tell us."

*Block 5: When to iterate*
Common failure modes in LLM statistical output and how to diagnose them:
- Correct code, wrong model (the LLM solved a different problem)
- Correct model, wrong interpretation (the math is right, the
  explanation confuses p-value with posterior probability)
- Frequentist answer dressed in Bayesian language
- Missing the prior entirely

**Worked example:** Complete prompting session for the medical testing
problem — initial prompt, LLM output, verification against hand
calculation, one iteration to fix an interpretation error, final output.
Shown as a dialogue, not a polished result.

**No frequentist/Bayesian comparison section** — this chapter is
a methods chapter. The comparison structure resumes in Chapter 3.

**Exercises:**
1. (Apply) Prompt an LLM to redo the Chapter 1 calculation for
   five different prevalence values. Verify two of them by hand.
2. (Analyze) Given a provided LLM output that contains an
   interpretation error, identify the error and write the
   corrected prompt.
3. (Create) Write a prompt for a new diagnostic problem (provided)
   that would produce both frequentist and Bayesian solutions with
   correct interpretations.

**Chapter bridge:** "From here forward, every chapter includes a
prompting section that applies this skill to that chapter's problems.
You won't need to implement everything from scratch — but you will
need to know enough to tell when the implementation is wrong."

---

## CHAPTER 3 — Counting and Estimating

**One-line:** The binomial problem — estimating a proportion —
run both ways, producing the book's first full side-by-side
comparison and the clearest possible illustration of the difference
between a confidence interval and a credible interval.

**The problem:** A quality control engineer tests 50 circuit boards
and finds 8 defective. What is the true defect rate? How confident
should she be in her estimate?

**Learning outcomes:**
1. (Apply) Construct a frequentist confidence interval for a proportion
2. (Apply) Build a Beta-Binomial Bayesian model and compute a
   credible interval
3. (Analyze) Explain the difference between what a confidence interval
   and a credible interval actually claim
4. (Evaluate) Assess when each approach is more useful for a
   quality control decision

**Frequentist solution:**
- Point estimate: p̂ = 8/50 = 0.16
- Standard error and normal approximation
- 95% confidence interval: [0.065, 0.255]
- What the CI actually means: 95% of intervals constructed
  this way contain the true rate — not a probability statement
  about this interval
- The practical problem: the engineer wants P(rate < 0.20) — and
  the confidence interval cannot give her that

**Where frequentist strains:**
The engineer needs to make a decision: is this batch acceptable?
She wants the probability the true defect rate is below a threshold.
The confidence interval does not give her this. It gives her a range,
with a frequentist guarantee about the procedure, not about this batch.

**Bayesian solution:**
- Prior: Beta(1,1) — uniform, no prior knowledge about this supplier
- Likelihood: Binomial(50, k, p)
- Posterior: Beta(9, 43) — conjugate update, closed form
- Posterior mean: 9/52 ≈ 0.173
- 95% credible interval: [0.081, 0.295]
- P(rate < 0.20 | data) = directly computable from the posterior
- The engineer can now answer her actual question

**Side-by-side comparison:**
| | Frequentist | Bayesian |
|---|---|---|
| Point estimate | 0.16 | 0.173 (posterior mean) |
| Interval | 95% CI [0.065, 0.255] | 95% CrI [0.081, 0.295] |
| Interval meaning | Procedure guarantee | Probability statement |
| P(rate < 0.20)? | Not available | Directly computable |
| Prior required? | No | Yes — uniform here |

**Why anyone uses frequentist methods here:**
Simple, fast, no prior required, widely accepted in manufacturing
quality standards. For large samples with no prior information,
the two approaches give nearly identical intervals. The frequentist
approach is a valid choice when the decision only requires the interval,
not a probability about a threshold.

**Prompting section:**
Prompt template for Beta-Binomial conjugate analysis. How to ask
for both approaches, how to verify the posterior by checking that
it peaks near the sample proportion, how to ask for P(p < threshold).

**Exercises:**
1. (Apply) A new supplier sends 30 boards; 3 are defective.
   Build both intervals. Does your conclusion about acceptability
   change between approaches?
2. (Analyze) Explain in plain language why the frequentist interval
   does not mean "there's a 95% chance the true rate is in this range."
3. (Evaluate) The engineer's quality standard requires P(defect rate
   < 0.15) > 0.80 before accepting a batch. Which approach can
   directly evaluate this criterion? Use the data from the chapter.

**Chapter bridge:** "The Beta-Binomial model works cleanly because
the prior and likelihood are conjugate — the math closes. In Chapter 4,
we'll compare two groups, where the clean closure starts to break down
and the choices each approach makes become more visible."

---

## CHAPTER 4 — Comparing Two Groups

**One-line:** The t-test and its Bayesian analog — same data,
different questions, and a first encounter with why statistically
significant results don't always replicate.

**The problem:** A university tests two versions of a statistics
tutorial. Group A (n=40) averages 72% on the post-test; Group B
(n=38) averages 76%. Is the new tutorial better?

**Learning outcomes:**
1. (Apply) Run and interpret a two-sample t-test
2. (Apply) Build a Bayesian two-group comparison with posterior
   distributions on both means
3. (Analyze) Explain the replication crisis as a consequence of
   ignoring prior probabilities, using Ioannidis's argument
4. (Evaluate) Assess what "statistically significant" does and
   does not establish about educational interventions

**Frequentist solution:**
- Two-sample t-test: t-statistic, degrees of freedom, p-value
- Effect size: Cohen's d
- The significance decision and what it licenses
- What it does not license: the probability the new tutorial is better

**Where frequentist strains:**
p < 0.05 tells us this result would be surprising if there were
no effect. It does not tell us the probability there is an effect.
Most educational interventions that "work" in one study fail to
replicate — and this chapter explains exactly why using Ioannidis's
Bayesian framing. The prior probability that any given educational
intervention produces a meaningful effect is low. Ignoring that
prior inflates apparent discovery rates.

**Bayesian solution:**
- Priors on both group means: weakly informative normal priors
- Posterior distributions on μ_A, μ_B, and the difference δ = μ_B - μ_A
- P(δ > 0 | data): the probability the new tutorial is actually better
- Credible interval on the effect size
- What changes with different priors — preview of Chapter 7

**Side-by-side comparison:**
| | Frequentist | Bayesian |
|---|---|---|
| Result | p = 0.03, significant | P(B better) = 0.91 |
| Effect size | Cohen's d = 0.31 | Posterior median δ = 4.1 points |
| Replication? | No prediction available | Posterior predictive check possible |
| Prior required? | No (hidden uniform) | Yes — named explicitly |

**Why anyone uses frequentist methods here:**
The t-test is fast, assumption-light, and its output (p-value)
is understood by every journal reviewer, IRB committee, and
department chair in the social sciences. Reporting a Bayesian
analysis in a field that expects p-values requires justification.
The frequentist approach is the lingua franca of educational research.

**The replication crisis sidebar:**
Ioannidis's argument in plain language: if most hypotheses tested
are false, and you use p < 0.05 as your threshold, most significant
results are false positives. This is not a misuse of statistics —
it is the correct consequence of applying NHST without priors.
The Bayesian approach requires stating the prior probability of
the hypothesis before seeing data — which forces the question
"how often are interventions like this actually effective?"

**Prompting section:**
Prompting for Bayesian two-group comparison. How to specify weakly
informative priors for test scores. How to extract P(δ > 0) from
LLM output and verify it makes intuitive sense.

**Exercises:**
1. (Apply) A new drug shows p = 0.04 in a trial of 30 patients.
   Using Ioannidis's argument, what additional information would
   you need before concluding the drug works?
2. (Analyze) A researcher says "we replicated the finding — both
   studies had p < 0.05." What is wrong with this reasoning?
3. (Evaluate) Given the tutorial data from this chapter, would you
   recommend the university adopt the new tutorial? Write a one-paragraph
   recommendation that uses both the frequentist and Bayesian results.

**Chapter bridge:** "Both approaches so far have dealt with
well-specified, relatively simple models. In Chapter 5, we add
a continuous predictor — regression — where the Bayesian solution
starts returning answers the frequentist solution structurally cannot."

---

## CHAPTER 5 — Regression, Both Ways

**One-line:** Linear regression as a frequentist workhorse and as
a Bayesian model — the solutions converge on the line, but diverge
on everything else that matters for decision-making.

**The problem:** A retail analyst has sales figures and advertising
spend for 60 weeks. She wants to know: does advertising drive sales,
and by how much? Should the company increase its advertising budget
next quarter?

**Learning outcomes:**
1. (Apply) Fit and interpret a frequentist linear regression model
2. (Apply) Specify and fit a Bayesian linear regression with priors
   on slope and intercept
3. (Analyze) Explain what a posterior predictive distribution is
   and why it's more useful than a prediction interval for decisions
4. (Evaluate) Assess the practical implications of the two approaches
   for the analyst's budget recommendation

**Frequentist solution:**
- OLS regression: coefficient estimates, standard errors, t-tests
- R², residual diagnostics
- 95% prediction interval for next quarter's sales
- The limit: the slope estimate is a point estimate with a standard
  error — not a probability distribution

**Where frequentist strains:**
The analyst's question is "should we increase the budget?" — a
decision under uncertainty. The frequentist answer gives her a
point estimate of the effect and a significance test. It cannot
directly give her P(sales increase > X | budget increase). The
prediction interval tells her where a new observation might fall —
not the probability the investment pays off.

**Bayesian solution:**
- Priors: weakly informative normal on slope and intercept,
  half-normal on σ
- Posterior distributions over all parameters
- Posterior predictive distribution for next quarter
- P(sales > threshold | budget increase): directly answerable
- Asymmetry named explicitly: this solution requires more specification
  and more computation than OLS, and is worth it when the decision
  requires probability statements about outcomes

**Side-by-side comparison:**
| | Frequentist | Bayesian |
|---|---|---|
| Slope estimate | 2.3 (SE = 0.4) | Posterior: mean 2.3, 95% CrI [1.5, 3.1] |
| Prediction | Interval [X, Y] | Full predictive distribution |
| P(ROI > 0)? | Not available | Directly computable |
| Computation | Closed form | MCMC or approximation |

**Why anyone uses frequentist regression:**
OLS is fast, interpretable, assumption-transparent, and produces
identical point estimates to MAP Bayesian regression with flat priors.
For description and explanation in stable settings, OLS is excellent.
The Bayesian approach earns its complexity cost when decisions require
probability statements about outcomes — not just estimates of effects.

**Prompting section:**
Prompting for Bayesian regression. How to specify weakly informative
priors for business data. How to ask for a posterior predictive
distribution and interpret it. How to extract P(outcome > threshold).

**Exercises:**
1. (Apply) Using the provided sales dataset from the companion website,
   fit both models and report: the slope estimate, the 95% interval
   (CI or CrI), and the probability that a 10% budget increase
   produces a sales increase of at least 5%.
2. (Analyze) The frequentist model shows p = 0.08 for the advertising
   coefficient. A manager concludes "advertising doesn't work."
   What has the manager missed?
3. (Evaluate) The analyst's company uses a decision threshold of
   P(ROI > 0) > 0.85 before approving budget increases. Can the
   frequentist model satisfy this criterion directly? What would
   you do?

**Chapter bridge:** "Regression assumes we know which model to fit.
In Chapter 6, we compare models — and the two approaches handle
that comparison in fundamentally different ways."

---

## CHAPTER 6 — Model Comparison

**One-line:** How do you choose between two models? Frequentist
model comparison requires choosing a test; Bayesian model comparison
produces a probability — and the difference matters most when
the models are close.

**The problem:** An epidemiologist is modeling disease spread.
She has two candidate models: a simple linear trend and an
exponential growth model. Both fit the early data reasonably well.
Which should she use to forecast the next 30 days?

**Learning outcomes:**
1. (Apply) Compare two models using AIC and likelihood ratio test
2. (Apply) Compute a Bayes factor comparing two models
3. (Analyze) Explain what AIC measures vs. what a Bayes factor measures
4. (Evaluate) Assess when model comparison produces a clear answer
   and when it doesn't — and what to do in each case

**Frequentist solution:**
- Likelihood ratio test for nested models
- AIC and BIC for non-nested models
- The winner: exponential (lower AIC by 4.2)
- The limit: AIC ranks models; it does not give the probability
  that the winning model is correct

**Where frequentist strains:**
The epidemiologist needs to communicate uncertainty to public health
officials. "The exponential model fits better" is not the same as
"there is an 85% probability the exponential model is the right one."
Frequentist model comparison produces rankings, not probabilities.
When models are close (ΔAIC < 4), the guidance is genuinely ambiguous.

**Bayesian solution:**
- Bayes factor: BF₁₀ = P(data | exponential) / P(data | linear)
- Jeffreys's classification of evidence strength
- Posterior model probabilities given equal priors
- Model averaging: using both models weighted by posterior probability
- When BF is close to 1 — what it means and what to do

**Side-by-side comparison:**
| | Frequentist | Bayesian |
|---|---|---|
| Output | ΔAIC = 4.2, exponential preferred | BF = 8.3, moderate evidence for exponential |
| Communicable? | "Fits better" | "8x more likely given the data" |
| Model averaging | Not standard | Natural — weight by posterior probability |
| Prior required? | No | Yes — on model parameters |

**Why anyone uses AIC:**
Fast, no prior required, well-understood by reviewers, and for
large samples with well-specified models, AIC and Bayes factors
often agree. AIC is the default in ecological, economic, and
epidemiological modeling for good reasons.

**Prompting section:**
Prompting for Bayes factor computation. How to ask for both AIC
and Bayes factor on the same model comparison. How to interpret
close calls and ask for model-averaged predictions.

**Exercises:**
1. (Apply) Using the provided epidemic dataset, compute AIC for
   both models and the Bayes factor. Do they agree on the winner?
2. (Analyze) ΔAIC = 1.8. What does this tell you? What does it
   not tell you? How does the Bayes factor change your conclusion?
3. (Evaluate) The epidemiologist must brief officials tomorrow.
   Write a two-sentence summary of the model comparison results
   that accurately represents what both approaches found.

**Chapter bridge:** "Model comparison assumes the models we're
comparing are the models worth comparing. In Chapter 7, we look
at the assumptions hidden inside both approaches — and make the
Bayesian ones explicit for the first time."

---

## CHAPTER 7 — Priors: Where Does Your Assumption Come From?

**One-line:** Every statistical analysis has prior assumptions.
Frequentist methods hide theirs in the machinery. Bayesian methods
name theirs explicitly. This chapter makes both visible — and shows
what changes when you change them.

**The problem:** Two analysts look at the same clinical trial data.
One concludes the treatment works. One concludes the evidence
is too weak to act on. Both used valid statistical methods.
How is this possible?

**Learning outcomes:**
1. (Analyze) Identify the implicit prior assumptions in a standard
   frequentist t-test
2. (Apply) Run the same Bayesian analysis with three different priors
   and document what changes
3. (Evaluate) Defend a prior choice using domain knowledge,
   pilot data, or principled ignorance
4. (Evaluate) Assess when prior sensitivity matters and when it doesn't

**The fairness test — why frequentist methods have real advantages:**
Frequentist methods don't require prior specification. In genuinely
novel situations with no prior knowledge — new drug classes, new
phenomena, exploratory research — specifying a prior is difficult
and potentially misleading. The demand for explicit priors is a
feature when knowledge exists and a burden when it doesn't.
Regulators (FDA, EMA) often require frequentist analyses precisely
because they are harder to game with convenient priors. This is
a real advantage, not a strawman.

**The hidden prior demonstration:**
A standard t-test implicitly assumes a uniform (flat) prior on
the true mean — it treats all possible values as equally likely
before seeing the data. This is itself a prior. It's just undeclared.
For a drug trial where the compound has failed three prior Phase II
trials, treating all effect sizes as equally likely is a strong
assumption — and usually a wrong one. The question is not whether
to have a prior. It's whether to name it.

**Bayesian solution — three priors, same data:**
- Prior 1: Uniform — "I know nothing"
- Prior 2: Weakly informative — "Effects of this size are plausible
  but large effects are unlikely" (half-normal on effect size)
- Prior 3: Informative — "Previous trials showed small or null effects"
  (normal centered near zero with small variance)
- Results: posterior distributions under each prior, side by side
- What changes: the tails. The point estimate barely moves.
  The probability of a large effect changes substantially.

**Prior sensitivity analysis:**
If your conclusion depends heavily on your prior choice, you need
a stronger prior justification — or you need more data. If your
conclusion is robust across reasonable priors, you can report
with confidence. Sensitivity analysis is not a weakness of the
Bayesian approach; it is its epistemic honesty.

**Why anyone uses frequentist methods (continued):**
In regulated industries, preregistered research, and large-sample
settings, the implicit uniform prior is a feature: it guarantees
reproducibility and removes the analyst's ability to choose a prior
that supports their preferred conclusion. The tradeoff is real.

**Prompting section:**
How to specify three different priors for the same problem and
run sensitivity analysis via LLM. How to ask for a prior sensitivity
plot and interpret it.

**Exercises:**
1. (Apply) Using the clinical trial data from this chapter, run
   the analysis under all three priors. Report: where do the
   posteriors agree? Where do they diverge?
2. (Analyze) A pharmaceutical company's statistician uses a prior
   centered on a large positive effect for their own drug.
   What concern does this raise, and how would you address it?
3. (Evaluate) A colleague says "Bayesian methods are subjective
   because they require priors." Write a response that is fair
   to both the concern and the Bayesian counterargument.

**Chapter bridge:** "Prior sensitivity matters most when data is
sparse. Chapter 8 takes you into the hardest inferential conditions:
small samples, rare events, and weak signals — exactly where
the prior does the most work."

---

## CHAPTER 8 — When Data Is Sparse

**One-line:** Small samples, rare events, and underpowered studies —
where frequentist methods break down, produce inflated estimates,
or simply refuse to run, and where Bayesian priors do their
most important work.

**The problem:** A hospital tracks rare surgical complications.
In 200 procedures over two years, 3 complications occurred.
Is the complication rate acceptable? Is it getting better or worse?
Standard frequentist tests produce wide intervals and ambiguous results.

**Learning outcomes:**
1. (Apply) Identify when standard frequentist methods are unreliable
   for sparse data
2. (Apply) Use informative priors to stabilize Bayesian estimates
   in small samples
3. (Analyze) Explain why statistically significant effects in
   underpowered studies are systematically too large (winner's curse)
4. (Evaluate) Assess the tradeoff between waiting for more data
   and acting on sparse evidence

**Frequentist solution:**
- Proportion test: 3/200 = 0.015, 95% CI [0.003, 0.043]
- The CI is technically correct but practically useless for the
  hospital's accreditation threshold
- Comparing to last year (2/150): p = 0.71, not significant
- The limit: with counts this small, the normal approximation
  fails and the test has almost no power

**Where frequentist strains — the winner's curse:**
Studies that achieve significance with small samples tend to report
effect sizes much larger than the true effect. When power is low,
the only way to clear the significance threshold by chance is with
an unusually large observed effect. This means published estimates
from underpowered studies are systematically inflated — not because
of fraud, but as a mathematical consequence of the threshold.
This is Bernoulli's fallacy in practice.

**Bayesian solution:**
- Prior from published literature on complication rates for
  this procedure type: Beta(3, 200) — encodes "typically around 1.5%"
- Posterior: Beta(6, 397)
- Posterior mean: 1.49%, 95% CrI [0.55%, 3.18%]
- Tighter and more actionable than the frequentist CI
- Year-over-year comparison: posterior on the change, with probability
  that the rate has improved

**Bayesian shrinkage:**
With sparse data, Bayesian estimates shrink toward the prior —
which is the right thing to do when the data are too sparse to
speak for themselves. This is not bias; it is regularization.
The hospital's estimate is pulled toward the known distribution
of outcomes for this procedure, which is more accurate than
treating 3 events as the only evidence.

**Why anyone uses frequentist methods here:**
In purely exploratory settings with genuinely no prior knowledge —
a novel procedure with no literature — the frequentist approach
makes the sparsity visible rather than smoothing it away with
a prior. Reporting "the data are too sparse to conclude anything"
is sometimes the honest answer.

**Prompting section:**
How to specify an informative prior from published literature.
How to ask an LLM to extract a prior from a reported mean and
confidence interval. How to run a Bayesian trend analysis with
sparse counts.

**Exercises:**
1. (Apply) A rare disease affects 0.1% of the population.
   In a study of 500 patients, 1 develops the disease after
   a new drug. Build both a frequentist and Bayesian estimate
   of the drug's effect on disease incidence.
2. (Analyze) A study with n=20 reports a significant effect
   (p = 0.04, d = 0.8). A replication with n=200 finds p = 0.06,
   d = 0.2. Using the winner's curse, explain what likely happened.
3. (Evaluate) When is Bayesian shrinkage helpful? When could it
   lead you astray? Give one example of each.

**Chapter bridge:** "Sparse data at the observation level is one
challenge. Chapter 9 introduces a different kind of sparsity:
data with natural grouping structure, where some groups have
many observations and some have few — and where borrowing
strength across groups is the central statistical question."

---

## CHAPTER 9 — Hierarchical Problems

**One-line:** Data with natural grouping structure — students in
schools, patients in hospitals, users in cities — requires models
that share information across groups. This is where the frequentist
and Bayesian approaches diverge most sharply, and where the
Bayesian asymmetry is most pronounced.

**Asymmetry notice (stated explicitly at chapter opening):**
"This chapter spends more space on the Bayesian solution than
any prior chapter. That asymmetry is the lesson. Hierarchical
Bayesian models are substantially more complex than their
frequentist analogs — and the extra complexity buys something
real: a principled way to share information across groups
that frequentist mixed models approximate but do not fully
characterize. By the end of this chapter, you'll understand
what the complexity buys."

**The problem:** A school district wants to assess math performance
across 30 schools. Some schools have 200 students tested; some
have 8. How do you estimate each school's true performance
without letting small schools produce wildly unstable estimates?

**Learning outcomes:**
1. (Understand) Explain the partial pooling problem and why it
   requires a hierarchical model
2. (Apply) Fit a frequentist mixed-effects model for grouped data
3. (Apply) Specify and interpret a Bayesian hierarchical model
4. (Analyze) Compare complete pooling, no pooling, and partial
   pooling — what each assumes and what each gets wrong
5. (Evaluate) Assess when the additional complexity of a Bayesian
   hierarchical model is worth the cost

**Frequentist solution:**
- Complete pooling: ignore school membership, treat all students
  the same. Simple, wrong.
- No pooling: estimate each school separately. Unstable for small schools.
- Mixed-effects model (lme4 or equivalent): fixed effects for
  district-wide predictors, random effects for schools
- The limit: random effects in mixed models are estimated, not
  given a full posterior distribution — the uncertainty in the
  school-level estimates is not fully propagated

**Where frequentist strains:**
For the 4 schools with fewer than 10 students, the no-pooling
estimates are nearly meaningless. The mixed-effects model handles
this by shrinking small-school estimates toward the district mean —
but it does not give you a posterior distribution over each school's
true performance, and the uncertainty in the shrinkage itself
is not reported.

**Bayesian solution:**
- Hyperprior on school-level means: Normal(μ_district, τ)
- Prior on district mean μ_district: weakly informative
- Prior on between-school variance τ: half-normal
- School-level posteriors: each school gets a full posterior
  distribution, with uncertainty that reflects both its own
  data and the district-wide distribution
- Partial pooling is automatic and calibrated: small schools
  shrink more, large schools retain their own data

**Side-by-side comparison:**
| | Frequentist mixed model | Bayesian hierarchical |
|---|---|---|
| Small school estimates | Shrunk, unstable SE | Full posterior, calibrated |
| Uncertainty in shrinkage | Not propagated | Fully propagated |
| District-level inference | Fixed effect | Posterior on hyperparameter |
| Computation | Fast (REML) | Slow (MCMC) |
| Interpretability | Standard in social science | Requires explanation |

**Why anyone uses frequentist mixed models:**
Fast, widely understood, output interpretable to education
researchers and policy makers, implemented in standard software.
For large, balanced datasets where the variance components are
well-identified, mixed models and Bayesian hierarchical models
give nearly identical answers. The Bayesian approach earns its
complexity cost when group sizes are very unequal, when the
uncertainty in variance components matters, or when you need
full posterior distributions for decision-making.

**Prompting section:**
This chapter's prompting section is longer than previous chapters —
specifying a hierarchical model requires more precision. How to
describe a two-level hierarchy to an LLM. How to specify hyperpriors.
How to ask for school-level posterior distributions and interpret them.

**Exercises:**
1. (Apply) Using the school district dataset from the companion
   website, fit both the mixed-effects model and the Bayesian
   hierarchical model. Compare the estimates for the 5 smallest
   schools. What changes?
2. (Analyze) A school with 6 students scores 95% average.
   The district average is 72%. Under complete pooling, no pooling,
   and partial pooling, what is your estimate of this school's
   true performance? Which do you trust most and why?
3. (Evaluate) A district official wants to rank all 30 schools
   and publish the rankings. Using what you know from this chapter,
   what concerns would you raise about this plan?

**Chapter bridge:** "Hierarchical models handle grouped structure
in cross-sectional data. Chapter 10 introduces structure in time —
and sequential updating, which is Bayesian inference in its most
natural form."

---

## CHAPTER 10 — Time and Sequence

**One-line:** Time series analysis and sequential updating —
where the Bayesian approach is most intuitive, because the posterior
from today is the prior for tomorrow.

**The problem:** An inventory manager tracks weekly demand for
a product over 52 weeks. She needs to forecast next quarter's
demand for ordering decisions. Demand is trending upward but
noisy. How should she update her forecast as new data arrives?

**Learning outcomes:**
1. (Apply) Fit a frequentist ARIMA model and produce a point forecast
2. (Apply) Build a Bayesian structural time series model with
   sequential updating
3. (Analyze) Explain sequential updating as a natural consequence
   of Bayesian inference
4. (Evaluate) Assess the practical value of a predictive distribution
   vs. a point forecast for inventory decisions

**Frequentist solution:**
- ARIMA model selection (ACF/PACF)
- Point forecast with prediction interval
- The limit: the prediction interval grows as the horizon extends —
  but it doesn't tell the manager the probability of stocking out

**Bayesian solution:**
- Bayesian structural time series: local level + trend components
- Sequential updating: after each week, posterior becomes next week's prior
- Predictive distribution for next quarter
- P(demand > threshold | data): directly computable for reorder decisions
- The natural updating demo: show the forecast narrowing as weeks pass

**Sequential updating as the Bayesian core:**
This chapter demonstrates Bayesian inference in its most intuitive
form. The manager starts with a prior on demand. Each week's data
updates the posterior. The posterior becomes the prior for the
following week. This is not a special feature of time series —
it is what Bayesian inference always does. Time series just makes
the sequential structure visible.

**Why anyone uses ARIMA:**
Fast, well-understood, implemented everywhere, and for stationary
series with enough data, produces forecasts as accurate as Bayesian
alternatives at much lower computational cost. The Bayesian approach
earns its complexity when the decision requires probability
statements about future values, not just point forecasts.

**Prompting section:**
How to prompt for ARIMA model selection and Bayesian structural
time series in the same session. How to ask for a sequential
updating visualization. How to extract P(future value > threshold).

**Exercises:**
1. (Apply) Using the BLS employment data from the companion website,
   fit both an ARIMA model and a Bayesian structural time series
   for an occupation category of your choice. Compare the 12-week
   forecasts.
2. (Analyze) The ARIMA prediction interval for week 52 is [8,200, 14,600]
   units. What can the manager conclude? What can she not conclude?
3. (Evaluate) The manager's reorder threshold is 10,000 units.
   Which approach can directly compute the probability of needing
   to reorder? Use the Bayesian model to compute it.

**Chapter bridge:** "Time series is about sequential decisions over
time. Chapter 11 is about classification decisions — where the
output of inference is not an estimate or a forecast, but an
assignment: this case is class A or class B. The decision-theoretic
framing becomes explicit."

---

## CHAPTER 11 — Classification and Decision

**One-line:** Classification as statistical inference — where the
choice of threshold is a decision under a loss function, and
making that loss function explicit is the difference between
a model and a decision tool.

**The problem:** A loan officer builds a model to predict default.
The model outputs a probability. She needs to decide: above what
probability does she decline the loan? The threshold is not
a statistical question. It is a decision under costs.

**Learning outcomes:**
1. (Apply) Fit frequentist logistic regression and interpret the
   output as a classification model
2. (Apply) Build a Bayesian logistic regression with posterior
   predictive classification
3. (Analyze) Explain what loss function is implied by a given
   classification threshold
4. (Evaluate) Assess the decision-theoretic implications of
   threshold choices under asymmetric costs

**Frequentist solution:**
- Logistic regression: coefficient estimates, odds ratios, p-values
- Default threshold of 0.5: what it implies about costs
- ROC curve and AUC
- The limit: logistic regression gives a probability, but the
  threshold choice is not part of the model — it is imported
  from outside, usually arbitrarily

**Bayesian solution:**
- Bayesian logistic regression: posterior distributions on
  all coefficients
- Posterior predictive probability for each applicant
- Explicit loss function: cost of false positive (declined good loan)
  vs. false negative (approved bad loan)
- Optimal threshold derived from the posterior and the loss function
- Uncertainty in the threshold itself: the posterior on the optimal
  threshold given uncertainty in parameters

**The loss function revelation:**
A threshold of 0.5 assumes false positives and false negatives
are equally costly. For loan decisions, they are not. Stating
the loss function explicitly makes the decision defensible
and auditable. The frequentist model produces the probability;
the Bayesian framework integrates the probability with the costs.

**Why anyone uses frequentist logistic regression:**
It is the industry standard for credit scoring, fraud detection,
and medical diagnosis. Regulators, auditors, and courts understand
it. The output (log-odds, coefficients) is interpretable. For large
datasets where parameter uncertainty is small, the frequentist and
Bayesian point estimates are identical. The Bayesian approach earns
its complexity when parameter uncertainty is significant enough to
affect the threshold choice — typically in small or imbalanced datasets.

**Connection to Irreducibly Human series:**
BLS/O*NET data: predicting occupational vulnerability to automation
is a classification problem. This chapter's framework applies
directly to that problem — and the threshold choice (at what
probability do we call an occupation "at risk"?) is exactly
the kind of decision-theoretic question the series is built around.
Students can use the companion website's O*NET data for one exercise.

**Prompting section:**
How to specify an asymmetric loss function to an LLM for threshold
optimization. How to ask for posterior predictive distributions
from Bayesian logistic regression. How to request a decision-theoretic
analysis of a classification threshold.

**Exercises:**
1. (Apply) Using the provided loan dataset, fit both models.
   At threshold 0.5, what are the false positive and false negative
   rates? How do these change at threshold 0.3? At 0.7?
2. (Analyze) The bank estimates the cost of approving a bad loan
   is 5× the cost of declining a good loan. What threshold does
   this loss function imply? Use the Bayesian model to find it.
3. (Evaluate — O*NET connection) Using the occupation dataset
   on the companion website, build a classifier that predicts
   whether an occupation has above-median automation exposure.
   What threshold would you recommend, and what loss function
   does it imply?

**Chapter bridge:** "Chapters 1–11 have given you the toolkit.
Chapter 12 turns you loose on a real dataset of your choice —
the full comparative analysis, both frameworks, your judgment."

---

## CHAPTER 12 — A Real Problem, Both Ways

**One-line:** One real dataset, one real question, both frameworks
deployed completely — the deliverable is not which approach won
but a written comparison that demonstrates statistical judgment.

**The problem:** Student-selected from the companion website
dataset library. Each dataset comes with 2–3 pre-specified
analysis questions that support both frequentist and Bayesian
treatment. Students choose the dataset; the questions are provided.

**Learning outcomes:**
1. (Apply) Conduct a complete frequentist analysis for a
   self-selected real dataset
2. (Apply) Conduct a complete Bayesian analysis for the same dataset
3. (Evaluate) Compare the outputs of both analyses and identify
   where they agree, where they diverge, and why
4. (Create) Produce a written methodological justification for
   a preferred approach given the analysis goals

**Dataset library (companion website):**
All datasets drawn from BLS/O*NET and related public sources.
Selection criteria:
- Real, documented, publicly available
- Two plausible analysis questions per dataset
- Tractable in a single work session
- Domain-agnostic (student in any major can engage)
- Includes a data preparation prompt (pointing to the companion
  data preparation reference) for students who need it

Dataset categories available:
- Occupational wage distributions (BLS)
- Employment trend by occupation cluster (BLS/O*NET)
- Automation exposure by occupation (O*NET)
- Educational attainment and earnings (BLS)
- Regional labor market variation (BLS)

**Chapter structure:**
This chapter is a guided project, not a lecture chapter.
It provides:
1. Dataset selection guide with selection prompt template
2. Analysis scaffold: the six questions every comparative analysis
   must answer (see below)
3. Worked partial example: one dataset analyzed halfway,
   showing what a strong comparison looks like
4. Writing guide: how to document a methodological choice

**The six questions every comparative analysis must answer:**
1. What is the data generating process? What does each framework assume about it?
2. What did the frequentist analysis find? What can it not tell you?
3. What did the Bayesian analysis find? What prior did you use and why?
4. Where do the analyses agree? Where do they diverge?
5. Which approach better serves the analysis goal, and why?
6. What would change your conclusion?

**Deliverable:** A written comparative analysis (4–6 pages) that
answers all six questions. Not a lab report — an argument about
method, grounded in results.

**Prompting section:**
Dataset selection prompt template. Analysis scaffold prompts.
How to prompt for a comparative summary that answers all six questions.

**No traditional exercises** — the chapter IS the exercise.

**Chapter bridge:** "Chapter 12 asked you to choose. Chapter 13
gives you a framework for making that choice systematically —
not for every problem, but for the problems you'll actually face."

---

## CHAPTER 13 — Choosing

**One-line:** Not a verdict — a framework for choosing between
statistical approaches based on what the problem actually requires,
what the decision maker actually needs, and what the data can
actually support.

**The problem:** You now have both toolkits. When do you use which?
The answer is not always "Bayesian" — and this chapter explains why.

**Learning outcomes:**
1. (Analyze) Identify the decision factors that favor frequentist
   methods for a given problem
2. (Analyze) Identify the decision factors that favor Bayesian
   methods for a given problem
3. (Evaluate) Apply a structured decision framework to method
   selection for novel problems
4. (Create) Write a methodological justification for approach
   selection that would satisfy a skeptical reviewer

**Content blocks:**

*Block 1: When frequentist methods are the right choice*
- Large samples where prior information is genuinely absent
- Regulated environments where prior-free analysis is required
  (clinical trials, manufacturing quality standards)
- Exploratory research where the goal is hypothesis generation,
  not hypothesis confirmation
- Audiences who need p-values and can't be persuaded otherwise
- Computational constraints where MCMC is not feasible

*Block 2: When Bayesian methods earn their complexity cost*
- Decision problems requiring P(outcome > threshold)
- Small samples where prior knowledge can stabilize estimates
- Sequential updating problems where data arrives over time
- Hierarchical data where partial pooling matters
- Problems where parameter uncertainty affects the decision
- When you need to communicate probability, not just significance

*Block 3: The decision framework*
A structured guide — not a flowchart, a set of questions:
1. What quantity does the decision maker actually need?
   (Probability vs. significance vs. point estimate)
2. Is prior information available and defensible?
3. How large is the sample relative to the effect size?
4. What audience will receive the results?
5. What are the computational and time constraints?

*Block 4: What the book has not covered*
Honest accounting of what's beyond this text:
- Full MCMC implementation (pointer to McElreath)
- Non-parametric Bayesian methods
- Frequentist corrections for multiple comparisons
- Robust statistics for non-normal data
- Causal inference (pointer to companion volume
  `causal-inference-with-case-studies`)

*Block 5: The metacognitive close*
"You have built both toolkits. The question is no longer which
approach is correct — it is which approach is correct for this
problem, this data, this decision, and this audience. That is
a judgment, not a formula. Statistics can inform judgments.
It cannot replace them."

**Prompting section:**
How to prompt an LLM to help you select a statistical approach
for a new problem. Template: "Given [PROBLEM DESCRIPTION], which
statistical approach would you recommend and why? What are the
main assumptions of each approach for this problem?"

**Exercises:**
1. (Evaluate) For each of five provided problem descriptions,
   recommend an approach and justify it using the decision framework.
2. (Create) Take the analysis from Chapter 12 and write a
   methodological justification for your approach choice that
   addresses the most likely objection from a reviewer who
   prefers the other approach.
3. (Evaluate) A colleague says "I always use Bayesian methods
   because they're more principled." Respond to this claim using
   what you know from the full book.

---

## Semester Map

| Week | Chapter | Act |
|---|---|---|
| 0 (pre-course) | Ch 0 — Probability Foundations | Pre-arc |
| 1 | Ch 1 — The Same Question, Two Answers | Act One |
| 2 | Ch 2 — Prompting for Statistics | Act One |
| 3 | Ch 3 — Counting and Estimating | Act One |
| 4 | Ch 4 — Comparing Two Groups | Act One |
| 5 | **Exam 1 / Act One Review** | — |
| 6 | Ch 5 — Regression, Both Ways | Act Two |
| 7 | Ch 6 — Model Comparison | Act Two |
| 8 | Ch 7 — Priors | Act Two |
| 9 | Ch 8 — When Data Is Sparse | Act Two |
| 10 | Ch 9 — Hierarchical Problems | Act Two |
| 11 | **Exam 2 / Project Milestone** | — |
| 12 | Ch 10 — Time and Sequence | Act Three |
| 13 | Ch 11 — Classification and Decision | Act Three |
| 14 | Ch 12 — A Real Problem, Both Ways | Act Three |
| 15 | Ch 13 — Choosing | Act Three |

**Chapter count:** 13 primary + Chapter 0. TARGET MET (12–14).
**Semester fit:** 15 weeks with 2 exam/review weeks. CLEAN.

---

## Open Questions Log

| # | Question | Stakes | Status |
|---|---|---|---|
| 1 | Working title for Kindle listing? | Cover, SEO, series positioning | OPEN |
| 2 | Companion website URL and launch timeline | Chapter 12 depends on it | OWNED — data downloaded, site before book ships |
| 3 | Data preparation reference book — which one? | Ch 12 pointer | OPEN |
| 4 | Does Ch 13 include a printable decision guide artifact? | Feature, /m2 | OPEN |
| 5 | Does the book reference Clayton's *Bernoulli's Fallacy* explicitly? | Framing, bibliography | OPEN |
| 6 | Series branding — does this carry the Irreducibly Human mark? | Cover, positioning | OPEN |

---

*Built from: intake-bayesian-howto.md + arc-bayesian-howto.md*
*Design decisions confirmed: comparative anatomy, explicit asymmetry,
Chapter 0 prerequisites, Chapter 2 prompting primer, Option B
prompt-as-skill, BLS/O*NET companion datasets, Bear Brown LLC
$1/Kindle Unlimited publishing, Irreducibly Human series context.*
