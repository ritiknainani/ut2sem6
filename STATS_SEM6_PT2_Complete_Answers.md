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

```
X₂ - X̄₂ = b₂₁.₃ (X₁ - X̄₁) + b₂₃.₁ (X₃ - X̄₃)
```

### Step 1: Calculate Partial Regression Coefficients

**Formula for b₂₁.₃:**

```
                r₁₂ - r₂₃ × r₁₃       σ₂
b₂₁.₃  =  ────────────────────── × ────
                1 - r₁₃²               σ₁
```

**Substituting:**

```
         0.8 - (0.6 × 0.7)       8
b₂₁.₃ = ──────────────────── × ────
           1 - (0.7)²            10

         0.8 - 0.42
       = ──────────── × 0.8
          1 - 0.49

         0.38
       = ────── × 0.8
         0.51

       = 0.7451 × 0.8

       = 0.596  ✅ (matches hint)
```

**Formula for b₂₃.₁:**

```
                r₂₃ - r₁₂ × r₁₃       σ₂
b₂₃.₁  =  ────────────────────── × ────
                1 - r₁₃²               σ₃
```

**Substituting:**

```
         0.6 - (0.8 × 0.7)       8
b₂₃.₁ = ──────────────────── × ────
           1 - (0.7)²             5

         0.6 - 0.56
       = ──────────── × 1.6
          1 - 0.49

         0.04
       = ────── × 1.6
         0.51

       = 0.07843 × 1.6

       = 0.125  ✅ (matches hint)
```

### Step 2: Write the Regression Equation

```
┌─────────────────────────────────────────────────────────────────┐
│  X₂ - X̄₂ = 0.596 (X₁ - X̄₁) + 0.125 (X₃ - X̄₃)              │
└─────────────────────────────────────────────────────────────────┘
```

### Interpretation
- A unit ↑ in X₁ (keeping X₃ constant) → X₂ increases by **0.596**
- A unit ↑ in X₃ (keeping X₁ constant) → X₂ increases by **0.125**
- X₁ has a **significantly stronger influence** on X₂ than X₃

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
X̄₁ = 20/4 = 5,   X̄₂ = 24/4 = 6,   X̄₃ = 28/4 = 7
```

### Step 3: Normal Equations for X₁ = a + b₁X₂ + b₂X₃

The three normal equations are:
```
ΣX₁   = na + b₁(ΣX₂) + b₂(ΣX₃)
ΣX₁X₂ = a(ΣX₂) + b₁(ΣX₂²) + b₂(ΣX₂X₃)
ΣX₁X₃ = a(ΣX₃) + b₁(ΣX₂X₃) + b₂(ΣX₃²)
```

Substituting values:
```
20  = 4a  + 24b₁  + 28b₂       ... (i)
140 = 24a + 164b₁ + 188b₂      ... (ii)
160 = 28a + 188b₁ + 216b₂      ... (iii)
```

### Step 4: Solve the System

From equation (i):
```
a = (20 - 24b₁ - 28b₂) / 4 = 5 - 6b₁ - 7b₂
```

**Note:** In this dataset, X₁, X₂, X₃ are in perfect linear relationship: X₁ = X₂ - 1 = X₃ - 2

Substituting a = 5 - 6b₁ - 7b₂ into (ii) and (iii) and solving simultaneously:

After solving: **b₁ = 1, b₂ = 0, a = -1**

```
┌──────────────────────────────────────────┐
│  X₁ = -1 + 1 × X₂ + 0 × X₃ = X₂ - 1   │
└──────────────────────────────────────────┘
```

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
Ȳ = 54/6 = 9,   X̄₁ = 48/6 = 8,   X̄₂ = 102/6 = 17
```

### Step 3: Normal Equations for Ŷ = a + b₁X₁ + b₂X₂

```
ΣY   = na + b₁(ΣX₁) + b₂(ΣX₂)
ΣYX₁ = a(ΣX₁) + b₁(ΣX₁²) + b₂(ΣX₁X₂)
ΣYX₂ = a(ΣX₂) + b₁(ΣX₁X₂) + b₂(ΣX₂²)
```

