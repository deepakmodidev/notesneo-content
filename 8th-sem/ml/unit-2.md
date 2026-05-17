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

### **High Priority Topics** (15 marks questions)

1. **PCA — Definition, Steps, Advantages & Disadvantages** — (2023: 15 marks, 2022: 15 marks)
2. **Data Preprocessing (Normalization, Mean, Standardization, Covariance)** — (2024: 15 marks)
3. **Dataset as a Matrix + Advantages of Matrix Representation** — (2024: 15 marks)
4. **Feature Extraction vs Feature Selection (Subset Selection)** — (2022: 15 marks)
5. **Dimensionality Reduction (Advantages & Disadvantages)** — (2023: 15 marks)

### **Medium Priority Topics** (Short answers)

1. **Dimensionality Reduction (Definition + Importance)** — 2024 (2.5 marks)
2. **Column Vector** — 2024 (2.5 marks)
3. **Dataset as a Matrix** — 2024 (2.5 marks)
4. **PCA — Dimensionality Reduction** — 2024 (2.5 marks)
5. **Two Data Preprocessing Techniques** — 2024 (2.5 marks)

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

> PYQ: What is Dimensionality reduction? (2023, 7.5 marks)  
> PYQ: Define Dimensionality Reduction and why it is important in Machine Learning? (2024, 2.5 marks)

**Definition:**

**Dimensionality Reduction** is the process of **reducing the number of features (dimensions)** in a dataset while **retaining as much important information as possible**.

Instead of working with 100 features, we may reduce to 10 features that capture most of the information.

**Simple Analogy:**

Imagine you have a 3D sculpture. To describe it to someone, you could draw a 2D shadow (projection) of it. The shadow is simpler but still represents the key shape of the object. Dimensionality reduction works the same way — it projects high-dimensional data into a lower dimension without losing the main structure.

---

### **1.3 Why is Dimensionality Reduction Needed?**

> PYQ: Write advantages and Disadvantages of Dimensionality Reduction. (2023, 7.5 marks)  
> PYQ: Compare Feature Extraction and Feature Selection techniques. Explain how dimensionality can be reduced using subset selection procedure. (2022, 15 marks)

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

#### **Advantages of Dimensionality Reduction**

> PYQ: Write advantages and Disadvantages of Dimensionality Reduction. (2023, 7.5 marks)

1. **Data Compression** — reduces storage space needed for the dataset.
2. **Less Computation Time** — fewer features = faster training.
3. **Removes Redundant Features** — drops correlated / duplicated columns.
4. **Improved Visualization** — high-dimensional data can be plotted in 2D / 3D for better understanding.
5. **Overfitting Prevention** — fewer features reduce model complexity and improve generalization.
6. **Feature Extraction** — pulls out the most informative features automatically (useful for downstream ML models).
7. **Data Preprocessing** — acts as a preprocessing step that improves the performance of the actual ML model.
8. **Improved Performance** — by reducing noise and irrelevant information, the model trains on cleaner signal.

#### **Disadvantages of Dimensionality Reduction**

1. **Information Loss** — some data is always lost when dimensions are reduced.
2. **Linear Correlations Only** — PCA finds only linear correlations between variables, which is sometimes undesirable.
3. **Mean/Covariance Insufficient** — PCA fails when mean and covariance are not enough to define the dataset.
4. **Choosing k is Hard** — we may not know how many principal components to retain; thumb rules are applied in practice.
5. **Interpretability** — reduced dimensions are not easily interpretable; relationship between original features and new features is hard to explain.
6. **Overfitting Risk** — in some cases dimensionality reduction itself can lead to overfitting, especially when the number of components is chosen based on the training data.
7. **Sensitivity to Outliers** — many techniques (like PCA) are sensitive to outliers, which can bias the representation.
8. **Computational Complexity** — some techniques (e.g., manifold learning) are computationally expensive on large datasets.

---

### **1.4 Feature Selection vs Feature Extraction**

> PYQ: Compare Feature Extraction and Feature Selection techniques. (2022, part of 15 marks)

Both techniques reduce dimensionality, but in **very different ways**.

| # | Feature Selection | Feature Extraction |
|--|---|---|
| 1 | Selects a **subset** of relevant features from the original set | Extracts a **new set** of features that are more informative and compact |
| 2 | Reduces the dimensionality of the feature space and simplifies the model | Captures essential information and represents it in a lower-dimensional feature space |
| 3 | Categorized into **Filter, Wrapper, Embedded** methods | Categorized into **Linear and Non-linear** methods |
| 4 | Requires **domain knowledge** and feature engineering | Can be applied to **raw data** without feature engineering |
| 5 | Improves **interpretability** and reduces overfitting | Improves **model performance** and handles non-linear relationships |
| 6 | May lose information if wrong features are selected | May introduce noise/redundancy if extracted features are not informative |

