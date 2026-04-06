# 🎯 Quantitative Analysis (QA) — Unit Test 2 (PT-II) Complete Guide
## Mumbai University | Computer Engineering | SEM 6 | REV-2019

---

# 📊 PART A: QUESTION BANK ANALYSIS & PAST TREND PATTERNS

## Exam Format (PT-II / Unit Test 2)
| Parameter | Detail |
|-----------|--------|
| **Total Marks** | 20 Marks |
| **Duration** | 1 Hour |
| **Syllabus Coverage** | Module 4 (Multiple Regression), Chapter 5 (Estimation), Chapter 6 (Hypothesis Testing) |
| **Question Style** | Mix of theory + numerical + proof-based |

---

## 🔥 Topic-Wise Priority Analysis (Based on MU Past Trends)

| Priority | Topic | QB Questions | Frequency | Expected Marks |
|----------|-------|-------------|-----------|----------------|
| 🔴 **HIGHEST** | Multiple Linear Regression (Numerical) | M4-Q1,Q2,Q3,Q6 | **Almost Every Exam** | 5-10 marks |
| 🔴 **HIGHEST** | Hypothesis Testing — Z-Test Numerical | C6-Q5,Q6 | **Every Exam** | 5-8 marks |
| 🟠 **HIGH** | Partial & Multiple Correlation Coefficient | M4-Q4,Q5 | **Very Frequent** | 5-8 marks |
| 🟠 **HIGH** | Type I & Type II Error | C6-Q3 | **Very Frequent** | 5 marks |
| 🟡 **MEDIUM** | Point Estimation & Properties | C5-Q1,Q4 | **Frequent** | 5 marks |
| 🟡 **MEDIUM** | Unbiased Estimator Proofs | C5-Q3,Q6 | **Frequent** | 5 marks |
| 🟢 **STANDARD** | Types of Estimation | C5-Q2 | **Frequent** | 5 marks |
| 🟢 **STANDARD** | MLE with Advantages/Disadvantages | C5-Q5 | **Moderate** | 5 marks |
| 🔵 **MODERATE** | Null vs Alternative Hypothesis | C6-Q1,Q2 | **Frequent** | 5 marks |
| 🔵 **MODERATE** | Neyman-Pearson Lemma | C6-Q4 | **Occasional** | 5 marks |

---

## 📈 Pattern Classification

### Pattern 1: Numerical / Problem-Solving (MOST IMPORTANT)
| Q# | Topic |
|----|-------|
| M4-Q1 | Regression equation from correlation coefficients |
| M4-Q2,Q3 | Multiple linear regression from data |
| M4-Q4 | Partial correlation computation |
| M4-Q6 | Multiple regression + R² + F-test |
| C5-Q1 | Point estimation (mean, std dev, SE) |
| C6-Q6 | Z-test / t-test numerical |

### Pattern 2: Concept + Proof (Theory with Mathematical Derivation)
| Q# | Topic |
|----|-------|
| C5-Q3 | Prove sample mean is unbiased estimator |
| C5-Q6 | Prove sample variance is unbiased estimator |
| C6-Q4 | Neyman-Pearson Lemma |

### Pattern 3: Define & Explain (Structured Theory)
| Q# | Topic |
|----|-------|
| C5-Q2 | Types of estimation |
| C5-Q4 | Point estimation + properties |
| C5-Q5 | MLE method |
| C6-Q1,Q2 | Hypothesis testing definitions |
| C6-Q3 | Type I & Type II errors |
| M4-Q5 | Partial/Multiple correlation definitions |

> [!TIP]
> **Exam Strategy**: Numericals carry the most marks. Always show **every step**, use **tables for computation**, **box your final answers**, and **state formulas before substituting**.

---

# 📝 PART B: COMPLETE ANSWERS

---

# MODULE 4: MULTIPLE REGRESSION & CORRELATION

---

## M4-Q1) Regression Equation of X₂ on X₁ and X₃

**Given:** r₁₂ = 0.8, r₁₃ = 0.7, r₂₃ = 0.6, σ₁ = 10, σ₂ = 8, σ₃ = 5
**Hint:** b₂₁.₃ = 0.596, b₂₃.₁ = 0.125

### Formula for Multiple Regression Equation of X₂ on X₁ and X₃:

$$X_2 - \bar{X}_2 = b_{21.3}(X_1 - \bar{X}_1) + b_{23.1}(X_3 - \bar{X}_3)$$

### Step 1: Calculate Partial Regression Coefficients

**Formula for $b_{21.3}$:**
$$b_{21.3} = \left(\frac{r_{12} - r_{23} \cdot r_{13}}{1 - r_{13}^2}\right) \cdot \frac{\sigma_2}{\sigma_1}$$

**Substituting:**
$$\begin{aligned}
b_{21.3} &= \left[\frac{0.8 - (0.6 \cdot 0.7)}{1 - 0.7^2}\right] \cdot \frac{8}{10} \\
&= \left[\frac{0.8 - 0.42}{1 - 0.49}\right] \cdot 0.8 \\
&= \left[\frac{0.38}{0.51}\right] \cdot 0.8 \\
&= 0.7451 \cdot 0.8 = 0.596 \quad \text{(Correct)}
\end{aligned}$$

**Formula for $b_{23.1}$:**
$$b_{23.1} = \left(\frac{r_{23} - r_{12} \cdot r_{13}}{1 - r_{13}^2}\right) \cdot \frac{\sigma_2}{\sigma_3}$$

**Substituting:**
$$\begin{aligned}
b_{23.1} &= \left[\frac{0.6 - (0.8 \cdot 0.7)}{1 - 0.7^2}\right] \cdot \frac{8}{5} \\
&= \left[\frac{0.6 - 0.56}{1 - 0.49}\right] \cdot 1.6 \\
&= \left[\frac{0.04}{0.51}\right] \cdot 1.6 \\
&= 0.0784 \cdot 1.6 = 0.125 \quad \text{(Correct)}
\end{aligned}$$

