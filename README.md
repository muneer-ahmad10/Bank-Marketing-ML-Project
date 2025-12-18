# Bank-Marketing-ML-Project
Data Preprocessing &amp; Feature Engineering Report

# 📊 Bank Marketing ML Project – Data Preprocessing & Feature Engineering Report

## 📌 Project Overview

This project focuses on preparing the **Bank Marketing dataset** for machine learning by applying correct **data cleaning, feature selection, encoding, and transformation techniques**. The goal is to build a **leakage-free, production-ready preprocessing pipeline** suitable for real-world ML models.

---

## 🎯 Objective

* Remove leaky and redundant features
* Handle multicollinearity
* Encode categorical variables correctly
* Prevent data leakage
* Prepare model-ready numerical data

---

## 🗂 Dataset Description

The dataset contains customer information, campaign details, and macroeconomic indicators collected during a bank’s direct marketing campaigns.

**Target Variable:**

* `y` → Whether the client subscribed to a term deposit (`yes` / `no`)

---

## 🧹 Feature Selection & Column Dropping

### ❌ Dropped Feature

* **`duration`**

  * Reason: **Data Leakage**
  * The call duration is only known *after* the call ends and cannot be used for real-time prediction.

### ❌ Dropped Highly Correlated Features

Based on correlation analysis:

* `nr.employed`
* `cons.price.idx`

These variables were highly correlated with other macroeconomic indicators and added redundant information.

---

## 📊 Final Feature Set

### 🔢 Numerical Features

* `age`
* `campaign`
* `pdays`
* `previous`
* `cons.conf.idx`
* `euribor3m`

### 🔠 Categorical Features

* `job`
* `marital`
* `education`
* `housing`
* `loan`
* `contact`
* `month`
* `poutcome`

---

## 🧠 Feature Engineering Strategy

> **Note:** A full `Pipeline` was not used in this project. Instead, a `ColumnTransformer` was applied directly after the train–test split to keep preprocessing explicit and easy to understand.

### 1️⃣ Ordinal Encoding

Applied to the `education` column due to its inherent order:

```
university.degree > professional.course > high.school > basic.9y > basic.6y > basic.4y > illiterate > unknown
```

Used **OrdinalEncoder** with explicitly defined category order.

---

### 2️⃣ One-Hot Encoding

Applied to nominal categorical variables using **OneHotEncoder** with:

* `handle_unknown='ignore'`
* `drop='first'` to avoid dummy variable trap

---

### 3️⃣ ColumnTransformer

A **ColumnTransformer** was used directly (without wrapping it inside a Pipeline) to apply different transformations to different feature groups.

This approach was chosen to:

* Keep preprocessing steps transparent
* Avoid abstraction while learning core ML concepts
* Explicitly control `fit` and `transform` on train and test data

The transformer was **fitted only on training data** and applied to test data separately, ensuring no data leakage.

---

## 🔀 Train-Test Split

The dataset was split **before fitting any transformer** using the following configuration:

* **70% Training data**
* **30% Testing data** (`test_size = 0.3`)
* Stratified on the target variable to preserve class distribution

This ensured that preprocessing decisions were learned only from training data and prevented information leakage from the test set.

---

## 🎯 Target Encoding

The target variable `y` was encoded using **LabelEncoder**:

```
no  → 0
yes → 1
```

Encoding was fitted **only on training data** and applied to the test set.

---

## ✅ Final Preprocessing Checklist

✔ Leaky feature removed (`duration`)
✔ Multicollinearity handled
✔ Correct encoding strategies applied
✔ Train-test leakage prevented
✔ Model-ready numerical dataset created

---

## 🚀 Next Steps

* Train baseline models (Logistic Regression)
* Try tree-based models (Random Forest, Gradient Boosting)
* Handle class imbalance
* Evaluate using ROC-AUC, Precision, Recall, and Confusion Matrix

---

## 🧠 Key Learning

> *Feature engineering is not about writing more code, but about making correct data decisions.*

---

📌 **This preprocessing pipeline is suitable for both academic submission and real-world ML deployment.**


