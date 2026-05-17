---
title: "Unit 3: Supervised Learning"
description: "k-NN, Naïve Bayes, Decision Trees, Linear Regression, Logistic Regression, and Support Vector Machines — definitions, working, formulas, and examples."
author: "Deepak Modi"
date: "2026-05-10"
pdfUrl: ""
---

## Syllabus:

**Supervised Learning:** Definition, how it works. Types of Supervised learning algorithms: k-Nearest Neighbours, Naïve Bayes, Decision Trees, Linear Regression, Logistic Regression, Support Vector Machines.

---

## 🎯 PYQ Analysis for Unit 3

### **High Priority Topics** (15 marks questions)

1. **Decision Trees (Algorithm + Types)** — (2024: 15 marks, 2023: 15 marks)
2. **Naive Bayes (Assumptions, Working, Why "Naive")** — (2023: 15 marks, 2022: 7.5 marks)
3. **Support Vector Machine (Goal + Margin)** — (2022: 15 marks)
4. **Supervised Learning (Definition + Working Principle)** — (2024: 15 marks)
5. **Importance of Labelled Data + Decision Trees** — (2024: 15 marks)
6. **Regression (with Example)** — (2022: 7.5 marks)

### **Medium Priority Topics** (Short answers)

1. **Support Vectors** — 2023 (2.5 marks)
2. **K-NN as Lazy Learner** — 2023 (2.5 marks)
3. **Underfitting** — 2023 (2.5 marks)
4. **Logistic Regression** — 2023 (2.5 marks)
5. **Linear Regression** — 2022 (2.5 marks)

---

## **Section 1: Supervised Learning — Overview**

> PYQ: Define Supervised Learning and explain its working principle. Provide a step-by-step example of how a supervised learning algorithm processes training data and makes predictions. (2024, 15 marks)  
> PYQ: Discuss the importance of labelled data in Supervised Learning and its role in training predictive models. Also, explain Decision Trees by taking a suitable example. (2024, 15 marks)  
> PYQ: Underfitting. (2023, 2.5 marks)

### **1.1 Definition**

**Supervised Learning** is a type of ML where the model is trained on a **labeled dataset** — every input (X) has a known correct output (Y). The model learns to map X → Y, and then uses that mapping to predict Y for new, unseen inputs.

**How It Works:**

```
  Training Phase:
  ──────────────
  Labeled Data (X, Y) ──► ML Algorithm ──► Trained Model

  Prediction Phase:
  ─────────────────
  New Input (X_new) ──► Trained Model ──► Predicted Output (Ŷ)
```

### **1.2 Two Types of Supervised Learning**

| Type | Output | Example |
|------|--------|---------|
| **Classification** | Discrete class label | Spam / Not Spam |
| **Regression** | Continuous numeric value | House price prediction |

### **1.3 General Workflow**

1. Collect labeled data.
2. Split into **Training set** and **Test set** (e.g., 80/20 split).
3. Choose an algorithm.
4. Train the model on the training set.
5. Evaluate on the test set.
6. Tune and deploy.

---

### **1.4 Working Principle of Supervised Learning**

> PYQ: Explain the working principle of Supervised Learning. (2024, part of 15 marks)

The general workflow of a supervised learning algorithm consists of the following steps:

| Step | Description |
|---|---|
| **1. Data Collection** | Gather **labelled** data (features + correct outputs) |
| **2. Data Preprocessing** | Clean and prepare the data (handle missing values, encode categories, normalize if needed) |
| **3. Model Selection** | Choose a suitable algorithm (e.g., Linear Regression, Decision Tree, SVM) |
| **4. Training** | Feed the input–output pairs to the model so it can **learn the mapping** between them |
| **5. Evaluation** | Test the model on unseen data using metrics like accuracy, precision, recall, RMSE |
| **6. Prediction** | Use the trained model to make predictions on completely new data |

---

### **1.5 Step-by-Step Example — House Price Prediction**

> PYQ: Provide a step-by-step example of how a supervised learning algorithm processes training data and makes predictions. (2024, part of 15 marks)

Let's walk through a complete supervised learning workflow with a **regression example** — predicting the price of a house based on its size (in square feet).

#### **Step 1: Dataset (Labelled)**

| House Size (sqft) | Price ($) |
|---|---|
| 1000 | 200,000 |
| 1500 | 300,000 |
| 2000 | 400,000 |
| 2500 | 500,000 |

Here:
- **Feature (X):** House Size
- **Label (Y):** Price

#### **Step 2: Choose Model**

Use **Linear Regression**, assuming a relationship of the form:

```
Price = m × Size + c
```

#### **Step 3: Training**

The algorithm computes the **best-fit line** by finding the optimal values of `m` (slope) and `c` (intercept) that **minimize the prediction error**.

For this dataset, it learns:

```
Price = 200 × Size
```

(That is, m = 200 and c = 0.)

#### **Step 4: Prediction**

For a **new house** with Size = **1800 sqft**, the model predicts:

