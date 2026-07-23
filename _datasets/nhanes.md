---
title: "NHANES — National Health and Nutrition Examination Survey"
slug: nhanes
blurb: "CDC's rolling health survey combining interviews with physical examinations; the workhorse for population health questions."
source_name: "CDC / NCHS"
source_url: "https://www.cdc.gov/nchs/nhanes/"
years: "1999–present, 2-year cycles"
license: "Public domain"
---

NHANES is unusual among public health datasets: participants are not just
interviewed but physically examined, so blood pressure, anthropometrics, and
laboratory values are measured rather than self-reported.

## Structure and access from R

The `nhanesA` package pulls cycle tables directly:

```r
library(nhanesA)

demo  <- nhanes("DEMO_L")   # demographics
bpx   <- nhanes("BPXO_L")   # oscillometric blood pressure
sleep <- nhanes("SLQ_L")    # sleep questionnaire
```

## Things to watch

The survey design is complex — stratified, clustered, and oversampled for
several subpopulations. Any estimate that ignores the design weights
(`WTMEC2YR` for examined participants) describes the sample, not the U.S.
population. Use the `survey` package and combine weights correctly when
pooling cycles.