### Step 2: Write the Regression Equation
$$\boxed{X_2 - \bar{X}_2 = 0.596(X_1 - \bar{X}_1) + 0.125(X_3 - \bar{X}_3)}$$

### Interpretation
- A unit increase in $X_1$ results in an increase of **0.596** in $X_2$ (holding $X_3$ constant).
- A unit increase in $X_3$ results in an increase of **0.125** in $X_2$ (holding $X_1$ constant).
- $X_1$ has a significantly stronger influence on $X_2$ than $X_3$.

---

## M4-Q2) Multiple Linear Regression of X₁ on X₂ and X₃

**Given Data:**

| X₁ | 2 | 4 | 6 | 8 |
|----|---|---|---|---|
| X₂ | 3 | 5 | 7 | 9 |
| X₃ | 4 | 6 | 8 | 10 |

### Step 1: Compute Required Sums (n = 4)

| i | X₁ | X₂ | X₃ | X₁X₂ | X₁X₃ | X₂X₃ | X₂² | X₃² |
|---|----|----|----|----|----|----|----|----|
| 1 | 2 | 3 | 4 | 6 | 8 | 12 | 9 | 16 |
| 2 | 4 | 5 | 6 | 20 | 24 | 30 | 25 | 36 |
| 3 | 6 | 7 | 8 | 42 | 48 | 56 | 49 | 64 |
| 4 | 8 | 9 | 10 | 72 | 80 | 90 | 81 | 100 |
| **Σ** | **20** | **24** | **28** | **140** | **160** | **188** | **164** | **216** |

### Step 2: Compute Means

```
X̄₁ = 20/4 = 5,  X̄₂ = 24/4 = 6,  X̄₃ = 28/4 = 7
```

### Step 3: Normal Equations for X₁ = a + b₁X₂ + b₂X₃

The three normal equations are:
```
ΣX₁ = na + b₁ΣX₂ + b₂ΣX₃
ΣX₁X₂ = aΣX₂ + b₁ΣX₂² + b₂ΣX₂X₃
ΣX₁X₃ = aΣX₃ + b₁ΣX₂X₃ + b₂ΣX₃²
```

Substituting:
```
20 = 4a + 24b₁ + 28b₂       ... (i)
140 = 24a + 164b₁ + 188b₂    ... (ii)
160 = 28a + 188b₁ + 216b₂    ... (iii)
```

### Step 4: Solve the System

From equation (i): a = (20 - 24b₁ - 28b₂)/4 = 5 - 6b₁ - 7b₂

**Note:** In this dataset, X₁, X₂, X₃ are in perfect linear relationship: X₁ = X₂ - 1 = X₃ - 2

Substituting a = 5 - 6b₁ - 7b₂ into (ii) and (iii) and solving simultaneously:

After solving: **b₁ = 1, b₂ = 0, a = -1** (or equivalently b₁ = 0, b₂ = 1, a = -5 — both valid due to perfect multicollinearity)

$$\boxed{X_1 = -1 + 1 \cdot X_2 + 0 \cdot X_3 = X_2 - 1}$$

> [!NOTE]
> Since all three variables are perfectly linearly related (X₁ = X₂ - 1 = X₃ - 2), there is perfect multicollinearity. Show all normal equation steps in exam for full marks.

---

## M4-Q3) Multiple Linear Regression of Y on X₁ and X₂

**Given Data:**

| Y | 4 | 6 | 7 | 9 | 13 | 15 |
|---|---|---|---|---|----|----|
| X₁ | 15 | 12 | 8 | 6 | 4 | 3 |
| X₂ | 30 | 24 | 20 | 14 | 10 | 4 |

### Step 1: Compute Required Sums (n = 6)

| i | Y | X₁ | X₂ | YX₁ | YX₂ | X₁X₂ | X₁² | X₂² | Y² |
|---|---|----|----|-----|-----|------|-----|-----|-----|
| 1 | 4 | 15 | 30 | 60 | 120 | 450 | 225 | 900 | 16 |
| 2 | 6 | 12 | 24 | 72 | 144 | 288 | 144 | 576 | 36 |
| 3 | 7 | 8 | 20 | 56 | 140 | 160 | 64 | 400 | 49 |
| 4 | 9 | 6 | 14 | 54 | 126 | 84 | 36 | 196 | 81 |
| 5 | 13 | 4 | 10 | 52 | 130 | 40 | 16 | 100 | 169 |
| 6 | 15 | 3 | 4 | 45 | 60 | 12 | 9 | 16 | 225 |
| **Σ** | **54** | **48** | **102** | **339** | **720** | **1034** | **494** | **2188** | **576** |

### Step 2: Compute Means

```
Ȳ = 54/6 = 9,  X̄₁ = 48/6 = 8,  X̄₂ = 102/6 = 17
```

### Step 3: Normal Equations for Ŷ = a + b₁X₁ + b₂X₂

```
ΣY = na + b₁ΣX₁ + b₂ΣX₂
ΣYX₁ = aΣX₁ + b₁ΣX₁² + b₂ΣX₁X₂
ΣYX₂ = aΣX₂ + b₁ΣX₁X₂ + b₂ΣX₂²
```

Substituting:
```
54 = 6a + 48b₁ + 102b₂         ... (i)
339 = 48a + 494b₁ + 1034b₂      ... (ii)
720 = 102a + 1034b₁ + 2188b₂    ... (iii)
```

### Step 4: Solve

From (i): **a = 9 - 8b₁ - 17b₂**

Substituting into (ii):
```
339 = 48(9 - 8b₁ - 17b₂) + 494b₁ + 1034b₂
339 = 432 - 384b₁ - 816b₂ + 494b₁ + 1034b₂
339 = 432 + 110b₁ + 218b₂
110b₁ + 218b₂ = -93        ... (iv)
```

