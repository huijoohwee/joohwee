---
theme: seriph
background: https://source.unsplash.com/collection/94734566/1920x1080
class: text-center
highlighter: shiki
lineNumbers: false
info: |
  ## Phishing Detection ML Pipeline
  AIAP Batch 22 Technical Assessment
  HUI Joo Hwee
drawings:
  persist: false
transition: slide-left
title: Phishing Detection Pipeline
mdc: true
---

# Phishing Detection ML Pipeline

CyberProtect Real-Time Fraud Prevention System

<div class="pt-12">
  <span @click="$slidev.nav.next" class="px-2 py-1 rounded cursor-pointer" hover="bg-white bg-opacity-10">
    Press Space for next page <carbon:arrow-right class="inline"/>
  </span>
</div>

<div class="abs-br m-6 flex gap-2">
  <a href="https://github.com/huijoohwee/aiap22-hui-joo-hwee-045B" target="_blank" alt="GitHub"
    class="text-xl slidev-icon-btn opacity-50 !border-none !hover:text-white">
    <carbon-logo-github />
  </a>
</div>

<!--
Hi, I'm Joo Hwee. Today I'll present my phishing detection ML pipeline—a real-time fraud prevention system for CyberProtect's browser extension. 

This presentation covers: business problem, EDA insights, pipeline architecture, model comparison, and deployment recommendations.

Let's dive in!
-->

---
layout: center
class: text-center
---

# The Business Problem

<div class="grid grid-cols-2 gap-4 pt-8">
  <div>
    <h3>😱 Customer Pain</h3>
    <ul class="text-left">
      <li>Users click phishing links → credential theft</li>
      <li>Financial fraud & data breaches</li>
      <li>Trust erosion in CyberProtect brand</li>
    </ul>
  </div>
  
  <div>
    <h3>🎯 Business Requirement</h3>
    <ul class="text-left">
      <li><strong>Real-time detection</strong> (browser extension)</li>
      <li><strong>High recall</strong> (catch ≥70% attacks)</li>
      <li><strong>Low false alarms</strong> (FPR ≤5% ideal)</li>
    </ul>
  </div>
</div>

<div class="pt-8 text-2xl font-bold text-red-500">
  55% Baseline Accuracy = 45% Missed Attacks 🚨
</div>

<!--
The problem: CyberProtect users are exposed to phishing attacks. Without ML, a naive "always predict legitimate" model achieves 55% accuracy—missing 45% of phishing sites.

Business requirements: Real-time detection in a browser extension, high recall to catch most attacks, and low false positive rate to avoid user frustration.

My goal: Build a production-ready ML pipeline that dramatically reduces fraud exposure.
-->

---

# Solution Overview

<div class="grid grid-cols-2 gap-8">

<div>

## 📊 What I Delivered

- **EDA Notebook** (eda.ipynb)
  - Identified top 10 predictive features
  - Found 377 data quality issues
  - Documented MNAR patterns

- **ML Pipeline** (12 Python modules)
  - Custom LogReg + KNN implementations
  - XGBoost for production
  - Threshold tuning framework

- **Production Artifacts**
  - Trained models (3 algorithms)
  - Preprocessor pipeline
  - Comprehensive README

</div>

<div>

## 🎯 Key Results

<div class="text-center pt-4">
  <div class="text-6xl font-bold text-green-500">86%</div>
  <div class="text-xl">Recall (XGBoost)</div>
  <div class="text-sm text-gray-400">vs 55% baseline</div>
</div>

<div class="text-center pt-6">
  <div class="text-4xl font-bold text-blue-500">0.888</div>
  <div class="text-xl">ROC AUC</div>
  <div class="text-sm text-gray-400">Exceeds 0.80 requirement</div>
</div>

<div class="text-center pt-6">
  <div class="text-4xl font-bold text-orange-500">18%</div>
  <div class="text-xl">False Positive Rate</div>
  <div class="text-sm text-gray-400">Trade-off: tunable via threshold</div>