```
Price = 200 × 1800 = $360,000
```

#### **Step 5: Evaluation**

The trained model is tested on **unseen data** using error metrics:

- **Mean Squared Error (MSE)**
- **R² Score** (for regression)
- **Accuracy / Precision / Recall** (for classification)

#### **Key Algorithms in Supervised Learning**

| Algorithm | Use Case |
|---|---|
| **Linear Regression** | Predict continuous values |
| **Logistic Regression** | Binary classification |
| **Decision Tree** | Both classification and regression |
| **K-Nearest Neighbors (KNN)** | Classification |
| **Support Vector Machine (SVM)** | Classification with clear margins |
| **Naïve Bayes** | Text classification |

#### **Benefits of Supervised Learning**

- ✅ Clear objective due to labelled data
- ✅ Accurate predictions with sufficient training data
- ✅ Easy to evaluate using performance metrics

#### **Limitations**

- ❌ Requires a **large amount** of labelled data (expensive to obtain)
- ❌ Cannot handle classes/situations not seen during training
- ❌ May overfit or underfit depending on model complexity

---

### **1.6 Importance of Labelled Data in Supervised Learning**

> PYQ: Discuss the importance of labelled data in Supervised Learning and its role in training predictive models. (2024, part of 15 marks)

Supervised learning **cannot exist without labelled data** — that is, every input must come with a corresponding correct output. Examples:

- Predicting house prices → label = price
- Classifying emails → label = spam / ham

#### **Role of Labelled Data in Supervised Learning**

| Role of Labelled Data | Explanation |
|---|---|
| **Guides Model Learning** | Helps the algorithm understand the mapping between input features and the desired output |
| **Error Measurement** | Enables computation of **loss / error** during training, which is then minimized through optimization |
| **Model Validation** | Used in test / validation sets to **evaluate model accuracy and generalization** |
| **Improves Accuracy** | More and more diverse labelled examples help the model **learn patterns better** |
| **Supports Fine-Tuning** | Allows **parameter tuning** based on labelled feedback during cross-validation |

Without labelled data, supervised learning models **cannot learn predictive tasks** — labels are the foundation of this learning paradigm.

#### **Role of Labelled Data in Building Predictive Models**

When building a predictive model, labelled data is essential in every phase:

1. **Training Phase** — the model learns patterns from features paired with their correct outputs.
2. **Testing Phase** — labelled test data is used to validate **how well the model generalizes** to unseen examples.
3. **Performance Metrics** — labels enable calculation of **accuracy, precision, recall, F1-score**, etc.
4. **Supervised Feedback Loop** — the model **updates its parameters** based on how close (or far) its predictions are from the actual labels.

> **Bottom line:** Labelled data is the *teacher* in supervised learning — without it, the model has nothing to learn from and nothing to be measured against.

---

## **Section 2: k-Nearest Neighbours (k-NN)**

> PYQ: K-NN is called Lazy Learner. Explain it. (2023, 2.5 marks)

### **2.1 What is k-NN?**

**Definition:**

**k-Nearest Neighbours (k-NN)** is a simple, non-parametric supervised learning algorithm. To classify a new data point, it looks at the **k closest training points** (neighbours) and assigns the **majority class** among them.

> k-NN is called a **lazy learner** — it does not build an explicit model during training. It memorizes the entire training dataset.

**Simple Analogy:**

To guess which neighbourhood a house belongs to, you look at the 3 nearest houses (k=3). If 2 of 3 are in "Area A", you classify the house as "Area A".

---

### **2.2 How k-NN Works**

**Algorithm Steps:**

```
1. Store all training data points.

2. For a new input point X_new:
   a. Calculate distance from X_new to every training point.
   b. Sort distances in ascending order.
   c. Select the top k nearest neighbours.
   d. Count the class labels of the k neighbours.
   e. Assign the majority class as the prediction.
```

**Diagram:**

```
         ●  ■                  Legend:
       ●   ●                   ● = Class A
        ✦ ← new point          ■ = Class B
       ■   ●                   ✦ = query point
         ■  ●

   k=3 nearest neighbours: ●, ●, ■
   Majority = ●  → Predict Class A
```

---

### **2.3 Distance Metrics**

The "closeness" between two points is measured by a **distance function**.

#### **Euclidean Distance (most common):**

```
d(A, B) = √[(a₁-b₁)² + (a₂-b₂)² + ... + (aₙ-bₙ)²]

For 2D:
d(A, B) = √[(a₁-b₁)² + (a₂-b₂)²]
```

#### **Manhattan Distance:**

```
d(A, B) = |a₁-b₁| + |a₂-b₂| + ... + |aₙ-bₙ|
```

#### **Minkowski Distance (generalizes both):**

```
d(A, B) = [Σ|aᵢ-bᵢ|ᵖ]^(1/p)

p=1 → Manhattan
p=2 → Euclidean
```

---

### **2.4 Worked Example**

**Dataset:**

