# What Makes a Good Wine?

### Same question. Better analytical judgment.

This is the interactive portfolio version of **“Vino, at its finest,”** a 2022 graduate statistics project by [Jada Mylan Smith](https://github.com/Jadamylan) and Chandnee Das for STAT 632 at CSU East Bay.

**Portfolio site:** [jadamylan.github.io/wine-quality-analysis](https://jadamylan.github.io/wine-quality-analysis/)

The original project asked:

> **Which measurable chemical properties of Portuguese Vinho Verde help explain perceived wine quality?**

I keep this project in my portfolio for two reasons:

1. the original analysis still shows a solid statistics foundation
2. revisiting it makes it easy to show how differently I think about modeling now

---

## The dataset

The 2022 analysis used the Cortez et al. wine-quality dataset, which combines physicochemical lab measurements with an expert quality score.

The original project narrowed the combined red + white data to **white wine**:

- **4,898 observations**
- **11 physicochemical measures**
- quality scores observed from **3 to 9**

---

## What we did in 2022

The original workflow included:

1. exploratory correlation
2. multiple linear regression
3. model selection using AIC and adjusted R²
4. variable transformations
5. model diagnostics and outlier investigation
6. regression trees

### Reported model results

| Model | Adj. R² | AIC |
|---|---:|---:|
| Full (`lm1`) | 0.2775 | 11131 |
| Reduced (`lm2`) | 0.2778 | 11127 |
| Log transform (`lm3`) | 0.2818 | 11100 |
| Outlier check (`lm4`) | 0.2861 | 11058 |

The most interesting part is the ceiling.

Even after several modeling choices, the analysis explained only about **29% of the observed variation in quality**.

That is not a failed result.

It is a reminder that a lab sheet is only one part of why humans decide a wine is good.

---

## What stood out

In the original analysis:

- **alcohol** had a positive relationship with quality and appeared as the first regression-tree split
- **volatile acidity** had a negative relationship with quality
- **density** had a strong negative correlation and appeared as an important tree splitter

The original course-project materials are preserved in [STAT632-Final-Project-details](https://github.com/Jadamylan/STAT632-Final-Project-details).

---

## 2022 Jada vs. 2026 Jada

This is the part of the project I care about most now.

If I started the analysis today, I would make several different choices.

### 1. Treat the outcome more carefully

The quality score is **ordered and discrete**.

I would compare the original linear-regression framing with an **ordinal model** instead of automatically treating the outcome like a fully continuous measurement.

### 2. Separate model fitting from model evaluation

The original project focused heavily on fit statistics.

A modern rerun should include:

- train / test separation
- repeated cross-validation
- MAE / RMSE where appropriate
- out-of-sample comparison

### 3. Compare explanation and prediction on purpose

I would keep an interpretable baseline, then compare it with:

- random forest
- gradient boosting
- GAMs

The goal would not be “use the fanciest model.”

It would be to understand what predictive flexibility actually buys us.

### 4. Bring the missing context into the question

Chemistry leaves a lot unexplained.

If richer data were available, I would want variables such as:

- producer
- vintage
- region
- fermentation approach
- aging
- sensory / tasting context

The unexplained portion is not just model error. It is also a clue that the dataset does not contain the whole experience.

---

## What this site is — and is not

The current site visualizes **results reported in the 2022 project**.

It is intentionally **not** presented as a new row-level rerun.

Before publishing any new coefficients, cross-validated metrics, feature importance, or a “build your wine” predictor, the original row-level CSV should be restored to `data/` and the refreshed analysis should be reproducible from code.

That distinction matters to me.

---

## Repository layout

```text
wine-quality-analysis/
├── index.html
├── README.md
├── .nojekyll
└── data/
    └── .gitkeep
```

Planned modern-analysis extension:

```text
analysis/
├── original-analysis.R
└── modern-analysis.R
```

---

## Data source

UCI / Cortez et al. **Wine Quality** dataset: Portuguese Vinho Verde physicochemical measurements and expert quality scores.

---

**Tools / methods:** R · regression · model diagnostics · regression trees · statistical storytelling · GitHub Pages