</div>

</div>

</div>

<!--
My solution: comprehensive EDA notebook uncovering data quality issues, a modular ML pipeline with 12 Python modules, and 3 trained models.

Results: XGBoost achieves 86% recall (31% improvement over baseline), 0.888 ROC AUC (exceeds requirement), but 18% FPR suggests threshold tuning needed for production.

All artifacts saved: models, preprocessor, and detailed README for deployment.
-->

---
layout: two-cols
---

# EDA Highlights

## Top 3 Findings

1️⃣ **DomainAgeMonths** (r=0.333)
- Strongest predictor of phishing risk
- Younger domains → higher fraud
- Missing values → MNAR pattern

2️⃣ **377 Impossible Values**
- NoOfImage < 0 (data corruption)
- Fixed via clipping to 0
- Validates synthetic data assumption

3️⃣ **10 Skewed Features**
- |skew| > 1 (heavy right tails)
- Requires log-transformation
- Improves gradient descent convergence

::right::

<div class="pl-4">

## Correlation with Target

```python {1|3-5|7-9|all}
# Top 10 Predictive Features
feature_corr = {
  'DomainAgeMonths': 0.333,
  'IsResponsive': 0.330,
  'Robots': 0.242,
  
  'NoOfiFrame': 0.150,
  'NoOfExternalRef': 0.128,
  'NoOfSelfRef': 0.114,
  # ... 4 more features
}
```

<div class="pt-4">

**Business Insight**:
- New domains without metadata → phishing
- Created missing-value flags (MNAR signal)
- Binned DomainAgeMonths into risk categories

</div>

</div>

<!--
EDA uncovered three critical findings:

First, DomainAgeMonths is the strongest predictor with correlation 0.333—younger domains are riskier. Missing values aren't random; phishing sites deliberately hide age.

Second, 377 rows had negative image counts—impossible values indicating data corruption. I clipped these to zero.

Third, 10 features are heavily skewed (|skew| > 1), requiring log-transformation to improve model convergence.

Business insight: new domains without metadata are strong phishing indicators. I created missing-value flags to capture this MNAR pattern.
-->

---

# Pipeline Architecture

```mermaid {scale: 0.8}
graph TD
    A[SQLite DB<br/>phishing.db] --> B[Data Loader<br/>11,430 rows × 15 cols]
    B --> C{Data Quality<br/>Validation}
    C -->|✓ Pass| D[Feature Engineering<br/>Missing flags + Domain bins]
    C -->|✗ Fail| E[Error Report]
    D --> F[Preprocessing<br/>Clip + Log + Impute + Scale]
    F --> G[Stratified Split<br/>70/15/15]
    G --> H[Train 3 Models<br/>LogReg | KNN | XGBoost]
    H --> I[Validation Eval<br/>Tune Thresholds]
    I --> J[Test Set Eval<br/>Final Metrics]
    J --> K[Save Artifacts<br/>models/ + results/]
    
    style A fill:#e1f5ff
    style H fill:#fff4e1
    style J fill:#e7f5e7
    style K fill:#f5e1ff
```

<!--
My pipeline follows this flow:

1. Load from SQLite and validate schema (11,430 rows, 15 columns)
2. Quality checks catch schema mismatches, impossible values
3. Feature engineering: missing-value flags, domain age bins, external/self-reference ratios
4. Preprocessing: clip negatives, log-transform skewed features, impute, scale
5. Stratified 70/15/15 split preserves 55:45 class balance
6. Train 3 diverse models: Logistic Regression, KNN, XGBoost
7. Tune thresholds on validation set to maximize recall with FPR ≤5%
8. Evaluate on test set for unbiased metrics
9. Save all artifacts: models, preprocessor, metrics JSON

Every step addresses an EDA finding. This isn't arbitrary—it's data-driven.
-->

---
layout: two-cols
---

# EDA → Preprocessing

## Traceability Table

