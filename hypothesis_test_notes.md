# Hypothesis Test Notes — Campaign Experiment Analysis

## Metric Being Tested
**Paid Conversion Rate** — the proportion of users who converted to a paid subscription within 30 days of signup.

## Reason for Choosing This Metric
Paid Conversion Rate is the North Star metric for this experiment. It directly measures whether the new onboarding campaign achieves its core business objective: converting free/trial users into paying customers. It connects directly to revenue growth and is the most meaningful signal of campaign effectiveness.

---

## Hypotheses

**Null Hypothesis (H₀):**
The paid conversion rate of the Treatment group is equal to or less than the paid conversion rate of the Control group.
> H₀: p_treatment ≤ p_control

**Alternate Hypothesis (H₁):**
The paid conversion rate of the Treatment group is greater than the paid conversion rate of the Control group.
> H₁: p_treatment > p_control

---

## Test Design

| Parameter | Value |
|-----------|-------|
| Test Type | Two-Proportion Z-Test |
| Tails | One-tailed (right-tailed) — testing for improvement only |
| Significance Level (α) | 0.05 |
| Confidence Level | 95% |

**Why one-tailed?**
The business question is directional: "Did the campaign *improve* conversion?" We are not testing for any difference — only improvement. A one-tailed test is more powerful for this specific hypothesis.

**Why Z-test?**
Both group sample sizes are large (n > 30) and the metric is a binary proportion (converted / not converted), making a two-proportion Z-test the appropriate choice.

---

## Test Inputs

| Input | Value |
|-------|-------|
| Control group size (n) | 690 |
| Control conversions | 22 |
| Control conversion rate | 3.19% |
| Treatment group size (n) | 710 |
| Treatment conversions | 50 |
| Treatment conversion rate | 7.04% |
| Pooled proportion | 0.0514 |
| Standard Error | 0.011807 |

---

## Test Output

| Output | Value |
|--------|-------|
| Z-Statistic | **3.2640** |
| P-Value (one-tailed) | **0.000549** |
| 95% CI for difference | [+1.56%, +6.15%] |
| Critical Z (α=0.05) | 1.645 |
| Lift | +120.9% relative improvement |

---

## Decision Rule
- If p-value < 0.05 → Reject H₀ (statistically significant improvement)
- If p-value ≥ 0.05 → Fail to reject H₀ (insufficient evidence)

**Result: p-value = 0.000549 < 0.05 → REJECT H₀**

---

## Business Interpretation
The Treatment group achieved a paid conversion rate of 7.04% vs 3.19% in the Control group — a statistically significant improvement of +120.9% (Z=3.26, p=0.0005). The 95% confidence interval for the difference [+1.56%, +6.15%] does not include zero, confirming the result is not due to chance.

**However**, the hypothesis test result alone is not sufficient to recommend a full launch. Guardrail metrics must also be evaluated:

- Support ticket rate increased significantly in Treatment (37.3% vs 22.0%, p<0.001) — a major red flag indicating the new experience causes confusion or friction for a large portion of users.
- Refund requests appeared only in the Treatment group (3 refunds vs 0 in Control).
- Engagement score improved in Treatment (62.9 vs 57.0), which is a positive signal.

**Interpretation Logic:**
Even though the primary metric improved significantly, the simultaneous spike in support tickets suggests the campaign may be driving conversions through pressure or confusion rather than genuine value — creating long-term retention risk. The recommendation is a conditional/phased launch, not an immediate full rollout.

---

## Limitations
- Sample size for converters is small (72 total converters), making ARPU and days-to-convert estimates less stable.
- The experiment ran across different signup dates — potential temporal confounds.
- Support ticket rate increase needs root cause investigation before dismissing.
