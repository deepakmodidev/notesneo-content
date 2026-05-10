---
title: "Unit 2: Dimensionality Reduction"
description: "Dataset representation (vectors, matrices), data preprocessing (normalization, standardization, covariance), and PCA for dimensionality reduction."
author: "Deepak Modi"
date: "2026-05-10"
pdfUrl: ""
---

## Syllabus:

**Dimensionality Reduction:** Definition, Row vector and Column vector, how to represent a dataset, how to represent a dataset as a Matrix, Data preprocessing in Machine Learning: Feature Normalization, Mean of a data matrix, Column Standardization, Co-variance of a Data Matrix, Principal Component Analysis for Dimensionality reduction.

---

## 🎯 PYQ Analysis for Unit 2

> PYQs will be added after analysis — check back soon.

---

## **Section 1: Dimensionality Reduction**

### **1.1 What is Dimensionality?**

In Machine Learning, **dimensionality** refers to the **number of features (columns / attributes)** in a dataset.

**Example:**

A dataset of houses may have features:
- Size (sq ft), No. of Rooms, Location, Price, Age, Floor, Parking, Garden, ...

If there are **100 features**, we say the dataset has **100 dimensions**.

---

### **1.2 What is Dimensionality Reduction?**

**Definition:**

**Dimensionality Reduction** is the process of **reducing the number of features (dimensions)** in a dataset while **retaining as much important information as possible**.

Instead of working with 100 features, we may reduce to 10 features that capture most of the information.

**Simple Analogy:**

Imagine you have a 3D sculpture. To describe it to someone, you could draw a 2D shadow (projection) of it. The shadow is simpler but still represents the key shape of the object. Dimensionality reduction works the same way — it projects high-dimensional data into a lower dimension without losing the main structure.

---

### **1.3 Why is Dimensionality Reduction Needed?**

**The Curse of Dimensionality:**
- As features increase, the data becomes **sparse** in the high-dimensional space.
- ML models need **exponentially more data** to learn as dimensions grow.
- Beyond a certain point, adding more features **hurts model performance**.

**Problems with Too Many Dimensions:**
1. **Overfitting** — model memorizes training data, fails on new data.
2. **High Computation Cost** — more features = more memory and time.
3. **Irrelevant Features** — some features add noise, not signal.
4. **Visualization** — we can only visualize 2D or 3D data.
5. **Multicollinearity** — many features may be correlated (redundant).

**Benefits of Dimensionality Reduction:**

✅ Reduces training time.  
✅ Removes noise and redundant features.  
✅ Prevents overfitting.  
✅ Makes data easier to visualize.  
✅ Improves model accuracy in many cases.

**Two Main Approaches:**

| Approach | Technique | Description |
|----------|-----------|-------------|
| **Feature Selection** | Filter, Wrapper, Embedded | Select a subset of original features |
| **Feature Extraction** | PCA, LDA, Autoencoders | Create new (fewer) features from originals |

---

## **Section 2: Vectors and Dataset Representation**

### **2.1 Row Vector**

**Definition:**

A **Row Vector** is a matrix with **only one row** and **multiple columns**. It represents a single data point (one example/sample) with all its features.

**Notation:**

```
Row vector:  x = [x₁  x₂  x₃  ...  xₙ]

Shape: (1 × n)  → 1 row, n columns
```

**Example:**

One student's exam record:

```
x = [85  72  90  65  78]
     M1  M2  M3  M4  M5
```
Here, each value is a score in a subject — one row = one student.

---

### **2.2 Column Vector**

**Definition:**

A **Column Vector** is a matrix with **only one column** and **multiple rows**. It represents a single feature across all data points (all values of one attribute).

**Notation:**

```
Column vector:
        ┌ x₁ ┐
        │ x₂ │
   x =  │ x₃ │
        │ .. │
        └ xₙ ┘

Shape: (n × 1)  → n rows, 1 column
```

**Example:**

All students' scores in subject Math (M1):

```
     ┌ 85 ┐
     │ 72 │
x =  │ 90 │
     │ 65 │
     └ 78 ┘
```
Here, each value is one student's Math score — one column = one feature.

**Comparison:**