| EDA Finding | Solution | Rationale |
|-------------|----------|-----------|
| 377 negative NoOfImage | Clip to 0 | Fix impossible values |
| 10 features \|skew\|>1 | Log-transform | Improve convergence |
| DomainAgeMonths missing (top predictor) | Median + missing flag | Preserve MNAR signal |
| 14.47% outliers in NoOfiFrame | Clip at 99th percentile | Reduce adversarial impact |
| 55:45 class imbalance | Stratified splits | Prevent distribution shift |

::right::

<div class="pl-4">

## Code Example

```python {1-3|5-8|10-13|all}
# Fix impossible values (EDA: 377 rows)
X['NoOfImage'] = X['NoOfImage'].clip(lower=0)

# Log-transform skewed features
skewed_cols = ['NoOfPopup', 'NoOfiFrame', ...]
for col in skewed_cols:
    X[col] = np.log1p(X[col])  # log(1+x)

# Missing-value flags (MNAR pattern)
for col in ['DomainAgeMonths', 'Robots']:
    X[f'{col}_missing'] = X[col].isna()

# Median imputation (robust to outliers)
X[col] = X[col].fillna(X[col].median())
```

</div>

<!--
Every preprocessing step is justified by EDA:

Row 1: Fix 377 negative NoOfImage values → clip to 0
Row 2: Log-transform 10 skewed features → improve convergence
Row 3: Create missing flags for DomainAgeMonths → preserve MNAR signal (phishing sites hide age)
Row 4: Clip outliers at 99th percentile → reduce adversarial manipulation
Row 5: Stratified splits → maintain 55:45 class balance

This traceability is critical for audit readiness. Every transformation has an EDA-backed rationale.
-->

---

# Model Comparison

<div class="grid grid-cols-3 gap-4 pt-4">

<div class="border-2 border-blue-500 rounded-lg p-4">
  <h3 class="text-center text-blue-500">Logistic Regression</h3>
  <div class="text-center pt-2">
    <div class="text-3xl font-bold">81%</div>
    <div class="text-sm">Recall</div>
  </div>
  <div class="text-center pt-2">
    <div class="text-2xl font-bold">0.825</div>
    <div class="text-sm">ROC AUC</div>
  </div>
  <div class="pt-4 text-xs">
    <div><strong>Pros:</strong> Interpretable coefficients, fast inference (~1ms)</div>
    <div><strong>Cons:</strong> Linear boundary misses complex patterns</div>
    <div><strong>Use:</strong> Regulatory explainability</div>
  </div>
</div>

<div class="border-2 border-green-500 rounded-lg p-4">
  <h3 class="text-center text-green-500">XGBoost</h3>
  <div class="text-center pt-2">
    <div class="text-3xl font-bold">86%</div>
    <div class="text-sm">Recall</div>
  </div>
  <div class="text-center pt-2">
    <div class="text-2xl font-bold">0.888</div>
    <div class="text-sm">ROC AUC</div>
  </div>
  <div class="pt-4 text-xs">
    <div><strong>Pros:</strong> Best performance, handles interactions</div>
    <div><strong>Cons:</strong> Black-box (needs SHAP), 18% FPR</div>
    <div><strong>Use:</strong> Production deployment</div>
  </div>
</div>

<div class="border-2 border-orange-500 rounded-lg p-4">
  <h3 class="text-center text-orange-500">KNN</h3>
  <div class="text-center pt-2">
    <div class="text-3xl font-bold">82%</div>
    <div class="text-sm">Recall</div>
  </div>
  <div class="text-center pt-2">
    <div class="text-2xl font-bold">0.809</div>
    <div class="text-sm">ROC AUC</div>
  </div>
  <div class="pt-4 text-xs">
    <div><strong>Pros:</strong> Non-parametric, no assumptions</div>
    <div><strong>Cons:</strong> Slow inference (distance calcs)</div>
    <div><strong>Use:</strong> Baseline comparison</div>
  </div>
</div>

</div>

