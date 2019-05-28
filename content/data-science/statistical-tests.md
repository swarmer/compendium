+++
title = "Statistical tests"
weight = 1
sort_by = "weight"
+++


## Difference between samples

### Student's t-test for independent samples

A t-test is a test using using a statistic that is sampled from Student's t-distribution when the
null hypothesis is true. t-distribution is the distribution of means estimated from
a number of values sampled from a normal distributions.

Null hypothesis: means of two populations are equal.
The test is not robust to outliers.

Assumptions:
- Distributions are normal.
- Sample sizes are equal (This is especially important if sample sizes are different.
    In this case, Welch's t-test can be used).
- Samples are independent


### Mann-Whitney U-test

A more robust test that additionally only requires data to be ordinal (not necessarily numeric).  
This test is almost as efficient as t-test for normal data, and for non-normal distributions
can be significantly more efficient.

Null hypothesis: distributions of two populations are equal.
The test is robust to outliers.

Assumptions:
- Samples are independent.
- If the null hypothesis is false, probability that a value from the first distribution is higher
    than a value from the second distribution is different from the opposite case.


### Chi-squared test

A test using the Chi-squared distribution — distribution of a sum of squares of a number of standard
normal random variables.  
This test that can be used for non-ordered, discrete, data.

Null hypothesis: a distribution is equal to a predefiend table of theoretical frequencies.

Assumptions:
- If comparing several samples, they need to be independent.
- The number of observations is not too low (above 5) in at least the vast majority of cells.


### Z-test

For any test, the test statistic of which is approximately normally distributed, a corresponding
F-test can be constructed. The advantage of Z-test is that critical don't depend on sample size.

For Z-test to be applicable, the sample size needs to be large enough (roughly over 30)
and variance needs to be known.


## Univariate ANOVA

### One-way ANOVA (F-test)

F-distributed values can appear as ratios of two chi-squared variates scaled by their
degrees of freedom.

Null hypothesis: several populations have the same mean.
The test is not robust to outliers.

Assumptions:
- Data is normally distributed.
- Variances are equal.
- Observations within and between groups are independent.


### Kruskal–Wallis H-test (one-way ANOVA on ranks)

The non-parametric form of one-way ANOVA.

Null hypothesis: medians of groups are equal.

- (When testing medians) the shapes of distributions of groups are the same.


### F-test of equality of variances

Null hypothesis: two distributions have the same variance.

Assumptions:
- Distributions are normal (very important).
    Alternatives that are more robust to non-normality are:
    Levene's test, Bartlett's test, Brown–Forsythe test.


## Multivariate ANOVA

- TODO


## Difference between paired samples

### Dependent t-test for paired samples

Null hypothesis: two means are equal.
This test is not robust to outliers.

Assumptions:
- Dependent variable is continuous.
- Dependent variable is approximately normally distributed.
- Observations are independent.


### Wilcoxon signed-rank test

A non-parametric test for paired sample difference.

Null hypothesis: two means are equal.

Assumptions:
- Observations are selected randomly and are independent.
- Dependent variable is continuous.


## Repeated measures ANOVA (rANOVA)

### F-test

Null hypothesis: several populations have the same mean.

Assumptions:
- Dependent variables are normally distributed.
- Sphericity - differences scores must have the same variance when comparing any two levels of
    within-subjects factor.
- Subjects are selected randomly and are independent from each other.


### Friedman test

A non-parametric test that is robust to non-normality and outliers.

Null hypothesis: several populations have the same mean.

Assumptions:
- Data is ordinal or numeric.


## Multiple comparisons tests and corrections

For equal variances:
- Bonferroni correction
- Scheffe's method
- Tukey's range test

For unequal variances and sample sizes:
- Tamhane's T2 test
- Dunnett's T3 test
- Games-Howell test


## Distribution tests

- Kolmogorov–Smirnov: for any distribution
- Shapiro–Wilk: test for normality
  