Substituting into (iii):
```
720 = 102(9 - 8b₁ - 17b₂) + 1034b₁ + 2188b₂
720 = 918 - 816b₁ - 1734b₂ + 1034b₁ + 2188b₂
720 = 918 + 218b₁ + 454b₂
218b₁ + 454b₂ = -198       ... (v)
```

From (iv): $b_1 = \frac{-93 - 218b_2}{110}$

Substituting into (v):
$$\begin{aligned}
218 \cdot \left(\frac{-93 - 218b_2}{110}\right) + 454b_2 &= -198 \\
\frac{-20274 - 47524b_2}{110} + 454b_2 &= -198 \\
-20274 - 47524b_2 + 49940b_2 &= -21780 \\
2416b_2 &= -1506 \\
b_2 &= -0.6233
\end{aligned}$$

$$b_1 = \frac{-93 - 218(-0.6233)}{110} = \frac{-93 + 135.88}{110} = 0.3898$$

**Calculated Coefficients:**
$$\begin{aligned}
a &= 9 - 8(0.3898) - 17(-0.6233) \\
&= 9 - 3.118 + 10.596 \\
&= 16.478
\end{aligned}$$

$$\boxed{\hat{Y} = 16.478 + 0.390 X_1 - 0.623 X_2}$$

> [!IMPORTANT]
> In exam: Always show (1) Computation table, (2) Normal equations, (3) Substitution steps, (4) Final boxed equation. Each step fetches marks.

---

## M4-Q4) Partial Correlation Coefficients

**Given:** r₁₂ = 0.7, r₁₃ = 0.61, r₂₃ = 0.4

### Formulas:

$$r_{23.1} = \frac{r_{23} - r_{12} \cdot r_{13}}{\sqrt{(1-r_{12}^2)(1-r_{13}^2)}}$$

$$r_{13.2} = \frac{r_{13} - r_{12} \cdot r_{23}}{\sqrt{(1-r_{12}^2)(1-r_{23}^2)}}$$

$$r_{12.3} = \frac{r_{12} - r_{13} \cdot r_{23}}{\sqrt{(1-r_{13}^2)(1-r_{23}^2)}}$$

### Calculations for Partial Correlation:

- **Coefficient $r_{23.1}$ (Correlation between $X_2$ and $X_3$ given $X_1$):**
$$\begin{aligned}
r_{23.1} &= \frac{0.4 - (0.7 \cdot 0.61)}{\sqrt{(1 - 0.7^2)(1 - 0.61^2)}} \\
&= \frac{0.4 - 0.427}{\sqrt{0.51 \cdot 0.6279}} \\
&= \frac{-0.027}{0.5659} = -0.0477
\end{aligned}$$
$$\boxed{r_{23.1} = -0.0477}$$

- **Coefficient $r_{13.2}$ (Correlation between $X_1$ and $X_3$ given $X_2$):**
$$\begin{aligned}
r_{13.2} &= \frac{0.61 - (0.7 \cdot 0.4)}{\sqrt{(1 - 0.7^2)(1 - 0.4^2)}} \\
&= \frac{0.61 - 0.28}{\sqrt{0.51 \cdot 0.84}} \\
&= \frac{0.33}{0.6545} = 0.5042
\end{aligned}$$
$$\boxed{r_{13.2} = 0.5042}$$

- **Coefficient $r_{12.3}$ (Correlation between $X_1$ and $X_2$ given $X_3$):**
$$\begin{aligned}
r_{12.3} &= \frac{0.7 - (0.61 \cdot 0.4)}{\sqrt{(1 - 0.61^2)(1 - 0.4^2)}} \\
&= \frac{0.7 - 0.244}{\sqrt{0.6279 \cdot 0.84}} \\
&= \frac{0.456}{0.7262} = 0.6280
\end{aligned}$$
$$\boxed{r_{12.3} = 0.6280}$$

### Interpretation
- $r_{23.1} \approx -0.048$: Almost **no correlation** between $X_2$ and $X_3$ when $X_1$ is constant.
- $r_{13.2} \approx 0.504$: **Moderate positive** correlation between $X_1$ and $X_3$ when $X_2$ is constant.
- $r_{12.3} \approx 0.628$: **Strong positive** correlation between $X_1$ and $X_2$ when $X_3$ is constant.

---

## M4-Q5) Definitions — Regression & Correlation Terms

### (a) Partial Regression Coefficient

**Definition:** The partial regression coefficient **b₁₂.₃** measures the **change in X₁ per unit change in X₂**, while **keeping X₃ constant**.

**Formula:**
$$b_{12.3} = \frac{r_{12} - r_{13} \cdot r_{23}}{1 - r_{23}^2} \times \frac{\sigma_1}{\sigma_2}$$

**Key Points:**
- Measures the **net effect** of one independent variable on the dependent variable
- Removes (controls for) the effect of other variables
- Can be positive or negative
- **Range:** -∞ to +∞

### (b) Partial Correlation Coefficient

**Definition:** The partial correlation coefficient **r₁₂.₃** measures the **linear relationship between X₁ and X₂** after **removing (controlling for) the effect of X₃**.

**Formula:**
$$r_{12.3} = \frac{r_{12} - r_{13} \cdot r_{23}}{\sqrt{(1-r_{13}^2)(1-r_{23}^2)}}$$

**Key Points:**
- Measures **net correlation** between two variables after eliminating effect of others
- **Range:** -1 ≤ r₁₂.₃ ≤ +1
- If r₁₂.₃ = 0, X₁ and X₂ are uncorrelated after removing X₃'s effect
- **Higher order:** r₁₂.₃₄ removes effect of both X₃ and X₄

### (c) Multiple Correlation Coefficient

**Definition:** The multiple correlation coefficient **R₁.₂₃** measures the **strength of linear relationship** between one dependent variable (X₁) and **two or more independent variables** (X₂, X₃) **simultaneously**.