| Point | x₁ | x₂ | Class |
|-------|----|----|-------|
| A | 1 | 2 | C1 |
| B | 2 | 3 | C1 |
| C | 3 | 1 | C2 |
| D | 5 | 4 | C2 |

**Query point:** Q = (3, 3), k = 3

**Calculate Euclidean distances from Q to each point:**

```
d(Q, A) = √[(3-1)² + (3-2)²] = √[4+1]   = √5   ≈ 2.24
d(Q, B) = √[(3-2)² + (3-3)²] = √[1+0]   = √1   = 1.00
d(Q, C) = √[(3-3)² + (3-1)²] = √[0+4]   = √4   = 2.00
d(Q, D) = √[(3-5)² + (3-4)²] = √[4+1]   = √5   ≈ 2.24
```

**Sort and pick k=3 nearest:**

```
1. B — distance 1.00 → Class C1
2. C — distance 2.00 → Class C2
3. A — distance 2.24 → Class C1  (tie broken by order)
```

**Vote:** C1: 2,  C2: 1  →  **Predict Class C1**

---

### **2.5 Choosing k**

| k value | Effect |
|---------|--------|
| **k=1** | Very sensitive to noise, can overfit |
| **k=large** | Smoother boundary, may underfit |
| **Odd k** | Avoids ties in binary classification |
| **Best practice** | Use cross-validation to find optimal k |

---

### **2.6 Advantages and Disadvantages**

**Advantages:**

✅ Simple, easy to understand and implement.  
✅ No training phase (lazy learner).  
✅ Naturally handles multi-class problems.  
✅ Adapts automatically to new training data.

**Disadvantages:**

❌ Slow at prediction time (computes all distances).  
❌ High memory usage (stores entire training set).  
❌ Sensitive to irrelevant features and scale.  
❌ Struggles with high-dimensional data.

**Applications:**
- Recommendation systems
- Image recognition
- Medical diagnosis
- Anomaly detection

---

## **Section 3: Naïve Bayes**

> PYQ: Explain Naive Bayes Classifier. (2022, 7.5 marks)  
> PYQ: What are the basic assumptions used in Naive Bayes classifier? Why is it called Naive Bayes? Also discuss the working of Naive Bayes algorithm. (2023, 15 marks)

### **3.1 What is Naïve Bayes?**

**Definition:**

**Naïve Bayes** is a probabilistic classification algorithm based on **Bayes' Theorem**. It assumes that all features are **independent** of each other given the class — this is the "naïve" assumption.

---

### **3.2 Why is it Called "Naïve Bayes"?**

> PYQ: Why is it called Naive Bayes? (2023, part of 15 marks)

The name **Naïve Bayes** has two parts — each with a clear meaning:

#### **"Naïve" — because of the independence assumption**

It is called **naïve** because it makes a **strong (unrealistic) assumption** that **every pair of features is independent** of each other, given the class label. In the real world, features are usually correlated — so this assumption is almost always violated, yet the algorithm still works surprisingly well in practice.

> **Example:** To identify a fruit as an **apple**, the model checks features like *colour = red*, *shape = round*, *taste = sweet* — and assumes these features are completely independent of each other. In reality, "red" and "sweet" might be related, but the Naïve Bayes classifier ignores that link.

#### **"Bayes" — because it uses Bayes' Theorem**

It is called **Bayes** because the algorithm is built directly on the principle of **Bayes' Theorem** — a fundamental result in probability that lets us compute the probability of a hypothesis given some observed evidence.

---

### **3.3 Basic Assumptions of Naïve Bayes**

> PYQ: What are the basic assumptions used in Naive Bayes classifier? (2023, part of 15 marks)

The Naïve Bayes classifier makes the following **fundamental assumptions** about the data:

**1. Feature Independence (the "naïve" assumption)**

The features of the data are **conditionally independent** of each other, given the class label. Knowing the value of one feature gives no information about another feature within the same class.

**2. Continuous Features are Normally Distributed**

If a feature is **continuous** (numeric), it is assumed to follow a **normal (Gaussian) distribution** within each class. This is the basis for **Gaussian Naïve Bayes**.

**3. Discrete Features Follow Multinomial Distribution**

If a feature is **discrete** (e.g., word counts in text classification), it is assumed to follow a **multinomial distribution** within each class. This is the basis for **Multinomial Naïve Bayes**.

**4. Features are Equally Important**

All features are assumed to **contribute equally** to the prediction of the class label — there is no built-in feature weighting.

**5. No Missing Data**

The dataset is assumed to contain **no missing values**. Missing data must be imputed or removed before training.

---

### **3.4 Bayes' Theorem**

**Formula:**

```
          P(X | C) × P(C)
P(C | X) = ──────────────────
                P(X)

Where:
  P(C | X) = Posterior — probability of class C given features X
  P(X | C) = Likelihood — probability of seeing X given class C
  P(C)     = Prior — probability of class C in training data
  P(X)     = Evidence — probability of seeing X (normalizing constant)
```