Substituting:
```
54  = 6a   + 48b₁   + 102b₂       ... (i)
339 = 48a  + 494b₁  + 1034b₂      ... (ii)
720 = 102a + 1034b₁ + 2188b₂      ... (iii)
```

### Step 4: Solve

From (i): **a = 9 - 8b₁ - 17b₂**

Substituting into (ii):
```
339 = 48(9 - 8b₁ - 17b₂) + 494b₁ + 1034b₂
339 = 432 - 384b₁ - 816b₂ + 494b₁ + 1034b₂
339 = 432 + 110b₁ + 218b₂

∴ 110b₁ + 218b₂ = -93        ... (iv)
```

Substituting into (iii):
```
720 = 102(9 - 8b₁ - 17b₂) + 1034b₁ + 2188b₂
720 = 918 - 816b₁ - 1734b₂ + 1034b₁ + 2188b₂
720 = 918 + 218b₁ + 454b₂

∴ 218b₁ + 454b₂ = -198       ... (v)
```

From (iv): b₁ = (-93 - 218b₂) / 110

Substituting into (v):
```
218 × (-93 - 218b₂)/110 + 454b₂ = -198

(-20274 - 47524b₂) / 110 + 454b₂ = -198

Multiply everything by 110:
-20274 - 47524b₂ + 49940b₂ = -21780

2416b₂ = -21780 + 20274 = -1506

b₂ = -1506 / 2416 = -0.6233
```

```
b₁ = (-93 - 218 × (-0.6233)) / 110
   = (-93 + 135.88) / 110
   = 42.88 / 110
   = 0.3898
```

Calculating a:
```
a = 9 - 8(0.3898) - 17(-0.6233)
  = 9 - 3.118 + 10.596
  = 16.478
```

```
┌─────────────────────────────────────────────────┐
│  Ŷ = 16.478 + 0.390 × X₁ - 0.623 × X₂         │
└─────────────────────────────────────────────────┘
```

> [!IMPORTANT]
> In exam: Always show (1) Computation table, (2) Normal equations, (3) Substitution steps, (4) Final boxed equation. Each step fetches marks.

---

## M4-Q4) Partial Correlation Coefficients

**Given:** r₁₂ = 0.7, r₁₃ = 0.61, r₂₃ = 0.4

### Formulas:

```
            r₂₃ - r₁₂ × r₁₃
r₂₃.₁ = ─────────────────────────────
         √[(1 - r₁₂²)(1 - r₁₃²)]

            r₁₃ - r₁₂ × r₂₃
r₁₃.₂ = ─────────────────────────────
         √[(1 - r₁₂²)(1 - r₂₃²)]

            r₁₂ - r₁₃ × r₂₃
r₁₂.₃ = ─────────────────────────────
         √[(1 - r₁₃²)(1 - r₂₃²)]
```

### Calculations:

**i) r₂₃.₁ (Correlation between X₂ and X₃, removing effect of X₁):**
```
         0.4 - (0.7 × 0.61)
r₂₃.₁ = ─────────────────────────────
         √[(1 - 0.49)(1 - 0.3721)]

         0.4 - 0.427
       = ──────────────────
         √[0.51 × 0.6279]

         -0.027
       = ────────
         √0.3202

         -0.027
       = ────────
          0.5659

       = -0.0477
```
```
┌─────────────────────────┐
│  r₂₃.₁ = -0.0477       │
└─────────────────────────┘
```

**ii) r₁₃.₂ (Correlation between X₁ and X₃, removing effect of X₂):**
```
         0.61 - (0.7 × 0.4)
r₁₃.₂ = ─────────────────────────────
         √[(1 - 0.49)(1 - 0.16)]

         0.61 - 0.28
       = ──────────────────
         √[0.51 × 0.84]

         0.33
       = ────────
         √0.4284

         0.33
       = ────────
         0.6545

       = 0.5042
```
```
┌─────────────────────────┐
│  r₁₃.₂ = 0.5042        │
└─────────────────────────┘
```