**Formula:**
$$R_{1.23} = \sqrt{\frac{r_{12}^2 + r_{13}^2 - 2r_{12} \cdot r_{13} \cdot r_{23}}{1 - r_{23}^2}}$$

**Key Points:**
- **Range:** 0 ≤ R₁.₂₃ ≤ 1 (always non-negative)
- R² = Coefficient of Multiple Determination (proportion of variance explained)
- R₁.₂₃ ≥ |r₁₂| and R₁.₂₃ ≥ |r₁₃| (always ≥ any individual correlation)
- Used to assess **goodness of fit** of multiple regression

```
Diagram: Relationship between Correlation Types

Simple Correlation (r₁₂)
    ↓ (extend to more variables)
Partial Correlation (r₁₂.₃) ← removes effect of X₃
    ↓ (combine all)
Multiple Correlation (R₁.₂₃) ← overall fit of regression
```

---

# CHAPTER 5: ESTIMATION THEORY

---

## C5-Q1) Point Estimation — Numerical Computation

**Given:** Random sample of n = 6: {6, 10, 13, 14, 18, 20}

### (1) Population Mean (Point Estimate)

$$\bar{X} = \frac{\sum X_i}{n} = \frac{6 + 10 + 13 + 14 + 18 + 20}{6} = \frac{81}{6} = 13.5$$

$$\boxed{\bar{X} = 13.5}$$

### (2) Population Standard Deviation (Point Estimate)

| Xᵢ | Xᵢ - X̄ | (Xᵢ - X̄)² |
|-----|---------|------------|
| 6 | -7.5 | 56.25 |
| 10 | -3.5 | 12.25 |
| 13 | -0.5 | 0.25 |
| 14 | 0.5 | 0.25 |
| 18 | 4.5 | 20.25 |
| 20 | 6.5 | 42.25 |
| **Σ** | **0** | **131.50** |

**Sample Standard Deviation (s):**

$$s = \sqrt{\frac{\sum(X_i - \bar{X})^2}{n-1}} = \sqrt{\frac{131.50}{5}} = \sqrt{26.3} = 5.128$$

$$\boxed{s = 5.128}$$

> [!NOTE]
> We use (n-1) in denominator for **unbiased** estimate of population variance. If asked for population SD directly, some use n in denominator: σ̂ = √(131.50/6) = √21.917 = 4.682

### (3) Standard Error of Mean
$$SE(\bar{X}) = \frac{s}{\sqrt{n}}$$

**Substituting:**
$$SE(\bar{X}) = \frac{5.128}{\sqrt{6}} = \frac{5.128}{2.449} = 2.094$$

$$\boxed{SE(\bar{X}) = 2.094}$$

**Interpretation:** The sample mean of 13.5 is expected to deviate from the true population mean by approximately $\pm 2.094$ units.

---

## C5-Q2) Types of Estimation

### Definition
**Estimation** is the process of using **sample data** to make inferences about **unknown population parameters** (like μ, σ², p).

### Two Main Types:

### Type 1: Point Estimation
**Definition:** A **single value** (statistic) is used to estimate an unknown population parameter.

| Aspect | Detail |
|--------|--------|
| **Output** | Single numerical value |
| **Example** | X̄ = 13.5 is a point estimate of μ |
| **Advantage** | Simple, easy to compute |
| **Disadvantage** | No information about accuracy/reliability |

**Examples:**
- Sample mean X̄ estimates population mean μ
- Sample proportion p̂ estimates population proportion p
- Sample variance S² estimates population variance σ²

### Type 2: Interval Estimation
**Definition:** An **interval (range)** of values within which the population parameter is expected to lie, with a specified **confidence level**.

| Aspect | Detail |
|--------|--------|
| **Output** | Range [L, U] with confidence level |
| **Example** | μ ∈ (11.4, 15.6) with 95% confidence |
| **Advantage** | Provides measure of precision/reliability |
| **Disadvantage** | More complex to compute |

**Formula for Confidence Interval for Mean (σ known):**
$$\bar{X} - Z_{\alpha/2} \cdot \frac{\sigma}{\sqrt{n}} \leq \mu \leq \bar{X} + Z_{\alpha/2} \cdot \frac{\sigma}{\sqrt{n}}$$

### Comparison Table

| Parameter | Point Estimation | Interval Estimation |
|-----------|-----------------|-------------------|
| **Output** | Single value | Range of values |
| **Precision** | No measure of precision | Confidence level given |
| **Formula** | X̄, S², p̂ | (X̄ ± Zα/2 · σ/√n) |
| **Information** | Less informative | More informative |
| **Computation** | Simple | More complex |
| **Example** | μ̂ = 13.5 | μ ∈ (11.4, 15.6) at 95% |

```
Diagram: Types of Estimation

              Estimation
             /          \
     Point Estimation   Interval Estimation
     (Single Value)     (Confidence Interval)
         |                    |
     X̄ = 13.5          (11.4, 15.6) at 95%
         •               [----•----]
   (just a point)      (range with confidence)
```

---

## C5-Q3) Prove: Sample Mean is an Unbiased Estimator of Population Mean

### Statement
Prove that $E(\bar{X}) = \mu$, i.e., the expected value of the sample mean equals the population mean.

### Proof

**Let** $X_1, X_2, \dots, X_n$ be a random sample from a population with mean $\mu$ and variance $\sigma^2$.

**Step 1:** Define the sample mean:
$$\bar{X} = \frac{1}{n}\sum_{i=1}^{n} X_i$$

**Step 2:** Take expectation on both sides:
$$E(\bar{X}) = E\left(\frac{1}{n}\sum_{i=1}^{n} X_i\right)$$

**Step 3:** Use linearity of expectation:
$$E(\bar{X}) = \frac{1}{n}\sum_{i=1}^{n} E(X_i)$$