**For Classification (we compare classes, so P(X) cancels):**

```
P(C | X) ∝ P(X | C) × P(C)

Pick class C that maximizes:
  P(C | X₁, X₂, ..., Xₙ)

Naïve independence assumption:
  P(X₁, X₂, ..., Xₙ | C) = P(X₁|C) × P(X₂|C) × ... × P(Xₙ|C)
```

---

### **3.5 How Naïve Bayes Works**

**Steps:**

```
1. Training:
   a. Calculate P(C) for each class (prior).
   b. For each feature and each class, calculate P(Xᵢ | C) (likelihood).

2. Prediction (for new point X):
   a. For each class C, compute:
         Score(C) = P(C) × P(X₁|C) × P(X₂|C) × ... × P(Xₙ|C)
   b. Predict class with highest Score.
```

---

### **3.6 Worked Example**

**Dataset — Play Tennis:**

| Day | Outlook | Humidity | Wind | Play? |
|-----|---------|----------|------|-------|
| 1 | Sunny | High | Weak | No |
| 2 | Sunny | High | Strong | No |
| 3 | Overcast | High | Weak | Yes |
| 4 | Rain | Normal | Weak | Yes |
| 5 | Rain | Normal | Strong | No |
| 6 | Overcast | Normal | Strong | Yes |
| 7 | Sunny | Normal | Weak | Yes |

**Predict:** Outlook=Sunny, Humidity=Normal, Wind=Weak  →  Play?

**Step 1: Prior probabilities**
```
P(Yes) = 4/7 ≈ 0.571
P(No)  = 3/7 ≈ 0.429
```

**Step 2: Likelihoods**
```
For Yes (4 examples):
  P(Outlook=Sunny  | Yes) = 1/4 = 0.25
  P(Humidity=Normal| Yes) = 3/4 = 0.75
  P(Wind=Weak      | Yes) = 3/4 = 0.75

For No (3 examples):
  P(Outlook=Sunny  | No)  = 2/3 ≈ 0.67
  P(Humidity=Normal| No)  = 1/3 ≈ 0.33
  P(Wind=Weak      | No)  = 1/3 ≈ 0.33
```

**Step 3: Posterior scores**
```
Score(Yes) = P(Yes) × 0.25 × 0.75 × 0.75
           = 0.571 × 0.1406
           ≈ 0.0803

Score(No)  = P(No) × 0.67 × 0.33 × 0.33
           = 0.429 × 0.0729
           ≈ 0.0313
```

**Prediction: Yes** (0.0803 > 0.0313) ✅

---

### **3.7 Laplace Smoothing**

**Problem:** If any P(Xᵢ|C) = 0 (feature never seen in training), the whole product = 0.

**Solution — Laplace Smoothing (add-1 smoothing):**

```
            count(Xᵢ, C) + 1
P(Xᵢ | C) = ─────────────────────
             count(C) + |vocab|
```

---

### **3.8 Types of Naïve Bayes**

| Type | Feature Distribution | Use Case |
|------|---------------------|----------|
| **Gaussian NB** | Continuous, normal distribution | Iris flower classification |
| **Multinomial NB** | Discrete counts | Text classification |
| **Bernoulli NB** | Binary features | Spam detection |

---

### **3.9 Advantages and Disadvantages**

**Advantages:**

✅ Very fast — simple multiplication of probabilities.  
✅ Works well with small datasets.  
✅ Handles high-dimensional data (text classification).  
✅ Naturally handles multi-class problems.

**Disadvantages:**

❌ Naïve independence assumption is rarely true in practice.  
❌ Poor estimator of probabilities (scores, not calibrated).  
❌ Struggles with feature interactions.

**Applications:**
- Spam filtering
- Sentiment analysis
- Document classification
- Medical diagnosis

---

## **Section 4: Decision Trees**

> PYQ: Explain Decision Trees algorithm in ML and discuss its types. (2023, 15 marks)  
> PYQ: Explain Decision Trees by taking a suitable example. (2024, part of 15 marks)

### **4.1 What is a Decision Tree?**

**Definition:**

A **Decision Tree** is a tree-structured model where:
- Each **internal node** represents a test on a feature.
- Each **branch** represents the outcome of the test.
- Each **leaf node** represents a class label (classification) or a value (regression).

**Simple Analogy:**

Think of a decision tree like a **flowchart** or a **20-questions game** — at each step you ask a yes/no question and follow the appropriate branch until you reach an answer.

---

### **4.2 Structure of a Decision Tree**

```
                    [Outlook?]               ← Root Node
                   /    |    \
             Sunny/  Overcast\ Rain\
                /       |       \
        [Humidity?]  [Yes ✓]  [Wind?]      ← Internal Nodes
          /    \               /    \
       High   Normal       Strong  Weak
        /        \            |      |
     [No ✗]   [Yes ✓]    [No ✗] [Yes ✓]   ← Leaf Nodes
```

---

### **4.3 How to Build a Decision Tree — Key Concepts**