<div class="pt-6 text-center">

## 🏆 **Recommendation: XGBoost** (Best Recall + ROC AUC)

<div class="text-sm pt-2 text-gray-400">
Custom LogReg implementation demonstrates depth | KNN validates non-parametric approach | XGBoost for production
</div>

</div>

<!--
I trained 3 diverse models covering different inductive biases:

Logistic Regression: 81% recall, 0.825 ROC AUC. Pros: interpretable coefficients for regulatory requirements, fast inference. Cons: linear boundary can't capture complex interactions. Use case: explainability.

XGBoost: 86% recall, 0.888 ROC AUC—best overall. Pros: handles feature interactions via trees, industry standard. Cons: black-box (requires SHAP), 18% FPR needs tuning. Use case: production.

KNN: 82% recall, 0.809 ROC AUC. Pros: non-parametric, no distributional assumptions. Cons: slow inference due to distance calculations. Use case: baseline.

Recommendation: XGBoost for production, with threshold tuning to balance recall vs FPR.

Note: I implemented custom LogReg (NumPy gradient descent) and KNN to demonstrate understanding beyond sklearn.
-->

---
layout: center
---

# Threshold Tuning

<div class="grid grid-cols-2 gap-8 pt-8">

<div>

## Methodology

1. **Validation Set** (prevents overfitting)
2. **Sweep 0.0 → 1.0** (step=0.01)
3. **Calculate FPR & Recall** per threshold
4. **Maximize Recall** subject to FPR ≤ 5%
5. **Apply to Test Set** (unbiased estimate)

<div class="pt-4 text-sm text-gray-400">
Why validation-based? Tuning on test set leaks information → overly optimistic metrics
</div>

</div>

<div>

## Trade-off Analysis

| Threshold | Recall | FPR | Decision |
|-----------|--------|-----|----------|
| 0.50 (default) | 86% | 18% | ❌ Too many false alarms |
| 0.65 (tuned FPR≤5%) | 75% | 4.8% | ✅ **Balanced** |
| 0.88 (tuned FPR≤3%) | 12% | 2.8% | ❌ Misses too many attacks |

<div class="pt-4 bg-blue-100 rounded p-3">
  <strong>Business Recommendation:</strong><br/>
  Deploy at threshold=0.65 (75% recall, 5% FPR)<br/>
  A/B test with warning UX (not blocking)
</div>

</div>

</div>

<!--
Threshold tuning is critical for balancing recall vs false positives.

Methodology: On validation set, I swept thresholds from 0 to 1 in steps of 0.01. For each threshold, I calculated FPR and recall, then selected the threshold maximizing recall subject to FPR ≤ 5%.

Trade-off: Default threshold (0.5) gives 86% recall but 18% FPR—1 in 5 legitimate users sees false warning. Tuning to FPR ≤ 5% (threshold=0.65) reduces recall to 75% but only 5% false alarms. Stricter FPR ≤ 3% (threshold=0.88) drops recall to 12%—unacceptable for fraud detection.

Business recommendation: Deploy at threshold=0.65, A/B test with warning UX (not blocking) to measure user tolerance. Monitor false positive rate by category (e.g., e-commerce may have higher FP).
-->

---

# Deployment Strategy

<div class="grid grid-cols-2 gap-8">

<div>

## Technical Requirements

✅ **Latency**: <100ms inference
- XGBoost model: ~15MB
- Achieves ~50ms on single core
- Horizontal scaling via Kubernetes

✅ **Memory**: <100MB total
- Model: 15MB
- Preprocessor: 3MB
- Feature store: 5MB
- **Headroom**: 77MB available

✅ **Throughput**: 100K+ predictions/day
- 3 replicas (load balanced)
- Auto-scale on CPU >70%

</div>

<div>

## Monitoring & Retraining

📊 **Feature Drift Detection**
- Track top 3 predictors (DomainAgeMonths, IsResponsive, Robots)
- Alert if distribution shift > 10% (KL divergence)