**iii) r₁₂.₃ (Correlation between X₁ and X₂, removing effect of X₃):**
```
         0.7 - (0.61 × 0.4)
r₁₂.₃ = ─────────────────────────────
         √[(1 - 0.3721)(1 - 0.16)]

         0.7 - 0.244
       = ──────────────────
         √[0.6279 × 0.84]

         0.456
       = ────────
         √0.5274

         0.456
       = ────────
         0.7262

       = 0.6280
```
```
┌─────────────────────────┐
│  r₁₂.₃ = 0.6280        │
└─────────────────────────┘
```

### Interpretation
- r₂₃.₁ ≈ -0.048 → Almost **no correlation** between X₂ and X₃ when X₁ is held constant
- r₁₃.₂ ≈ 0.504 → **Moderate positive** correlation between X₁ and X₃ when X₂ is held constant
- r₁₂.₃ ≈ 0.628 → **Strong positive** correlation between X₁ and X₂ when X₃ is held constant

---

## M4-Q5) Definitions — Regression & Correlation Terms

### (a) Partial Regression Coefficient

**Definition:** The partial regression coefficient **b₁₂.₃** measures the **change in X₁ per unit change in X₂**, while **keeping X₃ constant**.

**Formula:**
```
            r₁₂ - r₁₃ × r₂₃       σ₁
b₁₂.₃ = ────────────────────── × ────
             1 - r₂₃²              σ₂
```

**Key Points:**
- Measures the **net effect** of one independent variable on the dependent variable
- Removes (controls for) the effect of other variables
- Can be positive or negative
- **Range:** -∞ to +∞

### (b) Partial Correlation Coefficient

**Definition:** The partial correlation coefficient **r₁₂.₃** measures the **linear relationship between X₁ and X₂** after **removing (controlling for) the effect of X₃**.

**Formula:**
```
            r₁₂ - r₁₃ × r₂₃
r₁₂.₃ = ─────────────────────────────
         √[(1 - r₁₃²)(1 - r₂₃²)]
```

**Key Points:**
- Measures **net correlation** between two variables after eliminating effect of others
- **Range:** -1 ≤ r₁₂.₃ ≤ +1
- If r₁₂.₃ = 0, X₁ and X₂ are uncorrelated after removing X₃'s effect
- **Higher order:** r₁₂.₃₄ removes effect of both X₃ and X₄

### (c) Multiple Correlation Coefficient

**Definition:** The multiple correlation coefficient **R₁.₂₃** measures the **strength of linear relationship** between one dependent variable (X₁) and **two or more independent variables** (X₂, X₃) **simultaneously**.

**Formula:**
```
              ┌─────────────────────────────────────┐
              │  r₁₂² + r₁₃² - 2×r₁₂×r₁₃×r₂₃     │
R₁.₂₃ = √   │ ─────────────────────────────────── │
              │           1 - r₂₃²                  │
              └─────────────────────────────────────┘
```

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

```
X̄ = ΣXᵢ / n = (6 + 10 + 13 + 14 + 18 + 20) / 6 = 81 / 6 = 13.5
```
```
┌──────────────────┐
│  X̄ = 13.5        │
└──────────────────┘
```

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

```
s = √[ Σ(Xᵢ - X̄)² / (n-1) ]
  = √[ 131.50 / 5 ]
  = √26.3
  = 5.128
```
```
┌──────────────────┐
│  s = 5.128       │
└──────────────────┘
```

> [!NOTE]
> We use (n-1) in denominator for **unbiased** estimate of population variance. If asked for population SD directly, some use n in denominator: σ̂ = √(131.50/6) = √21.917 = 4.682

### (3) Standard Error of Mean

**Formula:**
```
SE(X̄) = s / √n
```

**Substituting:**
```
SE(X̄) = 5.128 / √6 = 5.128 / 2.449 = 2.094
```
```
┌──────────────────────┐
│  SE(X̄) = 2.094       │
└──────────────────────┘
```

**Interpretation:** The sample mean of 13.5 is expected to deviate from the true population mean by approximately ±2.094 units.

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
```
X̄ - Z(α/2) × (σ/√n)  ≤  μ  ≤  X̄ + Z(α/2) × (σ/√n)
```

### Comparison Table