#### **Entropy (Measure of Impurity)**

**Definition:** Entropy measures the **impurity or disorder** in a dataset. A pure node (all same class) has entropy = 0.

**Formula:**

```
           c
H(S) = -  Σ  pᵢ × log₂(pᵢ)
          i=1

Where:
  S  = dataset
  c  = number of classes
  pᵢ = proportion of class i in S
```

**Examples:**

```
Pure node (all Yes):    H = -(1×log₂1) = 0
50-50 split:            H = -(0.5×log₂0.5 + 0.5×log₂0.5) = 1
```

---

#### **Information Gain (Choosing the Best Feature)**

**Definition:** Information Gain measures how much a feature **reduces entropy** (disorder). The feature with the **highest information gain** is chosen as the splitting node.

**Formula:**

```
IG(S, A) = H(S) - Σ [ |Sᵥ|/|S| × H(Sᵥ) ]
                 v∈A

Where:
  A  = feature being tested
  Sᵥ = subset where feature A = value v
```

---

#### **Gini Impurity (Alternative to Entropy)**

**Formula:**

```
          c
Gini = 1 - Σ pᵢ²
          i=1

Pure node: Gini = 0
50-50:     Gini = 1 - (0.5² + 0.5²) = 0.5
```

---

### **4.4 ID3 Algorithm**

**ID3 (Iterative Dichotomiser 3)** is the classic decision tree building algorithm using **Information Gain**.

**Steps:**

```
1. If all examples have same class → return leaf node with that class.
2. If no features left → return leaf with majority class.
3. Else:
   a. Calculate Information Gain for each feature.
   b. Select feature with highest IG as root.
   c. For each value of that feature:
      - Create a sub-branch.
      - Recursively apply steps 1–3 on the subset.
```

---

### **4.5 Worked Example — Entropy & Info Gain**

**Dataset (14 examples, 9 Yes, 5 No):**

```
Outlook:    Sunny(5):  2Yes, 3No
            Overcast(4): 4Yes, 0No
            Rain(5):   3Yes, 2No
```

**Step 1: Entropy of full dataset S:**
```
H(S) = -(9/14)×log₂(9/14) - (5/14)×log₂(5/14)
     = -(0.643×(-0.637)) - (0.357×(-1.485))
     = 0.410 + 0.530
     = 0.940
```

**Step 2: Entropy of each subset for Outlook:**
```
H(Sunny)    = -(2/5)log₂(2/5) - (3/5)log₂(3/5)
            = -(0.4×(-1.322)) - (0.6×(-0.737))
            = 0.529 + 0.442 = 0.971

H(Overcast) = -(4/4)log₂(4/4) = -(1×0) = 0.000   (pure node)

H(Rain)     = -(3/5)log₂(3/5) - (2/5)log₂(2/5)
            = 0.971
```

**Step 3: Information Gain for Outlook:**
```
IG(S, Outlook) = H(S) - [5/14×H(Sunny) + 4/14×H(Overcast) + 5/14×H(Rain)]
               = 0.940 - [5/14×0.971 + 4/14×0 + 5/14×0.971]
               = 0.940 - [0.347 + 0 + 0.347]
               = 0.940 - 0.694
               = 0.246
```

If Outlook has the highest IG among all features → it becomes the **root node**.

---

### **4.6 Types of Decision Tree Algorithm**

> PYQ: Explain Decision Trees algorithm in ML and discuss its types. (2023, 15 marks)

Based on the **type of target variable** they predict, decision trees fall into **two main categories**:

#### **(1) Classification Tree**

A **Classification Tree** is used to classify data into **discrete classes or categories**.

- **Target variable:** **categorical** (e.g., Yes/No, Spam/Not Spam, Cat/Dog/Bird).
- **Splitting criterion:** **Information Gain** (entropy) or **Gini Impurity** — picks the feature that produces the purest class split.
- **Leaf node output:** a **class label** (the majority class in that leaf).
- **Examples:**
  - Email → Spam or Not Spam
  - Tumour → Malignant or Benign
  - Loan applicant → Approve or Reject

```
        [Outlook?]
        /    |    \
   Sunny  Overcast  Rain
     │       │       │
   [No]    [Yes]   [Yes]      ← leaf = class label
```

#### **(2) Regression Tree**

A **Regression Tree** is used to predict a **continuous numerical value** instead of a class.

- **Target variable:** **continuous** (e.g., price, temperature, age).
- **Splitting criterion:** **Variance reduction** (or Mean Squared Error) — picks the feature that minimizes prediction error in the children.
- **Leaf node output:** a **numerical value** (typically the **mean** of all training samples in that leaf).
- **Examples:**
  - Predict house price from size, location, rooms.
  - Predict daily temperature from humidity, pressure.
  - Predict student marks from study hours.

```
        [Size > 1500 sqft?]
         /              \
       Yes               No
        │                 │
   [Price ≈ 80L]    [Size > 800 sqft?]
                       /        \
                     Yes         No
                      │           │
                 [Price ≈ 50L] [Price ≈ 25L]
```

