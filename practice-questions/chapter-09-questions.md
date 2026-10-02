## Chapter 9: Probability Distributions and Hypothesis Testing — Practice Questions

**Q1.** A data scientist runs a hypothesis test comparing conversion rates and obtains a p-value of 0.03 with a pre-registered significance level of 0.05. Which conclusion is correct?

A) Reject the null hypothesis; the result is statistically significant at alpha=0.05
B) There is a 3% probability that the null hypothesis is true
C) Accept the alternative hypothesis as proven true
D) The test is inconclusive because p is close to zero

<details>
<summary>Answer</summary>

**Correct: A**

p=0.03 < alpha=0.05 means the observed data would be unlikely under the null, so we reject the null hypothesis at the chosen significance level.

**Why the others are wrong:**
- A p-value is not the probability the null is true; it's the probability of observing data this extreme given the null is true.
- Statistics never 'prove' a hypothesis true — we only reject or fail to reject the null.
- 0.03 is a low, not high, p-value; this describes the opposite behavior of an inconclusive result.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q2.** A retailer wants to compare average customer spend across four different store layouts to see if any layout differs significantly from the others. Which test BEST fits this requirement?

A) One-way ANOVA
B) Two-sample t-test
C) Chi-squared test of independence
D) Paired t-test

<details>
<summary>Answer</summary>

**Correct: A**

ANOVA is designed to compare means across three or more independent groups using a single omnibus test, avoiding inflated Type I error from multiple pairwise t-tests.

**Why the others are wrong:**
- A two-sample t-test only compares two groups, not four.
- Chi-squared tests categorical association/frequency data, not continuous means.
- A paired t-test requires matched observations from the same subjects, not independent store layouts.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q3.** A survey records whether customers are 'Satisfied' or 'Unsatisfied' and whether they are from 'Urban' or 'Rural' regions. The analyst wants to know if satisfaction is associated with region. Which test BEST fits this requirement?

A) One-way ANOVA
B) Paired t-test
C) Poisson regression
D) Chi-squared test of independence

<details>
<summary>Answer</summary>

**Correct: D**

The chi-squared test of independence evaluates association between two categorical variables using a contingency table, exactly matching satisfaction vs region.

**Why the others are wrong:**
- ANOVA compares means of continuous variables across groups, not categorical frequency counts.
- A paired t-test requires continuous matched-pair data, not independent categorical counts.
- Poisson regression models count outcomes as a function of predictors, not a simple 2x2 association test.

</details>

---

**Q4.** A company measures blood pressure in the same 50 patients before and after a treatment. Which test correctly accounts for the paired structure of this data?

A) Independent two-sample t-test
B) One-way ANOVA
C) Chi-squared test
D) Paired t-test

<details>
<summary>Answer</summary>

**Correct: D**

Paired t-tests are used when the same subjects are measured twice (before/after), because it analyzes the differences within pairs, controlling for individual variability.

**Why the others are wrong:**
- An independent two-sample t-test assumes two separate, unrelated groups — not the same patients measured twice.
- ANOVA is for three or more independent groups, not a two-condition paired design.
- Chi-squared applies to categorical frequency data, not continuous paired measurements.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q5.** A call center wants to model the number of customer complaints received per hour, where complaints occur independently at a constant average rate. Which distribution BEST models this scenario?

A) Normal distribution
B) Binomial distribution
C) Exponential distribution
D) Poisson distribution

<details>
<summary>Answer</summary>

**Correct: D**

The Poisson distribution models the count of independent events occurring at a constant average rate within a fixed interval, exactly matching complaints per hour.

**Why the others are wrong:**
- Normal distribution models continuous, symmetric data, not discrete event counts.
- Binomial requires a fixed number of trials with success/failure outcomes, not an open-ended count per time interval.
- Exponential models the time between events, not the count of events in an interval.

</details>

---

**Q6.** An analyst lowers the significance level (alpha) from 0.05 to 0.01 to be more conservative about false positives. What is the direct tradeoff of this change, all else being equal?

A) Type I error risk decreases; Type II error risk decreases
B) Type I error risk increases; Type II error risk decreases
C) Both Type I and Type II error risk remain unchanged
D) Type I error risk decreases; Type II error risk increases

<details>
<summary>Answer</summary>

**Correct: D**

Lowering alpha makes it harder to reject the null (reducing false positives/Type I error) but increases the chance of failing to detect a true effect (Type II error), holding sample size and effect size constant.

**Why the others are wrong:**
- Type I and Type II error move in opposite directions when only alpha changes, not the same direction.
- Lowering alpha decreases, not increases, Type I error risk by definition.
- The tradeoff is a core exam concept; error rates are directly affected by the chosen alpha threshold.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q7.** A team runs 20 independent hypothesis tests at alpha=0.05 without any adjustment. Which correction should they apply to control the family-wise error rate?

A) Apply Bonferroni correction by dividing alpha by the number of tests (0.05/20 = 0.0025)
B) Increase alpha to 0.10 for each test
C) Run a single ANOVA instead and ignore individual p-values
D) No correction is needed if each test uses a different dataset

<details>
<summary>Answer</summary>

**Correct: A**

The Bonferroni correction divides the desired overall alpha by the number of comparisons, giving a stricter per-test threshold (here 0.0025) to control the family-wise error rate across multiple comparisons.

**Why the others are wrong:**
- Increasing alpha would make false positives more likely, worsening the multiple comparisons problem.
- Replacing all pairwise tests with ANOVA doesn't apply when the tests measure different hypotheses/variables, not group means.
- Running multiple tests, even on different datasets, still inflates the overall chance of at least one false positive without correction.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q8.** Which statement correctly describes the Central Limit Theorem (CLT)?

A) The population must be normally distributed for the CLT to apply
B) The CLT guarantees that individual data points become normally distributed as sample size grows
C) The CLT only applies to binomial and Poisson distributions, not continuous data
D) The sampling distribution of the sample mean approaches a normal distribution as sample size increases, regardless of the population's shape

<details>
<summary>Answer</summary>

**Correct: D**

The CLT states that as sample size increases (commonly n≥30 as a rule of thumb), the distribution of the sample mean approaches normality regardless of the underlying population distribution's shape.

**Why the others are wrong:**
- The CLT specifically applies even when the population is NOT normally distributed — that's its key value.
- The CLT concerns the sampling distribution of the mean, not the distribution of individual raw data points.
- The CLT is a general theorem applicable across distribution types, not limited to binomial and Poisson.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

