# What Makes a Good Wine?

Interactive portfolio site for **“Vino, at its finest”** — a 2022 graduate statistics project by [Jada Mylan Smith](https://github.com/Jadamylan) and Chandnee Das (STAT 632, CSU East Bay).

**Live site:** [https://jadamylan.github.io/wine-quality-analysis/](https://jadamylan.github.io/wine-quality-analysis/)

The page is a single static `index.html` file. Open it locally in a browser, or visit the GitHub Pages URL above.

---

## Original 2022 analysis

The original question was straightforward: **which measurable chemical properties of Portuguese Vinho Verde help explain perceived wine quality?**

The work used the Cortez et al. wine-quality dataset (physicochemical tests plus an expert quality score). The combined red-and-white table was narrowed to **white wine**: 4,898 observations, 11 lab measures, and a discrete quality score observed from 3 to 9.

### Methodology

The 2022 analysis mixed classical regression with tree-based exploration:

1. **Exploratory correlation** across acidity, sugar, chlorides, sulfur dioxide, density, pH, sulphates, and alcohol.
2. **Multiple linear regression** with quality as the response.
3. **Model selection** from a full model (`lm1`) to a reduced model (`lm2`) using AIC / adjusted R², retaining 8 predictors.
4. **Transformations**, including a log transform on volatile acidity (`lm3`) to handle skew.
5. **Diagnostics and outlier investigation** (`lm4`).
6. **Regression trees**, where alcohol was the first split and volatile acidity / density were important later splitters.

Reported adjusted R² values were modest even after those steps:

| Model | Adj. R² | AIC |
|---|---|---|
| Full (`lm1`) | 0.2775 | 11131 |
| Reduced (`lm2`) | 0.2778 | 11127 |
| Log transform (`lm3`) | 0.2818 | 11100 |
| Outlier check (`lm4`) | 0.2861 | 11058 |

That ceiling is part of the finding. Chemistry explained about **29%** of the variation in quality. The rest is human taste, context, and variables the lab sheet never measured.

### What stood out

- **Alcohol** had a positive relationship with quality and was the first split in the regression tree.
- **Volatile acidity** had a negative relationship; the log transform improved that term.
- **Density** showed a strong negative correlation and appeared as an important tree splitter.

The original project write-up is archived at [STAT632-Final-Project-details](https://github.com/Jadamylan/STAT632-Final-Project-details).

---

## What this site is (and is not)

This version visualizes **results reported in the 2022 project**. It is labeled that way on the page on purpose.

It is **not** yet a fresh row-level rerun. Add `data/wine-quality-white-and-red.csv` before presenting any new coefficients, cross-validated metrics, or a “build your wine” predictor as newly estimated.

---

## 2026 extension

The interesting professional story is not “I redid an old assignment.” It is **2022 Jada vs. 2026 Jada**: same question, a more mature analytical stack.

Planned next pass:

- Treat quality as **ordered and discrete** (ordinal logistic regression), not only as a continuous score.
- Add a **train/test split** and repeated cross-validation; report MAE / RMSE.
- Compare the interpretable linear model with **random forest, gradient boosting, and GAMs**.
- Bring **red wine** back and test type interactions.
- Add **feature importance / SHAP-style** explanations.
- If new data exists, add producer, vintage, region, and fermentation/aging variables — the missing ~70% is the interesting part.

Code for that rerun will live under `analysis/` once the original CSV is in `data/`.

---

## Repository layout

Current (GitHub Pages–ready):

```text
wine-quality-analysis/
├── index.html          ← site root (required for Pages)
├── README.md
├── .nojekyll           ← skip Jekyll so the HTML is served as-is
└── data/
    └── .gitkeep        ← add wine-quality-white-and-red.csv here
```

Intended later:

```text
wine-quality-analysis/
├── index.html
├── README.md
├── data/
│   └── wine-quality-white-and-red.csv
├── analysis/
│   ├── original-analysis.R
│   └── modern-analysis.R
└── assets/
    ├── images/
    └── charts/
```

---

## GitHub Pages

This repo is configured to deploy from the `main` branch, folder `/` (root). After the first Pages build, the public URL is:

`https://jadamylan.github.io/wine-quality-analysis/`

If you ever need to turn Pages back on: **Settings → Pages → Build and deployment → Deploy from a branch → `main` / `/ (root)`**.

Official docs: [Creating a GitHub Pages site](https://docs.github.com/en/pages/getting-started-with-github-pages/creating-a-github-pages-site).

---

## Data

UCI / Cortez et al. *Wine Quality* dataset (Portuguese Vinho Verde physicochemical tests and expert quality scores). Place the combined red-and-white CSV at `data/wine-quality-white-and-red.csv` when you are ready to rerun the analysis.