| Parameter | Point Estimation | Interval Estimation |
|-----------|-----------------|-------------------|
| **Output** | Single value | Range of values |
| **Precision** | No measure of precision | Confidence level given |
| **Formula** | X̄, S², p̂ | X̄ ± Z(α/2) × σ/√n |
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
Prove that **E(X̄) = μ**, i.e., the expected value of the sample mean equals the population mean.

### Proof

**Let** X₁, X₂, ..., Xₙ be a random sample from a population with mean μ and variance σ².

**Step 1:** Define the sample mean:
```
X̄ = (1/n) × Σ Xᵢ  (i = 1 to n)
```

**Step 2:** Take expectation on both sides:
```
E(X̄) = E[ (1/n) × Σ Xᵢ ]
```

**Step 3:** Use linearity of expectation (E of sum = sum of E):
```
E(X̄) = (1/n) × Σ E(Xᵢ)
```

**Step 4:** Since each Xᵢ comes from the same population, E(Xᵢ) = μ for all i:
```
E(X̄) = (1/n) × (μ + μ + ... + μ)    [n times]
      = (1/n) × nμ
      = μ
```

### Conclusion
```
┌──────────────────────┐
│  E(X̄) = μ            │
│                      │
│  ∴ X̄ is UNBIASED     │
│  estimator of μ      │
└──────────────────────┘
```

**Consistency Check:** Since Var(X̄) = σ²/n → 0 as n → ∞, X̄ is also a **consistent** estimator.

---

## C5-Q4) Point Estimation — Definition and Properties

### Definition
**Point Estimation** is a method of using a **single value** computed from sample data (a **statistic**) to estimate the value of an unknown **population parameter**.

- The statistic used is called the **estimator** (e.g., X̄)
- The computed value is called the **estimate** (e.g., X̄ = 13.5)

### Properties of a Good Point Estimator

| # | Property | Definition | Mathematical Condition |
|---|----------|-----------|----------------------|
| 1 | **Unbiasedness** | Expected value of estimator = parameter | E(θ̂) = θ |
| 2 | **Consistency** | As n → ∞, estimator converges to true value | P(\|θ̂ - θ\| > ε) → 0 as n → ∞ |
| 3 | **Efficiency** | Has **minimum variance** among all unbiased estimators | Var(θ̂) ≤ Var(θ̃) for all unbiased θ̃ |
| 4 | **Sufficiency** | Uses **all information** in the sample about θ | P(X\|T) doesn't depend on θ |
| 5 | **Min. Variance** | Smallest variance among unbiased estimators (MVUE) | Achieves Cramér-Rao Lower Bound |

### Detailed Explanation with Examples

**1. Unbiasedness:**
- X̄ is unbiased for μ because E(X̄) = μ
- S² = Σ(Xᵢ-X̄)²/(n-1) is unbiased for σ² because E(S²) = σ²
- **BUT:** S is BIASED for σ → E(S) ≠ σ

**2. Consistency:**
- X̄ is consistent because Var(X̄) = σ²/n → 0 as n → ∞
- By Chebyshev's inequality: P(|X̄ - μ| > ε) ≤ σ²/(nε²) → 0

**3. Efficiency:**
- Among all unbiased estimators of μ:
  - X̄ has minimum variance = σ²/n
  - Median has higher variance = πσ²/(2n)
  - ∴ X̄ is more efficient than Median
  - Relative Efficiency = Var(Median)/Var(X̄) = π/2 ≈ 1.57

**4. Sufficiency:**
- For Normal distribution: X̄ is sufficient for μ
- It captures ALL information about μ from the sample

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

| Step | Action |
|------|--------|
| **Step 1** | Write the **likelihood function**: L(θ) = ∏ f(xᵢ; θ) |
| **Step 2** | Take the **log-likelihood**: ln L(θ) = Σ ln f(xᵢ; θ) |
| **Step 3** | **Differentiate** w.r.t. θ and set = 0: d(ln L)/dθ = 0 |
| **Step 4** | **Solve** for θ̂ (the MLE) |
| **Step 5** | Verify it's a **maximum** (second derivative < 0) |

### Example: MLE for Normal Distribution Mean

**Given:** X₁, X₂, ..., Xₙ ~ N(μ, σ²), find MLE of μ