**Key takeaway:**
- **Feature Selection** = keeps original features (just throws some away).
- **Feature Extraction** = creates new features (e.g., principal components in PCA).

---

### **1.5 Subset Selection Procedure**

> PYQ: Explain how dimensionality can be reduced using subset selection procedure. (2022, part of 15 marks)

**What is Subset Selection?**

**Subset selection** (also called **feature selection**, **variable selection**, or **attribute selection**) is the process of selecting a **subset of relevant features** (variables, predictors) from the original set for use in model construction.

**Why use Subset Selection?**

1. **Simplification** of models — easier to interpret by researchers/users.
2. **Shorter training times** — fewer features = faster computation.
3. **Avoid the curse of dimensionality.**
4. **Enhanced generalization** — reduces overfitting by removing redundant/irrelevant features.

**Central premise:** The data contains many features that are either **redundant** or **irrelevant**, and can be removed without much loss of information.

**Two Main Approaches:**

1. **Forward Selection** — start empty, keep adding features.
2. **Backward Selection** — start with all, keep removing features.

---

#### **A. Forward Selection**

**Idea:** Start with **no features**, and add them **one at a time** — at each step, add the feature that decreases the validation error the most. Stop when no further addition improves performance.

**Notation:**
- **n** = number of input variables.
- **x₁, x₂, ..., xₙ** = input variables.
- **Fᵢ** = a subset of the set of input variables.
- **E(Fᵢ)** = error on the validation sample when only the inputs in Fᵢ are used.

**Algorithm:**

```
1. Set F₀ = ∅  and  E(F₀) = ∞

2. For i = 0, 1, 2, ..., repeat until E(Fᵢ₊₁) ≥ E(Fᵢ):

   (a) For each input variable xⱼ not in Fᵢ:
         Train the model with input variables Fᵢ ∪ {xⱼ}
         Calculate E(Fᵢ ∪ {xⱼ}) on the validation set.

   (b) Choose xₘ that causes the least error:
         m = arg min  E(Fᵢ ∪ {xⱼ})
                 j

   (c) Set Fᵢ₊₁ = Fᵢ ∪ {xₘ}.

3. The set Fᵢ is output as the best subset.
```

**Remarks:**

1. **Stopping criterion:** stop if adding any feature does **not** decrease the error E. You may stop earlier if the decrease is too small — a **user-defined threshold** based on application constraints.

2. **Complexity:** To reduce from **n** features to **k** features, we train and test the model:

```
n + (n-1) + (n-2) + ... + (n-k) times  =  O(n²)
```

So forward selection can be **expensive** for very high n.

---

#### **B. Backward Selection**

**Idea:** Start with **all features**, and remove them **one at a time** — at each step, remove the feature whose removal causes the **least increase** in error. Stop when removing any feature significantly increases the error.

**Algorithm:**

```
1. Set F₀ = {x₁, x₂, ..., xₙ}  and  E(F₀) = ∞

2. For i = 0, 1, 2, ..., repeat until E(Fᵢ₊₁) > E(Fᵢ):

   (a) For each input variable xⱼ in Fᵢ:
         Train the model with input variables Fᵢ − {xⱼ}
         Calculate E(Fᵢ − {xⱼ}) on the validation set.

   (b) Choose xₘ that causes the least error after removal:
         m = arg min  E(Fᵢ − {xⱼ})
                 j

   (c) Set Fᵢ₊₁ = Fᵢ − {xₘ}.

3. The set Fᵢ is output as the best subset.
```

---

#### **Forward vs Backward Selection — Comparison**

| Aspect | Forward Selection | Backward Selection |
|---|---|---|
| **Start** | Empty set ∅ | Full set {x₁, ..., xₙ} |
| **Operation** | Add features one by one | Remove features one by one |
| **Stops when** | Adding feature ≥ no improvement | Removing feature increases error |
| **Speed** | Faster when target subset is **small** | Faster when target subset is **large** |
| **Risk** | May miss good features that work in **combination** | More accurate, but slower for large n |
| **Best for** | When you suspect only few features matter | When you suspect most features matter |

**Both are O(n²)** in worst case but **forward is usually preferred** when the optimal subset size k is small (k ≪ n).

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

> PYQ: Explain column vector. (2024, 2.5 marks)

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

> PYQ: What is a dataset? Explain with a suitable example. (2024, part of 15 marks)

**Definition:**

A **dataset** is a **structured collection of data** used for analysis, training, and testing in machine learning. It typically consists of **rows** and **columns**, where:

- Each **row** represents a single **instance** or **data point** (one example / observation / sample).
- Each **column** represents a **feature** (also called an *attribute* or *variable*).
- Optionally, one column is the **label** (also called the *target variable*) — the value the model must predict.

**Example Dataset — Purchase Prediction:**