#### **Classification Tree vs Regression Tree**

| Aspect | Classification Tree | Regression Tree |
|---|---|---|
| **Target variable** | Categorical (discrete) | Continuous (numerical) |
| **Output at leaf** | Class label (majority vote) | Numerical value (mean / median) |
| **Splitting criterion** | Information Gain / Gini Impurity | Variance Reduction / MSE |
| **Use case** | Spam detection, tumour classification | House price, temperature prediction |
| **Evaluation metric** | Accuracy, Precision, Recall, F1 | MSE, RMSE, MAE, R² |

> The combined family is also called **CART (Classification and Regression Trees)** — a single algorithm that supports both modes depending on the target type.

---

### **4.7 Overfitting and Pruning**

- A decision tree can grow too deep and **overfit** (memorize training data).
- **Pruning** cuts unnecessary branches:
  - **Pre-pruning:** Stop growing when improvement is small.
  - **Post-pruning:** Grow full tree, then remove low-value branches.

---

### **4.8 Advantages and Disadvantages**

**Advantages:**

✅ Easy to understand and visualize.  
✅ No need for feature scaling.  
✅ Handles both numerical and categorical data.  
✅ Implicitly performs feature selection.

**Disadvantages:**

❌ Prone to **overfitting** (especially deep trees).  
❌ Unstable — small changes in data can change the tree.  
❌ Biased toward features with more values.

**Applications:**
- Medical diagnosis
- Credit risk scoring
- Fraud detection
- Customer segmentation

---

## **Section 5: Linear Regression**

> PYQ: Explain Linear Regression. (2022, 2.5 marks)  
> PYQ: Explain regression with an example. (2022, 7.5 marks)

### **5.1 What is Linear Regression?**

**Definition:**

**Linear Regression** is a supervised learning algorithm used for **regression** (predicting continuous values). It models the relationship between input features (X) and the output (Y) as a **straight line (linear equation)**.

---

### **5.2 The Linear Equation**

**Simple Linear Regression (one feature):**

```
Ŷ = w₀ + w₁X

Where:
  Ŷ  = predicted value
  X  = input feature
  w₀ = intercept (bias) — where the line crosses Y-axis
  w₁ = slope (weight) — how much Y changes per unit of X
```

**Multiple Linear Regression (n features):**

```
Ŷ = w₀ + w₁X₁ + w₂X₂ + ... + wₙXₙ

Or in matrix form:
Ŷ = Xw
```

**Diagram:**

```
  Y
  │           /
  │         /  ← Regression Line (Ŷ = w₀ + w₁X)
  │       / ●
  │     /●
  │   /   ●
  │ /  ●
  │/●
  └────────────→ X
```

---

### **5.3 Cost Function — Mean Squared Error (MSE)**

We measure how well the line fits using **Mean Squared Error**:

```
         1   m
MSE  =  ─── Σ (yᵢ - ŷᵢ)²
         m  i=1

Where:
  yᵢ  = actual value
  ŷᵢ  = predicted value
  m   = number of samples
```

The goal of training is to **minimize MSE** by finding the best values of w₀ and w₁.

---

### **5.4 Finding Optimal Weights**

#### **Method 1: Ordinary Least Squares (Closed-form)**

```
Analytical solution:
  w = (XᵀX)⁻¹ Xᵀy
```

Best for small datasets with few features.

#### **Method 2: Gradient Descent (Iterative)**

```
Repeat until convergence:

  w₀ := w₀ - α × ∂MSE/∂w₀
  w₁ := w₁ - α × ∂MSE/∂w₁

Where α = learning rate

Partial derivatives:
  ∂MSE/∂w₀ = (-2/m) Σ(yᵢ - ŷᵢ)
  ∂MSE/∂w₁ = (-2/m) Σ(yᵢ - ŷᵢ)×xᵢ
```

---

### **5.5 Worked Example**

**Data:**

| X (hours studied) | Y (marks) |
|-------------------|-----------|
| 1 | 50 |
| 2 | 60 |
| 3 | 70 |
| 4 | 80 |

**Using formulas:**
```
n = 4
ΣX  = 1+2+3+4 = 10
ΣY  = 50+60+70+80 = 260
ΣXY = (1×50)+(2×60)+(3×70)+(4×80) = 50+120+210+320 = 700
ΣX² = 1+4+9+16 = 30

w₁ = (nΣXY - ΣXΣY) / (nΣX² - (ΣX)²)
   = (4×700 - 10×260) / (4×30 - 100)
   = (2800 - 2600) / (120 - 100)
   = 200 / 20
   = 10

w₀ = (ΣY - w₁ΣX) / n
   = (260 - 10×10) / 4
   = (260 - 100) / 4
   = 40

Equation:  Ŷ = 40 + 10X

Predict for X=5:  Ŷ = 40 + 10×5 = 90 marks
```

---

