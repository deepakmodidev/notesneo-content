---
title: "Unit 4: Unsupervised Learning & Evaluation"
description: "K-Means Clustering, Ensemble Methods (Boosting, Bagging, Random Forests), and model evaluation metrics — accuracy, confusion matrix, precision, recall, F1, ROC-AUC, MAD."
author: "Deepak Modi"
date: "2026-05-10"
pdfUrl: ""
---

## Syllabus:

**Unsupervised Learning:** Clustering: K-means. Ensemble Methods: Boosting, Bagging, Random Forests. Evaluation: Performance measurement of models in terms of accuracy, confusion matrix, precision & recall, F1-score, Receiver Operating Characteristic (ROC) curve and AUC, Median Absolute Deviation (MAD), Distribution of errors.

---

## 🎯 PYQ Analysis for Unit 4

### **High Priority Topics** (15 marks questions)

1. **Bagging vs Boosting vs Random Forest** — (2024: 15 marks, 2023: 15 marks)
2. **ROC and AUC** — (2024: 15 marks, 2023: 7.5 marks, 2022: 7.5 marks)
3. **Confusion Matrix** — (2023: 7.5 marks, 2022: 7.5 marks)
4. **K-Means Algorithm with Example** — (2022: 7.5 marks)
5. **Random Forest Algorithm** — (2022: 7.5 marks)

### **Medium Priority Topics** (Short answers)

1. **Boosting** — 2022 (2.5 marks)
2. **Median Absolute Deviation (MAD)** — 2023 (2.5 marks), 2022 (2.5 marks)
3. **F1-Score** — 2023 (2.5 marks)

---

## **Section 1: Unsupervised Learning — Overview**

### **1.1 Definition**

**Unsupervised Learning** is a type of ML where the model is given **only input data (X) — no labels (Y)**. The model tries to find **hidden patterns, structures, or groupings** on its own.

```
Input:   X₁, X₂, X₃, ..., Xₘ   (no labels)
           │
           ▼
     ML Algorithm
           │
           ▼
  Output: Groups / Patterns / Structure
```

### **1.2 Types of Unsupervised Learning**

| Type | Goal | Example |
|------|------|---------|
| **Clustering** | Group similar data points | Customer segmentation |
| **Association** | Find co-occurrence rules | Market basket analysis |
| **Dimensionality Reduction** | Reduce features | PCA (covered in Unit 2) |
| **Anomaly Detection** | Find outliers | Fraud detection |

---

## **Section 2: K-Means Clustering**

> PYQ: Explain the k-Means Algorithm with an example. (2022, 7.5 marks)

### **2.1 What is Clustering?**

**Definition:**

**Clustering** is the process of **grouping similar data points together** (into clusters) such that:
- Points **within the same cluster** are as similar as possible.
- Points **in different clusters** are as different as possible.

**Analogy:**

Imagine sorting a basket of mixed fruits into groups — oranges together, apples together, bananas together — without being told the fruit names. You group them by similarity (colour, shape, size).

---

### **2.2 What is K-Means?**

**Definition:**

**K-Means** is the most popular clustering algorithm. It partitions a dataset of **m points** into **k clusters**, where each point belongs to the cluster with the **nearest mean (centroid)**.

**"K"** = number of clusters (chosen by the user before training).

---

### **2.3 K-Means Algorithm — Step by Step**

```
Input: Dataset X, number of clusters k

Step 1: Initialize
  ─ Randomly select k data points as initial centroids
    μ₁, μ₂, ..., μₖ

Step 2: Assignment (E-step)
  ─ For each data point xᵢ:
      Assign it to the nearest centroid:
      cᵢ = argmin_j  ||xᵢ - μⱼ||²

Step 3: Update (M-step)
  ─ Recompute each centroid as the mean of its assigned points:
      μⱼ = (1/|Cⱼ|) Σ xᵢ   for all xᵢ in cluster j

Step 4: Repeat
  ─ Repeat Steps 2 & 3 until centroids stop moving
    (convergence — assignments don't change)

Output: k clusters with final centroids
```