**Step 4:** Since each $X_i$ is from the same population, $E(X_i) = \mu$:
$$\begin{aligned}
E(\bar{X}) &= \frac{1}{n} \underbrace{(\mu + \mu + \dots + \mu)}_{n \text{ times}} \\
&= \frac{1}{n} \cdot n\mu = \mu
\end{aligned}$$

### Conclusion
$$\boxed{E(\bar{X}) = \mu}$$

Since $E(\bar{X}) = \mu$, the sample mean $\bar{X}$ is an **unbiased estimator** of the population mean $\mu$.

**Consistency Check:** Since $\text{Var}(\bar{X}) = \frac{\sigma^2}{n}$, as $n \to \infty$, $\text{Var}(\bar{X}) \to 0$. Thus, $\bar{X}$ is also a **consistent** estimator.

---

## C5-Q4) Point Estimation — Definition and Properties

### Definition
**Point Estimation** is a method of using a **single value** computed from sample data (a **statistic**) to estimate the value of an unknown **population parameter**.

- The statistic used is called the **estimator** (e.g., X̄)
- The computed value is called the **estimate** (e.g., X̄ = 13.5)

### Properties of a Good Point Estimator

| # | Property | Definition | Mathematical Condition |
|---|----------|-----------|----------------------|
| 1 | **Unbiasedness** | The expected value of the estimator equals the parameter | E(θ̂) = θ |
| 2 | **Consistency** | As sample size n → ∞, the estimator converges to the true value | P(\|θ̂ - θ\| > ε) → 0 as n → ∞ |
| 3 | **Efficiency** | Among all unbiased estimators, it has the **minimum variance** | Var(θ̂) ≤ Var(θ̃) for all unbiased θ̃ |
| 4 | **Sufficiency** | The estimator uses **all information** in the sample about the parameter | T(X) is sufficient if P(X\|T) doesn't depend on θ |
| 5 | **Minimum Variance** | Has the smallest variance among the class of unbiased estimators (MVUE) | Achieves Cramér-Rao Lower Bound |

### Detailed Explanation with Examples

**1. Unbiasedness:**
```
X̄ is unbiased for μ because E(X̄) = μ
S² = Σ(Xᵢ-X̄)²/(n-1) is unbiased for σ² because E(S²) = σ²
BUT: S is BIASED for σ (E(S) ≠ σ)
```

**2. Consistency:**
```
X̄ is consistent because Var(X̄) = σ²/n → 0 as n → ∞
By Chebyshev's inequality: P(|X̄ - μ| > ε) ≤ σ²/(nε²) → 0
```

**3. Efficiency:**
```
Among all unbiased estimators of μ:
- X̄ has minimum variance = σ²/n
- Median has higher variance = πσ²/(2n)
∴ X̄ is more efficient than Median
Relative Efficiency = Var(Median)/Var(X̄) = π/2 ≈ 1.57
```

**4. Sufficiency:**
```
For Normal distribution: X̄ is sufficient for μ
It captures ALL information about μ from the sample
```

```
Diagram: Properties of Good Estimator

              Good Point Estimator
         /    |      |       |       \
  Unbiased  Consistent  Efficient  Sufficient  Min Variance
  E(θ̂)=θ   n→∞,θ̂→θ   Min Var    Uses all     Achieves
                        among     info from    Cramér-Rao
                       unbiased   sample       bound
```

---

## C5-Q5) Method of Maximum Likelihood Estimation (MLE)

### Definition
The **Maximum Likelihood Estimation (MLE)** method estimates the parameter θ by finding the value that **maximizes the likelihood function** — i.e., the value of θ that makes the observed data **most probable**.

### Steps of MLE Method

**Step 1:** Write the **likelihood function** L(θ):
$$L(\theta) = \prod_{i=1}^{n} f(x_i; \theta)$$

**Step 2:** Take the **log-likelihood** (easier to work with):
$$\ln L(\theta) = \sum_{i=1}^{n} \ln f(x_i; \theta)$$

**Step 3:** Differentiate w.r.t. θ and set equal to **zero**:
$$\frac{d}{d\theta} \ln L(\theta) = 0$$

**Step 4:** Solve for θ̂ (the MLE)

**Step 5:** Verify it's a **maximum** (second derivative < 0)

### Example: MLE for Normal Distribution Mean

**Given:** $X_1, X_2, \dots, X_n \sim N(\mu, \sigma^2)$, find the MLE of $\mu$.

**Step 1: Likelihood function $L(\mu)$:**
$$L(\mu) = \prod_{i=1}^{n} \frac{1}{\sqrt{2\pi}\sigma} \exp\left(-\frac{(x_i-\mu)^2}{2\sigma^2}\right)$$

**Step 2: Log-likelihood $\ln L(\mu)$:**
$$\ln L(\mu) = -\frac{n}{2}\ln(2\pi) - n\ln(\sigma) - \frac{1}{2\sigma^2}\sum_{i=1}^n(x_i - \mu)^2$$

**Step 3: Differentiate w.r.t. $\mu$ and set to zero:**
$$\frac{\partial \ln L}{\partial \mu} = \frac{1}{\sigma^2}\sum_{i=1}^n(x_i - \mu) = 0$$

**Step 4: Solve for $\hat{\mu}$:**
$$\sum x_i - n\mu = 0 \implies \hat{\mu} = \frac{\sum x_i}{n} = \bar{X}$$

$$\boxed{\hat{\mu}_{MLE} = \bar{X}}$$

### Advantages of MLE

| # | Advantage |
|---|-----------|
| 1 | **Consistent** — converges to true value as n → ∞ |
| 2 | **Asymptotically efficient** — achieves minimum variance for large samples |
| 3 | **Asymptotically normal** — distribution approaches normal for large n |
| 4 | **Invariance property** — if θ̂ is MLE of θ, then g(θ̂) is MLE of g(θ) |
| 5 | **Widely applicable** — can be used for any parametric distribution |
| 6 | MLE is a **sufficient statistic** if one exists |

### Disadvantages of MLE

