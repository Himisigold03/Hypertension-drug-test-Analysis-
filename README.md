# Effectiveness of Two Antihypertensive Drugs Over 12 Weeks: A Simulated Randomised Trial

![Python](https://img.shields.io/badge/Python-3.9%2B-blue) ![Excel](https://img.shields.io/badge/Excel-Data%20Analysis%20ToolPak-green) ![Status](https://img.shields.io/badge/Status-Completed-brightgreen) ![Data](https://img.shields.io/badge/Data-Simulated-orange)

> A health-data analysis project that evaluates how well two drugs lower systolic blood pressure, what influences treatment response, and what side effects come with each drug. The full analysis is done twice, in **Excel** and in **Python**, so the two can be compared.

> **Note:** The dataset is **simulated for practice**. It contains no real patient information, and the findings must not be used for clinical decisions.

---

## Table of Contents
1. [Introduction](#1-introduction)
2. [Research Topic](#2-research-topic)
3. [Aim, Objectives and Hypotheses](#3-aim-objectives-and-hypotheses)
4. [Dataset](#4-dataset)
5. [Tools Used](#5-tools-used)
6. [Methodology](#6-methodology)
7. [Results (Chapter 4)](#7-results-chapter-4)
8. [Discussion](#8-discussion)
9. [Limitations](#9-limitations)
10. [Conclusion and Recommendations](#10-conclusion-and-recommendations)
11. [Repository Structure](#11-repository-structure)
12. [How to Reproduce the Analysis](#12-how-to-reproduce-the-analysis)
13. [Skills Demonstrated](#13-skills-demonstrated)
14. [Author and Contact](#14-author-and-contact)

---

## 1. Introduction

High blood pressure (hypertension) is one of the most common long-term health conditions and a major risk factor for heart disease and stroke. It often occurs together with obesity, diabetes and high cholesterol, and patients do not all respond to treatment in the same way. Doctors and researchers therefore need to know three things: whether a drug works, for whom it works best, and what side effects it causes.

This project analyses a simulated randomised trial of 500 patients to answer those questions. It follows the full data-analysis workflow: understanding the question, inspecting and cleaning the data, describing it, testing hypotheses, modelling, and reporting the results in plain language.

## 2. Research Topic

**Effectiveness of Two Antihypertensive Drugs Over 12 Weeks and the Roles of Adherence, Metabolic Risk, and Lifestyle: A Simulated Randomised Trial**

**Problem statement:** Hypertension often occurs alongside obesity, diabetes and high cholesterol, and patients do not respond equally to treatment. This study asks whether the drugs work, for whom, and at what cost in side effects.

## 3. Aim, Objectives and Hypotheses

**Aim:** To evaluate the effect of Drug A and Drug B on blood pressure and identify factors that influence treatment response.

**Objectives**
1. Describe baseline characteristics of the three groups and confirm they are comparable.
2. Compare the change in systolic blood pressure (SBP) (Week 12 minus Baseline) across Placebo, Drug A and Drug B.
3. Determine whether adherence modifies the drug effect.
4. Identify baseline predictors of BP reduction (age, BMI, glucose, HbA1c, smoking, activity).
5. Compare adverse event rates and weigh benefit against harm.

**Hypotheses**
- **H₀:** Mean SBP change does not differ between groups.
- **H₁:** At least one drug produces a greater reduction than placebo.
- **Secondary:** Patients with higher adherence show larger reductions.

## 4. Dataset

| Item | Detail |
|---|---|
| Source | Simulated clinical trial data created for practice |
| Participants | 500 (Placebo = 172, Drug A = 168, Drug B = 160) |
| Variables | 19 (demographic, clinical, treatment and outcome) |
| Duration | 12 weeks of treatment |
| Format | `.csv` (raw) and `.xlsx` (cleaned, with analysis sheets) |

**Data dictionary**

| Variable | Description | Type |
|---|---|---|
| Patient_ID | Unique patient identifier | Text |
| Enrolment_Date | Date patient entered the study | Date |
| Age_Years | Age at enrolment | Numeric |
| Sex | Male / Female | Categorical |
| Zone | Geopolitical zone of residence | Categorical |
| BMI | Body mass index (kg/m²) | Numeric |
| Smoking_Status | Never / Former / Current | Categorical |
| Physical_Activity | Low / Moderate / High | Ordinal |
| Family_History_HTN | Family history of hypertension (Yes/No) | Binary |
| Baseline_SBP, Baseline_DBP | Systolic and diastolic BP at enrolment (mmHg) | Numeric |
| Fasting_Glucose_mgdL | Fasting blood glucose (mg/dL) | Numeric |
| HbA1c_pct | Glycated haemoglobin (%) | Numeric |
| Total_Cholesterol_mgdL | Total cholesterol (mg/dL) | Numeric |
| Treatment_Group | Placebo / Drug A / Drug B | Categorical |
| Adherence_pct | % of prescribed doses taken | Numeric |
| Week12_SBP, Week12_DBP | BP after 12 weeks (mmHg) | Numeric |
| Adverse_Event | Any adverse event reported (Yes/No) | Binary |
| **SBP_Change** *(derived)* | Baseline SBP − Week 12 SBP (positive = BP fell) | Numeric |

The raw file was deliberately messy (missing values, impossible ages, one extreme SBP, inconsistent Sex labels) to practise data cleaning.

## 5. Tools Used

| Tool | Purpose |
|---|---|
| **Microsoft Excel** (Data Analysis ToolPak) | Data cleaning, pivot tables, descriptive statistics, t-tests, ANOVA, correlation, regression, chi-square |
| **Python 3** | Full re-analysis and reproducibility |
| `pandas`, `numpy` | Data handling and cleaning |
| `scipy.stats` | Statistical tests |
| `statsmodels` | Multiple linear regression |
| `matplotlib` | Charts |
| **Microsoft Word** | Write-up of Chapter 4 |
| **Git and GitHub** | Version control and documentation |

## 6. Methodology

### 6.1 Study design
Simulated, parallel-group, randomised, placebo-controlled trial with three arms and a 12-week follow-up.

### 6.2 Data preparation
1. **Inspection:** checked size, data types, ranges, missing values and category labels.
2. **Inconsistent labels:** `male`, `F`, `FEMALE` standardised to `Male` / `Female`.
3. **Impossible values:** ages of 250 and −4 and one SBP of 310 treated as data-entry errors and corrected.
4. **Outliers:** identified with the IQR rule (below Q1 − 1.5 × IQR or above Q3 + 1.5 × IQR).
5. **Missing values:** replaced with the column median. The original columns were kept so changes can be traced.
6. **New variable:** `SBP_Change = Baseline_SBP − Week12_SBP`.

### 6.3 Statistical methods

| Objective | Method | Why this method |
|---|---|---|
| 1. Baseline comparability | Mean ± SD, % ; chi-square test; one-way ANOVA | Describes groups and checks they started alike |
| 2. SBP change by group | Paired t-test; one-way ANOVA; Welch t-tests with Bonferroni correction (α = 0.0167) | Compares means of 3 groups, then pairs |
| 3. Adherence | Pearson correlation (overall and by group) | Measures the strength of a linear relationship |
| 4. Predictors | Multiple linear regression (dummy variables; Placebo, Never smoker and Low activity as references) | Estimates each factor's effect while holding others constant |
| 5. Adverse events | Chi-square test of association | Compares proportions across groups |

Significance level: **p < 0.05**.

---

## 7. Results (Chapter 4)

> The full written chapter is in [`docs/Chapter_4_Results.docx`](docs/Chapter_4_Results.docx).

### 7.1 Baseline characteristics (Objective 1)

Of the 500 participants, 267 (53.4%) were female, the mean age was 51.96 years and the mean BMI was 28.0 kg/m². The groups were similar at baseline, except for physical activity.

| Characteristic | Overall | Placebo | Drug A | Drug B | p-value |
|---|---|---|---|---|---|
| Female (%) | 53.4 | 52.9 | 56.0 | 51.2 | 0.686 |
| Current smoker (%) | 19.2 | 16.3 | 23.2 | 18.1 | 0.568 |
| Former smoker (%) | 19.2 | 19.8 | 19.0 | 18.8 |  |
| Low activity (%) | 41.6 | 33.7 | 48.2 | 43.1 | 0.044 |
| Moderate activity (%) | 38.8 | 47.1 | 33.9 | 35.0 |  |
| High activity (%) | 19.6 | 19.2 | 17.9 | 21.9 |  |
| Family history of HTN (%) | 39.2 | 37.8 | 36.9 | 43.1 | 0.461 |
| Age (years) | 52.0 ± 12.3 | 52.1 ± 13.2 | 51.7 ± 12.0 | 52.1 ± 11.7 | 0.936 |
| BMI (kg/m²) | 28.0 ± 5.0 | 28.1 ± 4.8 | 28.4 ± 4.8 | 27.4 ± 5.3 | 0.187 |
| Baseline SBP (mmHg) | 128.4 ± 12.1 | 128.1 ± 12.0 | 128.4 ± 12.1 | 128.7 ± 12.2 | 0.926 |
| Fasting glucose (mg/dL) | 108.4 ± 17.0 | 108.1 ± 16.8 | 107.6 ± 17.1 | 109.5 ± 17.3 | 0.570 |
| HbA1c (%) | 5.23 ± 0.58 | 5.25 ± 0.60 | 5.20 ± 0.58 | 5.24 ± 0.58 | 0.780 |

*Categorical variables are % of each column; numerical variables are mean ± SD. One p-value per variable (chi-square for categories, ANOVA for numbers).*

**Interpretation:** The groups were comparable in every measured characteristic except physical activity (p = 0.044); the Placebo group had fewer low-activity participants (33.7% vs 48.2% and 43.1%). Adjusting for activity later did not change the drug effects (Section 7.4).

### 7.2 Effect on systolic blood pressure (Objective 2)

Overall, SBP fell from 128.41 to 118.30 mmHg, a mean fall of 10.11 mmHg (paired t = 25.72, df = 499, p < 0.001).

| Group | n | Baseline SBP | Week 12 SBP | SBP reduction |
|---|---|---|---|---|
| Placebo | 172 | 128.1 ± 12.0 | 124.1 ± 13.0 | **4.0 ± 7.5** |
| Drug A | 168 | 128.4 ± 12.1 | 117.8 ± 12.9 | **10.6 ± 7.6** |
| Drug B | 160 | 128.7 ± 12.2 | 112.5 ± 13.7 | **16.1 ± 6.7** |

![Boxplot of SBP reduction by group](images/fig1_boxplot.png)

- **One-way ANOVA:** F(2, 497) = 115.66, p < 0.001. The null hypothesis is **rejected**. Treatment group alone explains about 31.8% of the variation in SBP change.
- **Pairwise Welch t-tests** (Bonferroni α = 0.0167):

| Comparison | Mean difference (mmHg) | t | df | p-value |
|---|---|---|---|---|
| Drug A vs Placebo | 6.64 | 8.13 | 337 | < 0.001 |
| Drug B vs Placebo | 12.12 | 15.59 | 330 | < 0.001 |
| Drug B vs Drug A | 5.48 | 6.93 | 324 | < 0.001 |

**Interpretation:** Both drugs lowered blood pressure more than placebo, and Drug B worked best.

### 7.3 Adherence and treatment response (Objective 3)

Mean adherence was 82.2% and did not differ between groups (p = 0.297).

| Group | n | Pearson r | p-value |
|---|---|---|---|
| All participants | 500 | 0.113 | 0.012 |
| Placebo | 172 | -0.096 | 0.212 |
| Drug A | 168 | 0.271 | < 0.001 |
| Drug B | 160 | 0.127 | 0.109 |

**Interpretation:** Higher adherence was weakly linked to a bigger fall in SBP overall. The link was clearest for Drug A, weaker and non-significant for Drug B, and absent for Placebo (which has no active ingredient). These by-group results are exploratory and show association, not cause.

### 7.4 Predictors of SBP reduction (Objective 4)

A first model with only adherence, age, BMI and glucose explained just 1.3% of the variation (R² = 0.013, p = 0.160) because it left out treatment group. The extended model below explains **34.0%** (R² = 0.340, adjusted R² = 0.325, F(11, 488) = 22.82, p < 0.001).

| Predictor | B | 95% CI | p-value |
|---|---|---|---|
| Constant | -0.823 | -8.85 to 7.20 | 0.840 |
| Drug A (vs Placebo) | 6.635 | 5.08 to 8.19 | < 0.001 ✔ |
| Drug B (vs Placebo) | 12.162 | 10.59 to 13.74 | < 0.001 ✔ |
| Adherence (per 1%) | 0.051 | 0.00 to 0.10 | 0.038 ✔ |
| Age (per year) | -0.004 | -0.06 to 0.05 | 0.890 |
| BMI (per kg/m²) | 0.025 | -0.12 to 0.17 | 0.728 |
| Fasting glucose (per mg/dL) | -0.011 | -0.07 to 0.04 | 0.686 |
| HbA1c (per 1%) | 0.048 | -1.50 to 1.59 | 0.951 |
| Current smoker (vs never) | 2.372 | 0.70 to 4.04 | 0.005 ✔ |
| Former smoker (vs never) | 0.499 | -1.17 to 2.17 | 0.557 |
| Moderate activity (vs low) | 1.279 | -0.17 to 2.73 | 0.084 |
| High activity (vs low) | 0.107 | -1.64 to 1.86 | 0.905 |

✔ = statistically significant.

**Interpretation:**
- Treatment group was the strongest predictor: Drug A gave an extra 6.64 mmHg fall and Drug B an extra 12.16 mmHg fall compared with Placebo.
- Every 10-point increase in adherence was linked to about 0.5 mmHg of extra reduction.
- Current smokers had a 2.37 mmHg larger fall, but this reflects their higher starting BP (132.2 vs 128.2 mmHg in never-smokers), not a benefit of smoking.
- Age, BMI, glucose, HbA1c and physical activity were not significant. Adjusting for activity left the drug effects almost unchanged.

### 7.5 Adverse events and benefit–harm balance (Objective 5)

| Group | n | Adverse event n (%) | Mean SBP reduction (mmHg) |
|---|---|---|---|
| Placebo | 172 | 12 (7.0) | 4.0 |
| Drug A | 168 | 30 (17.9) | 10.6 |
| Drug B | 160 | 48 (30.0) | 16.1 |

Chi-square test: χ² = 29.77, df = 2, p < 0.001 (all expected counts > 5).

![Adverse events by group](images/fig2_adverse_events.png)

**Interpretation:** Adverse events rose with treatment strength. Drug B gave the biggest BP fall but also the most side effects (about 3 in 10 users); Drug A gave a smaller fall with fewer side effects. The better choice depends on the BP reduction needed and the side-effect risk that is acceptable.

### 7.6 Summary of findings

| Objective | Key finding | Decision |
|---|---|---|
| 1. Baseline | Groups similar except physical activity (p = 0.044) | Largely comparable |
| 2. SBP change | Placebo 4.0, Drug A 10.6, Drug B 16.1 mmHg; ANOVA p < 0.001 | H₀ rejected |
| 3. Adherence | Overall r = 0.113; Drug A r = 0.271 | Secondary hypothesis partly supported |
| 4. Predictors | Treatment, adherence and current smoking significant; R² = 0.340 | Partly supported |
| 5. Adverse events | 7.0% vs 17.9% vs 30.0%; p < 0.001 | Significant difference |

---

## 8. Discussion

The results show a clear, graded effect: Placebo lowered SBP by about 4 mmHg, Drug A by about 11 mmHg and Drug B by about 16 mmHg. Because patients were randomly allocated and the groups were alike at baseline, the difference can reasonably be credited to the drugs. The small fall on Placebo is expected, since readings often drift down over time even without active treatment.

Adherence mattered most for Drug A, which suggests that missed doses reduce the benefit of that drug. The extended regression confirmed that treatment group is by far the most important predictor, and that age, BMI, glucose and HbA1c did not change who responded in this dataset.

The trade-off between benefit and harm is the key practical finding: the drug that lowers BP most (Drug B) also causes the most adverse events.

## 9. Limitations

- **Simulated data:** results show the analysis method, not real clinical effects.
- **Baseline imbalance:** physical activity differed slightly between groups (p = 0.044), although adjusting for it did not change the conclusions.
- **Multiple testing:** many tests were run; some significant results (for example the smoking effect) may be chance or reflect baseline differences.
- **Adverse events:** recorded as yes/no only, with no information on severity or type.
- **Missing data:** missing values were replaced with the mean, which reduces natural variation. Multiple imputation would be more rigorous.
- **Exploratory subgroups:** the by-group adherence correlations are exploratory.
- **Short follow-up:** only 12 weeks, so long-term effects are unknown.

## 10. Conclusion and Recommendations

**Conclusion:** Both Drug A and Drug B lowered systolic blood pressure significantly more than Placebo, and Drug B lowered it most. Better adherence was linked to larger reductions, mainly with Drug A. Drug B's greater effect came with a higher rate of adverse events.

**Recommendations / future work**
- Repeat the analysis on real trial data with ethical approval.
- Record the severity and type of adverse events.
- Add a longer follow-up period.
- Use multiple imputation for missing data.
- Test whether the drug effect differs by subgroup (for example, by smoking status or activity level).

---

## 11. Repository Structure

```
├── README.md
├── data/
│   ├── hypertension_trial_dataset.csv        # raw (messy) data
│   └── hypertension_trial_dataset.xlsx       # cleaned data + Excel analysis sheets
├── analysis/
│   └── hypertension_analysis.py              # full Python analysis
├── docs/
│   └── Chapter_4_Results.docx                # written results chapter
└── images/
    ├── fig1_boxplot.png
    └── fig2_adverse_events.png
```

## 12. How to Reproduce the Analysis

```bash
# 1. Clone the repository
git clone https://github.com/<your-username>/<repo-name>.git
cd <repo-name>

# 2. Install requirements
pip install pandas numpy scipy matplotlib statsmodels openpyxl

# 3. Run the analysis (from the folder that contains the data file)
python analysis/hypertension_analysis.py
```

The script has a switch, `USE_CLEANED_EXCEL`:
- `True` loads the cleaned Excel file and **reproduces the Chapter 4 numbers exactly**.
- `False` starts from the raw CSV and cleans it in Python. Results are very close but differ slightly (for example ANOVA F = 119.8 vs 115.7), because the few impossible and missing values are handled differently.

**Excel route:** open the `.xlsx` file and see the `Descriptive Analysis`, `Summary Analysis`, `Observed&Expected` and `Regression Statistics` sheets.

## 13. Skills Demonstrated

Data cleaning · Exploratory data analysis · Hypothesis testing (t-test, ANOVA, chi-square) · Correlation · Multiple linear regression with dummy variables · Pivot tables · Data visualisation · Statistical reporting · Excel and Python · Documentation with Git/GitHub

## 14. Author and Contact

**[Adeniyi Aishat Himisioluwa]** · [LinkedIn](https://www.linkedin.com/in/aishat-adeniyi-2b1a40264?utm_source=share&utm_campaign=share_via&utm_content=profile&utm_medium=android_app) · [Email](mailto: aishatadeniyi418@gmail.com)

---

*Disclaimer: This project uses simulated data for learning purposes only. It must not be used for medical advice or clinical decision-making.*