**Flow Diagram:**

```
  Initialize k centroids
         │
         ▼
  Assign each point to
  nearest centroid
         │
         ▼
  Recompute centroids
  (mean of cluster)
         │
         ▼
  Centroids changed?
    /         \
  Yes          No
   │            │
   └──────┐     ▼
          │   DONE ✓
          ▼
  (loop back to assign)
```

---

### **2.4 Worked Example**

**Dataset (6 points, 2D), k=2:**

```
Points:  A(1,1), B(1,2), C(2,1), D(5,4), E(6,5), F(5,5)
```

**Iteration 1:**

**Step 1 — Initialize centroids:** Pick A(1,1) and D(5,4) randomly.
```
μ₁ = (1,1)    μ₂ = (5,4)
```

**Step 2 — Assign each point:**
```
Point A(1,1): d(μ₁)=0.00, d(μ₂)=5.00  → Cluster 1
Point B(1,2): d(μ₁)=1.00, d(μ₂)=4.24  → Cluster 1
Point C(2,1): d(μ₁)=1.00, d(μ₂)=3.61  → Cluster 1
Point D(5,4): d(μ₁)=5.00, d(μ₂)=0.00  → Cluster 2
Point E(6,5): d(μ₁)=6.40, d(μ₂)=1.41  → Cluster 2
Point F(5,5): d(μ₁)=5.66, d(μ₂)=1.00  → Cluster 2
```

**Step 3 — Recompute centroids:**
```
Cluster 1 = {A, B, C}
  μ₁ = ((1+1+2)/3, (1+2+1)/3) = (4/3, 4/3) ≈ (1.33, 1.33)

Cluster 2 = {D, E, F}
  μ₂ = ((5+6+5)/3, (4+5+5)/3) = (16/3, 14/3) ≈ (5.33, 4.67)
```

**Iteration 2 — Reassign with new centroids:**
```
Distances from new μ₁=(1.33,1.33) and μ₂=(5.33,4.67):

A(1,1) → Cluster 1  ✓
B(1,2) → Cluster 1  ✓
C(2,1) → Cluster 1  ✓
D(5,4) → Cluster 2  ✓
E(6,5) → Cluster 2  ✓
F(5,5) → Cluster 2  ✓
```

Assignments unchanged → **Convergence!**

**Final Clusters:**
```
Cluster 1: {A(1,1), B(1,2), C(2,1)}   centroid ≈ (1.33, 1.33)
Cluster 2: {D(5,4), E(6,5), F(5,5)}   centroid ≈ (5.33, 4.67)
```

---

### **2.5 Choosing K — The Elbow Method**

The user must specify **k** before running K-Means. To find the best k:

**Elbow Method:**
- Run K-Means for k = 1, 2, 3, ..., n.
- For each k, compute **WCSS** (Within-Cluster Sum of Squares):

```
WCSS = Σ  Σ  ||xᵢ - μⱼ||²
       j  xᵢ∈Cⱼ
```

- Plot k vs WCSS. The "elbow" (sharp bend) gives the best k.

```
WCSS
│\
│ \
│  \
│   \──────────────    ← elbow here (best k = 3)
│             (flat)
└──────────────────→ k
  1  2  3  4  5  6
```

---

### **2.6 Advantages and Disadvantages**

**Advantages:**

✅ Simple and fast — O(n·k·i) where i = iterations.  
✅ Scales well to large datasets.  
✅ Easy to implement and interpret.

**Disadvantages:**

❌ Must specify k in advance.  
❌ Sensitive to **initial centroid placement** (different runs → different results).  
❌ Assumes spherical, equally-sized clusters.  
❌ Sensitive to **outliers** (outliers distort centroids).  
❌ Fails on non-convex cluster shapes.

**Fix for initialization:** Use **K-Means++** — smarter initialization that spreads centroids apart.

**Applications:**
- Customer segmentation
- Document clustering
- Image compression
- Anomaly detection

---

## **Section 3: Ensemble Methods**

