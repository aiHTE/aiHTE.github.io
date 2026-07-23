---
title: "Inverse Probability Weighting"
slug: ipw
summary: "Reweight the observed sample so treatment is independent of measured confounders, then compare weighted means."
datasets: [nhanes]
---

## The estimand

Under conditional exchangeability, positivity, and consistency, the average
treatment effect is identified by the weighted contrast

$$\hat{\tau} = \frac{\sum_i \frac{A_i Y_i}{\hat{e}(X_i)}}{\sum_i \frac{A_i}{\hat{e}(X_i)}} - \frac{\sum_i \frac{(1-A_i) Y_i}{1-\hat{e}(X_i)}}{\sum_i \frac{1-A_i}{1-\hat{e}(X_i)}}$$

where $\hat{e}(X_i)$ is the estimated propensity score.

## Implementation in R

```r
library(WeightIt)
library(marginaleffects)

w <- weightit(short_sleep ~ age + bmi + income + shift_work,
              data = d, method = "glm", estimand = "ATE")

fit <- lm(sbp ~ short_sleep, data = d, weights = w$weights)
avg_comparisons(fit, variables = "short_sleep", vcov = "HC3")
```

## Diagnostics that matter

Check covariate balance after weighting (`cobalt::love.plot()`), and look at
the weight distribution — a handful of extreme weights means the positivity
assumption is straining, and trimming decisions should be reported, not
hidden.