| | Row Vector | Column Vector |
|--|------------|---------------|
| **Shape** | 1 × n | n × 1 |
| **Represents** | One data point (sample) | One feature (attribute) |
| **Example** | [85, 72, 90] — one student | [85, 72, 65] — all students' math marks |

---

### **2.3 How to Represent a Dataset**

**A dataset is a collection of data points (examples / samples).**

For ML:
- Each **row** = one **data point** (one example / observation).
- Each **column** = one **feature** (attribute / variable).

**Example Dataset (5 students, 3 subjects):**

| Student | Math | Physics | Chemistry |
|---------|------|---------|-----------|
| S1 | 85 | 78 | 90 |
| S2 | 72 | 65 | 80 |
| S3 | 90 | 88 | 92 |
| S4 | 60 | 70 | 65 |
| S5 | 78 | 82 | 75 |

- **Rows (m = 5):** number of samples
- **Columns (n = 3):** number of features

---

### **2.4 How to Represent a Dataset as a Matrix**

The dataset is stored as a **2D matrix X** of shape **(m × n)**:
- **m** = number of rows (data points / samples)
- **n** = number of columns (features / dimensions)

**Matrix Notation:**

```
       Feature 1   Feature 2   Feature 3
           ↓           ↓           ↓
       ┌                               ┐
 S1 →  │  x₁₁       x₁₂       x₁₃   │
 S2 →  │  x₂₁       x₂₂       x₂₃   │
 S3 →  │  x₃₁       x₃₂       x₃₃   │
 S4 →  │  x₄₁       x₄₂       x₄₃   │
 S5 →  │  x₅₁       x₅₂       x₅₃   │
       └                               ┘

  X  =  m × n matrix
       (5 × 3 in this example)
```

**For the student example:**

```
        ┌ 85   78   90 ┐
        │ 72   65   80 │
   X =  │ 90   88   92 │
        │ 60   70   65 │
        └ 78   82   75 ┘

Shape: 5 × 3   (5 students, 3 features)
```

**How to access elements:**

