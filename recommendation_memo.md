# Recommendation Memo
**To:** Leadership / Product & Growth Teams
**From:** Business Analyst
**Re:** Campaign Experiment — Launch Decision
**Date:** June 2025

---

## Executive Summary
The new onboarding and activation campaign (Treatment) produced a statistically significant improvement in paid conversion rate (+120.9%, p=0.0005). However, a critical guardrail metric — support ticket rate — spiked by +69.4% in the Treatment group, which represents a material operational and retention risk. Based on this analysis, **a full immediate launch is not recommended**. A phased launch targeting the highest-performing, lowest-risk segments is the appropriate next step.

---

## Business Problem Statement
The company needs to decide whether to replace the existing onboarding experience with a new campaign-driven experience for all new users. The decision impacts the Product, Growth, and Customer Success teams. The primary metric that must improve is **paid conversion rate**. Risks to monitor include support load, refund rate, and long-term engagement quality. Evidence required: statistically significant conversion lift with no significant deterioration in guardrail metrics.

---

## North Star Metric
**Paid Conversion Rate** = Users who converted to paid / Total users in group

**Why this is the North Star:**
- It is the most direct measure of whether the campaign achieves its core objective
- It connects directly to revenue and business growth
- It captures the full funnel outcome (awareness → trial → payment)

**Why other metrics are supporting:**
- Landing page visit rate and trial start rate are intermediate funnel steps — necessary but not sufficient
- ARPU measures revenue quality but depends on conversion happening first
- Engagement score measures product value but does not guarantee monetization

**Risk of optimizing blindly:**
If conversion rate is maximized through aggressive prompts or dark patterns, users may convert but churn quickly, increasing refund rates and support burden — eroding LTV while short-term numbers look good.

---

## KPI Tree Summary

```
[NORTH STAR: Paid Conversion Rate]
         |
  ┌──────┼──────┐
  ▼      ▼      ▼
Activation  Engagement   Revenue
Funnel      Quality      Outcome
  |           |              |
Landing    Engagement     ARPU
Page Rate  Score          |
Trial      Days to        Revenue per
Start Rate Convert        Converted User
Onboarding Feature        Plan Mix
Completion Adoption

GUARDRAIL METRICS:
- Refund Rate (must stay near 0%)
- Support Ticket Rate (must not spike)
- Segment-level conversion decline
```

See `outputs/kpi_tree.png` for the full visual.

---

## Experiment Result Summary

| Metric | Control | Treatment | Lift | Significant? |
|--------|---------|-----------|------|--------------|
| Users | 690 | 710 | — | — |
| Landing Page Visit Rate | 60.9% | 65.5% | +7.6% | — |
| Trial Start Rate | 14.6% | 18.9% | +29.5% | — |
| Onboarding Completion Rate | 7.0% | 11.7% | +67.5% | — |
| **Paid Conversion Rate** | **3.19%** | **7.04%** | **+120.9%** | **Yes (p=0.0005)** |
| ARPU | ₹51.97 | ₹54.25 | +4.4% | — |
| Refund Rate | 0.00% | 0.42% | — | ⚠️ Watch |
| Support Ticket Rate | 22.0% | 37.3% | +69.4% | ⚠️ Yes (p<0.001) |
| Avg Engagement Score | 57.03 | 62.94 | +10.4% | ✅ Yes |

---

## Hypothesis Test Interpretation
A two-proportion Z-test (one-tailed, α=0.05) was conducted on paid conversion rate.

- Z-statistic: **3.264**
- P-value: **0.000549** (< 0.05)
- 95% CI for difference: **[+1.56%, +6.15%]**
- **Decision: Reject H₀ — the improvement is statistically significant**

The conversion improvement is real and not due to random chance. However, statistical significance alone is not sufficient for a launch decision.

---

## Guardrail Analysis

### 1. Support Ticket Rate ⚠️ RISK — HIGH
- Control: 22.0% | Treatment: 37.3% | Increase: +69.4%
- Statistically significant (p < 0.001)
- **Interpretation:** Nearly 4 in 10 Treatment users raised a support ticket. This strongly suggests the new onboarding experience is causing confusion, friction, or unmet expectations. If launched to all users, this would significantly increase Customer Success load and cost.

### 2. Refund Rate ⚠️ RISK — MONITOR
- Control: 0 refunds | Treatment: 3 refunds (0.42%)
- Small absolute numbers but the direction is concerning given Control had zero refunds.
- **Interpretation:** May indicate some users felt misled into converting. Root cause investigation needed.

### 3. Engagement Score ✅ POSITIVE
- Control: 57.03 | Treatment: 62.94 | Increase: +10.4%
- Statistically significant
- **Interpretation:** Users who converted in Treatment are more engaged, suggesting the campaign does attract genuinely interested users — not just impulse signups.

---

## Segment-Level Insights

- **By Region:** Treatment outperforms Control across all regions. North and East show the strongest conversion lift.
- **By Device:** Desktop users show the highest conversion rates in both groups. Mobile users in Treatment show a larger absolute lift.
- **By Plan Type:** Premium plan users in Treatment convert at higher rates. Free plan users show the largest relative lift but still low absolute conversion.

---

## Final Recommendation: 🟡 PHASED LAUNCH

**Do not launch to all users immediately.**

**Recommended approach:**
1. **Phase 1 (immediate):** Launch Treatment to Desktop users and Premium plan users in North/East regions — where conversion lift is highest and support ticket risk is more manageable.
2. **Phase 2:** Investigate root cause of support ticket spike. Audit the onboarding UX for friction points or confusing copy. Fix identified issues.
3. **Phase 3:** Re-run experiment with the improved experience before full rollout.

**Rationale:** The conversion improvement is significant and valuable. But a 69.4% spike in support tickets is not acceptable at scale — it would cost more in CS operations than the revenue gain justifies, and risks damaging brand trust.

---

## Risks and Limitations
- Support ticket spike root cause is unknown — could be UX confusion, technical bugs, or unmet expectations
- Only 72 total converters in the dataset — ARPU and days-to-convert estimates are noisy
- Experiment duration and temporal effects not fully controlled
- Refund data is early-stage; 30-day window may not capture full refund behavior

---

## Next Steps
1. Qualitative analysis: survey Treatment users who raised tickets to identify friction points
2. Fix identified UX issues in the new onboarding flow
3. Rerun A/B test with fixed experience (target n=500+ converters for stable ARPU estimates)
4. If support ticket rate drops below Control + 10% threshold → proceed to full launch
5. Set up ongoing monitoring dashboard for: conversion rate, ARPU, refund rate, support ticket rate by cohort