> PYQ: Compare and contrast Boosting, Bagging, and Random Forest as Ensemble Methods in Unsupervised Learning. Discuss how these methods combine multiple models and improve the overall performance. Provide insights into scenarios where each ensemble method is most effective. (2024, 15 marks)

### **3.1 What are Ensemble Methods?**

**Definition:**

**Ensemble Methods** combine **multiple individual models (weak learners)** to produce one **stronger, more accurate model**.

**Core Idea:** Wisdom of the crowd — many weak models voting together beat one strong model.

```
     Model 1 ─────┐
     Model 2 ─────┤── Combine ──► Final Prediction
     Model 3 ─────┘
```

**Why do they work?**
- Individual models may make different errors.
- Combining them **cancels out individual errors**.
- Result: lower variance, lower bias, higher accuracy.

**Three main strategies:**

| Method | Core Idea | Models Trained |
|--------|-----------|----------------|
| **Bagging** | Train models in parallel on random subsets | Independent |
| **Boosting** | Train models sequentially, each fixing previous errors | Sequential |
| **Random Forest** | Bagging + random feature selection | Independent |

---

### **3.2 Bagging (Bootstrap Aggregating)**

**Definition:**

**Bagging** creates multiple models by training each on a **random bootstrap sample** (sample with replacement) of the training data. Final prediction = **majority vote** (classification) or **average** (regression).

**"Bootstrap"** = random sampling with replacement.

**Algorithm:**

```
Input: Training dataset D, number of models B

For b = 1 to B:
  1. Draw a bootstrap sample Dᵦ from D (with replacement).
  2. Train a model Mᵦ on Dᵦ.

Prediction for new point X:
  Classification: majority vote of M₁(X), M₂(X), ..., Mᴮ(X)
  Regression:     average of M₁(X), M₂(X), ..., Mᴮ(X)
```

**Diagram:**

```
        Original Dataset (D)
               │
    ┌──────────┼──────────┐
    ▼          ▼          ▼
 Sample D₁  Sample D₂  Sample D₃   (bootstrap samples)
    │          │          │
  Model 1   Model 2   Model 3       (trained independently)
    │          │          │
    └──────────┼──────────┘
               ▼
          Majority Vote
               │
               ▼
         Final Prediction
```

**Out-of-Bag (OOB) Error:**
- Each bootstrap sample leaves out ~37% of training data.
- These left-out points can be used as a **validation set** for free.
- Called **Out-of-Bag error** — a built-in cross-validation estimate.

**Advantages:**

✅ Reduces **variance** (prevents overfitting).  
✅ Parallel training (fast).  
✅ Works well with high-variance models (e.g., deep decision trees).

**Disadvantages:**

❌ Does not reduce **bias**.  
❌ Less interpretable than a single model.

---

### **3.3 Boosting**

> PYQ: Explain Boosting. (2022, 2.5 marks)

**Definition:**

**Boosting** trains models **sequentially**. Each new model focuses on correcting the **mistakes** of the previous model by giving higher weight to misclassified samples.

**Core Idea:** Start weak, get stronger step by step.

**Algorithm (general):**

```
Input: Training dataset D, number of models T

1. Initialize equal weights for all training points: wᵢ = 1/m

For t = 1 to T:
  2. Train model Mₜ on weighted dataset.
  3. Calculate error: εₜ = Σ wᵢ × I(Mₜ(xᵢ) ≠ yᵢ)
  4. Compute model weight: αₜ = 0.5 × ln[(1-εₜ)/εₜ]
  5. Update sample weights:
       Misclassified: wᵢ ← wᵢ × e^(αₜ)   (increase weight)
       Correct:       wᵢ ← wᵢ × e^(-αₜ)  (decrease weight)
  6. Normalize weights.

Final prediction:
  Ŷ = sign[ Σ αₜ × Mₜ(X) ]
```

**Diagram:**

```
  Dataset
     │
     ▼
  Model 1 ──► Errors ──► Increase weights of errors
     │
     ▼
  Model 2 ──► Errors ──► Increase weights of errors
     │
     ▼
  Model 3 ──► ...
     │
     ▼
  Weighted Vote ──► Final Prediction
```

