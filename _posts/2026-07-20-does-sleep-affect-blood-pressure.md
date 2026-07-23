---
layout: post
title: "Does Sleep Duration Affect Blood Pressure? A First Pass with NHANES"
image: /assets/images/sleep-bp.png
abstract: >
  Short sleep is associated with hypertension in nearly every observational
  study, but association is cheap. In this notebook I take NHANES 2017–2020,
  draw the DAG I actually believe, and estimate the effect of habitual sleep
  duration on systolic blood pressure under explicit confounding assumptions
  using inverse probability weighting. The headline estimate survives some
  adjustment sets and not others — which is precisely the point.
datasets: [nhanes]
methodology: [ipw]
---

Every few months a headline announces that short sleepers have higher blood
pressure. The correlation is real. Whether *sleeping more* would *lower*
anyone's blood pressure is a different question, and it's the one worth asking.

## The setup

```r
library(tidyverse)
library(survey)

nhanes <- read_rds("data/nhanes_2017_2020.rds")

nhanes <- nhanes |>
  mutate(short_sleep = sleep_hours < 6,
         sbp = (bp_sys1 + bp_sys2) / 2)
```

## The DAG, stated out loud

Age, BMI, income, and shift work plausibly cause both sleep duration and
blood pressure. Caffeine is trickier — it may be a mediator rather than a
confounder, so I leave it out of the adjustment set and discuss the
sensitivity of that choice at the end.

$$\text{SBP}_i = \beta_0 + \beta_1 \cdot \text{ShortSleep}_i + \varepsilon_i \quad \text{(weighted)}$$

The full walkthrough, including the weight diagnostics, continues below…