**Step 1:** Likelihood function:
```
L(μ) = ∏ (1/√(2π)σ) × exp[-(xᵢ - μ)² / (2σ²)]
       i=1 to n
```

**Step 2:** Log-likelihood:
```
ln L(μ) = -(n/2) ln(2π) - n ln(σ) - (1/2σ²) × Σ(xᵢ - μ)²
```

**Step 3:** Differentiate w.r.t. μ and set to zero:
```
∂(ln L)/∂μ = (1/σ²) × Σ(xᵢ - μ) = 0
```

**Step 4:** Solve:
```
Σxᵢ - nμ = 0

μ̂ = Σxᵢ / n = X̄
```

```
┌──────────────────────┐
│  μ̂(MLE) = X̄          │
└──────────────────────┘
```

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
Show that **E(S²) = σ²** where S² = Σ(Xᵢ - X̄)² / (n-1)

### Proof

**Step 1:** Expand the sum of squares:
```
Σ(Xᵢ - X̄)² = ΣXᵢ² - nX̄²
```

**Step 2:** Take Expectation:
```
E[Σ(Xᵢ - X̄)²] = Σ E(Xᵢ²) - n × E(X̄²)
```

**Step 3:** Use the identity: E(X²) = Var(X) + [E(X)]²
```
E(Xᵢ²) = Var(Xᵢ) + [E(Xᵢ)]² = σ² + μ²

E(X̄²) = Var(X̄) + [E(X̄)]² = σ²/n + μ²
```

**Step 4:** Substitute:
```
E[Σ(Xᵢ - X̄)²] = n(σ² + μ²) - n(σ²/n + μ²)
                = nσ² + nμ² - σ² - nμ²
                = nσ² - σ²
                = (n-1)σ²
```

**Step 5:** Therefore:
```
E[S²] = E[ Σ(Xᵢ - X̄)² / (n-1) ]
      = (n-1)σ² / (n-1)
      = σ²
```

### Conclusion
```
┌──────────────────────────┐
│  E(S²) = σ²              │
│                          │
│  ∴ S² is UNBIASED        │
│  estimator of σ²         │
└──────────────────────────┘
```

> [!IMPORTANT]
> **Why (n-1) and not n?** If we divided by n, the expectation would be:
> E[Σ(Xᵢ-X̄)²/n] = (n-1)σ²/n ≠ σ² → This is BIASED (underestimates σ²).
> Dividing by (n-1) is called **Bessel's correction** and removes this bias.

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
| **Two-tailed** | H₁: μ ≠ μ₀ | Both tails | Z < -Z(α/2) or Z > Z(α/2) |
| **Right-tailed** | H₁: μ > μ₀ | Right tail only | Z > Z(α) |
| **Left-tailed** | H₁: μ < μ₀ | Left tail only | Z < -Z(α) |

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
| **Significance Level (α)** | Maximum probability of Type I error we allow | Usually α = 0.01 or 0.05 |
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
> **Common Exam Mistake:** Students confuse Type I and Type II. Remember:
> - Type **I** = **I**ncorrectly rejecting truth (False Positive)
> - Type **II** = **II**ncorrectly accepting falsehood (False Negative)

---

## C6-Q4) Neyman-Pearson Lemma

### Statement
The **Neyman-Pearson Lemma** provides the **most powerful test** for testing a **simple null hypothesis** against a **simple alternative hypothesis** at a given significance level α.

### Formal Statement
For testing H₀: θ = θ₀ vs H₁: θ = θ₁, the **most powerful test** of size α has a **critical region C** defined by:

```
L(θ₁)
────── ≥ k
L(θ₀)
```

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
```
         X̄ - μ₀
Z_calc = ─────────
          σ / √n
```

**Decision Rule:**
- Two-tailed: Reject H₀ if |Z_calc| > Z(α/2)
- Right-tailed: Reject H₀ if Z_calc > Z(α)
- Left-tailed: Reject H₀ if Z_calc < -Z(α)

**Critical Values:**
| α | Two-tailed Z(α/2) | One-tailed Z(α) |
|---|---------------------|-----------------|
| 0.05 | ±1.96 | ±1.645 |
| 0.01 | ±2.576 | ±2.326 |

### (b) Z-Test for Difference of Two Means

