
# 🏗️ Feature Engineering & Feature Selection

These two concepts are tightly related and often work hand-in-hand. The goal in both is to **make the input data more informative** and **increase model performance** by improving its ability to extract signal from features.

---

## 📌 1. Feature Engineering

**Definition:**  
Feature engineering is the process of transforming raw data into meaningful inputs that help a model better predict the target variable.

⚠️ Note: While data augmentation (e.g., image flips or synonym replacement) enriches datasets, it's typically not called feature engineering. Augmentation generates more training samples, whereas feature engineering transforms or refines features in-place.

---

### 🎯 Goals of Feature Engineering
- Make the signal in features easier to capture
- Reduce noise and redundancy
- Match model assumptions (linearity, scale, type)
- Encode domain knowledge

---

### 🧰 Common Techniques

#### 1. Drop Useless or Redundant Features
- Remove constant columns or identifiers (e.g., IDs)
- Drop high-missing or low-variance features
- Remove duplicate columns

#### 2. Convert to Correct Data Types
- Categorical ↔️ numerical (e.g., `pd.Categorical`, `LabelEncoder`)
- Date → datetime object → extract weekday, hour, etc.
- Parse strings into structured features (e.g., parse "2023-01-01" into Y/M/D)

#### 3. Derive New Features (Type 1 - Semantic Extraction)
- From existing features: e.g., extract domain from email, region from ZIP code
- Requires domain understanding and creativity

#### 4. Derive New Features (Type 2 - Transformations)
- Apply math transforms: `log(x+1)`, `sqrt(x)`, `1/x` for skew correction
- Normalize (StandardScaler, MinMaxScaler)
- Quantize into bins

#### 5. Feature Aggregation / Compression
- Combine features: ratios, diffs, sums (e.g., `price_per_unit`)
- Use dimensionality reduction (PCA, t-SNE, UMAP for visualization)
- Embed categorical features (e.g., Target Encoding)

#### 6. Imputation (Filling Missing Values)
- When missing data is ~5–10% in a feature
- Simple imputation:
  - Mean or median (for numeric)
  - Mode or random sample (for categorical)
- Advanced imputation:
  - Train a model using other features (excluding the target) to predict missing values
  - Use model as a feature-specific imputer and predict missing values like a test set

---

## 🧠 Connection to EDA

EDA (Exploratory Data Analysis) drives feature engineering:
- Univariate & multivariate analysis → discover strong/weak signals
- Visual inspection reveals noise, scaling issues
- Correlation matrix points to redundancy
- Clustering or class overlap may motivate feature creation

---

## 📌 2. Feature Selection

**Definition:**  
Feature selection is the process of identifying the most relevant subset of features to use in modeling.

🎯 Goal: Reduce dimensionality while maximizing predictive performance. It helps:
- Reduce overfitting
- Shorten training time
- Improve model interpretability

---

### 🧮 Common Techniques

#### 🔗 1. Correlation-Based Filtering
- Select features with high absolute correlation with target
- Drop highly collinear features (e.g., corr > 0.95 with another feature)
- Use mutual information for nonlinear relationships

#### 🔀 2. Greedy Techniques: Forward / Backward Selection
- Forward: Add features one by one, retain those improving validation metric
- Backward: Start with all features, remove one at a time
- Greedy: Doesn’t handle feature interactions or synergy well

#### 📊 3. Model-Based Selection
- Train models and use `.feature_importances_` (e.g., tree-based models)
- Coefficient magnitudes in linear/logistic regression
- Use regularized models (Lasso/Ridge) to enforce sparsity

#### 🌐 4. SHAP Values (Best-in-Class)
- Considers **interactions between features**
- Estimates contribution of each feature per sample
- **Model-agnostic** or **model-specific**
- Works well for both feature understanding and selection

#### 🧪 5. Permutation Importance
- Measures drop in model performance when a feature is shuffled
- Simple, interpretable, model-agnostic
- Slower than built-in methods

---

## 🧠 Feature Engineering vs Feature Selection

| Aspect              | Feature Engineering                                | Feature Selection                      |
|---------------------|----------------------------------------------------|----------------------------------------|
| Goal                | Improve data representation                        | Choose the most informative subset     |
| Based on            | Domain knowledge + statistics                      | Predictive power evaluation            |
| Output              | New/cleaned features                               | Subset of original or engineered ones  |
| Tied to EDA         | Strongly                                           | Strongly                               |
| Tools               | Transformations, embeddings, PCA                   | SHAP, permutation, recursive selection |

---

## ✅ Summary

- Feature engineering makes features **more learnable**.
- Feature selection picks **which features to keep**.
- Both are crucial, especially in classical ML.
- In deep learning, manual feature engineering is rare — but feature selection still matters in tabular DL and NLP preprocessing pipelines.
