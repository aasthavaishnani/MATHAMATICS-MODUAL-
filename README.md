# Spread Locator: A Statistical Distribution Analysis Model

## Project Overview
**Spread Locator** is a comprehensive statistical analysis project designed to model and evaluate health check-up metrics across individuals. This project combines theoretical foundations of probability distributions with practical data analysis and statistical hypothesis testing using Python.

---

# Part A - Theoretical Foundation

### 1. What is a Statistical Distribution?
A statistical distribution is a mathematical function that describes the probabilities of occurrence of different possible outcomes for a random variable. It shows how data values are spread across their range, providing essential insights into central tendency, variability, skewness, and overall structural pattern.

---

### 2. What is a Q-Q Plot and why is it used?
A Q-Q (Quantile-Quantile) plot is a visual diagnostic tool used to assess whether a sample dataset follows a specific theoretical distribution, most commonly the Normal Distribution. It plots sample quantiles against corresponding theoretical standard normal quantiles.
* **Why it is used:** It visually verifies the assumption of normality. If data follows the theoretical distribution, points fall closely along the 45-degree reference line ($y = x$). Deviations or S-shapes indicate heavy tails, light tails, or skewness.

---

### 3. Difference between Discrete and Continuous Distributions

| Feature | Discrete Distribution | Continuous Distribution |
| :--- | :--- | :--- |
| **Definition** | Models random variables taking distinct, separate, and countable outcomes. | Models random variables taking any real value within a continuous range. |
| **Data Values** | Whole numbers or countable values ($0, 1, 2, 3$). | Continuous real numbers ($10.5, 100.75, 499.99$). |
| **Measurement Function** | Probability Mass Function (PMF): $P(X = x)$. | Probability Density Function (PDF): $P(a \le X \le b)$. |
| **Example** | Number of doctor visits made by a patient in a month. | Patient's exact weight or fasting glucose level. |

---

### 4. What is Bernoulli Distribution?
The Bernoulli distribution is a discrete probability distribution for a single trial with exactly two mutually exclusive outcomes: "Success" ($1$) and "Failure" ($0$).
* **Parameters:** $p$ (probability of success) and $q = 1 - p$ (probability of failure).
* **PMF Formula:** $P(X = k) = p^k (1-p)^{1-k} \quad \text{for } k \in \{0, 1\}$
* **Example:** Individual diabetes diagnostic status (`diabetes = True` as $1$, `diabetes = False` as $0$).

---

### 5. What is Binomial Distribution?
The Binomial distribution models the number of successes in a fixed number ($n$) of independent Bernoulli trials with constant success probability ($p$).
* **Parameters:** $n$ (total trials) and $p$ (success probability).
* **PMF Formula:** 
  $$P(X = k) = \binom{n}{k} p^k (1-p)^{n-k} \quad \text{for } k = 0, 1, 2, \dots, n$$
* **Example:** Total number of patients diagnosed with hypertension out of 10 random clinic check-ups.

---

### 6. Explain Log-Normal Distribution
A Log-Normal distribution is a continuous distribution of a random variable whose natural logarithm is normally distributed. If $X$ is Log-Normal, then $Y = \ln(X)$ follows a Normal Distribution.
* **Key Characteristics:** Strictly positive ($X > 0$), right-skewed with a long right tail.
* **Example:** Patient fasting glucose levels or medical billing amounts where high values create a right-skewed tail.

---

### 7. Explain Power Law Distribution
A Power Law distribution is a continuous distribution where a relative change in one quantity produces a proportional relative change in another ($Y = c \cdot X^{-\alpha}$).
* **Key Characteristics:** Features extreme heavy tails and represents Pareto-style scaling dynamics.
* **Example:** Occurrence of rare severe healthcare complications across a population.

---

### 8. What is Box-Cox Transform?
The Box-Cox transformation is a parametric power transformation used to transform non-normal, skewed positive data into a distribution that closely approximates normality and stabilizes variance.
* **Formula:**
  $$y^{(\lambda)} = \begin{cases} \frac{y^\lambda - 1}{\lambda} & \text{if } \lambda \neq 0 \\ \ln(y) & \text{if } \lambda = 0 \end{cases}$$
* **Constraint:** Requires all input data values to be strictly positive ($y > 0$).

---

### 9. Explain Poisson Distribution with an Example
The Poisson distribution is a discrete probability distribution expressing the likelihood of a given number of independent events occurring within a fixed interval of time or space.
* **Key Assumptions:** Events occur independently at a constant average rate ($\lambda$).
* **PMF Formula:**
  $$P(X = k) = \frac{\lambda^k e^{-\lambda}}{k!} \quad \text{for } k = 0, 1, 2, \dots$$
* **Example:** Modeling the number of patients arriving at an emergency clinic per hour with an average arrival rate of $\lambda = 15$ patients/hour.

---

### 10. What is Z-score Probability?
A Z-score measures how many standard deviations ($\sigma$) a specific value ($x$) lies away from the population mean ($\mu$).
* **Formula:** $Z = \frac{x - \mu}{\sigma}$
* **Z-score Probability:** Cumulative standard normal probability associated with a calculated Z-score, used to find probabilities above/below critical health thresholds (e.g., $P(\text{blood\_pressure} > 140)$).

---

### 11. Differentiate Probability Density Function (PDF) and Cumulative Distribution Function (CDF)

| Feature | Probability Density Function (PDF) | Cumulative Distribution Function (CDF) |
| :--- | :--- | :--- |
| **Definition** | Relative likelihood density of a continuous variable taking a specific value. | Total cumulative probability that a random variable is less than or equal to a value ($X \le x$). |
| **Output Range** | Non-negative real values ($f(x) \ge 0$). | Strictly bounded between $0$ and $1$ ($0\% \le F(x) \le 100\%$). |
| **Interpretation** | Highlights peaks where observations are concentrated. | Shows accumulated percentage of data up to point $x$. |

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
   