**When to use:** Comparing means of two independent populations with known σ₁ and σ₂.

**Hypotheses:**
- H₀: μ₁ = μ₂ (or μ₁ - μ₂ = 0)
- H₁: μ₁ ≠ μ₂

**Test Statistic:**
```
            (X̄₁ - X̄₂) - 0
Z_calc = ─────────────────────
          √(σ₁²/n₁ + σ₂²/n₂)
```

**Decision:** Same as single mean Z-test

---

## C6-Q6) Numerical: Bulb Manufacturer's Claim

**Given:**
- Claimed mean life: μ₀ = 25 months
- Population standard deviation: σ = 5 months
- Sample size: n = 6
- Sample values: 24, 26, 30, 20, 20, 18
- Significance level: α = 0.01 (1%)
- Table values: t(0.01) = 4.032 (df=5), 3.707 (df=6), 3.499 (df=7)

### Step 1: State Hypotheses
```
H₀: μ = 25   (Manufacturer's claim is valid)
H₁: μ ≠ 25   (Manufacturer's claim is NOT valid)

This is a TWO-TAILED test.
```

### Step 2: Compute Sample Mean

```
X̄ = (24 + 26 + 30 + 20 + 20 + 18) / 6 = 138 / 6 = 23
```

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

```
S = √[ Σ(Xᵢ - X̄)² / (n-1) ] = √(102/5) = √20.4 = 4.517
```

### Step 4: Compute Test Statistic

Since n = 6 (small sample, σ unknown), we use a one-sample **t-test**:

```
              X̄ - μ₀       23 - 25       -2        -2
t_calc =  ───────── = ──────────── = ────────── = ───── = -1.085
            S / √n     4.517 / √6    4.517/2.449   1.844
```

### Step 5: Find Critical Value

```
Degrees of freedom (df) = n - 1 = 6 - 1 = 5
α = 0.01, two-tailed test
t_critical at df = 5, α = 0.01 (two-tailed) = ±4.032
```

### Step 6: Decision

```
|t_calc|   = |-1.085| = 1.085
t_critical = 4.032

Since |t_calc| (1.085) < t_critical (4.032)

→ We FAIL TO REJECT H₀
```

### Step 7: Conclusion

```
┌──────────────────────────────────────────────────────────────────┐
│  The manufacturer's claim is VALID at 1% level of significance. │
│                                                                  │
│  There is NOT enough statistical evidence to reject the claim    │
│  that the mean bulb life is 25 months.                          │
└──────────────────────────────────────────────────────────────────┘
```

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
| **Partial Regression Coeff** | b₁₂.₃ = [(r₁₂ - r₁₃×r₂₃)/(1-r₂₃²)] × (σ₁/σ₂) |
| **Partial Correlation** | r₁₂.₃ = (r₁₂ - r₁₃×r₂₃) / √[(1-r₁₃²)(1-r₂₃²)] |
| **Multiple Correlation** | R₁.₂₃ = √[(r₁₂² + r₁₃² - 2r₁₂×r₁₃×r₂₃) / (1-r₂₃²)] |
| **Point Estimation** | Single value; Properties: Unbiased, Consistent, Efficient, Sufficient |
| **Interval Estimation** | X̄ ± Z(α/2) × σ/√n |
| **Unbiased Estimator** | E(θ̂) = θ; X̄ is unbiased for μ; S² is unbiased for σ² |
| **MLE** | Maximize L(θ) = ∏f(xᵢ;θ); Take log, differentiate, set = 0 |
| **Hypothesis Testing** | State H₀/H₁ → Choose α → Compute test stat → Compare with critical → Decide |
| **Type I Error (α)** | Reject H₀ when H₀ is TRUE (False Positive) |
| **Type II Error (β)** | Fail to reject H₀ when H₀ is FALSE (False Negative) |
| **Power of Test** | 1 - β (ability to detect false H₀) |
| **Z-Test** | Z = (X̄ - μ₀) / (σ/√n); Use when σ known, n ≥ 30 |
| **t-Test** | t = (X̄ - μ₀) / (S/√n); Use when σ unknown, n < 30 |
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
*Last Updated: April 6, 2026*