**Popular Boosting Algorithms:**

| Algorithm | Description |
|-----------|-------------|
| **AdaBoost** | Original boosting — adjusts sample weights |
| **Gradient Boosting** | Fits each model to residual errors |
| **XGBoost** | Optimized gradient boosting with regularization |
| **LightGBM** | Fast, scalable gradient boosting |

**Advantages:**

✅ Reduces **both bias and variance**.  
✅ Often achieves best accuracy on tabular data.  
✅ Handles complex patterns.

**Disadvantages:**

❌ Sequential — cannot parallelize easily.  
❌ Prone to **overfitting** if too many rounds.  
❌ Sensitive to **noisy data and outliers** (amplifies errors).

---

### **3.4 Bagging vs Boosting**

> PYQ: Differentiate between Bagging and Boosting techniques. (2023, 15 marks)

| Feature | Bagging | Boosting |
|---------|---------|----------|
| **Training** | Parallel | Sequential |
| **Focus** | Reduces Variance | Reduces Bias |
| **Weights** | All samples equal | Misclassified get higher weight |
| **Error Fixed** | Overfitting | Underfitting |
| **Speed** | Faster | Slower |
| **Overfitting Risk** | Low | Higher (needs tuning) |
| **Example** | Random Forest | AdaBoost, XGBoost |

---

### **3.5 Random Forest**

> PYQ: Describe the Random Forest algorithm to improve classifier accuracy. (2022, 7.5 marks)

**Definition:**

**Random Forest** is an ensemble method that builds many **decision trees** using:
1. **Bagging** — each tree is trained on a bootstrap sample.
2. **Random Feature Selection** — at each split, only a **random subset of features** is considered (not all features).

The final prediction is the **majority vote** (classification) or **average** (regression) of all trees.

**Algorithm:**

```
Input: Dataset D, number of trees T, features m (subset size)

For t = 1 to T:
  1. Draw bootstrap sample Dₜ from D.
  2. Grow a decision tree on Dₜ:
       At each node, randomly pick m features (m < total features).
       Split on the best among those m features.
  3. Grow tree fully (no pruning).

Prediction:
  Classification: majority vote of all T trees
  Regression: average of all T trees
```

**Diagram:**

```
      Dataset D
          │
    ┌─────┼─────┐
    ▼     ▼     ▼
   D₁    D₂    D₃    ← bootstrap samples
    │     │     │
   T₁    T₂    T₃    ← trees (random features at each split)
    │     │     │
    └─────┼─────┘
          ▼
     Majority Vote
          │
          ▼
    Final Prediction
```

**Why random feature selection?**

- If one feature is very strong, all trees in bagging will use it → trees are **correlated**.
- Randomly selecting features at each split **decorrelates trees**.
- Decorrelated trees make better ensemble predictions.

**Feature Importance in Random Forest:**
- Tracks how often each feature is used for splits and how much it reduces impurity.
- Gives a natural **feature importance ranking**.

**Advantages:**

✅ Very accurate — one of the best general-purpose algorithms.  
✅ Handles thousands of features without feature selection.  
✅ Provides feature importance scores.  
✅ Robust to overfitting.  
✅ Handles missing values well.  
✅ OOB error is a built-in validation estimate.

**Disadvantages:**

❌ Slow to predict (must traverse T trees).  
❌ Not interpretable (black box).  
❌ More memory usage.

**Applications:**
- Stock market prediction
- Medical diagnosis
- Credit scoring
- Remote sensing (land cover classification)

---

### **3.6 Comparison: Bagging vs Boosting vs Random Forest**

> PYQ: Compare and contrast Boosting, Bagging, and Random Forest as Ensemble Methods. Provide insights into scenarios where each ensemble method is most effective. (2024, 15 marks)

While Bagging, Boosting, and Random Forest are all **ensemble methods**, each combines models differently. Here is a side-by-side comparison.

#### **Side-by-Side Comparison**