- **xᵢⱼ** = element in row **i**, column **j**
- **x₁₂** = 78 (Student 1's Physics score)
- **x₃₁** = 90 (Student 3's Math score)

**Special Cases:**

| Case | Shape | Name |
|------|-------|------|
| m=1 | 1 × n | Row vector (one sample) |
| n=1 | m × 1 | Column vector (one feature) |
| m=n | n × n | Square matrix |

---

## **Section 3: Data Preprocessing in Machine Learning**

### **3.1 Why Preprocess Data?**

Real-world data is **raw, messy, and inconsistent**. Before feeding it to an ML algorithm, it must be cleaned and transformed. This is called **Data Preprocessing**.

**Problems in Raw Data:**
- Missing values
- Inconsistent formats
- Features on very different scales (e.g., age: 25, salary: 50000)
- Redundant features

**Preprocessing Steps Covered Here:**
1. Computing the Mean of a data matrix
2. Feature Normalization
3. Column Standardization
4. Computing the Covariance matrix

---

### **3.2 Mean of a Data Matrix**

**Definition:**

The **mean (average)** of a data matrix is calculated **column-wise** (per feature). It gives the average value of each feature across all data points.

**Formula:**

```
For feature j:
          m
         Σ  xᵢⱼ
μⱼ =    i=1
        ─────────
            m

Where:
  xᵢⱼ = value in row i, column j
  m   = number of data points (rows)
  μⱼ  = mean of feature j
```

**Example:**

Dataset (3 students, 2 features):

```
        ┌ 80   60 ┐
   X =  │ 90   70 │
        └ 70   80 ┘
```

**Calculate mean of each column:**

```
μ₁ (Math mean)    = (80 + 90 + 70) / 3 = 240 / 3 = 80

μ₂ (Physics mean) = (60 + 70 + 80) / 3 = 210 / 3 = 70
```

**Mean vector:**

```
μ = [80,  70]
```

**Use of Mean:**
- Used for centering data (subtracting mean from each value).
- Used in normalization, standardization, and PCA.

---

### **3.3 Feature Normalization**

**Definition:**

**Feature Normalization** (also called **Min-Max Scaling**) rescales each feature so that its values fall in the range **[0, 1]** (or sometimes [−1, 1]).

**Why needed?**

- If Math scores range from 0–100 and Age ranges from 18–25, the algorithm may give more weight to Math just because the values are larger.
- Normalization puts all features on the **same scale** so no feature dominates.

**Formula (Min-Max Normalization):**

```
         xᵢⱼ - min(xⱼ)
x'ᵢⱼ =  ─────────────────
         max(xⱼ) - min(xⱼ)

Where:
  xᵢⱼ     = original value
  min(xⱼ) = minimum value of feature j
  max(xⱼ) = maximum value of feature j
  x'ᵢⱼ    = normalized value (between 0 and 1)
```

**Example:**

Feature values (Math): [60, 70, 80, 90, 100]

```
min = 60,  max = 100

Normalize 60:  (60 - 60) / (100 - 60) = 0/40  = 0.00
Normalize 70:  (70 - 60) / (100 - 60) = 10/40 = 0.25
Normalize 80:  (80 - 60) / (100 - 60) = 20/40 = 0.50
Normalize 90:  (90 - 60) / (100 - 60) = 30/40 = 0.75
Normalize 100: (100 - 60)/ (100 - 60) = 40/40 = 1.00
```

**Result:** [0.00, 0.25, 0.50, 0.75, 1.00]

**Properties:**
- Output is always in [0, 1].
- Sensitive to outliers (extreme values distort the range).

---

### **3.4 Column Standardization (Z-Score Normalization)**

**Definition:**

**Column Standardization** (Z-Score Standardization) transforms each feature so that it has a **mean of 0** and a **standard deviation of 1**.

**Why used instead of normalization?**

- Normalization is sensitive to outliers.
- Standardization is more **robust** — it works well even when outliers are present.
- Required by many algorithms: PCA, SVM, KNN, Logistic Regression.

**Formulas:**

**Step 1 — Calculate Mean (μⱼ):**
```
         Σ xᵢⱼ
μⱼ =   ─────────
            m
```

**Step 2 — Calculate Standard Deviation (σⱼ):**
```
            ______________________
           /  1  m
σⱼ =     /  ─── Σ (xᵢⱼ - μⱼ)²
        \/    m  i=1
```

**Step 3 — Standardize:**
```
         xᵢⱼ - μⱼ
z'ᵢⱼ =  ──────────
            σⱼ
```

**Example:**

Feature (Math scores): [60, 70, 80, 90, 100]

```
Mean:  μ = (60+70+80+90+100) / 5 = 400 / 5 = 80

Variance:
  σ² = [(60-80)² + (70-80)² + (80-80)² + (90-80)² + (100-80)²] / 5
     = [400 + 100 + 0 + 100 + 400] / 5
     = 1000 / 5
     = 200

Std Dev:  σ = √200 ≈ 14.14

Standardize:
  z(60)  = (60 - 80)  / 14.14 = -20/14.14 ≈ -1.41
  z(70)  = (70 - 80)  / 14.14 = -10/14.14 ≈ -0.71
  z(80)  = (80 - 80)  / 14.14 =   0/14.14 =  0.00
  z(90)  = (90 - 80)  / 14.14 =  10/14.14 ≈ +0.71
  z(100) = (100 - 80) / 14.14 =  20/14.14 ≈ +1.41
```

**Result:** [-1.41, -0.71, 0.00, +0.71, +1.41]

**Properties:**
- Mean of standardized column = 0.
- Standard deviation of standardized column = 1.
- Values can be negative (unlike normalization).
- Robust to outliers.

**Normalization vs Standardization:**

| | Normalization | Standardization |
|--|---------------|-----------------|
| **Range** | [0, 1] | (-∞, +∞) |
| **Mean** | Not fixed | Always 0 |
| **Std Dev** | Not fixed | Always 1 |
| **Outlier Sensitivity** | High | Low |
| **Formula** | (x - min)/(max - min) | (x - μ)/σ |
| **Use When** | Features need bounded output | Features need mean=0, σ=1 |

---

### **3.5 Covariance of a Data Matrix**

**Definition:**

**Covariance** measures how much two features **change together**. It tells us the **relationship (direction)** between two variables.

**Interpretation:**

| Covariance | Meaning |
|------------|---------|
| **Positive** | Both features increase together |
| **Negative** | One increases, other decreases |
| **Zero** | No linear relationship between them |

**Formula (Covariance between feature j and feature k):**

```
           1   m
Cov(j,k) = ─── Σ  (xᵢⱼ - μⱼ)(xᵢₖ - μₖ)
           m  i=1

Where:
  xᵢⱼ = value of feature j in sample i
  μⱼ  = mean of feature j
  m   = number of samples
```

**Note:** Some formulas use (m-1) in the denominator for an unbiased estimate.

---

### **3.6 Covariance Matrix**

When a dataset has **n features**, the **Covariance Matrix** is an **n × n** matrix where element (j, k) is the covariance between feature j and feature k.

**Structure:**

```
           F1        F2        F3
        ┌                          ┐
  F1 →  │Cov(1,1) Cov(1,2) Cov(1,3)│
  F2 →  │Cov(2,1) Cov(2,2) Cov(2,3)│
  F3 →  │Cov(3,1) Cov(3,2) Cov(3,3)│
        └                          ┘

Diagonal elements: Cov(j,j) = Variance of feature j
Off-diagonal elements: Covariance between two different features
```

**Properties:**
- Covariance matrix is always **symmetric**: Cov(j,k) = Cov(k,j)
- Diagonal = **variance** of each feature
- Off-diagonal = **covariance** between pairs of features

---

### **3.7 Worked Example — Covariance Matrix**

**Dataset (3 samples, 2 features):**

```
        F1   F2
        ┌        ┐
  S1 →  │ 2    4 │
  S2 →  │ 4    6 │
  S3 →  │ 6    8 │
        └        ┘
```

**Step 1: Calculate means:**
```
μ₁ = (2 + 4 + 6) / 3 = 12/3 = 4
μ₂ = (4 + 6 + 8) / 3 = 18/3 = 6
```

**Step 2: Center the data (subtract mean):**
```
        F1-μ₁   F2-μ₂
  S1:   2-4=-2  4-6=-2
  S2:   4-4= 0  6-6= 0
  S3:   6-4=+2  8-6=+2
```

**Step 3: Calculate covariances:**
```
Cov(F1,F1) = [(-2)(-2) + (0)(0) + (2)(2)] / 3
           = [4 + 0 + 4] / 3 = 8/3 ≈ 2.67

Cov(F2,F2) = [(-2)(-2) + (0)(0) + (2)(2)] / 3
           = 8/3 ≈ 2.67

Cov(F1,F2) = [(-2)(-2) + (0)(0) + (2)(2)] / 3
           = [4 + 0 + 4] / 3 = 8/3 ≈ 2.67
```

**Covariance Matrix:**

```
        ┌ 2.67   2.67 ┐
  Σ =   └ 2.67   2.67 ┘
```

**Interpretation:** Cov(F1,F2) = 2.67 > 0 → F1 and F2 increase together (positive relationship).

---

## **Section 4: Principal Component Analysis (PCA)**

### **4.1 What is PCA?**

**Definition:**

**Principal Component Analysis (PCA)** is a **dimensionality reduction technique** that transforms the original features into a new set of features called **Principal Components** (PCs). These components:
- Are uncorrelated with each other.
- Are ordered so that the **first PC captures the most variance**, the second captures the next most, and so on.

The goal is to **keep the most informative components** and **discard the rest**, reducing dimensionality without losing much information.

**Simple Analogy:**

Imagine looking at a 3D object from different angles. From some angles, you see the object's full shape clearly. PCA finds the **best angle** to view the data so that as much information as possible is visible in fewer dimensions.

---

### **4.2 Key Concepts in PCA**

| Term | Meaning |
|------|---------|
| **Principal Components (PCs)** | New axes in the transformed space |
| **Eigenvectors** | Direction of each principal component |
| **Eigenvalues** | Amount of variance captured by each PC |
| **Variance** | How spread out the data is along a direction |
| **Explained Variance Ratio** | % of total variance captured by each PC |

---

### **4.3 Intuition Behind PCA**

**Why eigenvectors and eigenvalues?**

- **Eigenvectors** point in the directions of maximum variance in the data.
- **Eigenvalues** tell how much variance each eigenvector captures.
- The first eigenvector (PC1) captures the **most variance**.
- The second eigenvector (PC2) is **perpendicular** to PC1 and captures the next most.

**Diagram:**

```
  PC2 (less variance)
   ↑
   │         ● ●
   │       ●   ●
   │         ●   ●
   │       ●   ●
   └───────────────────→ PC1 (most variance)

Data is elongated along PC1.
If we keep only PC1, we preserve most information.
```

---

### **4.4 Steps of PCA**

**Step-by-Step Process:**

```
   ┌──────────────────────────────┐
   │ Step 1: Standardize the Data │
   └────────────┬─────────────────┘
                ▼
   ┌──────────────────────────────┐
   │ Step 2: Compute Covariance   │
   │         Matrix               │
   └────────────┬─────────────────┘
                ▼
   ┌──────────────────────────────┐
   │ Step 3: Compute Eigenvalues  │
   │         and Eigenvectors     │
   └────────────┬─────────────────┘
                ▼
   ┌──────────────────────────────┐
   │ Step 4: Sort by Eigenvalue   │
   │         (Descending)         │
   └────────────┬─────────────────┘
                ▼
   ┌──────────────────────────────┐
   │ Step 5: Select Top k         │
   │         Principal Components │
   └────────────┬─────────────────┘
                ▼
   ┌──────────────────────────────┐
   │ Step 6: Project Data onto    │
   │         New Feature Space    │
   └──────────────────────────────┘
```

---

### **4.5 Detailed Explanation of Each Step**

#### **Step 1: Standardize the Data**

- Apply **column standardization** (mean=0, σ=1) to all features.
- This ensures no feature dominates due to its scale.

```
         xᵢⱼ - μⱼ
z'ᵢⱼ =  ──────────
            σⱼ
```

---

#### **Step 2: Compute the Covariance Matrix**

- Calculate the **n × n covariance matrix** of the standardized data.

```
        1
Σ  =   ───  Xᵀ X     (after mean-centering)
        m
```

- Diagonal: variance of each feature.
- Off-diagonal: how features are correlated.

---

#### **Step 3: Compute Eigenvalues and Eigenvectors**

- Solve the **characteristic equation**:

```
det(Σ - λI) = 0

Where:
  λ = eigenvalue
  I = identity matrix
```

- For each eigenvalue λ, solve **(Σ - λI)v = 0** for eigenvector **v**.

- **Eigenvalue** → amount of variance the component explains.
- **Eigenvector** → direction of the component.

---

#### **Step 4: Sort by Eigenvalue (Descending)**

- Sort eigenvalues from **largest to smallest**.
- The corresponding eigenvectors are sorted in the same order.

```
λ₁ ≥ λ₂ ≥ λ₃ ≥ ... ≥ λₙ
↓    ↓    ↓
PC1  PC2  PC3  ...  (ordered by importance)
```

- **PC1** explains the most variance.
- **PC2** explains the second most, and so on.

---

#### **Step 5: Select Top k Principal Components**

- Decide how many components **k** to keep.
- Common rule: keep enough PCs to explain **≥ 95% of total variance**.

```
                   Σᵢ₌₁ᵏ λᵢ
Explained Variance = ────────── × 100%
                    Σᵢ₌₁ⁿ λᵢ
```

**Example:**

```
Eigenvalues: λ₁ = 5.0,  λ₂ = 3.0,  λ₃ = 1.5,  λ₄ = 0.5
Total = 10.0

PC1 explains: 5.0/10.0 = 50%
PC2 explains: 3.0/10.0 = 30%
PC1+PC2 combined: 80%
PC1+PC2+PC3: 95%

→ Keep 3 components to explain 95% of variance.
→ Reduce from 4 features to 3 features.
```

---

#### **Step 6: Project Data onto New Feature Space**

- Create a **projection matrix W** from the top k eigenvectors.
- Multiply the original data matrix by W:

```
Z  =  X  ×  W

Where:
  X = original data matrix (m × n)
  W = top k eigenvectors   (n × k)
  Z = projected data       (m × k)
```

- **Z** is the reduced dataset with only **k** dimensions.

---

### **4.6 PCA Example (Worked)**

**Dataset (4 samples, 2 features):**

```
   F1   F2
    2    4
    4    6
    6    8
    8   10
```

**Step 1: Standardize**
```
μ₁ = 5,  σ₁ ≈ 2.24
μ₂ = 7,  σ₂ ≈ 2.24

Standardized:
   z₁    z₂
  -1.34  -1.34
  -0.45  -0.45
   0.45   0.45
   1.34   1.34
```

**Step 2: Covariance Matrix**
```
       ┌ 1.0  1.0 ┐
  Σ =  └ 1.0  1.0 ┘
```

**Step 3: Eigenvalues**
```
det(Σ - λI) = 0
(1-λ)² - 1 = 0
λ² - 2λ = 0
λ(λ - 2) = 0
λ₁ = 2,  λ₂ = 0
```

**Step 4: Eigenvectors**
```
For λ₁ = 2:  v₁ = [1/√2, 1/√2] = [0.71, 0.71]
For λ₂ = 0:  v₂ = [1/√2,-1/√2] = [0.71,-0.71]
```

**Step 5: Select PC1 only (explains 100% of variance)**
```
W = [0.71, 0.71]ᵀ
```

**Step 6: Project**
```
Z = Standardized data × W

Z₁ = (-1.34)(0.71) + (-1.34)(0.71) = -1.90
Z₂ = (-0.45)(0.71) + (-0.45)(0.71) = -0.64
Z₃ = ( 0.45)(0.71) + ( 0.45)(0.71) =  0.64
Z₄ = ( 1.34)(0.71) + ( 1.34)(0.71) =  1.90

Reduced dataset: [-1.90, -0.64, 0.64, 1.90]
(2 features → 1 feature, no information lost here)
```

---

### **4.7 Advantages and Disadvantages of PCA**

**Advantages:**

✅ Reduces training time and memory.  
✅ Removes correlated (redundant) features.  
✅ Reduces overfitting.  
✅ Enables 2D/3D visualization of high-dimensional data.  
✅ Noise reduction (low-variance components often = noise).

**Disadvantages:**

❌ Principal components are **hard to interpret** (not original features).  
❌ Sensitive to **outliers** (which skew the covariance matrix).  
❌ Assumes **linear** relationships between features.  
❌ Requires **standardized** data (preprocessing needed).  
❌ Information is **lost** (how much depends on k chosen).

---

### **4.8 When to Use PCA**

- When you have **many features** (high-dimensional data).
- When many features are **correlated** with each other.
- When you want to **visualize** data in 2D or 3D.
- When training is **too slow** due to many features.
- When model is **overfitting** due to too many features.

---

## **Quick Revision Points**

### **Core Definitions:**
- **Dimensionality** = number of features in dataset.
- **Dimensionality Reduction** = reduce features while keeping information.
- **Row Vector** = 1 × n — represents one sample.
- **Column Vector** = n × 1 — represents one feature.
- **Dataset Matrix** = m × n — m samples, n features.

### **Preprocessing Formulas:**

| Technique | Formula | Output |
|-----------|---------|--------|
| **Mean** | μⱼ = Σxᵢⱼ / m | Average per feature |
| **Normalization** | (x - min) / (max - min) | [0, 1] |
| **Standardization** | (x - μ) / σ | Mean=0, σ=1 |
| **Covariance** | Cov(j,k) = Σ(xᵢⱼ-μⱼ)(xᵢₖ-μₖ)/m | Relationship strength |

### **PCA — 6 Steps:**
1. Standardize data
2. Compute covariance matrix
3. Compute eigenvalues & eigenvectors
4. Sort by eigenvalue (descending)
5. Select top k components
6. Project data onto new space

### **Key PCA Facts:**
- Eigenvector = direction of PC.
- Eigenvalue = variance explained by PC.
- PC1 = most variance, PC2 = second most, etc.
- PCs are always **perpendicular** (orthogonal) to each other.
- **Explained variance ratio** = λᵢ / Σλ × 100%.

---

## **Expected Exam Questions**

> PYQs will be added after analysis — check back soon.

---

_These notes were compiled by [Deepak Modi](https://deepakmodi.dev)_  
_Last updated: May 2026_