### **5.6 Advantages and Disadvantages**

**Advantages:**

✅ Simple and fast.  
✅ Easily interpretable (slope tells effect of each feature).  
✅ Works well when relationship is truly linear.

**Disadvantages:**

❌ Assumes a linear relationship (fails on non-linear data).  
❌ Sensitive to outliers.  
❌ Assumes features are independent (multicollinearity hurts it).

---

## **Section 6: Logistic Regression**

> PYQ: Explain Logistic Regression. (2023, 2.5 marks)

### **6.1 What is Logistic Regression?**

**Definition:**

**Logistic Regression** is a supervised learning algorithm used for **binary classification** (output is 0 or 1). Despite the name, it is a **classification** algorithm, not regression.

It models the **probability** that an input belongs to a class using the **sigmoid function**.

---

### **6.2 The Sigmoid Function**

```
         1
σ(z) = ──────────
        1 + e^(-z)

Where:
  z = w₀ + w₁X₁ + w₂X₂ + ... = linear combination of inputs

Output: always between 0 and 1 (interpreted as probability)
```

---

### **6.3 Decision Rule**

```
        ┌ 1  (Class 1)  if P(Y=1|X) ≥ 0.5   [i.e., z ≥ 0]
Ŷ  =   │
        └ 0  (Class 0)  if P(Y=1|X) < 0.5   [i.e., z < 0]
```

The **decision boundary** is the line where z = 0.

---

### **6.4 Cost Function — Log Loss (Binary Cross-Entropy)**

```
J(w) = -(1/m) Σ [yᵢ log(ŷᵢ) + (1-yᵢ) log(1-ŷᵢ)]

Where:
  yᵢ  = actual label (0 or 1)
  ŷᵢ  = predicted probability
```

Weights are updated using **gradient descent** to minimize J(w).

---

### **6.5 Linear Regression vs Logistic Regression**

| Feature | Linear Regression | Logistic Regression |
|---------|-------------------|---------------------|
| **Task** | Regression | Classification |
| **Output** | Continuous value | Probability (0–1) |
| **Function** | Linear (y = wx + b) | Sigmoid (σ(z)) |
| **Loss** | MSE | Log Loss |
| **Decision** | No threshold | Threshold at 0.5 |
| **Example** | Predict house price | Predict spam or not |

---

### **6.6 Advantages and Disadvantages**

**Advantages:**

✅ Probabilistic output (useful for confidence scores).  
✅ Fast to train and predict.  
✅ Easy to interpret with feature weights.  
✅ Works well for linearly separable data.

**Disadvantages:**

❌ Assumes linear decision boundary.  
❌ Fails on complex, non-linear problems.  
❌ Sensitive to outliers and correlated features.

**Applications:**
- Email spam detection
- Disease prediction (diabetes, cancer risk)
- Credit approval
- Customer churn prediction

---

## **Section 7: Support Vector Machines (SVM)**

> PYQ: What is the goal of the Support Vector Machine (SVM)? Also discuss the margin. (2022, 15 marks)  
> PYQ: Support Vectors. (2023, 2.5 marks)

### **7.1 What is SVM?**

**Definition:**

A **Support Vector Machine (SVM)** is a supervised learning algorithm that finds the **best hyperplane** (decision boundary) that **maximally separates** the two classes.

**Key Idea:** Don't just find any line that separates classes — find the one with the **largest margin** (gap) between classes.

---

### **7.2 Key Concepts**

#### **Hyperplane**

A **hyperplane** is a decision boundary that separates two classes.
- In 2D: a **line**.
- In 3D: a **plane**.
- In n-D: a **hyperplane**.

**Equation:**

```
w·x + b = 0

Where:
  w = weight vector (normal to hyperplane)
  x = input feature vector
  b = bias
```

---

#### **Support Vectors**

**Support Vectors** are the **data points closest to the hyperplane** (from each class). They are the critical points — they "support" or define the hyperplane.

---

#### **Margin**

