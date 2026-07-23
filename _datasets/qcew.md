---
title: "QCEW — Quarterly Census of Employment and Wages"
slug: qcew
blurb: "Near-universe administrative counts of U.S. employment and wages by county and industry, quarterly since 1975."
source_name: "U.S. Bureau of Labor Statistics"
source_url: "https://www.bls.gov/cew/"
years: "1975–present, quarterly"
license: "Public domain"
---

QCEW is derived from unemployment insurance filings, which makes it a census
rather than a survey: roughly 95% of U.S. jobs are covered. That makes it the
natural panel for county-level policy evaluations.

## Access from R

The BLS open data files can be read directly:

```r
library(tidyverse)

qcew <- read_csv(
  "https://data.bls.gov/cew/data/api/2024/1/area/17031.csv"
)
```

## Things to watch

Suppression: cells that could identify individual employers are withheld,
which is nonrandom (small rural counties, concentrated industries). Decide
explicitly how suppressed county-industry cells enter your panel before
estimating anything.
