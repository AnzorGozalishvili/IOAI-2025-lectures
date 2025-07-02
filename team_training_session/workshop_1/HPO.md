
# 🧠 HPO Workshop Plan for IOAI 2025

### 🎯 Goal:
Equip students with practical, strategic, and in-depth knowledge of hyperparameter optimization (HPO) for improving ML/DL model performance in competition environments like IOAI 2025.

---

## 📋 Workshop Structure

---

## 1️⃣ What is HPO?

### ✅ Key Concepts to Explain:
- **Definition**: Tuning the model's external settings (hyperparameters) to improve its performance.
- **Hyperparameters**: Set before training (e.g., learning rate, batch size, depth).
- **Model parameters**: Learned from data during training (e.g., weights in a neural net).
- **Why it matters**: Good HPO can significantly boost performance — especially when feature engineering has plateaued.

### 🧠 Quick Warm-Up Talking Points:
- HPO **consumes too much compute** on large DL models.
- **Classical ML models** expose many sensitive hyperparameters.
- **Deep Learning models** are more robust and benefit more from **data-centric improvements**.
- **DL HPO is pipeline-based** (batch size, learning rate), while **Classical ML is model-based** (max_depth, n_estimators).
- Classical ML models **must complete full runs** — no step-wise feedback like backprop in DL.

---

## 2️⃣ HPO on Classical ML Models (scikit-learn)

### 🧭 Step-by-Step:

#### 🔍 1. Identify Hyperparameters
- Use model documentation
- Examples:
  - RandomForest: `n_estimators`, `max_depth`, `min_samples_split`
  - SVM: `C`, `kernel`, `gamma`

#### 🎯 2. Select Important Ones
- Focus on the **most sensitive** ones (use prior experience or domain intuition)

#### 📦 3. Define Search Space
- Use appropriate scale:
  - Linear: `[10, 50, 100]`
  - Log: `[1e-4, 1e-3, 1e-2]`
  - Categorical: `['gini', 'entropy']`

#### ⏱️ 4. Estimate Compute and Time
- Multiply number of trials × training time per model

#### 🔁 5. Define Search Strategy
- Grid Search (exhaustive)
- Random Search (fast baseline)
- **Bayesian Optimization** (Optuna preferred)

#### 🧰 6. Choose Tools & Libraries
- `GridSearchCV`, `RandomizedSearchCV`
- ✅ Recommended: `Optuna`, `Hyperopt` for flexible, efficient tuning

#### 🔍 7. Validation Strategy
- Use **StratifiedKFold** for classification
- Avoid data leakage and overfitting to CV

#### 🚀 8. Run HPO
- Use reproducibility (random seed)
- Limit trial count, monitor time

#### 📈 9. Analyze Results
- Optuna dashboards or `study.best_trial`
- Plot learning curves, sensitivity analysis

#### 🏆 10. Retrain Final Model
- Use best parameters on full training set
- Validate on hold-out if available

---

## 3️⃣ HPO on Deep Learning Models (PyTorch)

### 🧭 Step-by-Step:

#### 🔍 1. Identify Hyperparameters
| Type             | Examples                                |
|------------------|------------------------------------------|
| Architecture     | dropout rate, hidden size               |
| Optimization     | learning rate, weight decay             |
| Data pipeline    | batch size, augmentation                |
| Training control | epochs, early stopping patience         |

#### 🎯 2. Select Important Ones
- Especially: `learning_rate`, `dropout`, `batch_size`, `optimizer`

#### 📦 3. Define Search Space
- Log scale for learning rate
- Float for dropout
- Categorical for batch size or optimizer

#### ⏱️ 4. Estimate Compute/Time
- Use:
  - Small datasets (e.g. MNIST)
  - Small models (MLP, shallow CNN)
  - Limited epochs (e.g. 3–5 per trial)

#### 🔁 5. Define Search Strategy
- Use **Bayesian Optimization** (Optuna)
- Support pruning and custom objective metrics

#### 🧰 6. Choose Tools
- ✅ Recommended: **Optuna**
- Also viable: Ray Tune, Ax

#### 🔍 7. Validation Strategy
- Hold-out split (e.g. 80/20)
- Fixed `random_seed` for reproducibility

#### 🚀 8. Run HPO
- Optuna `study.optimize()`
- Log metrics, possibly use `wandb` or `TensorBoard`

#### 📈 9. Analyze Results
- Use:
  - `optuna.visualization.plot_optimization_history`
  - `study.best_trial`

#### 🏆 10. Retrain Best Model
- Use best config
- Run full training (with early stopping)

---

## 🔧 4️⃣ Tools & Libraries

| Tool                   | Search Type         | Easy to Use | Control | Competition Grade |
|------------------------|---------------------|-------------|---------|-------------------|
| GridSearchCV (sklearn) | Grid Search         | ✅✅        | ❌      | ⚠️ Too slow       |
| RandomizedSearchCV     | Random Search       | ✅✅        | ❌      | ⚠️ Limited        |
| Optuna                 | Bayesian Optimization | ✅✅✅    | ✅✅✅  | ✅✅✅             |
| Ray Tune               | Distributed/Bayesian | ✅✅        | ✅✅    | ✅✅              |

---

## 🏁 5️⃣ Best Practices for AI Competitions

- 🧪 Start with baseline models + minimal tuning
- 🎯 Focus on high-impact hyperparameters first
- 🛑 Use early stopping & pruning for bad trials
- 🧠 Don’t overfit to validation — use final hold-out
- 🧵 Track everything (logs, trials, metrics)
- 🕹️ Budget time: estimate total trial cost
- 🧬 Fix random seeds for repeatability
- 📊 Visualize: Optuna dashboards, SHAP, etc.
