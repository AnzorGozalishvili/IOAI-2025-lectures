
# 🧠 Diagnosing and Curing Overfitting & Underfitting

---

## 🔴 Overfitting

Overfitting occurs when a model learns not just the underlying patterns in the training data, but also the noise. This leads to excellent training performance, but poor generalization to unseen data.

---

### 🔍 How to Identify Overfitting

**Most Common: Loss Graph Analysis**
- Training loss continues to decrease
- Validation loss stops decreasing or increases after a certain point

**Other Signs:**
- High variance between train and validation accuracy
- Large performance drop on test/validation sets
- Perfect predictions on training set, erratic predictions elsewhere
- Very low training loss, but poor real-world accuracy

---

### 🧰 Curing Overfitting

#### 🔢 Classical ML — Model Too Complex

**Symptoms:**  
Model performs well on training, poorly on validation. Classical models with too many parameters.

**Fixes:**  
- Reduce model complexity (simpler models, regularization)
- Limit tree depth, reduce estimators
- Use regularization (L1, L2)

---

#### 🔍 Classical ML — Simple Dataset

**Symptoms:**  
Many samples, but few informative features. High similarity between samples.

**Fixes:**  
- Use PCA or LDA to reduce feature dimensionality
- Use smaller models that generalize better
- Avoid overfitting by aligning model size with feature space

---

#### 🤖 Deep Learning — Regularization Needed

**Symptoms:**  
Training loss very low, validation loss high.

**Fixes:**  
- Increase dropout
- Add L2 regularization (weight decay)
- Use label smoothing
- Apply early stopping and gradient clipping

---

#### 🎨 Deep Learning — Low Data Complexity

**Symptoms:**  
Training set is easily fit, model does not generalize.

**Fixes:**  
- Apply data augmentation (flipping, cropping, replacements)
- Use synthetic data if applicable
- Mixup or CutMix for vision tasks

---

#### 🧱 Deep Learning — Model Too Large

**Symptoms:**  
Overfitting even with regularization.

**Fixes:**  
- Reduce number of layers or filters
- Use smaller architectures (MobileNet, DistilBERT)
- Freeze layers during fine-tuning

---

#### 🔁 Deep Learning — Fine-tuning Pretrained Models

**Symptoms:**  
Rapid overfitting even on large datasets.

**Fixes:**  
- Use early stopping
- Save checkpoints per epoch
- Select best checkpoint based on validation score
- Use layer-wise learning rate control

---

#### 🔬 Any Model — Error Analysis

**Strategy:**  
- Compare easy and hard samples
- Investigate misclassifications
- Check class distribution

**Fixes:**  
- Remove label noise
- Improve features
- Augment underrepresented cases

---

## 🔵 Underfitting

Underfitting happens when the model fails to capture the underlying patterns in the data. This results in both high training and validation loss.

---

### 🔍 How to Identify Underfitting

**Symptoms:**
- High training and validation loss
- Loss plateaus early
- Low accuracy on both sets
- Predictions converge to mean

---

### 🧰 Curing Underfitting

#### 🔢 Classical ML — Model Too Simple

**Symptoms:**  
Low-capacity models can't reduce error even with lots of data.

**Fixes:**  
- Use more complex models (ensemble, boosting, SVMs)
- Add polynomial features or kernel transformations

---

#### 🧠 Classical ML — Weak Feature Set

**Symptoms:**  
More complex models don't help.

**Fixes:**  
- Perform feature-target correlation
- Engineer new features
- Use domain knowledge
- Extract text/image metadata where relevant

---

#### 🧱 Deep Learning — Model Too Small / Over-Regularized

**Symptoms:**  
Training and validation loss plateau at high value.

**Fixes:**  
- Reduce dropout
- Reduce L2 weight decay
- Add more layers or units
- Ensure no layers are frozen unintentionally

---

#### 🏷️ Deep Learning — Label or Data Problem

**Symptoms:**  
Model fails to learn even with sufficient capacity.

**Fixes:**  
- Manually inspect labels
- Try overfitting on one batch
- Use curriculum learning

---

#### 📉 Data Scaling or Transformation Issue

**Symptoms:**  
Loss remains high; gradients don’t help.

**Fixes:**  
- Normalize/standardize features
- Use log or quantile transform for skewed data

---

#### 🔁 Overuse of Data Augmentation

**Symptoms:**  
Loss remains high due to noisy or distorted training inputs.

**Fixes:**  
- Reduce augmentation intensity
- Mix original and augmented samples

---

#### 🐞 Setup or Code Bug

**Symptoms:**  
Loss doesn’t change or is constant.

**Fixes:**  
- Check loss computation
- Check that optimizer is hooked to model
- Confirm weights require gradients

---

## ✅ Summary Table

| Issue         | Symptom                            | Fixes |
|---------------|-------------------------------------|-------|
| Overfitting   | Low train loss, high val loss       | Regularization, augmentation, early stopping |
| Underfitting  | High train/val loss, flat curves    | Increase capacity, fix data, reduce regularization |
