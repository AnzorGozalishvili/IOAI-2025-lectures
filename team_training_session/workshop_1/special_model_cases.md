
# ⚖️ Special Cases in Model Optimization

This section covers nuanced, less frequently discussed situations that can strongly influence model quality and reliability.

---

## 🧭 1. Model Calibration

### What is it?

Model calibration refers to adjusting the predicted **probabilities** so they better reflect actual likelihoods. Especially relevant for classification problems with:

- Imbalanced datasets  
- Threshold-sensitive metrics (e.g., F1, precision, recall)  
- Real-world decision boundaries where "confidence" matters (e.g., medical risk, fraud)

---

### 🚨 Symptoms of Miscalibrated Model

- Model always predicts high probabilities for one class  
- Predicted class probabilities don’t match actual frequencies  
- F1 is low despite decent accuracy  
- ROC-AUC is high but threshold-based metrics (precision/recall) are poor

---

### 🧪 Techniques

#### ➤ Post-hoc Calibration:
- **Platt Scaling** (logistic regression on logits)
- **Isotonic Regression** (non-parametric)
- **Beta Calibration** (better for imbalanced sets)

Use `sklearn.calibration.CalibratedClassifierCV`

#### ➤ Threshold Tuning:
- Adjust decision threshold (`y_pred > t`) based on validation set  
- Optimize threshold for F1, precision, recall, etc.

#### ➤ Custom Loss or Sampling:
- Use Focal Loss for imbalance  
- Resample minority class or apply class weights during training

---

## 📈 2. Non-Normal Target Distributions (Regression)

### Problem

Many regression models assume target values follow a roughly normal distribution. If your target is:

- Log-normal (e.g., incomes, time durations)
- Heavy-tailed (e.g., extreme event probabilities)
- Truncated (e.g., percentages, rates)

... then you may need to transform it or use a specialized loss.

---

### ⚠️ When to Transform the Target?

Use transformations when:
- Skewness > ±1 (log, sqrt, Box-Cox)
- Outliers dominate training
- Variance of error grows with magnitude of target (heteroscedasticity)

#### Common Transformations:
- `log(y + 1)` → use inverse transform at inference time
- `Box-Cox` (parametric)
- `QuantileTransformer` → robust to outliers

---

### 🧠 Alternative: Use Different Loss Function

If transformation hurts interpretability or causes mismatch, use:

| Distribution | Suggested Loss Function |
|--------------|-------------------------|
| Normal       | MSE                     |
| Skewed       | MAE or Huber Loss       |
| Poisson      | Poisson loss            |
| Count Data   | Negative Binomial loss  |
| Probabilistic | CRPS, quantile loss     |

💡 In probabilistic forecasting (e.g., estimating intervals), use quantile regression or pinball loss.

---

## 🧩 Summary Table

| Problem                        | Solution                                 |
|-------------------------------|------------------------------------------|
| Class imbalance, poor F1      | Calibrate with Platt/Isotonic, tune threshold |
| Probabilities misaligned      | Post-hoc calibration, retrain with class weights |
| Target heavily skewed         | Log/Box-Cox transform, or MAE loss       |
| Outliers dominate regression  | Huber loss or quantile loss              |
| Count or rate targets         | Use Poisson/Negative Binomial loss       |
