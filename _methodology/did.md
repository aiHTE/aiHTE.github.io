---
title: "Difference-in-Differences"
slug: did
summary: "Identify treatment effects from policy timing by comparing changes in treated units to changes in untreated units."
datasets: [qcew]
---

## The estimand

With staggered adoption, the modern target is the group-time average
treatment effect $ATT(g, t)$: the effect at time $t$ for units first treated
in period $g$, aggregated afterward into event-study or overall summaries.

## Implementation in R

```r
library(did)

atts <- att_gt(yname = "log_emp", tname = "quarter",
               idname = "county_fips", gname = "first_treated",
               control_group = "notyettreated", data = panel)

aggte(atts, type = "dynamic")   # event study
aggte(atts, type = "simple")    # overall ATT
```

## Assumptions to defend

Parallel trends is untestable but pressure-testable: plot pre-treatment
event-study coefficients, and take anticipation seriously — if units respond
before the law takes effect, shift the treatment date rather than explaining
the pre-trend away.