| Feature | **Bagging** | **Boosting** | **Random Forest** |
|---|---|---|---|
| **Execution** | Parallel | Sequential | Parallel |
| **Focus** | Reduces variance | Reduces bias | Reduces variance + prevents overfitting |
| **Model Dependency** | Independent models | Models depend on previous ones | Independent decision trees |
| **Sample Strategy** | Bootstrap (with replacement) | Re-weighted samples (focus on errors) | Bootstrap + random feature subset |
| **Base Learner** | Any (often decision trees) | Any (often weak learners) | Always decision trees |
| **Performance** | Stable results | Higher accuracy but risk of overfitting | Balanced trade-off |
| **Speed** | Fast (can be parallelized) | Slower (sequential steps) | Moderate |
| **Aggregation** | Majority vote / average | Weighted sum | Majority vote / average |
| **Example Algorithm** | Bagged Decision Trees | AdaBoost, XGBoost, Gradient Boosting | Random Forest |

#### **How Each Combines Models to Improve Performance**

**Bagging (Bootstrap Aggregation):**
- Multiple models are trained **in parallel** on **bootstrapped subsets** of data.
- Final prediction is a **majority vote** (classification) or **average** (regression).
- Reduces **variance** and increases **stability** of the model.

**Boosting:**
- Models are trained **sequentially**, where each new model **focuses on errors** made by the previous one.
- Misclassified data points are **re-weighted** so the next learner pays more attention to them.
- Final model is a **weighted sum** of all weak learners — reduces both **bias and variance**.

**Random Forest:**
- Builds many **decision trees** using bagging **plus** a **random subset of features at each split**.
- Random feature selection **decorrelates** the trees, which makes the ensemble stronger.
- Final prediction is a **majority vote** (classification) or **average** (regression).

#### **Use Cases & Effectiveness Scenarios**

| Scenario | Most Effective Method | Why |
|---|---|---|
| **High-variance models (e.g., deep decision trees)** | **Bagging** | Reduces variance and prevents overfitting on unstable learners |
| **High-bias models (e.g., shallow trees, stumps)** | **Boosting** | Iteratively reduces bias by focusing on errors |
| **Large, high-dimensional datasets** | **Random Forest** | Random feature selection handles many features and resists overfitting |
| **Need for interpretability** | **Random Forest** | Tree structures + feature importance allow some interpretability |
| **Anomaly / outlier detection** | **Boosting** (e.g., AdaBoost, Isolation Forest) | Focuses iteratively on hard-to-fit points |
| **Unstructured / noisy data** | **Bagging** | Averaging reduces noise and increases reliability |
| **Need for top accuracy on tabular data** | **Boosting** (XGBoost / LightGBM) | Typically delivers state-of-the-art results |
| **Need for stable, low-tuning baseline** | **Random Forest** | Works well out of the box, minimal hyperparameter tuning |

#### **Summary**

- **Bagging** = best when the base model is **unstable** and overfitting is the problem.
- **Boosting** = best when the base model is **too simple** and bias is the problem.
- **Random Forest** = best **all-rounder** — combines the variance-reduction of bagging with the decorrelation of random feature selection, giving balanced, robust performance.

---

## **Section 4: Model Evaluation**

### **4.1 Why Evaluate?**

A trained model must be tested on **unseen data** to check if it generalizes well. Evaluation metrics tell us **how good** the model is and **where it fails**.

---

### **4.2 Confusion Matrix**

> PYQ: Confusion Matrix. (2023, 7.5 marks)  
> PYQ: Confusion Matrix. (2022, 7.5 marks)

**Definition:**

A **Confusion Matrix** is a table that compares the **predicted class labels** against the **actual class labels** for a classification model.

**For binary classification (2 classes: Positive and Negative):**

```
                    PREDICTED
                  Positive   Negative
              ┌──────────┬──────────┐
ACTUAL  Pos   │    TP    │    FN    │
        Neg   │    FP    │    TN    │
              └──────────┴──────────┘
```

