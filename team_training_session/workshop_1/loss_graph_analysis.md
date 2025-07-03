
# 📉 Loss Graph Analysis Scenarios

Understand how to interpret training/validation loss curves and troubleshoot model behavior effectively.

---

## 🧪 Loss Values Outside Expected Range

**Symptoms:**  
Loss curve values are too high or too low, or don’t match manual calculations.

**Causes:**  
- Logging error or incorrect loss calculation  
- Log scale errors  
- Incorrect target or activation used  
- Masking errors (e.g., padding not ignored)

**Fixes:**  
- Manually compute min/max expected loss and compare  
- Assert loss value ranges early in training  
- Use consistent loss functions and data shapes

---

## 🚀 Loss Has Big Jumps (High Learning Rate)

**Symptoms:**  
Loss curve has sharp, irregular spikes, can't converge.

**Causes:**  
- Learning rate too high  
- Model overshooting local minima  
- Inability to fit tight regions in the loss landscape

**Fixes:**  
- Reduce learning rate  
- Use learning rate schedulers  
- Use a warm-up phase or gradient clipping

---

## 🔁 High Variance in Loss Surface

**Symptoms:**  
Frequent local fluctuations in loss, not decreasing smoothly.

**Causes:**  
- Inconsistent batches  
- High variance in data or gradient flow  
- Batch size too small

**Fixes:**  
- Use BatchNorm or LayerNorm  
- Increase batch size  
- Smooth loss plot using moving averages

---

## ⚠️ Validation Loss Better Than Training Loss

**Symptoms:**  
Validation loss lower than training loss.

**Causes:**  
- Data leakage (validation samples in train set)  
- Outliers or noisy samples in training set

**Fixes:**  
- Double-check data splits  
- Clean or analyze training data  
- Remove or cap outliers

---

## ✅ Training Loss Slightly Higher Than Validation Loss

**Symptoms:**  
Train loss slightly above val loss, both decreasing steadily.

**Causes:**  
- Normal regularization effect  
- Dropout only applied during training

**Fixes:**  
- No action needed — likely good generalization  
- Can fine-tune regularization if needed

---

## 🚨 Training Loss Low, Validation Loss High (Dynamic)

**Symptoms:**  
Training loss decreases well, but validation loss stagnates or increases.

**Causes:**  
- Overfitting to training data  
- Low data diversity or information leakage  
- Duplicates or non-representative validation data

**Fixes:**  
- Add data augmentation  
- Use regularization (dropout, weight decay)  
- Use early stopping  
- Increase validation size

---

## ❗ Both Losses Are High

**Symptoms:**  
Training and validation losses are both high and not improving.

**Causes:**  
- Model is underfitting  
- Learning rate too low  
- Model architecture too shallow  
- Dataset too difficult or imbalanced

**Fixes:**  
- Increase model capacity  
- Raise learning rate  
- Train on a smaller subset to verify learnability  
- Check for bugs in pipeline or loss computation

---

## ❌ Loss Flatlines at High Value

**Symptoms:**  
Loss stays constant (e.g., ~0.69 for BCE) across epochs.

**Causes:**  
- Output activation mismatch (e.g. using sigmoid + cross entropy)  
- Frozen model weights  
- Learning rate too small

**Fixes:**  
- Check loss function and model output compatibility  
- Unfreeze layers  
- Increase learning rate

---

## 💥 Loss Explodes (NaN or INF)

**Symptoms:**  
Loss suddenly becomes NaN or inf.

**Causes:**  
- Numerical instability  
- Very high learning rate  
- Bad initialization or log(0)/div by 0

**Fixes:**  
- Use gradient clipping  
- Normalize input data  
- Lower the learning rate

---

## 📉 Spiky Loss with Small Batches

**Symptoms:**  
Loss varies sharply per step, even if trending down.

**Causes:**  
- Small batch size (high variance gradients)

**Fixes:**  
- Use larger batch size  
- Smooth loss curve with moving average  
- Don’t overinterpret each step

---

## 🧩 Validation Loss Stalls While Training Improves

**Symptoms:**  
Train loss improves, val loss flat or rises.

**Causes:**  
- Overfitting  
- Distribution mismatch  
- Training data too easy compared to val

**Fixes:**  
- Early stopping  
- Increase validation size  
- Improve validation diversity