| # | Disadvantage |
|---|-------------|
| 1 | Can be **biased** for small samples (e.g., MLE of σ² = Σ(Xᵢ-X̄)²/n, not n-1) |
| 2 | Requires knowledge of the **probability distribution** form |
| 3 | May be **computationally intensive** (no closed-form solution sometimes) |
| 4 | May converge to **local maximum** instead of global maximum |
| 5 | Sensitive to **model misspecification** |
| 6 | May not exist for certain distributions or data |

---

## C5-Q6) Prove: Sample Variance S² is an Unbiased Estimator of σ²

### Statement
Show that $E(S^2) = \sigma^2$ where $S^2 = \frac{\sum(X_i - \bar{X})^2}{n-1}$

### Proof

**Step 1:** Expand the sum of squares:
$$\sum_{i=1}^{n}(X_i - \bar{X})^2 = \sum_{i=1}^{n}X_i^2 - n\bar{X}^2$$

**Step 2:** Apply the expectation operator:
$$E\left[\sum(X_i - \bar{X})^2\right] = \sum E(X_i^2) - nE(\bar{X}^2)$$

**Step 3:** Use the identity $E(X^2) = \text{Var}(X) + [E(X)]^2$:
- $E(X_i^2) = \sigma^2 + \mu^2$
- $E(\bar{X}^2) = \frac{\sigma^2}{n} + \mu^2$

**Step 4:** Substitute and simplify:
$$\begin{aligned}
E\left[\sum(X_i - \bar{X})^2\right] &= n(\sigma^2 + \mu^2) - n\left(\frac{\sigma^2}{n} + \mu^2\right) \\
&= n\sigma^2 + n\mu^2 - \sigma^2 - n\mu^2 \\
&= (n-1)\sigma^2
\end{aligned}$$

**Step 5:** Final confirmation:
$$E(S^2) = E\left[\frac{\sum(X_i - \bar{X})^2}{n-1}\right] = \frac{(n-1)\sigma^2}{n-1} = \sigma^2$$

### Conclusion
$$\boxed{E(S^2) = \sigma^2}$$

Hence, $S^2 = \frac{\sum(X_i - \bar{X})^2}{n-1}$ is an **unbiased estimator** of the population variance $\sigma^2$.