| Term | Full Form | Meaning |
|------|-----------|---------|
| **TP** | True Positive | Predicted Positive, Actually Positive ✅ |
| **TN** | True Negative | Predicted Negative, Actually Negative ✅ |
| **FP** | False Positive | Predicted Positive, Actually Negative ❌ (Type I error) |
| **FN** | False Negative | Predicted Negative, Actually Positive ❌ (Type II error) |

**Example:**

10 emails: 6 spam, 4 not-spam.  
Model predicts: 5 spam, 5 not-spam.

```
              Predicted
              Spam   Not-Spam
Actual Spam  │ 4  │   2  │   (4 correct, 2 missed)
       Not   │ 1  │   3  │   (1 false alarm, 3 correct)
```

TP=4, FN=2, FP=1, TN=3

---

### **4.3 Accuracy**

**Definition:** Percentage of all predictions that were correct.

**Formula:**

```
              TP + TN
Accuracy  =  ─────────────────────
             TP + TN + FP + FN
```

**Example:**
```
Accuracy = (4+3) / (4+2+1+3) = 7/10 = 0.70 = 70%
```

**Limitation:** Misleading when classes are **imbalanced**.

> Example: 95% of emails are "Not Spam". A model that predicts everything as "Not Spam" gets 95% accuracy but catches zero spam.

---

### **4.4 Precision**

**Definition:** Of all the samples predicted as Positive, how many were actually Positive?

**Formula:**

```
              TP
Precision = ────────
            TP + FP
```

**Example:**
```
Precision = 4 / (4+1) = 4/5 = 0.80 = 80%
```

**High Precision needed when:** False Positives are costly.
- Example: Cancer treatment — don't want to treat healthy people.

---

### **4.5 Recall (Sensitivity / True Positive Rate)**

**Definition:** Of all actual Positive samples, how many did the model correctly find?

**Formula:**

```
            TP
Recall =  ────────
          TP + FN
```

**Example:**
```
Recall = 4 / (4+2) = 4/6 ≈ 0.67 = 67%
```

**High Recall needed when:** False Negatives are costly.
- Example: Disease detection — don't want to miss actual sick patients.

---

### **4.6 Precision vs Recall Trade-off**

```
         High Precision ←──────────────────→ High Recall
              │                                   │
         Few FP                              Few FN
         (don't cry wolf)              (catch everything)
              │                                   │
         Spam filter                       Cancer screening
         (avoid blocking                  (avoid missing
          good emails)                      sick patients)
```

- **Increasing threshold** → Higher Precision, Lower Recall.
- **Decreasing threshold** → Higher Recall, Lower Precision.

---

### **4.7 F1-Score**

> PYQ: F1-score. (2023, 2.5 marks)

**Definition:**

**F1-Score** is the **harmonic mean** of Precision and Recall. It balances both when you need a single metric.

**Formula:**

```
              2 × Precision × Recall
F1-Score  =  ────────────────────────
               Precision + Recall
```

**Example:**
```
F1 = 2 × 0.80 × 0.67 / (0.80 + 0.67)
   = 2 × 0.536 / 1.47
   = 1.072 / 1.47
   ≈ 0.729 = 72.9%
```

**When to use F1:** When the dataset is **imbalanced** and you need to balance Precision and Recall.

**Summary of all 4 metrics:**

| Metric | Formula | Meaning |
|--------|---------|---------|
| **Accuracy** | (TP+TN)/(TP+TN+FP+FN) | Overall correctness |
| **Precision** | TP/(TP+FP) | Quality of positive predictions |
| **Recall** | TP/(TP+FN) | Coverage of actual positives |
| **F1-Score** | 2×P×R/(P+R) | Balance of Precision and Recall |

---

### **4.8 ROC Curve and AUC**

> PYQ: Explain ROC and AUC. (2022, 7.5 marks)  
> PYQ: ROC and AUC. (2023, 7.5 marks)  
> PYQ: Describe the Receiver Operating Characteristic (ROC) curve and Area Under the Curve (AUC) as evaluation metrics for binary classification models. How does the ROC curve visualize the trade-off between a true positive rate and a false positive rate? What insights can be derived from the AUC value? (2024, 15 marks)