📉 **Performance Decay**
- Weekly evaluation on recent phishing samples
- Alert if recall drops below 70%

🔄 **Retraining Cadence**
- **Scheduled**: Quarterly (phishing tactics evolve 3-6 month cycles)
- **Event-Driven**: Triggered by drift/decay alerts

🔐 **Adversarial Defense**
- Monitor for feature manipulation (artificially aged domains)
- Flag anomalies (old domain + suspicious content)

</div>

</div>

<!--
Deployment considerations for production readiness:

Technical requirements: Latency under 100ms (XGBoost achieves 50ms on single core), memory under 100MB (current: 23MB total), throughput 100K+ daily predictions (horizontal scaling with 3 replicas).

Monitoring: Track feature drift in top predictors (DomainAgeMonths, IsResponsive, Robots). Alert if distributions shift >10%. Weekly performance checks—alert if recall drops below 70%.

Retraining: Quarterly scheduled retraining (phishing tactics evolve every 3-6 months). Event-driven triggers on feature drift or performance decay.

Adversarial defense: Monitor for feature manipulation (e.g., attackers aging domains). Flag anomalies like old domains with suspicious content patterns.
-->

---
layout: center
class: text-center
---

# Key Takeaways

<div class="grid grid-cols-2 gap-8 pt-12">

<div>

## 🎯 Business Impact

<div class="text-6xl font-bold text-green-500 pt-4">31%</div>
<div class="text-xl pt-2">Improvement over baseline</div>
<div class="text-sm text-gray-400">(55% → 86% recall)</div>

<div class="pt-6 text-left text-sm">
✅ Catches 86% of phishing attacks<br/>
✅ 0.888 ROC AUC (exceeds 0.80 requirement)<br/>
✅ Production-ready artifacts (models + preprocessor)<br/>
⚠️ 18% FPR needs threshold tuning for deployment
</div>

</div>

<div>

## 🔬 Technical Depth

<div class="text-left pt-4">

1. **EDA-Driven**: Every preprocessing step justified
2. **Custom Implementations**: NumPy LogReg + KNN
3. **Rigorous Evaluation**: Threshold tuning on validation set
4. **Production Awareness**: Monitoring, retraining, adversarial defense

</div>

<div class="pt-6 bg-yellow-100 rounded p-4 text-left text-sm">
<strong>Next Steps:</strong><br/>
- A/B test threshold=0.65 with warning UX<br/>
- Implement SHAP for XGBoost explainability<br/>
- Add ensemble method (stack LogReg + XGBoost)
</div>

</div>

</div>

<!--
Key takeaways:

Business impact: 31% improvement over baseline (55% → 86% recall), 0.888 ROC AUC exceeding requirements, production-ready artifacts. Trade-off: 18% FPR suggests threshold tuning to 0.65 for deployment.

Technical depth: EDA-driven preprocessing (every step justified), custom NumPy implementations (LogReg gradient descent, KNN), rigorous threshold tuning on validation set, production awareness (monitoring, retraining, adversarial defense).

Next steps: A/B test threshold=0.65, implement SHAP for explainability, explore ensemble methods (stacking).

Thank you! Happy to answer questions on EDA, preprocessing, model choices, or deployment strategy.
-->

---
layout: end
class: text-center
---

# Questions?

<div class="pt-8">

📧 huijoohwee@live.com  
🔗 [github.com/huijoohwee/aiap22-hui-joo-hwee-045B](https://github.com/huijoohwee/aiap22-hui-joo-hwee-045B)

</div>

<div class="pt-12 text-sm text-gray-400">
Presentation built with Slidev | Press 'o' for overview | Press 'd' for dev tools
</div>

<!--
Thank you for your time! I'm ready to answer questions on:
- EDA methodology and findings
- Preprocessing pipeline design
- Model selection rationale
- Threshold tuning approach
- Deployment considerations
- Group exercise collaboration

Feel free to dive deep into any technical component!
-->

---