> [!IMPORTANT]
> **Why $n-1$?** If we divided by $n$, the expectation would be $\frac{n-1}{n}\sigma^2$, which underestimates the true variance. Dividing by $n-1$ (Bessel's correction) removes this bias.

---

# CHAPTER 6: HYPOTHESIS TESTING

---

## C6-Q1) Define and Explain Hypothesis and Tests of Hypothesis

### Definition of Hypothesis
A **statistical hypothesis** is a **statement (claim/assumption)** about a population parameter (such as μ, σ², p) that can be **tested using sample data**.

### Types of Hypotheses

| Type | Symbol | Definition | Example |
|------|--------|-----------|---------|
| **Null Hypothesis** | H₀ | Statement of **no effect/no difference**; assumed true until evidence says otherwise | H₀: μ = 25 |
| **Alternative Hypothesis** | H₁ or Hₐ | Statement that **contradicts** H₀; what we want to prove | H₁: μ ≠ 25 |

### Tests of Hypothesis — Definition
A **test of hypothesis** is a **statistical procedure** that uses sample data to decide whether to **reject or fail to reject** the null hypothesis H₀.

### Steps in Hypothesis Testing

```
Step 1: State H₀ and H₁
Step 2: Choose significance level α (usually 0.01 or 0.05)
Step 3: Select appropriate test statistic (Z, t, χ², F)
Step 4: Determine critical region (rejection region)
Step 5: Compute the test statistic from sample data
Step 6: Make decision — Reject H₀ or Fail to Reject H₀
Step 7: State conclusion in context
```

### Types of Tests

| Test Type | H₁ Form | Rejection Region | Example |
|-----------|---------|-----------------|---------|
| **Two-tailed** | H₁: μ ≠ μ₀ | Both tails | Z < -Zα/2 or Z > Zα/2 |
| **Right-tailed** | H₁: μ > μ₀ | Right tail only | Z > Zα |
| **Left-tailed** | H₁: μ < μ₀ | Left tail only | Z < -Zα |

```
Diagram: Hypothesis Testing Process

State H₀, H₁  →  Choose α  →  Select Test  →  Compute Test  →  Decision
                                Statistic      Statistic
                                                   ↓
                                       ┌──────────┴──────────┐
                                       ↓                     ↓
                              |Z_calc| > Z_crit      |Z_calc| ≤ Z_crit
                              REJECT H₀               FAIL TO REJECT H₀
```

---

## C6-Q2) Differentiate Between Null and Alternative Hypothesis

| Parameter | Null Hypothesis (H₀) | Alternative Hypothesis (H₁) |
|-----------|----------------------|------------------------------|
| **Definition** | Statement of no effect, status quo | Statement of effect, research claim |
| **Symbol** | H₀ | H₁ or Hₐ |
| **Nature** | Conservative, default position | Challenger, what researcher wants to prove |
| **Contains** | Equality sign (=, ≤, ≥) | Inequality sign (≠, <, >) |
| **Assumed** | True until proven false | Accepted only if H₀ is rejected |
| **Burden of Proof** | On the researcher to disprove | Evidence must support it |
| **Example** | H₀: μ = 50 (no change) | H₁: μ ≠ 50 (there is a change) |
| **Error if wrong** | Type I error (rejecting true H₀) | Type II error (failing to reject false H₀) |
| **Decision** | Reject or Fail to Reject | Accept if H₀ rejected |
| **Analogy** | "Innocent until proven guilty" | "The accused is guilty" |

### Examples

| Scenario | H₀ | H₁ |
|----------|----|----|
| Drug effectiveness | Drug has no effect (μ = 0) | Drug has effect (μ ≠ 0) |
| Machine accuracy | Mean output = 500g | Mean output ≠ 500g |
| Exam scores | Average score = 60 | Average score > 60 |
| Bulb lifetime | Mean life = 25 months | Mean life ≠ 25 months |

---

## C6-Q3) Type I and Type II Error — Detailed Explanation

### Definitions

| Error | Definition | Probability | Also Called |
|-------|-----------|-------------|------------|
| **Type I Error (α)** | **Rejecting H₀ when H₀ is actually TRUE** | P(Reject H₀ \| H₀ true) = α | False Positive, Producer's risk |
| **Type II Error (β)** | **Failing to reject H₀ when H₀ is actually FALSE** | P(Fail to reject H₀ \| H₁ true) = β | False Negative, Consumer's risk |

### Decision Table (VERY IMPORTANT for Exam)

|  | **H₀ is TRUE** | **H₀ is FALSE** |
|--|----------------|-----------------|
| **Reject H₀** | ❌ **Type I Error (α)** | ✅ **Correct Decision** (Power = 1-β) |
| **Fail to Reject H₀** | ✅ **Correct Decision** (1-α) | ❌ **Type II Error (β)** |

### Key Concepts

| Concept | Definition | Formula |
|---------|-----------|---------|
| **Significance Level (α)** | Maximum probability of Type I error we are willing to accept | Usually α = 0.01 or 0.05 |
| **Power of Test** | Probability of correctly rejecting a false H₀ | Power = 1 - β |
| **Confidence Level** | Probability of correctly not rejecting a true H₀ | 1 - α |

### Relationship Between α and β

```
As α increases → β decreases (and vice versa)
They are INVERSELY related (for fixed sample size)

To reduce BOTH α and β simultaneously → Increase sample size n
```

### Real-World Examples

**Type I Error (False Positive):**
- Convicting an innocent person in court
- Fire alarm going off when there's no fire
- Concluding a drug works when it actually doesn't

**Type II Error (False Negative):**
- Acquitting a guilty person
- Fire alarm NOT going off during an actual fire
- Concluding a drug doesn't work when it actually does

```
Diagram: Type I and Type II Errors

        Reality
        ┌──────────┬───────────┐
        │  H₀ TRUE │ H₀ FALSE  │
Decision├──────────┼───────────┤
Reject  │ TYPE I   │ CORRECT   │
H₀      │ Error α  │ Power=1-β │
        ├──────────┼───────────┤
Don't   │ CORRECT  │ TYPE II   │
Reject  │ (1-α)    │ Error β   │
        └──────────┴───────────┘
```

> [!WARNING]
> **Common Exam Mistake:** Students confuse Type I and Type II. Remember: Type **I** = **I**ncorrectly rejecting truth. Type **II** = **II**ncorrectly accepting falsehood.

---

## C6-Q4) Neyman-Pearson Lemma

### Statement
The **Neyman-Pearson Lemma** provides the **most powerful test** for testing a **simple null hypothesis** against a **simple alternative hypothesis** at a given significance level α.

### Formal Statement
For testing H₀: θ = θ₀ vs H₁: θ = θ₁, the **most powerful test** of size α has a **critical region C** defined by:

$$\frac{L(\theta_1)}{L(\theta_0)} \geq k$$

where:
- L(θ₁) = Likelihood function under H₁
- L(θ₀) = Likelihood function under H₀
- k is chosen such that P(Reject H₀ | H₀ true) = α

### Key Points

| Point | Detail |
|-------|--------|
| **Applicability** | Only for simple vs simple hypothesis (both H₀ and H₁ are specific values) |
| **Result** | Gives the **most powerful** (MP) critical region |
| **Likelihood Ratio** | λ = L(θ₁)/L(θ₀) — reject H₀ when this ratio is large |
| **Interpretation** | Data is much more likely under H₁ than H₀ → reject H₀ |
| **Power** | Among all tests of size α, the NP test has the **highest power (1-β)** |
| **Uniqueness** | The MP test is essentially unique (except on sets of probability zero) |

### Significance
- Foundation of **modern hypothesis testing theory**
- Provides theoretical justification for likelihood ratio tests
- Guarantees **optimality** — no other test can do better at the same α level
- Extends to **Uniformly Most Powerful (UMP)** tests for composite hypotheses

---

## C6-Q5) Hypothesis Testing — Z-Test

### (a) Z-Test for Single Mean

**When to use:** Population σ is **known**, sample size is large (n ≥ 30), or population is normal.

**Hypotheses:**
- H₀: μ = μ₀
- H₁: μ ≠ μ₀ (two-tailed) OR μ > μ₀ OR μ < μ₀

**Test Statistic:**
$$Z_{calc} = \frac{\bar{X} - \mu_0}{\sigma / \sqrt{n}}$$

**Decision Rule:**
- Two-tailed: Reject H₀ if |Z_calc| > Z_{α/2}
- Right-tailed: Reject H₀ if Z_calc > Z_α
- Left-tailed: Reject H₀ if Z_calc < -Z_α

**Critical Values:**
| α | Two-tailed (Z_{α/2}) | One-tailed (Z_α) |
|---|----------------------|-------------------|
| 0.05 | ±1.96 | ±1.645 |
| 0.01 | ±2.576 | ±2.326 |

### (b) Z-Test for Difference of Two Means

**When to use:** Comparing means of two independent populations with known σ₁ and σ₂.

**Hypotheses:**
- H₀: μ₁ = μ₂ (or μ₁ - μ₂ = 0)
- H₁: μ₁ ≠ μ₂

**Test Statistic:**
$$Z_{calc} = \frac{(\bar{X}_1 - \bar{X}_2) - 0}{\sqrt{\frac{\sigma_1^2}{n_1} + \frac{\sigma_2^2}{n_2}}}$$

**Decision:** Same as single mean Z-test

---

## C6-Q6) Numerical: Bulb Manufacturer's Claim

**Given:**
- Claimed mean life: μ₀ = 25 months
- Population standard deviation: σ = 5 months
- Sample size: n = 6
- Sample values: 24, 26, 30, 20, 20, 18
- Significance level: α = 0.01 (1%)

### Step 1: State Hypotheses
```
H₀: μ = 25 (Manufacturer's claim is valid)
H₁: μ ≠ 25 (Manufacturer's claim is NOT valid)
```
This is a **two-tailed test**.

### Step 2: Compute Sample Mean

$$\bar{X} = \frac{24 + 26 + 30 + 20 + 20 + 18}{6} = \frac{138}{6} = 23$$

### Step 3: Compute Sample Standard Deviation

| Xᵢ | Xᵢ - X̄ | (Xᵢ - X̄)² |
|-----|---------|------------|
| 24 | 1 | 1 |
| 26 | 3 | 9 |
| 30 | 7 | 49 |
| 20 | -3 | 9 |
| 20 | -3 | 9 |
| 18 | -5 | 25 |
| **Σ** | **0** | **102** |

$$S = \sqrt{\frac{\sum(X_i - \bar{X})^2}{n-1}} = \sqrt{\frac{102}{5}} = \sqrt{20.4} = 4.517$$

### Step 4: Compute Test Statistic

Since $n = 6$ (small sample, $\sigma$ unknown), we use a one-sample **t-test**:

$$\begin{aligned}
t_{calc} &= \frac{\bar{X} - \mu_0}{S / \sqrt{n}} \\
&= \frac{23 - 25}{4.517 / \sqrt{6}} \\
&= \frac{-2}{1.844} = -1.085
\end{aligned}$$

### Step 5: Find Critical Value

- **Degrees of freedom (df):** $n - 1 = 6 - 1 = 5$
- **Significance level ($\alpha$):** 0.01, two-tailed.
- From Student's t-table, $t_{critical}$ at $df=5, \alpha=0.01$ is **$\pm 4.032$**.

### Step 6: Decision

$$\begin{aligned}
|t_{calc}| &= 1.085 \\
t_{critical} &= 4.032 \\
\text{Condition: } &|t_{calc}| < t_{critical}
\end{aligned}$$

$$\implies \text{FAIL TO REJECT } H_0$$

### Step 7: Conclusion

$$\boxed{\text{The manufacturer's claim is VALID at 1\% level of significance.}}$$

There is **not enough statistical evidence** to reject the claim that the mean bulb life is 25 months. This means the manufacturer's claim holds true based on the provided sample.

```
Diagram: t-Test Decision

          Rejection       Non-Rejection       Rejection
          Region           Region              Region
    ←─────────|═══════════════════════════|──────────→
           -4.032     t_calc = -1.085    +4.032
                     (falls in non-rejection region)
                     ∴ FAIL TO REJECT H₀ ✅
```

> [!IMPORTANT]
> **Exam Tips for Numericals:**
> 1. Always state H₀ and H₁ first
> 2. Show computation table for mean and SD
> 3. State formula before substituting values
> 4. Clearly compare |t_calc| with t_critical
> 5. Write conclusion in words, not just "Reject" or "Don't Reject"

---

# 📋 PART C: QUICK REVISION CHEAT SHEET

| Topic | Key Formula / Points |
|-------|---------------------|
| **Multiple Regression** | Ŷ = a + b₁X₁ + b₂X₂; Use 3 normal equations |
| **Partial Regression Coeff** | b₁₂.₃ = [(r₁₂ - r₁₃·r₂₃)/(1-r₂₃²)] × (σ₁/σ₂) |
| **Partial Correlation** | r₁₂.₃ = (r₁₂ - r₁₃·r₂₃)/√[(1-r₁₃²)(1-r₂₃²)] |
| **Multiple Correlation** | R₁.₂₃ = √[(r₁₂² + r₁₃² - 2r₁₂·r₁₃·r₂₃)/(1-r₂₃²)] |
| **Point Estimation** | Single value; Properties: Unbiased, Consistent, Efficient, Sufficient |
| **Interval Estimation** | X̄ ± Zα/2 · σ/√n |
| **Unbiased Estimator** | E(θ̂) = θ; X̄ is unbiased for μ; S² is unbiased for σ² |
| **MLE** | Maximize L(θ) = ∏f(xᵢ;θ); Take log, differentiate, set = 0 |
| **Hypothesis Testing** | State H₀/H₁ → Choose α → Compute test stat → Compare with critical → Decide |
| **Type I Error (α)** | Reject H₀ when H₀ is TRUE (False Positive) |
| **Type II Error (β)** | Fail to reject H₀ when H₀ is FALSE (False Negative) |
| **Power of Test** | 1 - β (ability to detect false H₀) |
| **Z-Test** | Z = (X̄ - μ₀)/(σ/√n); Use when σ known, n ≥ 30 |
| **t-Test** | t = (X̄ - μ₀)/(S/√n); Use when σ unknown, n < 30 |
| **Neyman-Pearson** | L(θ₁)/L(θ₀) ≥ k gives most powerful test |

---

> [!IMPORTANT]
> ### Last-Minute Exam Tips for MU PT-II (Quantitative Analysis):
> 1. **Multiple Regression numericals WILL come** — practice normal equations method thoroughly.
> 2. **Hypothesis Testing numerical is guaranteed** — know both Z-test and t-test conditions.
> 3. **Show computation tables** for EVERY numerical — examiners award significant step marks.
> 4. **Box your final answers** — makes them easy to find during rapid evaluation.
> 5. **State formulas BEFORE substituting** — earns formula marks even if the arithmetic is wrong.
> 6. **Draw diagrams** wherever possible — rejection regions, estimation types, and error tables.
> 7. **Time management**: 20 marks in 60 min = 3 min/mark. Don't spend >15 min on any single question.

---

*Prepared for: MU Sem 6 Quantitative Analysis (QA) PT-II | Computer Engineering | REV-2019 C-Scheme*
*Last Updated: April 5, 2026*