#### **ROC Curve**

**Definition:**

The **ROC Curve (Receiver Operating Characteristic Curve)** is a graph that shows the trade-off between:
- **True Positive Rate (TPR / Recall)** on the Y-axis.
- **False Positive Rate (FPR)** on the X-axis.

As the **classification threshold** changes from 0 to 1, both TPR and FPR change, tracing out the curve.

**Formulas:**

```
            TP
TPR  =  ────────   (= Recall = Sensitivity)
        TP + FN

            FP
FPR  =  ────────   (= 1 - Specificity)
        FP + TN
```

**How to Plot ROC Curve:**

1. Start with threshold = 1 (predict all Negative) → TPR=0, FPR=0.
2. Gradually lower threshold.
3. More positives are predicted → TPR increases, FPR also increases.
4. At threshold = 0 (predict all Positive) → TPR=1, FPR=1.

**Diagram:**

```
TPR
 1 │         ╭──────────
   │      ╭──╯     ← Good model (curves up-left)
   │   ╭──╯
   │╭──╯
 0 │╯______________
   0              1   FPR

   Diagonal line = Random classifier (AUC = 0.5)
   Top-left area = Best classifier (AUC = 1.0)
```

---

#### **AUC (Area Under the ROC Curve)**

**Definition:**

**AUC** is the **area under the ROC curve**. It measures the overall ability of the model to discriminate between classes.

**Interpretation:**

| AUC Value | Meaning |
|-----------|---------|
| **AUC = 1.0** | Perfect classifier |
| **AUC = 0.9–1.0** | Excellent |
| **AUC = 0.8–0.9** | Good |
| **AUC = 0.7–0.8** | Fair |
| **AUC = 0.6–0.7** | Poor |
| **AUC = 0.5** | Random guessing (no better than coin flip) |
| **AUC < 0.5** | Worse than random |

**Advantages of ROC-AUC:**
- Works well with **imbalanced datasets**.
- Threshold-independent — evaluates model across all thresholds.
- Single number summary of classifier performance.

---

### **4.9 Median Absolute Deviation (MAD)**

> PYQ: Median Absolute Deviation (MAD). (2022, 2.5 marks)  
> PYQ: Median Absolute Deviation. (2023, 2.5 marks)

**Definition:**

**MAD** is a **robust measure of variability** in predictions. It measures the median of the absolute differences between each prediction and the median prediction.

**Steps:**

```
Step 1: Find the median of all predictions/data:  M = median(y)

Step 2: Calculate absolute deviations:
         |y₁ - M|,  |y₂ - M|,  ...,  |yₙ - M|

Step 3: MAD = median of those absolute deviations
```

**Formula:**

```
MAD = median( |yᵢ - median(y)| )
```

**Example:**

Data: [2, 3, 5, 7, 11]

```
Step 1: Median = 5

Step 2: Absolute deviations:
  |2-5| = 3
  |3-5| = 2
  |5-5| = 0
  |7-5| = 2
  |11-5| = 6

  Sorted deviations: [0, 2, 2, 3, 6]

Step 3: MAD = median([0,2,2,3,6]) = 2
```

**Why MAD over Standard Deviation?**
- **Standard deviation** is sensitive to outliers (uses squared differences).
- **MAD** is **robust** — outliers don't distort it.

**Applications:**
- Regression model error analysis
- Outlier detection
- Robust statistics

---

### **4.10 Distribution of Errors**

**Definition:**

**Distribution of errors** (also called **residuals**) refers to analyzing the **pattern of prediction errors** made by an ML model.

```
Error / Residual = Actual Value (y) - Predicted Value (ŷ)
eᵢ = yᵢ - ŷᵢ
```

**Why Analyze Error Distribution?**

- Tells us if the model is making **systematic mistakes** or random ones.
- Helps diagnose model problems.

**Common Error Plots:**