The **margin** is the total distance between the two parallel boundary lines (one touching each class's closest points).

```
       Margin
      ←──────→
───────────────────   ← Upper boundary  (w·x + b = +1)
                  ●
    ●  ●  ●
──────────────────── ← Optimal Hyperplane  (w·x + b = 0)
         ■  ■  ■
              ■
───────────────────   ← Lower boundary  (w·x + b = -1)

● = Class +1    ■ = Class -1
```

**Margin width:**

```
        2
M  =  ─────
       ||w||
```

SVM maximizes **M** → minimizes ||w||.

---

### **7.3 Hard Margin vs Soft Margin**

| | Hard Margin SVM | Soft Margin SVM |
|--|-----------------|-----------------|
| **Assumption** | Data is perfectly separable | Allows some misclassifications |
| **Constraint** | All points outside margin | Some points can be inside margin |
| **Parameter** | None | C (penalty parameter) |
| **Sensitivity** | Very sensitive to outliers | More robust |

**C parameter (regularization):**
- **High C** → Small margin, fewer errors on training data (risk of overfit).
- **Low C** → Wide margin, allows more errors (better generalization).

---

### **7.4 The Kernel Trick**

**Problem:** Data is not always linearly separable in the original feature space.

**Solution:** The **kernel trick** maps data to a **higher-dimensional space** where it becomes separable, without explicitly computing the transformation.

```
Original 2D space         Higher-dimensional space
   (not separable)            (separable)
       ●●  ■■                 ●  ●
     ■    ●   ■      ────►        ─────────
       ●●  ■■               ■  ■
```

**Common Kernels:**

| Kernel | Formula | Use Case |
|--------|---------|----------|
| **Linear** | K(x,y) = xᵀy | Linearly separable data |
| **Polynomial** | K(x,y) = (xᵀy + c)ᵈ | Polynomial boundaries |
| **RBF / Gaussian** | K(x,y) = exp(-γ||x-y||²) | Most common, non-linear |
| **Sigmoid** | K(x,y) = tanh(αxᵀy + c) | Neural network-like |

---

### **7.5 SVM for Multi-Class**

SVM is inherently binary. Two strategies to extend it:
- **One-vs-One (OvO):** Train one SVM per pair of classes.
- **One-vs-All (OvA):** Train one SVM per class vs all others.

---

### **7.6 Advantages and Disadvantages**

**Advantages:**

✅ Works well with **high-dimensional** data.  
✅ Effective when number of features > number of samples.  
✅ Memory efficient (only support vectors matter).  
✅ Kernel trick handles non-linear problems.  
✅ Robust to overfitting (especially with soft margin).

**Disadvantages:**

❌ Slow on large datasets (quadratic programming).  
❌ Sensitive to feature scaling (needs normalization).  
❌ Choosing the right kernel and C is tricky.  
❌ Hard to interpret compared to Decision Trees.

**Applications:**
- Image classification
- Text and document categorization
- Bioinformatics (protein classification)
- Face detection

---

## **Quick Revision Points**

### **Algorithms at a Glance:**

| Algorithm | Type | Key Idea | Key Formula |
|-----------|------|----------|-------------|
| **k-NN** | Classification | Majority vote of k nearest neighbours | Euclidean distance |
| **Naïve Bayes** | Classification | Bayes theorem + independence assumption | P(C\|X) ∝ P(X\|C)P(C) |
| **Decision Tree** | Both | Split on highest info gain | IG = H(S) - ΣH(Sᵥ) |
| **Linear Regression** | Regression | Fit a line to minimize error | Ŷ = w₀ + w₁X |
| **Logistic Regression** | Classification | Sigmoid maps to probability | σ(z) = 1/(1+e^-z) |
| **SVM** | Both | Maximize margin between classes | Maximize 2/\|\|w\|\| |

### **Key Formulas:**

```
Euclidean Distance:   d = √[Σ(aᵢ-bᵢ)²]
Entropy:              H = -Σ pᵢ log₂(pᵢ)
Information Gain:     IG = H(S) - Σ|Sᵥ|/|S| H(Sᵥ)
Sigmoid:              σ(z) = 1 / (1 + e^(-z))
SVM Margin:           M = 2 / ||w||
Linear Regression:    Ŷ = w₀ + w₁X
MSE:                  (1/m) Σ(yᵢ - ŷᵢ)²
```

### **Classification vs Regression:**

| Algorithm | Classification | Regression |
|-----------|---------------|------------|
| k-NN | ✅ | ✅ |
| Naïve Bayes | ✅ | ❌ |
| Decision Tree | ✅ | ✅ |
| Linear Regression | ❌ | ✅ |
| Logistic Regression | ✅ | ❌ |
| SVM | ✅ | ✅ (SVR) |

---

## **Expected Exam Questions**

### **15-Mark Questions:**

1. What is the goal of the Support Vector Machine (SVM)? Also discuss the margin. *(2022)*
2. Explain Decision Trees algorithm in ML and discuss its types. *(2023)*
3. What are the basic assumptions used in Naive Bayes classifier? Why is it called Naive Bayes? Also discuss the working of Naive Bayes algorithm. *(2023)*
4. Define Supervised Learning and explain its working principle. Provide a step-by-step example of how a supervised learning algorithm processes training data and makes predictions. *(2024)*
5. Discuss the importance of labelled data in Supervised Learning and its role in training predictive models. Also, explain Decision Trees by taking a suitable example. *(2024)*

### **Short Answer Questions (2.5 marks):**

1. Explain Linear Regression. *(2022)*
2. Support Vectors. *(2023)*
3. K-NN is called Lazy Learner. Explain it. *(2023)*
4. Underfitting. *(2023)*
5. Logistic Regression. *(2023)*

### **Mixed (7.5 marks):**

1. Explain Naive Bayes Classifier. *(2022)*
2. Explain regression with an example. *(2022)*

---

_These notes were compiled by [Deepak Modi](https://deepakmodi.dev)_  
_Last updated: May 2026_
