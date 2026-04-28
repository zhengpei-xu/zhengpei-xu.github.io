---
title: 'Statistical and ML Metrics Dictionary'
date: 2026-04-28
permalink: '/posts/2026/04/Statistical and ML Metrics Dictionary/'
tags:
  - Statistical Model
  - Machine Learning
---


## Table of Contents

- [Part I: Statistical Metrics](#part-i-statistical-metrics)
  - [1. Descriptive & Distributional Statistics](#1-descriptive--distributional-statistics)
  - [2. Statistical Inference](#2-statistical-inference)
  - [3. Correlation & Association](#3-correlation--association)
  - [4. Information-Theoretic Metrics](#4-information-theoretic-metrics)
  - [5. GLM & Count Model Metrics](#5-glm--count-model-metrics)
  - [6. Model Selection Criteria](#6-model-selection-criteria)
  - [7. Spatial Statistics](#7-spatial-statistics)
- [Part II: Machine Learning Metrics](#part-ii-machine-learning-metrics)
  - [8. Classification — Threshold-Based](#8-classification--threshold-based)
  - [9. Classification — Threshold-Independent](#9-classification--threshold-independent)
  - [10. Multi-Class Extensions](#10-multi-class-extensions)
  - [11. Calibration Metrics](#11-calibration-metrics)
  - [12. Regression Metrics](#12-regression-metrics)
  - [13. Ranking & Retrieval Metrics](#13-ranking--retrieval-metrics)
  - [14. Clustering — External (with Ground Truth)](#14-clustering--external-with-ground-truth)
  - [15. Clustering — Internal (No Ground Truth)](#15-clustering--internal-no-ground-truth)
  - [16. Model Selection & Validation](#16-model-selection--validation)
  - [17. Feature Importance & Interpretability](#17-feature-importance--interpretability)
  - [18. Distance & Similarity Metrics](#18-distance--similarity-metrics)
- [Appendix: Common Notation](#appendix-common-notation)

---

# Part I: Statistical Metrics

---

## 1. Descriptive & Distributional Statistics

### Mean (Arithmetic)

- **Definition:** The sum of all values divided by the number of values.

$$\bar{x} = \frac{1}{N} \sum_{i=1}^{N} x_i$$

- **Range:** Any real number.
- **When to use:** Default summary of central tendency for symmetric, roughly normal distributions. Avoid when data is heavily skewed or contains extreme outliers — use median instead.

---

### Median

- **Definition:** The middle value when data are sorted. For even N, the average of the two middle values.

$$\text{Median} = \begin{cases} x_{(n+1)/2} & \text{if } N \text{ is odd} \\ \frac{1}{2}\left(x_{N/2} + x_{N/2+1}\right) & \text{if } N \text{ is even} \end{cases}$$

- **Range:** Any real number.
- **When to use:** Preferred over the mean when the distribution is skewed or contains outliers (e.g. income data, travel time distributions, collision counts with long tails).

---

### Mode

- **Definition:** The most frequently occurring value in a dataset.
- **Range:** Any value in the dataset.
- **When to use:** Useful for categorical data or discrete distributions. Also relevant for identifying peaks in multimodal distributions.

---

### Variance

- **Definition:** The average squared deviation from the mean.

$$\sigma^2 = \frac{1}{N} \sum_{i=1}^{N} (x_i - \bar{x})^2 \quad \text{(population)}, \qquad s^2 = \frac{1}{N-1} \sum_{i=1}^{N} (x_i - \bar{x})^2 \quad \text{(sample)}$$

- **Range:** [0, +∞).
- **When to use:** Measures spread. Foundation for many statistical tests. Use sample variance (N−1 denominator) when estimating from a sample.

---

### Standard Deviation

- **Definition:** The square root of variance. In the same units as the data.

$$\sigma = \sqrt{\sigma^2} = \sqrt{\frac{1}{N} \sum_{i=1}^{N} (x_i - \bar{x})^2}$$

- **Range:** [0, +∞).
- **When to use:** The default measure of spread for normally distributed data. More interpretable than variance due to same-unit property.

---

### Skewness

- **Definition:** Measures the asymmetry of a distribution about its mean.

$$\gamma_1 = \frac{1}{N} \sum_{i=1}^{N} \left(\frac{x_i - \bar{x}}{\sigma}\right)^3$$

- **Range:** (−∞, +∞). 0 = symmetric, positive = right-skewed, negative = left-skewed.
- **When to use:** Check before applying methods that assume normality. Heavily skewed data may need transformation (log, Box-Cox) before modelling.

---

### Kurtosis

- **Definition:** Measures the "tailedness" of a distribution — how much of the variance comes from extreme values.

$$\gamma_2 = \frac{1}{N} \sum_{i=1}^{N} \left(\frac{x_i - \bar{x}}{\sigma}\right)^4 - 3 \quad \text{(excess kurtosis; normal = 0)}$$

- **Range:** (−∞, +∞). Positive = heavy tails, negative = light tails.
- **When to use:** High kurtosis warns of outlier-prone data. Important when assessing whether standard error estimates are reliable.

---

### Interquartile Range (IQR)

- **Definition:** The range between the 25th and 75th percentiles.

$$\text{IQR} = Q_3 - Q_1$$

- **Range:** [0, +∞).
- **When to use:** Robust measure of spread that is not influenced by outliers. Used in box plots and for outlier detection (values beyond Q₁ − 1.5·IQR or Q₃ + 1.5·IQR).

---

### Coefficient of Variation (CV)

- **Definition:** The ratio of the standard deviation to the mean, expressed as a percentage.

$$CV = \frac{\sigma}{\bar{x}} \times 100\%$$

- **Range:** [0, +∞)%.
- **When to use:** Comparing variability across datasets with different units or scales. Undefined when mean is zero.

---

## 2. Statistical Inference

### p-value

- **Definition:** The probability of observing a test statistic at least as extreme as the one computed, assuming the null hypothesis is true.

$$p = P(T \geq t_{\text{obs}} \mid H_0)$$

- **Range:** [0, 1]. Smaller = stronger evidence against H₀. Reject H₀ if p < α (commonly 0.05).
- **When to use:** Standard hypothesis testing for any parametric or non-parametric test. Be aware that large N can produce small p for trivially small effects — always pair with effect size. **Not** the probability that H₀ is true.

---

### Confidence Interval (CI)

- **Definition:** A range of values that, under repeated sampling, would contain the true parameter at a given confidence level.

$$CI = \hat{\theta} \pm z_{\alpha/2} \times SE(\hat{\theta})$$

- **Range:** Width depends on SE and confidence level. For 95%: z = 1.96.
- **When to use:** Always report alongside point estimates. More informative than p-values alone because it conveys both the magnitude and precision of an estimate.

---

### Effect Size — Cohen's d

- **Definition:** The standardised difference between two group means.

$$d = \frac{\bar{x}_1 - \bar{x}_2}{s_{\text{pooled}}}, \qquad s_{\text{pooled}} = \sqrt{\frac{s_1^2 + s_2^2}{2}}$$

- **Range:** (−∞, +∞). |d|: 0.2 = small, 0.5 = medium, 0.8 = large.
- **When to use:** When comparing two groups and you want to quantify the practical significance of the difference, independent of sample size. Essential complement to p-values.

---

### Effect Size — Eta Squared (η²)

- **Definition:** The proportion of total variance explained by a factor in ANOVA.

$$\eta^2 = \frac{SS_{\text{effect}}}{SS_{\text{total}}}$$

- **Range:** [0, 1]. 0.01 = small, 0.06 = medium, 0.14 = large.
- **When to use:** After ANOVA to understand how much of the outcome variation is attributable to the grouping variable.

---

### Wald Test

- **Definition:** Tests whether an estimated parameter is significantly different from a hypothesised value (usually zero).

$$W = \frac{(\hat{\theta} - \theta_0)^2}{\text{Var}(\hat{\theta})} \sim \chi^2(1)$$

- **Range:** χ² statistic.
- **When to use:** Testing individual coefficient significance in GLMs and logistic regression. Faster to compute than the likelihood ratio test but less reliable for small samples.

---

### Likelihood Ratio Test (LRT)

- **Definition:** Compares two nested models by testing whether the additional parameters significantly improve the fit.

$$LR = -2 \left[ \ell(\text{reduced}) - \ell(\text{full}) \right] \sim \chi^2(df)$$

- **Range:** [0, +∞). df = difference in number of parameters. Significant if p < α.
- **When to use:** When comparing a simpler (nested) model against a more complex one — e.g. testing whether adding a variable improves a logistic regression or Poisson GLM. Generally preferred over the Wald test for small samples.

---

### Chi-Squared Test of Independence

- **Definition:** Tests whether two categorical variables are independent.

$$\chi^2 = \sum \frac{(O_i - E_i)^2}{E_i}$$

- **Range:** [0, +∞).
- **When to use:** Contingency table analysis with categorical variables. Requires expected cell counts ≥ 5; use Fisher's exact test otherwise.

---

### Fisher's Exact Test

- **Definition:** An exact test for independence in a 2×2 contingency table, based on the hypergeometric distribution.
- **Range:** p-value in [0, 1].
- **When to use:** Small sample sizes where χ² approximation is unreliable, or when any expected cell count is below 5.

---

### t-test (Independent / Paired)

- **Definition:** Tests whether the means of one or two groups differ significantly.

$$t = \frac{\bar{x}_1 - \bar{x}_2}{\sqrt{\dfrac{s_1^2}{n_1} + \dfrac{s_2^2}{n_2}}} \quad \text{(Welch's independent t-test)}$$

- **Range:** t statistic → p-value.
- **When to use:** Comparing means of two groups (independent) or before-and-after measurements (paired). Assumes approximate normality for small samples; robust for large N. Use Welch's variant when variances are unequal.

---

### Mann-Whitney U Test

- **Definition:** A non-parametric test comparing the distributions of two independent groups using ranks.
- **Range:** U statistic → p-value.
- **When to use:** Alternative to the independent t-test when the normality assumption is violated, data is ordinal, or the distribution is heavily skewed.

---

### Kruskal-Wallis Test

- **Definition:** Non-parametric extension of one-way ANOVA for comparing three or more independent groups.
- **Range:** H statistic → p-value.
- **When to use:** When comparing more than two groups and the assumptions of ANOVA (normality, homoscedasticity) are not met.

---

### Shapiro-Wilk Test

- **Definition:** Tests whether a sample comes from a normally distributed population.
- **Range:** W statistic in (0, 1]; associated p-value.
- **When to use:** Before applying parametric tests that assume normality. Most powerful normality test for small to moderate samples (N < 5000).

---

### Levene's Test

- **Definition:** Tests equality of variances across groups (homoscedasticity).
- **Range:** F statistic → p-value.
- **When to use:** Before ANOVA or t-test to check whether the equal-variance assumption holds. More robust to departures from normality than Bartlett's test.

---

### Durbin-Watson Test

- **Definition:** Tests for first-order autocorrelation in regression residuals.

$$DW = \frac{\sum_{t=2}^{N} (e_t - e_{t-1})^2}{\sum_{t=1}^{N} e_t^2}$$

- **Range:** [0, 4]. DW ≈ 2 = no autocorrelation. DW < 2 = positive, DW > 2 = negative.
- **When to use:** After fitting a regression model to time-series or sequentially ordered data. Violated autocorrelation inflates standard errors and invalidates inference.

---

## 3. Correlation & Association

### Pearson Correlation (r)

- **Definition:** Measures the linear relationship between two continuous variables.

$$r = \frac{\sum (x_i - \bar{x})(y_i - \bar{y})}{\sqrt{\sum (x_i - \bar{x})^2 \cdot \sum (y_i - \bar{y})^2}}$$

- **Range:** [−1, 1]. |r| > 0.7 typically considered strong.
- **When to use:** Both variables are continuous and the relationship is approximately linear. Sensitive to outliers.

---

### Spearman Rank Correlation (ρ)

- **Definition:** Measures monotonic (not necessarily linear) relationship between two variables using ranks.

$$\rho = 1 - \frac{6 \sum d_i^2}{N(N^2 - 1)}, \qquad d_i = \text{rank}(x_i) - \text{rank}(y_i)$$

- **Range:** [−1, 1].
- **When to use:** When the relationship is monotonic but not linear, when data is ordinal, or when outliers are present. Non-parametric alternative to Pearson.

---

### Kendall's Tau (τ)

- **Definition:** Measures ordinal association based on concordant and discordant pairs.

$$\tau = \frac{(\text{concordant pairs}) - (\text{discordant pairs})}{\binom{N}{2}}$$

- **Range:** [−1, 1].
- **When to use:** Small samples, ordinal data, or when there are many tied ranks. More robust than Spearman in small datasets.

---

### Point-Biserial Correlation

- **Definition:** Pearson correlation between a continuous and a dichotomous variable.
- **Range:** [−1, 1].
- **When to use:** Assessing the relationship between a binary variable (e.g. collision / no collision) and a continuous predictor.

---

### Cramér's V

- **Definition:** Measures the strength of association between two nominal (categorical) variables.

$$V = \sqrt{\frac{\chi^2}{N \cdot (\min(r, c) - 1)}}$$

- **Range:** [0, 1]. 0 = no association, 1 = perfect.
- **When to use:** After a chi-squared test on a contingency table to quantify association strength. Works for tables larger than 2×2.

---

## 4. Information-Theoretic Metrics

### Entropy

- **Definition:** Measures the uncertainty or disorder in a probability distribution.

$$H(X) = -\sum p(x) \log_2 p(x)$$

- **Range:** [0, log₂(n)]. 0 = deterministic, max = uniform distribution.
- **When to use:** Quantifying uncertainty in a categorical variable. Used in decision tree splitting (information gain) and as a baseline for mutual information.

---

### Cross-Entropy

- **Definition:** The average number of bits needed to encode data from distribution p using a code optimised for distribution q.

$$H(p, q) = -\sum p(x) \log q(x)$$

- **Range:** [H(p), +∞). Minimised when q = p.
- **When to use:** Standard loss function for classification models. Equivalent to negative log-likelihood.

---

### KL Divergence (Kullback-Leibler)

- **Definition:** Measures how one probability distribution diverges from a reference distribution.

$$D_{KL}(p \| q) = \sum p(x) \log \frac{p(x)}{q(x)}$$

- **Range:** [0, +∞). 0 = identical distributions.
- **When to use:** Comparing a learned distribution against a reference (e.g. in variational inference, generative models). Note: asymmetric — D_KL(p‖q) ≠ D_KL(q‖p).

---

### Mutual Information

- **Definition:** Quantifies the amount of information shared between two variables.

$$I(X; Y) = \sum_x \sum_y p(x,y) \log \frac{p(x,y)}{p(x) \cdot p(y)} = H(X) + H(Y) - H(X,Y)$$

- **Range:** [0, min(H(X), H(Y))]. 0 = independent.
- **When to use:** Feature selection (detecting non-linear dependencies), clustering evaluation (NMI), and measuring information overlap. More general than correlation — captures any statistical dependence.

---

### Jensen-Shannon Divergence

- **Definition:** A symmetric, bounded version of KL divergence.

$$JSD(p \| q) = \frac{1}{2} D_{KL}(p \| m) + \frac{1}{2} D_{KL}(q \| m), \qquad m = \frac{1}{2}(p + q)$$

- **Range:** [0, 1] (when using log₂). 0 = identical.
- **When to use:** When you need a symmetric measure of distributional difference. Its square root is a proper distance metric.

---

## 5. GLM & Count Model Metrics

### Deviance

- **Definition:** Twice the difference between the log-likelihood of the saturated model and the fitted model. Generalises the residual sum of squares to GLMs.

$$D = 2 \left[ \ell(\text{saturated}) - \ell(\text{fitted}) \right]$$

$$\text{For Poisson:} \quad D = 2 \sum \left[ y_i \log\frac{y_i}{\mu_i} - (y_i - \mu_i) \right]$$

- **Range:** [0, +∞). Lower = better fit.
- **When to use:** Assessing goodness-of-fit for GLMs (Poisson, logistic, negative binomial). The null deviance (intercept-only) minus residual deviance indicates variance explained.

---

### Pearson Chi-Squared Statistic

- **Definition:** Sum of squared Pearson residuals. Tests whether observed counts deviate from model expectations.

$$X^2 = \sum \frac{(y_i - \mu_i)^2}{\mu_i}$$

- **Range:** [0, +∞).
- **When to use:** Assessing fit of count models. X²/df approximates the overdispersion parameter — if substantially > 1, the Poisson variance assumption may be violated.

---

### Overdispersion Parameter (φ̂)

- **Definition:** Ratio of the Pearson χ² statistic to residual degrees of freedom.

$$\hat{\varphi} = \frac{X^2}{N - p}$$

- **Range:** [0, +∞). φ ≈ 1 = equidispersion.
- **When to use:** After fitting a Poisson model. φ̂ >> 1 indicates overdispersion (variance > mean) — switch to Negative Binomial or Quasi-Poisson. φ̂ << 1 suggests underdispersion.

---

### Pseudo-R² (McFadden)

- **Definition:** An R²-like goodness-of-fit measure for GLMs based on log-likelihood comparison with the null model.

$$R^2_{\text{McFadden}} = 1 - \frac{\ell(\text{fitted})}{\ell(\text{null})}$$

- **Range:** [0, 1). Values of 0.2–0.4 are considered excellent.
- **When to use:** Reporting model explanatory power for logistic regression, Poisson GLMs, etc. Not directly comparable to OLS R². Other variants (Nagelkerke, Cox-Snell, Efron) exist — always specify which.

---

### Hosmer-Lemeshow Test

- **Definition:** Groups predictions into deciles and compares observed vs expected outcomes to assess logistic regression calibration.

$$HL = \sum_{g=1}^{G} \frac{(O_g - E_g)^2}{E_g \cdot (1 - E_g / n_g)} \sim \chi^2(G - 2)$$

- **Range:** χ² statistic. Non-significant p = good calibration.
- **When to use:** After logistic regression to check whether predicted probabilities match observed frequencies. Losing favour to ECE in modern ML but still standard in epidemiology and public health.

---

### Vuong Test

- **Definition:** A non-nested model comparison test.

$$V = \frac{\sqrt{N} \cdot \bar{m}}{s_m}, \qquad m_i = \log\frac{f_1(y_i)}{f_2(y_i)}$$

- **Range:** Z-statistic. |V| > 1.96 suggests one model significantly better.
- **When to use:** Comparing non-nested count models — e.g. standard Poisson vs Zero-Inflated Poisson (ZIP), or Poisson vs Negative Binomial.

---

## 6. Model Selection Criteria

### AIC (Akaike Information Criterion)

- **Definition:** Balances goodness-of-fit (log-likelihood) against model complexity.

$$AIC = -2\,\ell(\hat{\theta}) + 2k$$

- **Range:** (−∞, +∞). Lower is better (relative measure). k = number of estimated parameters.
- **When to use:** Comparing models fitted on the **same** dataset. Favours predictive accuracy; tends to select slightly more complex models than BIC. Standard in ecology, spatial modelling, and epidemiology.

---

### BIC (Bayesian Information Criterion)

- **Definition:** Similar to AIC but with a stronger complexity penalty that depends on sample size.

$$BIC = -2\,\ell(\hat{\theta}) + k \ln(N)$$

- **Range:** (−∞, +∞). Lower is better.
- **When to use:** When you want a more parsimonious model than AIC selects, especially with large N. Asymptotically consistent (selects the true model as N → ∞). Penalises complexity more than AIC when N > 7.

---

### AICc (Corrected AIC)

- **Definition:** AIC with a finite-sample correction.

$$AIC_c = AIC + \frac{2k^2 + 2k}{N - k - 1}$$

- **Range:** (−∞, +∞). Lower is better.
- **When to use:** When the sample size is small relative to the number of parameters (rule of thumb: N/k < 40). Converges to AIC as N → ∞.

---

## 7. Spatial Statistics

### Moran's I (Global)

- **Definition:** A measure of global spatial autocorrelation — whether similar values cluster together in space.

$$I = \frac{N}{S_0} \cdot \frac{\sum_i \sum_j w_{ij}(x_i - \bar{x})(x_j - \bar{x})}{\sum_i (x_i - \bar{x})^2}, \qquad S_0 = \sum_i \sum_j w_{ij}$$

- **Range:** Approx [−1, 1]. Positive = clustering, near 0 = random, negative = dispersion.
- **When to use:** Testing whether a spatial pattern (e.g. collision rates, traffic stress scores) exhibits significant clustering or dispersion. First step in exploratory spatial data analysis (ESDA). Requires defining a spatial weights matrix W.

---

### Geary's C

- **Definition:** An alternative to Moran's I, more sensitive to local differences than global patterns.

$$C = \frac{(N-1)}{2 S_0} \cdot \frac{\sum_i \sum_j w_{ij}(x_i - x_j)^2}{\sum_i (x_i - \bar{x})^2}$$

- **Range:** [0, 2]. C < 1 = positive autocorrelation, C = 1 = random, C > 1 = negative.
- **When to use:** When you care about local dissimilarity rather than global pattern. Inversely related to Moran's I but captures different spatial features.

---

### Local Moran's I (LISA — Local Indicator of Spatial Association)

- **Definition:** Identifies local clusters and spatial outliers at each location.

$$I_i = z_i \sum_j w_{ij} z_j, \qquad z_i = \frac{x_i - \bar{x}}{\sigma}$$

- **Range:** Positive = local cluster (HH or LL), negative = spatial outlier (HL or LH).
- **When to use:** Identifying where significant spatial clusters or outliers exist — e.g. collision hotspots (High-High), unexpectedly safe areas near dangerous ones (Low-High). Produces a cluster map with four quadrants.

---

### Getis-Ord Gi* (Hotspot Statistic)

- **Definition:** Identifies statistically significant spatial clusters of high values (hotspots) and low values (coldspots).

$$G_i^* = \frac{\sum_j w_{ij} x_j - \bar{X} \sum_j w_{ij}}{S \sqrt{\dfrac{N \sum_j w_{ij}^2 - \left(\sum_j w_{ij}\right)^2}{N - 1}}}$$

- **Range:** Z-score. |Gi*| > 1.96 is significant at 95%.
- **When to use:** Hotspot mapping. Unlike LISA, Gi* identifies concentrations of high or low values (not dissimilarity). Standard tool for identifying collision hotspots, crime hotspots, disease clusters.

---

### Ripley's K Function

- **Definition:** Evaluates whether a point pattern is clustered, random, or dispersed at various spatial scales.

$$K(d) = \frac{A}{N^2} \sum_i \sum_{j \neq i} \mathbf{1}(d_{ij} \leq d)$$

- **Range:** K(d) > πd² indicates clustering at distance d.
- **When to use:** Analysing point patterns (e.g. collision locations) across multiple distance scales. The L function — L(d) = √(K(d)/π) − d — is easier to interpret (L > 0 = clustered).

---

### Semivariogram

- **Definition:** Describes how spatial dependence changes with distance. The foundation of geostatistics.

$$\gamma(h) = \frac{1}{2|N(h)|} \sum_{N(h)} \left[ z(s_i) - z(s_j) \right]^2$$

- **Range:** [0, +∞). Key parameters: nugget (intercept), sill (asymptote), range (distance at which spatial dependence vanishes).
- **When to use:** Before kriging or any geostatistical interpolation. Characterises the spatial structure of continuous data — determines how far apart points must be before they become independent.

---

### Spatial Lag Model Diagnostics (LM Tests)

- **Definition:** Lagrange Multiplier tests for spatial dependence in regression residuals. LM-Lag tests for spatial lag (endogenous interaction), LM-Error tests for spatial error (correlated errors).
- **Range:** χ² statistic → p-value.
- **When to use:** After OLS regression on spatial data to determine whether a spatial lag model, spatial error model, or both are needed. The robust versions (RLM-Lag, RLM-Error) help distinguish between the two.

---

### Spatial Weights Matrix (W)

- **Definition:** Encodes the spatial neighbourhood structure. Common types: contiguity (queen, rook), distance-based (k-nearest, distance band), kernel.
- **When to use:** Required for computing Moran's I, LISA, Gi*, and spatial regression models. The choice of W affects results — always perform sensitivity analysis with alternative specifications.

---

# Part II: Machine Learning Metrics

---

## 8. Classification — Threshold-Based

### Accuracy

- **Definition:** The proportion of all predictions that are correct.

$$\text{Accuracy} = \frac{TP + TN}{TP + TN + FP + FN}$$

- **Range:** [0, 1]. Higher is better.
- **When to use:** Only when classes are roughly balanced. **Avoid** for imbalanced datasets — a model always predicting the majority class can score high accuracy while being useless.

---

### Precision (Positive Predictive Value)

- **Definition:** Of all instances predicted positive, the proportion truly positive.

$$\text{Precision} = \frac{TP}{TP + FP}$$

- **Range:** [0, 1].
- **When to use:** When the **cost of false positives is high** — e.g. spam detection, medical screening follow-up costs. Answers: "When the model says positive, how often is it correct?"

---

### Recall (Sensitivity / True Positive Rate)

- **Definition:** Of all actual positive instances, the proportion correctly identified.

$$\text{Recall} = \frac{TP}{TP + FN}$$

- **Range:** [0, 1].
- **When to use:** When **missing a positive case is costly** — e.g. disease screening, fraud detection, safety-critical systems. Answers: "Of all actual positives, how many did we catch?"

---

### Specificity (True Negative Rate)

- **Definition:** Of all actual negatives, the proportion correctly identified.

$$\text{Specificity} = \frac{TN}{TN + FP} = 1 - FPR$$

- **Range:** [0, 1].
- **When to use:** When correctly identifying negatives matters — e.g. ruling out a condition. Paired with sensitivity in diagnostic test evaluation.

---

### F1 Score

- **Definition:** Harmonic mean of precision and recall.

$$F_1 = 2 \cdot \frac{\text{Precision} \times \text{Recall}}{\text{Precision} + \text{Recall}}$$

- **Range:** [0, 1].
- **When to use:** When you need a **single balanced metric** for precision and recall. Standard choice for imbalanced classification when both false positives and false negatives matter.

---

### F-beta Score

- **Definition:** Generalisation of F1 that allows tuning the precision-recall trade-off via β.

$$F_\beta = (1 + \beta^2) \cdot \frac{\text{Precision} \times \text{Recall}}{\beta^2 \cdot \text{Precision} + \text{Recall}}$$

- **Range:** [0, 1].
- **When to use:** β > 1 when **recall matters more** (e.g. F₂ for safety-critical applications where missing a dangerous case is worse than a false alarm). β < 1 when precision matters more (e.g. F₀.₅).

---

### Matthews Correlation Coefficient (MCC)

- **Definition:** A correlation coefficient between observed and predicted binary classifications using all four confusion matrix cells.

$$MCC = \frac{TP \cdot TN - FP \cdot FN}{\sqrt{(TP+FP)(TP+FN)(TN+FP)(TN+FN)}}$$

- **Range:** [−1, +1]. +1 = perfect, 0 = random, −1 = total disagreement.
- **When to use:** Widely regarded as the **best single metric for imbalanced binary classification**. Unlike F1, it uses all four quadrants of the confusion matrix and is symmetric between positive and negative classes.

---

### Cohen's Kappa (κ)

- **Definition:** Agreement between predicted and actual labels, adjusted for agreement occurring by chance.

$$\kappa = \frac{p_o - p_e}{1 - p_e}$$

- **Range:** [−1, +1]. 1 = perfect, 0 = no better than chance. p_o = observed accuracy, p_e = expected random accuracy.
- **When to use:** Comparing a classifier against random chance or comparing two classifiers/raters. Also used in inter-rater reliability studies. Accounts for class prevalence.

---

### Balanced Accuracy

- **Definition:** The arithmetic mean of recall for each class.

$$\text{Balanced Accuracy} = \frac{\text{Sensitivity} + \text{Specificity}}{2}$$

- **Range:** [0, 1].
- **When to use:** A simple adjustment to accuracy for **imbalanced datasets**. Equivalent to accuracy if classes are balanced. Less informative than MCC but more intuitive.

---

### False Positive Rate (FPR / Fall-out)

- **Definition:** Of all actual negatives, the proportion incorrectly classified as positive.

$$FPR = \frac{FP}{FP + TN} = 1 - \text{Specificity}$$

- **Range:** [0, 1]. Lower is better.
- **When to use:** X-axis of the ROC curve. Important when the cost of false alarms is relevant.

---

### False Negative Rate (FNR / Miss Rate)

- **Definition:** Of all actual positives, the proportion missed.

$$FNR = \frac{FN}{FN + TP} = 1 - \text{Recall}$$

- **Range:** [0, 1]. Lower is better.
- **When to use:** Safety-critical systems where missed detections have severe consequences.

---

### Negative Predictive Value (NPV)

- **Definition:** Of all instances predicted negative, the proportion truly negative.

$$NPV = \frac{TN}{TN + FN}$$

- **Range:** [0, 1].
- **When to use:** When a negative prediction must be trustworthy — e.g. "this road segment is safe" needs to be reliable.

---

## 9. Classification — Threshold-Independent

### AUC-ROC (Area Under the ROC Curve)

- **Definition:** Area under the Receiver Operating Characteristic curve (TPR vs FPR across all thresholds).

$$AUC = \int_0^1 TPR(FPR)\, d(FPR) = P(\text{score}_{+} > \text{score}_{-})$$

- **Range:** [0, 1]. 0.5 = random, 1.0 = perfect.
- **When to use:** Comparing overall discriminative ability of classifiers regardless of threshold. Works well when **classes are balanced**. For imbalanced data, AUC-PR is more informative.

---

### AUC-PR (Area Under the Precision-Recall Curve)

- **Definition:** Area under the Precision-Recall curve across all thresholds.

$$AUC\text{-}PR = \int_0^1 \text{Precision}(R)\, dR$$

- **Range:** [0, 1]. Baseline = class prevalence (not 0.5).
- **When to use:** When the **positive class is rare** — e.g. fatal collisions, fraud, rare events. More sensitive to performance differences on the minority class than AUC-ROC.

---

### Average Precision (AP)

- **Definition:** Discrete approximation of AUC-PR — weighted mean of precisions at each threshold.

$$AP = \sum_n (R_n - R_{n-1}) \cdot P_n$$

- **Range:** [0, 1].
- **When to use:** Same as AUC-PR. Standard metric in object detection (mAP) and information retrieval.

---

### Log Loss (Binary Cross-Entropy)

- **Definition:** Penalises the deviation of predicted probabilities from actual labels. Heavily punishes confident wrong predictions.

$$\text{LogLoss} = -\frac{1}{N} \sum_{i=1}^{N} \left[ y_i \log(p_i) + (1-y_i) \log(1-p_i) \right]$$

- **Range:** [0, +∞). Lower is better. 0 = perfect.
- **When to use:** When the model outputs **probabilities** and you care about calibration, not just ranking. Standard training loss for logistic regression and neural network classifiers.

---

### Brier Score

- **Definition:** Mean squared difference between predicted probabilities and actual binary outcomes.

$$BS = \frac{1}{N} \sum_{i=1}^{N} (p_i - y_i)^2$$

- **Range:** [0, 1]. Lower is better.
- **When to use:** Evaluating **probabilistic forecasts**. Decomposes into calibration + refinement + uncertainty, enabling diagnosis of why a model performs poorly.

---

### KS Statistic (Kolmogorov-Smirnov)

- **Definition:** Maximum vertical distance between the CDFs of positive and negative class scores.

$$KS = \max_x \left| F_{+}(x) - F_{-}(x) \right|$$

- **Range:** [0, 1]. Higher = better separation.
- **When to use:** Credit scoring, risk modelling. Identifies the threshold with maximum class separation. Common in financial model validation.

---

## 10. Multi-Class Extensions

### Macro-Averaged Precision / Recall / F1

- **Definition:** Compute the metric independently per class, then take the unweighted mean.

$$\text{Macro-}F_1 = \frac{1}{C} \sum_{c=1}^{C} F_{1,c}$$

- **Range:** [0, 1].
- **When to use:** When **all classes are equally important** regardless of their size. Gives equal weight to rare and common classes.

---

### Micro-Averaged Precision / Recall / F1

- **Definition:** Aggregate TP, FP, FN globally across all classes, then compute.

$$\text{Micro-Precision} = \frac{\sum_c TP_c}{\sum_c (TP_c + FP_c)}, \qquad \text{Micro-Recall} = \frac{\sum_c TP_c}{\sum_c (TP_c + FN_c)}$$

- **Range:** [0, 1].
- **When to use:** When you want an **overall performance measure** that is dominated by the majority class. Micro-precision = micro-recall = accuracy in multi-class settings.

---

### Weighted-Averaged Precision / Recall / F1

- **Definition:** Per-class metric weighted by class support (count).

$$\text{Weighted-}F_1 = \sum_{c=1}^{C} \frac{n_c}{N} \cdot F_{1,c}$$

- **Range:** [0, 1].
- **When to use:** When classes are imbalanced and you want a single number that **accounts for prevalence**.

---

### Confusion Matrix

- **Definition:** A C×C matrix where entry (i,j) counts samples with true class i predicted as class j.

$$M[i][j] = \text{count}(\text{true} = i,\ \text{predicted} = j)$$

- **When to use:** **Always inspect this first.** Reveals the full error pattern — which classes are confused with which. Foundation for all other classification metrics.

---

### G-Mean (Geometric Mean)

- **Definition:** Geometric mean of sensitivity and specificity.

$$G\text{-Mean} = \sqrt{\text{Sensitivity} \times \text{Specificity}}$$

- **Range:** [0, 1].
- **When to use:** Imbalanced classification where you want both classes predicted well. Zero if either class has zero recall.

---

### Multi-Class AUC (OvR / OvO)

- **Definition:** Extension of binary AUC-ROC to multi-class.

$$AUC_{OvR} = \frac{1}{C} \sum_{c=1}^{C} AUC_c, \qquad AUC_{OvO} = \frac{2}{C(C-1)} \sum_{i<j} AUC_{(i,j)}$$

- **Range:** [0, 1].
- **When to use:** Multi-class ranking evaluation. OvR is simpler; OvO is more fine-grained for models that produce pairwise scores.

---

## 11. Calibration Metrics

### Expected Calibration Error (ECE)

- **Definition:** Weighted average of the absolute gap between predicted probability and observed frequency across bins.

$$ECE = \sum_{b=1}^{B} \frac{n_b}{N} \left| \text{acc}_b - \text{conf}_b \right|$$

- **Range:** [0, 1]. Lower = better calibrated.
- **When to use:** When predicted probabilities are used for **downstream decisions** (resource allocation, risk scoring). A model can have high AUC but poor calibration. Common choice: 10–15 equal-width bins.

---

### Maximum Calibration Error (MCE)

- **Definition:** The worst-case calibration gap across all bins.

$$MCE = \max_b \left| \text{acc}_b - \text{conf}_b \right|$$

- **Range:** [0, 1].
- **When to use:** Safety-critical applications where even **one poorly calibrated probability region** is unacceptable.

---

### Calibration Curve (Reliability Diagram)

- **Definition:** Visual diagnostic plotting mean predicted probability vs observed fraction of positives per bin.
- **When to use:** Always plot alongside ECE. A perfectly calibrated model lies on the y = x diagonal. Reveals whether the model is over-confident (below diagonal) or under-confident (above).

---

## 12. Regression Metrics

### Mean Absolute Error (MAE)

- **Definition:** Average of absolute differences between predictions and actual values.

$$MAE = \frac{1}{N} \sum_{i=1}^{N} |y_i - \hat{y}_i|$$

- **Range:** [0, +∞). Lower is better. Same units as target.
- **When to use:** Default regression metric when you want **robustness to outliers** and equal treatment of all errors. More interpretable than MSE.

---

### Mean Squared Error (MSE)

- **Definition:** Average of squared differences between predictions and actuals.

$$MSE = \frac{1}{N} \sum_{i=1}^{N} (y_i - \hat{y}_i)^2$$

- **Range:** [0, +∞). Units are squared.
- **When to use:** When **large errors are disproportionately bad** and you want to penalise them. Differentiable, standard for optimisation.

---

### Root Mean Squared Error (RMSE)

- **Definition:** Square root of MSE.

$$RMSE = \sqrt{\frac{1}{N} \sum_{i=1}^{N} (y_i - \hat{y}_i)^2}$$

- **Range:** [0, +∞). Same units as target.
- **When to use:** When you want MSE's outlier sensitivity but in **interpretable units**. The most commonly reported regression metric.

---

### Mean Absolute Percentage Error (MAPE)

- **Definition:** Average of absolute percentage errors.

$$MAPE = \frac{100}{N} \sum_{i=1}^{N} \left| \frac{y_i - \hat{y}_i}{y_i} \right|$$

- **Range:** [0, +∞)%.
- **When to use:** When you want errors as **relative percentages** for easy communication. **Avoid** when actual values can be zero or near-zero.

---

### Symmetric MAPE (sMAPE)

- **Definition:** A modified MAPE that treats over- and under-predictions more symmetrically.

$$sMAPE = \frac{100}{N} \sum_{i=1}^{N} \frac{2|y_i - \hat{y}_i|}{|y_i| + |\hat{y}_i|}$$

- **Range:** [0, 200]%.
- **When to use:** Alternative to MAPE that partially addresses its asymmetry. Still problematic when both actual and predicted are near zero.

---

### R² (Coefficient of Determination)

- **Definition:** Proportion of variance in the target explained by the model.

$$R^2 = 1 - \frac{SS_{res}}{SS_{tot}} = 1 - \frac{\sum (y_i - \hat{y}_i)^2}{\sum (y_i - \bar{y})^2}$$

- **Range:** (−∞, 1]. 1 = perfect. Can be negative.
- **When to use:** Standard for reporting OLS regression fit. **Negative R² means worse than predicting the mean.** Always report for regression models but do not use as the sole criterion.

---

### Adjusted R²

- **Definition:** R² penalised for the number of predictors.

$$R^2_{adj} = 1 - (1 - R^2) \cdot \frac{N - 1}{N - p - 1}$$

- **Range:** (−∞, 1]. p = number of predictors.
- **When to use:** Comparing models with **different numbers of predictors**. Prevents selecting overfit models that add noise variables.

---

### Median Absolute Error (MedAE)

- **Definition:** Median of absolute differences between predictions and actuals.

$$\text{MedAE} = \text{median}\left(|y_i - \hat{y}_i|\right)$$

- **Range:** [0, +∞).
- **When to use:** When you want the **typical error**, uninfluenced by extreme outliers. More robust than both MAE and RMSE.

---

### Max Error

- **Definition:** The largest absolute error across all predictions.

$$\text{MaxError} = \max_i |y_i - \hat{y}_i|$$

- **Range:** [0, +∞).
- **When to use:** **Worst-case analysis** — critical when you need to bound the maximum possible prediction error.

---

### Explained Variance Score

- **Definition:** Proportion of target variance captured, allowing biased predictions.

$$EVS = 1 - \frac{\text{Var}(y - \hat{y})}{\text{Var}(y)}$$

- **Range:** (−∞, 1].
- **When to use:** Differs from R² only when predictions are biased (mean(y − ŷ) ≠ 0). Use alongside R² to diagnose systematic bias.

---

### Huber Loss

- **Definition:** Loss function that is quadratic for small errors and linear for large ones.

$$L_\delta(a) = \begin{cases} \frac{1}{2}a^2 & \text{if } |a| \leq \delta \\ \delta\left(|a| - \frac{1}{2}\delta\right) & \text{otherwise} \end{cases}$$

- **Range:** [0, +∞).
- **When to use:** Training regression models when data has **outliers** but you still want some sensitivity to large errors. Combines benefits of MSE and MAE.

---

### Quantile Loss (Pinball Loss)

- **Definition:** Asymmetric loss for quantile regression.

$$L_\tau(y, \hat{y}) = \tau \cdot \max(y - \hat{y},\, 0) + (1 - \tau) \cdot \max(\hat{y} - y,\, 0)$$

- **Range:** [0, +∞).
- **When to use:** When you want to predict a **specific quantile** rather than the mean — e.g. "the 90th percentile of travel time" or "the worst-case delay". τ = 0.5 recovers MAE.

---

## 13. Ranking & Retrieval Metrics

### Precision@k

- **Definition:** Fraction of the top-k predictions that are relevant.

$$P@k = \frac{|\text{relevant items in top } k|}{k}$$

- **Range:** [0, 1].
- **When to use:** Evaluating **top-k recommendation systems** or prioritised risk lists (e.g. "of the 10 road segments we flagged, how many are genuinely high-risk?").

---

### Recall@k

- **Definition:** Fraction of all relevant items appearing in the top-k.

$$R@k = \frac{|\text{relevant items in top } k|}{|\text{total relevant}|}$$

- **Range:** [0, 1].
- **When to use:** When you need to know **what proportion of true positives** are captured in the top-k.

---

### MAP (Mean Average Precision)

- **Definition:** Mean of average precision across all queries.

$$MAP = \frac{1}{Q} \sum_{q=1}^{Q} AP_q$$

- **Range:** [0, 1].
- **When to use:** Standard metric for information retrieval and ranked recommendation evaluation.

---

### NDCG (Normalised Discounted Cumulative Gain)

- **Definition:** Evaluates ranking quality using graded relevance, discounting items further down the list.

$$DCG@k = \sum_{i=1}^{k} \frac{2^{rel_i} - 1}{\log_2(i+1)}, \qquad NDCG@k = \frac{DCG@k}{IDCG@k}$$

- **Range:** [0, 1].
- **When to use:** When relevance is **graded** (not binary) and the **position** of relevant items matters. Top results should be more relevant.

---

### MRR (Mean Reciprocal Rank)

- **Definition:** Average of the reciprocal rank of the first relevant result across queries.

$$MRR = \frac{1}{Q} \sum_{q=1}^{Q} \frac{1}{\text{rank}_q}$$

- **Range:** [0, 1].
- **When to use:** When you only care about the **first correct result** — e.g. search engines, QA systems.

---

### Lift

- **Definition:** Ratio of the model's positive rate in a selected group compared to the overall rate.

$$\text{Lift} = \frac{\text{positive rate in selected group}}{\text{overall positive rate}}$$

- **Range:** [0, +∞). Lift > 1 = better than random.
- **When to use:** Marketing, credit risk, targeted interventions. "How much better than random is our targeting?"

---

## 14. Clustering — External (with Ground Truth)

### Adjusted Rand Index (ARI)

- **Definition:** Pairwise agreement between predicted clustering and true labels, adjusted for chance.

$$ARI = \frac{RI - E[RI]}{\max(RI) - E[RI]}$$

- **Range:** [−1, 1]. 1 = perfect, 0 = random agreement.
- **When to use:** When you have **true cluster labels** and want a chance-corrected measure. Preferred over raw Rand Index.

---

### Normalised Mutual Information (NMI)

- **Definition:** Mutual information between clustering and ground truth, normalised to [0,1].

$$NMI = \frac{2 \cdot I(U; V)}{H(U) + H(V)}$$

- **Range:** [0, 1].
- **When to use:** Comparing clusterings with **different numbers of clusters**. Information-theoretic and handles varying K well.

---

### Homogeneity

- **Definition:** Each cluster contains only members of a single class.

$$h = 1 - \frac{H(C|K)}{H(C)}$$

- **Range:** [0, 1].
- **When to use:** When **cluster purity** matters most. Satisfied trivially by assigning each point to its own cluster.

---

### Completeness

- **Definition:** All members of a given class are assigned to the same cluster.

$$c = 1 - \frac{H(K|C)}{H(K)}$$

- **Range:** [0, 1].
- **When to use:** When you want to ensure that entire classes are **captured within single clusters**.

---

### V-Measure

- **Definition:** Harmonic mean of homogeneity and completeness.

$$V = \frac{2hc}{h + c}$$

- **Range:** [0, 1].
- **When to use:** Balanced evaluation of clustering that rewards both purity and completeness. Analogous to F1 for clustering.

---

### Fowlkes-Mallows Index (FMI)

- **Definition:** Geometric mean of pairwise precision and pairwise recall.

$$FMI = \sqrt{PPV_{\text{pairs}} \times TPR_{\text{pairs}}}$$

- **Range:** [0, 1].
- **When to use:** Alternative to ARI that is more interpretable as a precision-recall analogue for pairs.

---

## 15. Clustering — Internal (No Ground Truth)

### Silhouette Score

- **Definition:** How similar a point is to its own cluster vs the nearest neighbouring cluster.

$$s(i) = \frac{b(i) - a(i)}{\max(a(i),\, b(i))}, \qquad \text{Overall} = \frac{1}{N}\sum_{i=1}^{N} s(i)$$

- **Range:** [−1, 1]. Higher = better. Negative = likely misclassified.
- **When to use:** General-purpose internal validation for **convex clusters**. Easy to interpret. Less suitable for density-based or non-convex clusters.

---

### Davies-Bouldin Index

- **Definition:** Average similarity ratio of each cluster with its most similar cluster.

$$DB = \frac{1}{K} \sum_{i=1}^{K} \max_{j \neq i} \frac{s_i + s_j}{d(c_i, c_j)}$$

- **Range:** [0, +∞). Lower = better.
- **When to use:** Comparing different values of K. Does not require computing pairwise distances for all points, so **more efficient** than silhouette for large datasets.

---

### Calinski-Harabasz Index (Variance Ratio Criterion)

- **Definition:** Ratio of between-cluster to within-cluster dispersion.

$$CH = \frac{B / (K - 1)}{W / (N - K)}$$

- **Range:** [0, +∞). Higher = better.
- **When to use:** Fast to compute. Favours **compact, well-separated globular clusters**. Best for k-means-like methods.

---

### Inertia (Within-Cluster SSE)

- **Definition:** Sum of squared distances from each point to its cluster centroid.

$$\text{Inertia} = \sum_{k=1}^{K} \sum_{x \in C_k} \|x - \mu_k\|^2$$

- **Range:** [0, +∞). Lower = better.
- **When to use:** Used in the **elbow method** for choosing K. Always decreases with more clusters — look for the "elbow" where marginal improvement diminishes.

---

### DBCV (Density-Based Cluster Validation)

- **Definition:** Validity index for density-based clusters using mutual reachability distances.

$$DBCV = \frac{1}{K} \sum_{c=1}^{K} V(c), \qquad V(c) = \frac{DSC(c) - DSPC(c)}{\max(DSC(c),\, DSPC(c))}$$

- **Range:** [−1, 1].
- **When to use:** Evaluating **DBSCAN or HDBSCAN** clusters with arbitrary shapes. Unlike silhouette, does not assume convex clusters.

---

## 16. Model Selection & Validation

### k-Fold Cross-Validation Score

- **Definition:** Data is split into k folds; model trains on k−1, tests on the held-out fold, repeated k times.

$$CV = \frac{1}{k} \sum_{i=1}^{k} \text{Score}(\text{fold}_i)$$

- **When to use:** **Standard evaluation protocol** to estimate generalisation performance and diagnose overfitting. Typical k = 5 or 10. Use stratified k-fold for imbalanced classification. Report both mean and standard deviation.

---

### Leave-One-Out Cross-Validation (LOOCV)

- **Definition:** Special case of k-fold where k = N.

$$LOOCV = \frac{1}{N} \sum_{i=1}^{N} L\left(y_i,\, f_{-i}(x_i)\right)$$

- **When to use:** Very small datasets where losing even a few samples to a test fold is costly. Unbiased but high-variance and computationally expensive.

---

### Bias-Variance Decomposition

- **Definition:** Decomposes expected prediction error into irreducible noise + bias² + variance.

$$E\left[(y - \hat{f}(x))^2\right] = \sigma^2 + \text{Bias}^2(\hat{f}) + \text{Var}(\hat{f})$$

- **When to use:** **Conceptual framework** for diagnosing whether a model underfits (high bias) or overfits (high variance). Not directly computed, but diagnosed via learning curves.

---

### Learning Curve

- **Definition:** Plots training and validation performance as a function of training set size.
- **When to use:** Diagnosing **bias-variance trade-off** visually. Converging low scores = underfit; diverging scores = overfit; converging high scores = good fit.

---

## 17. Feature Importance & Interpretability

### Gini Importance (Mean Decrease in Impurity)

- **Definition:** Total reduction in impurity attributed to a feature across all tree splits.

$$\text{Imp}(f) = \sum_{\text{nodes splitting on } f} \frac{n_{\text{node}}}{N} \cdot \Delta(\text{impurity})$$

- **Range:** [0, 1] when normalised.
- **When to use:** Quick feature ranking for **tree-based models** (Random Forest, Gradient Boosting). Biased towards high-cardinality and correlated features — use permutation importance for more reliable results.

---

### Permutation Importance

- **Definition:** Drop in model performance when a feature's values are randomly shuffled.

$$PI(f) = \text{Score}_{\text{original}} - \frac{1}{K}\sum_{k=1}^{K} \text{Score}_{\text{permuted},k}$$

- **Range:** Can be negative (feature hurts model).
- **When to use:** **Model-agnostic** feature importance. Compute on the validation set. More reliable than Gini importance for correlated features.

---

### SHAP Values (SHapley Additive exPlanations)

- **Definition:** Game-theoretic attribution of each feature's contribution to each individual prediction.

$$\phi_j = \sum_{S \subseteq F \setminus \{j\}} \frac{|S|!\,(p - |S| - 1)!}{p!} \left[ f(S \cup \{j\}) - f(S) \right]$$

- **Range:** (−∞, +∞). Sum of all φⱼ = f(x) − E[f(x)].
- **When to use:** When you need **instance-level** explanation — why did the model make this specific prediction? Satisfies desirable theoretical properties (local accuracy, missingness, consistency). Computationally expensive.

---

### Variance Inflation Factor (VIF)

- **Definition:** Measures multicollinearity for predictor j.

$$VIF_j = \frac{1}{1 - R_j^2}$$

- **Range:** [1, +∞). VIF > 5–10 = problematic.
- **When to use:** **Before fitting regression models** to detect and remove highly correlated predictors. High VIF inflates standard errors and destabilises coefficients.

---

## 18. Distance & Similarity Metrics

### Euclidean Distance (L2)

- **Definition:** Straight-line distance in n-dimensional space.

$$d(\mathbf{x}, \mathbf{y}) = \sqrt{\sum_{i=1}^{n} (x_i - y_i)^2}$$

- **Range:** [0, +∞).
- **When to use:** Default distance for k-means, kNN, and most geometric methods. Assumes all features are on **comparable scales** — standardise first if not.

---

### Manhattan Distance (L1)

- **Definition:** Sum of absolute differences along each dimension.

$$d(\mathbf{x}, \mathbf{y}) = \sum_{i=1}^{n} |x_i - y_i|$$

- **Range:** [0, +∞).
- **When to use:** Grid-based environments, high-dimensional data (less affected by curse of dimensionality than Euclidean), or when features are on **different scales** and not standardised.

---

### Cosine Similarity

- **Definition:** Cosine of the angle between two vectors.

$$\cos(\mathbf{x}, \mathbf{y}) = \frac{\mathbf{x} \cdot \mathbf{y}}{\|\mathbf{x}\| \cdot \|\mathbf{y}\|}$$

- **Range:** [−1, 1]. 1 = identical direction.
- **When to use:** Text analysis (TF-IDF, embeddings), recommendation systems — anywhere **direction matters more than magnitude**.

---

### Jaccard Index (IoU)

- **Definition:** Intersection over union of two sets.

$$J(A, B) = \frac{|A \cap B|}{|A \cup B|}$$

- **Range:** [0, 1].
- **When to use:** Comparing **sets or binary vectors** — e.g. object detection bounding boxes (IoU), set similarity, binary feature overlap.

---

### Mahalanobis Distance

- **Definition:** Scale-invariant distance accounting for correlations via the covariance matrix.

$$d(\mathbf{x}, \mathbf{y}) = \sqrt{(\mathbf{x} - \mathbf{y})^T \mathbf{S}^{-1} (\mathbf{x} - \mathbf{y})}$$

- **Range:** [0, +∞). S = covariance matrix.
- **When to use:** **Outlier detection**, classification with correlated features. Reduces to Euclidean when S = I. Accounts for the shape of the data distribution.

---

### Hamming Distance

- **Definition:** Number of positions where corresponding elements differ.

$$d(\mathbf{x}, \mathbf{y}) = \sum_{i=1}^{n} \mathbf{1}(x_i \neq y_i)$$

- **Range:** [0, n].
- **When to use:** **Categorical or binary data** — e.g. comparing one-hot encoded features, DNA sequences, error-correcting codes.

---

### Minkowski Distance (Lp)

- **Definition:** Generalised distance metric parameterised by p.

$$d(\mathbf{x}, \mathbf{y}) = \left(\sum_{i=1}^{n} |x_i - y_i|^p\right)^{1/p}$$

- **Range:** [0, +∞). p=1 → Manhattan, p=2 → Euclidean, p→∞ → Chebyshev.
- **When to use:** When you want to **tune the distance sensitivity** between Manhattan and Euclidean behaviour.

---

## Appendix: Common Notation

| Symbol | Meaning |
|--------|---------|
| $TP, TN, FP, FN$ | True Positives, True Negatives, False Positives, False Negatives |
| $N$ | Total number of samples |
| $C$ | Number of classes |
| $K$ | Number of clusters |
| $y_i$ | Actual (true) value for sample i |
| $\hat{y}_i$ (or $\mu_i$) | Predicted value for sample i |
| $\bar{y}$ | Mean of actual values |
| $p_i$ | Predicted probability for sample i |
| $\ell(\theta)$ | Log-likelihood of parameters θ |
| $k$ or $p$ | Number of model parameters / predictors |
| $w_{ij}$ | Spatial weight between locations i and j |
| $S_0$ | Sum of all spatial weights |
| $H(X)$ | Entropy of variable X |
| $I(X; Y)$ | Mutual information between X and Y |
| $SS_{res},\ SS_{tot}$ | Residual and total sum of squares |
| $SE$ | Standard error |
| $df$ | Degrees of freedom |
| $\alpha$ | Significance level (commonly 0.05) |
| $\beta$ | Type II error rate; also F-beta parameter |
