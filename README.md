# Inferential Statistics & Hypothesis Testing Analysis

## Project Overview
This project focuses on the implementation and analysis of **Inferential Statistics** and **Hypothesis Testing**. It covers fundamental statistical principles, hypothesis formulation, probability metrics, error analysis, and parametric/non-parametric tests to draw conclusions about population parameters from sample data.

---

# Theoretical Framework & Concepts

### 1. Inferential Statistics
Inferential statistics allows us to study sample data and make conclusions or predictions about a larger population. It uses probability principles to make decisions when collecting data from every individual in a population is not feasible.

---

### 2. Hypothesis Testing & Components
Hypothesis testing is a structured statistical method to determine if there is sufficient evidence in a sample to support a specific claim about a population.

* **Null Hypothesis ($H_0$):** The default assumption that there is no effect, no difference, or no relationship between variables.
* **Alternative Hypothesis ($H_1$ or $H_a$):** The claim that there is a significant effect, difference, or relationship. Accepted when $H_0$ is rejected.

---

### 3. Confidence Interval & Critical Value
* **Confidence Interval (CI):** An estimated range of values likely to contain the true population parameter (e.g., a 95% Confidence Interval).
* **Critical Value:** The threshold value determined by the significance level ($\alpha$) that separates the acceptance region from the rejection region of $H_0$.

---

### 4. P-Value Analysis
The **P-value** measures the probability of obtaining test results at least as extreme as the observed results, assuming the null hypothesis is true.

* **$p \le 0.05$:** Strong evidence against $H_0 \rightarrow$ Reject $H_0$.
* **$p > 0.05$:** Insufficient evidence against $H_0 \rightarrow$ Fail to reject $H_0$.

---

### 5. Type I and Type II Errors

| Error Type | Decision | Real Condition | Description |
| :--- | :--- | :--- | :--- |
| **Type I Error ($\alpha$)** | Reject $H_0$ | $H_0$ is True | **False Positive:** Concluding an effect exists when it does not. |
| **Type II Error ($\beta$)** | Fail to Reject $H_0$ | $H_0$ is False | **False Negative:** Failing to detect an effect that actually exists. |

---

### 6. Summary of Statistical Tests

| Statistical Test | Best Used For | Sample Size / Conditions |
| :--- | :--- | :--- |
| **Z-Test** | Comparing population means | Large samples ($n \ge 30$) with known population variance. |
| **T-Test** | Comparing means of 1 or 2 groups | Small samples ($n < 30$) or unknown population variance. |
| **Chi-Square Test ($\chi^2$)** | Categorical variable independence | Categorical data, comparing observed vs. expected frequencies. |
| **ANOVA** | Comparing means across $3+$ groups | Numerical data across multiple independent groups simultaneously. |

---

### 7. Covariance vs. Correlation

#### **Covariance**
Measures the direction of a linear relationship between two variables.
* **Positive:** Variables increase or decrease together.
* **Negative:** One variable increases while the other decreases.
* **Near Zero:** No linear relationship.
*(Note: Covariance indicates direction but not the strength of the relationship.)*

#### **Correlation ($r$)**
Measures both the **strength and direction** of a linear relationship on a scale from $-1$ to $+1$.
* **$+1$:** Perfect positive linear relationship.
* **$-1$:** Perfect negative linear relationship.
* **$0$:** No linear relationship.

---

# Part B - Data Analysis & Testing Tasks

## Dataset Schema
The project uses a synthetic medical health record dataset structured with the following fields:

| Field Name | Data Type | Description |
| :--- | :--- | :--- |
| `record_id` | String | Unique identifier for each health record |
| `age_group` | String | Categorical group (`18-25`, `26-35`, `36-45`, `46-60`, `60+`) |
| `age` | Int | Age of individuals in years |
| `weight` | Int | Weight of individuals in kg |
| `gender` | String | Gender (`Male`, `Female`, `Other`) |
| `region` | String | Geographic region (`North`, `South`, `East`, `West`) |
| `smoking_status` | String | Smoking habit (`Smoker`, `Non-Smoker`, `Former Smoker`) |
| `exercise_frequency`| String | Exercise frequency (`Daily`, `Weekly`, `Rarely`, `Never`) |
| `bmi` | Float | Body Mass Index |
| `blood_pressure` | Float | Systolic blood pressure (mmHg) |
| `diabetes` | Boolean | Diabetes status (`True`/`False`) |
| `hypertension` | Boolean | Hypertension status (`True`/`False`) |
| `cholesterol_level` | Float | Total cholesterol level (mg/dL) |
| `glucose_level` | Float | Fasting glucose level (mg/dL) |
| `visit_date` | Date | Check-up or diagnosis date |

---

## Formulated Hypotheses

1. **Hypothesis Pair 1 (Smoking vs. Diabetes):**
   * **$H_0$:** Smoking habit has no effect on diabetes prevalence.
   * **$H_1$:** Smoking habit significantly affects diabetes prevalence.

2. **Hypothesis Pair 2 (BMI across Diabetes Groups):**
   * **$H_0$:** There is no significant difference in mean BMI between Diabetic and Non-Diabetic individuals.
   * **$H_1$:** Diabetic individuals have a significantly different mean BMI compared to Non-Diabetic individuals.

---

## Summary of Statistical Decisions

| Test Performed | Variables Tested | Significance Level ($\alpha$) | Decision | Statistical Interpretation |
| :--- | :--- | :--- | :--- | :--- |
| **Two-Sample T-Test** | `bmi` across `diabetes` | $0.05$ | **Fail to Reject $H_0$** | Mean BMI does not significantly differ between diabetic and non-diabetic cohorts. |
| **Chi-Square Test** | `smoking_status` vs `diabetes` | $0.05$ | **Fail to Reject $H_0$** | Diabetes prevalence is independent of smoking status in the dataset. |
| **One-Way ANOVA** | `glucose_level` across `age_group` | $0.05$ | **Fail to Reject $H_0$** | Average fasting glucose levels remain consistent across all age demographics. |

---

## Tech Stack & Dependencies

* **Language:** Python 3.x
* **Libraries Used:**
  * `pandas` – Data structuring and aggregation
  * `numpy` – Numerical computing & normal distributions
  * `scipy.stats` – Statistical testing & probability distributions
  * `matplotlib` & `seaborn` – Diagnostic plots & correlation heatmaps

---

## How to Run

1. Clone the repository:
   ```bash
   git clone [https://github.com/YOUR_USERNAME/Spread-Locator.git](https://github.com/YOUR_USERNAME/Spread-Locator.git)
   cd Spread-Locator
   
