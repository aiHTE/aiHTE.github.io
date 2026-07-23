---
layout: post
title: "Replaying Card & Krueger with Modern Difference-in-Differences"
abstract: >
  The 1994 minimum wage study is the canonical difference-in-differences
  example, and also the canonical target of every modern DiD critique. This
  notebook re-analyzes county-level QCEW employment data with two-way fixed
  effects, then with the Callaway–Sant'Anna estimator, and shows where the
  two disagree and why staggered treatment timing is the culprit.
datasets: [qcew]
methodology: [did]
---

Two-way fixed effects was the workhorse of applied economics for two decades
before we collectively noticed it was quietly averaging treatment effects
with negative weights.

```r
library(did)

out <- att_gt(
  yname = "log_emp",
  tname = "quarter",
  idname = "county_fips",
  gname = "first_treated",
  data = qcew_panel
)
aggte(out, type = "dynamic")
```

The event-study plot tells the story better than the tables…