1. **Residual Plot:** Plot errors vs predicted values. Good model = random scatter around zero.

```
Error
  │   ●  ●
  │ ●       ●    ← Good (random scatter)
──┼──────────────→ Predicted value
  │   ●  ●
```

2. **Histogram of Errors:** Should be **normally distributed** (bell curve) with mean ≈ 0.

```
Count
  │      ╭───╮
  │   ╭──╯   ╰──╮
  │ ──╯           ╰──
  └──────────────────→ Error
          0
```

3. **Q-Q Plot:** Compares error distribution to normal distribution.

**Key Properties of a Well-Behaved Error Distribution:**

| Property | Meaning |
|----------|---------|
| **Mean ≈ 0** | No systematic bias |
| **Normal shape** | Errors are random, not patterned |
| **Constant variance** | Homoscedasticity (equal spread) |
| **No autocorrelation** | Errors are independent of each other |

**Common Error Metrics for Regression:**

| Metric | Formula | Meaning |
|--------|---------|---------|
| **MSE** | (1/m) Σ(yᵢ-ŷᵢ)² | Mean Squared Error — penalizes big errors |
| **RMSE** | √MSE | Root MSE — same unit as output |
| **MAE** | (1/m) Σ\|yᵢ-ŷᵢ\| | Mean Absolute Error — robust to outliers |
| **MAD** | median(\|yᵢ-median(y)\|) | Median Absolute Deviation — most robust |

---

## **Quick Revision Points**

### **K-Means:**
- Choose k → Initialize centroids → Assign points → Update centroids → Repeat.
- Distance: Euclidean.
- Best k: Elbow method (plot k vs WCSS).
- Problem: sensitive to initialization and outliers. Fix: K-Means++.

### **Ensemble Methods:**

| | Bagging | Boosting | Random Forest |
|--|---------|----------|---------------|
| Training | Parallel | Sequential | Parallel |
| Reduces | Variance | Bias+Variance | Variance |
| Key param | B (trees) | T, learning rate | T, m (features) |
| Example | Bagged Trees | AdaBoost, XGBoost | Random Forest |

### **Evaluation Metrics:**

```
Accuracy  = (TP+TN) / (TP+TN+FP+FN)
Precision = TP / (TP+FP)
Recall    = TP / (TP+FN)
F1-Score  = 2×P×R / (P+R)
TPR       = TP / (TP+FN)   [= Recall]
FPR       = FP / (FP+TN)
MAD       = median(|yᵢ - median(y)|)
```

### **ROC-AUC:**
- ROC plots TPR vs FPR at different thresholds.
- AUC = area under ROC curve.
- AUC = 1.0 → perfect; AUC = 0.5 → random.

### **Error Distribution:**
- Good model: errors are normally distributed, mean ≈ 0, random scatter.
- MAD is more robust than standard deviation for error analysis.

---

## **Expected Exam Questions**

### **15-Mark Questions:**

1. Differentiate between Bagging and Boosting techniques. *(2023)*
2. Compare and contrast Boosting, Bagging, and Random Forest as Ensemble Methods. Discuss how these methods combine multiple models and improve overall performance. Provide insights into scenarios where each ensemble method is most effective. *(2024)*
3. Describe the Receiver Operating Characteristic (ROC) curve and Area Under the Curve (AUC) as evaluation metrics for binary classification models. How does the ROC curve visualize the trade-off between TPR and FPR? What insights can be derived from the AUC value? *(2024)*

### **Short Answer Questions (2.5 marks):**

1. Boosting. *(2022)*
2. Median Absolute Deviation (MAD). *(2022, 2023)*
3. F1-score. *(2023)*

### **Mixed (7.5 marks):**

1. Explain the k-Means Algorithm with an example. *(2022)*
2. Describe the Random Forest algorithm to improve classifier accuracy. *(2022)*
3. ROC and AUC. *(2022, 2023)*
4. Confusion Matrix. *(2022, 2023)*

---

_These notes were compiled by [Deepak Modi](https://deepakmodi.dev)_  
_Last updated: May 2026_