| Person | Age | Income | Purchased |
|---|---|---|---|
| A | 25 | 50k | No |
| B | 35 | 60k | Yes |
| C | 45 | 80k | Yes |
| D | 20 | 30k | No |

Here:
- **Features:** Age, Income
- **Label (target):** Purchased
- **Rows (m=4):** number of samples
- **Columns:** 2 features + 1 label

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

> PYQ: How do you represent a dataset as a Matrix? (2024, 2.5 marks)  
> PYQ: What is a dataset? Explain with a suitable example. Demonstrate how to represent a dataset as a Matrix. Discuss the advantages of matrix representation in Machine Learning. (2024, 15 marks)

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

### **2.5 Advantages of Matrix Representation in Machine Learning**

> PYQ: Discuss the advantages of matrix representation in Machine Learning. (2024, part of 15 marks)

Why do almost all ML algorithms internally represent the dataset as a matrix? Because it unlocks a set of powerful, fast operations from **linear algebra**.

**1. Efficient Computation**

Most ML algorithms (e.g. **Linear Regression**, **Logistic Regression**, **Neural Networks**) are built on top of **linear algebra**. Matrix representation enables **fast calculations** using highly optimized libraries (NumPy, BLAS, LAPACK).

**2. Scalability**

Matrix form can handle **very large datasets** efficiently using operations like **matrix multiplication** and **dot products** — far faster than per-element Python loops.

**3. Parallelization**

Matrix operations can be **parallelized easily** on multi-core CPUs and especially on **GPUs**. This is why deep learning frameworks (PyTorch, TensorFlow) push everything into matrix form — it makes training **orders of magnitude faster**.

**4. Vectorization**

Vectorized matrix code **avoids slow Python loops** by replacing them with single matrix operations. The result is **cleaner code** and **massively faster execution** — a core principle behind every modern ML library.

**5. Ease of Mathematical Transformation**

Common preprocessing steps — **feature scaling, normalization, standardization, PCA** — are all **defined as matrix operations**. Once data is in matrix form, applying any of these is just one line of math.

**6. Uniform Representation**

A matrix gives a **single, uniform structure** for any dataset — images, text embeddings, sensor logs, tabular records — they all become an `m × n` matrix that any algorithm can consume.

**7. Compatibility with Optimization Algorithms**

Optimization techniques like **gradient descent** rely on matrix calculus (Jacobians, Hessians). Matrix form is **mandatory** for these to work efficiently.

**Summary Table:**

| Advantage | Why It Matters in ML |
|---|---|
| Efficient computation | Fast linear-algebra-backed training |
| Scalability | Handles millions of rows / features |
| Parallelization | Runs on GPUs in parallel |
| Vectorization | Replaces loops with single ops |
| Easy transformations | Scaling, PCA, normalization in one line |
| Uniform representation | Works for any data type |
| Optimization-friendly | Required by gradient descent and friends |

---

## **Section 3: Data Preprocessing in Machine Learning**

> PYQ: Discuss two techniques used in Data preprocessing Machine Learning. (2024, 2.5 marks)  
> PYQ: Describe the process of Data preprocessing in Machine Learning, focusing on Feature Normalization, Mean calculation, column standardization, and Covariance estimation. (2024, 15 marks)

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

> PYQ: Explain PCA with its advantages and disadvantages. (2022, 15 marks)  
> PYQ: What is PCA? Write down steps of a PCA algorithm with example. (2023, 15 marks)  
> PYQ: What is PCA, and how does it help with dimensionality reduction? (2024, 2.5 marks)

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

### **15-Mark Questions:**

1. Explain PCA with its advantages and disadvantages. *(2022)*
2. Compare Feature Extraction and Feature Selection techniques. Explain how dimensionality can be reduced using subset selection procedure. *(2022)*
3. What is PCA? Write down steps of a PCA algorithm with example. *(2023)*
4. (a) What is Dimensionality reduction? (b) Write advantages and disadvantages of Dimensionality Reduction. *(2023)*
5. What is a dataset? Explain with a suitable example. Demonstrate how to represent a dataset as a Matrix. Discuss the advantages of matrix representation in Machine Learning. *(2024)*
6. Describe the process of Data preprocessing in Machine Learning, focusing on Feature Normalization, Mean calculation, column standardization, and Covariance estimation. *(2024)*

### **Short Answer Questions (2.5 marks):**

1. Define Dimensionality Reduction and why it is important in Machine Learning. *(2024)*
2. Explain column vector. *(2024)*
3. How do you represent a dataset as a Matrix? *(2024)*
4. Discuss two techniques used in Data preprocessing Machine Learning. *(2024)*
5. What is PCA, and how does it help with dimensionality reduction? *(2024)*

---

_These notes were compiled by [Deepak Modi](https://deepakmodi.dev)_  
_Last updated: May 2026_
