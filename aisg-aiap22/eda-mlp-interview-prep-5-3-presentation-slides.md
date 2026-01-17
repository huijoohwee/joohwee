# Phishing Detection ML Pipeline
## AIAP Batch 22 Technical Assessment

**Hui Joo Hwee**  
huijoohwee@live.com

---

# Agenda (10 Minutes)

## Coverage
1. Business Problem Framing
2. EDA-Driven Pipeline Design  
3. Model Performance & Learnings
4. Growth Areas & Next Steps

## Core Message
**Systematic approach:**  
EDA → Evidence-based decisions → Production-ready pipeline

**Three competencies demonstrated:**
- Data quality remediation
- End-to-end automation
- Reproducible artifacts

---

# Opening: Three Core Competencies

### 1. Systematic EDA
- 6 critical quality issues identified
- 377 impossible values fixed
- Top predictors ranked

### 2. Production Pipeline
- Automated via `run.sh`
- Stratified data splits (70/15/15)
- Serialized artifacts ready

### 3. Evidence-Based
- Every preprocessing choice linked to EDA
- Decision logic documented
- Assumptions stated clearly

**Approach:** "I'm learning through doing—documenting decisions, building from first principles, prioritizing reproducibility."

---

# Business Problem: CyberProtect Phishing Detection

```mermaid
graph LR
    A[User visits website] --> B{ML Model<br/>Prediction}
    B -->|Phishing<br/>prob > 0.7| C[⚠️ Warning:<br/>Block access]
    B -->|Legitimate<br/>prob ≤ 0.7| D[✅ Allow:<br/>Safe to proceed]
    
    E[Data: 11,430 websites] --> F[Features:<br/>DomainAge, Robots,<br/>NoOfExternalRef...]
    F --> B
    
    style C fill:#ffebee,stroke:#c62828
    style D fill:#e8f5e9,stroke:#2e7d32
    style B fill:#e3f2fd,stroke:#1976d2
```

**Critical Challenge:**
- 55.04% baseline accuracy → **44.96% of attacks missed**
- Business impact: Customer fraud exposure, trust erosion, regulatory scrutiny

---

# Business KPIs & Target Metrics

## Hard Constraints
| Metric | Target | Rationale |
|--------|--------|-----------|
| **Recall** | ≥ 70% | Catch 7/10 phishing attacks |
| **FPR** | ≤ 3% | Minimize false alarms |
| **ROC AUC** | ≥ 0.80 | Strong discrimination |

## Deployment Requirements
- **Latency:** <100ms (browser extension)
- **Memory:** <100MB (client-side)
- **Explainability:** Regulatory compliance

**Solution:** 3 diverse models evaluated against all KPIs

---

# EDA Findings → Pipeline Decisions

| EDA Finding | Impact | Pipeline Solution | Implementation |
|-------------|--------|-------------------|----------------|
| **55:45 class imbalance** | Distribution shift risk | Stratified sampling | `data_splitter.py` |
| **DomainAgeMonths r=0.333** | Top predictor | Median imputation + bins | `feature_engineering.py` |
| **377 negative NoOfImage** | Impossible values | Clip to 0 | `preprocessing.py` |
| **10 features \|skew\| > 1** | Poor convergence | Log-transform + clip 99th | `preprocessing.py` |
| **NoOfiFrame 14.47% outliers** | Adversarial contamination | Clip at 99th percentile | `preprocessing.py` |
| **1 feature 20-70% missing** | MNAR fraud signal | `*_missing` binary flags | `feature_engineering.py` |

**Key Principle:** Every transformation is **evidence-based** and **traceable to EDA**

---

# Pipeline Architecture

```mermaid
graph TD
    A[(SQLite DB<br/>phishing.db)] -->|load_data| B[Validate Schema<br/>11,430 × 15 cols]
    B -->|check_quality| C{Data Quality<br/>Pass?}
    C -->|❌ Fail| D[❌ DataQualityError:<br/>Log & Exit]
    C -->|✅ Pass| E[Feature Engineering<br/>Missing flags, bins, ratios]
    
    E --> F[Preprocessing Pipeline<br/>Impute → Transform → Encode → Scale]
    F --> G[Stratified Split<br/>70% Train / 15% Val / 15% Test]
    
    G --> H[Train 3 Models<br/>Logistic, KNN, XGBoost]
    H --> I[Evaluate on Val Set<br/>Tune thresholds for FPR ≤ 3%]
    I --> J[Test Set Evaluation<br/>Final unbiased metrics]
    
    J --> K[Select Best Model<br/>Highest ROC AUC]
    K --> L[Persist Artifacts<br/>model.pkl, preprocessor.pkl,<br/>metrics.json]
    
    style D fill:#ffebee,stroke:#c62828
    style L fill:#e8f5e9,stroke:#2e7d32
    style K fill:#fff3e0,stroke:#f57c00
```

---

# Preprocessing Pipeline: Evidence-Based Order

```mermaid
graph LR
    A[Raw Features] -->|1. Imputation| B[Fill Missing:<br/>Median/Mode]
    B -->|2. Engineering| C[Create Features:<br/>Ratios, Bins, Flags]
    C -->|3. Encoding| D[Categorical → Numeric:<br/>OneHot, Frequency]
    D -->|4. Scaling| E[Standardize:<br/>Z-score/Robust]
    
    E --> F[Transformed Features<br/>Ready for Training]
    
    style A fill:#e3f2fd,stroke:#1976d2
    style F fill:#e8f5e9,stroke:#2e7d32
```

**Critical Design:**
1. **Imputation first** → Missing breaks downstream ops
2. **Engineering second** → Create domain features from clean data  
3. **Encoding third** → Categorical → numeric before scaling
4. **Scaling last** → Standardize final numeric features

**Saved as `preprocessor.pkl`** → Test data undergoes identical transformations

---

# Top 10 Predictive Features (by Correlation)

```mermaid
graph TD
    subgraph "Feature Importance Ranking"
        A[1. DomainAgeMonths: r=0.333<br/>Younger domains = higher risk]
        B[2. IsResponsive: r=0.330<br/>Non-responsive = suspicious]
        C[3. Robots: r=0.242<br/>Missing robots.txt = fraud signal]
        D[4. NoOfiFrame: r=0.150<br/>Excessive iFrames = obfuscation]
        E[5. NoOfExternalRef: r=0.128<br/>Link pattern differs]
    end
    
    subgraph "Feature Engineering Applied"
        F[DomainAge → Bins:<br/><6mo, 6-12mo, 12-24mo, >24mo]
        G[Missing flags:<br/>Robots_missing, IsResponsive_missing]
        H[External/Self Ratio:<br/>NoOfExternalRef / NoOfSelfRef + 1]
    end
    
    A --> F
    B --> G
    C --> G
    E --> H
    
    style A fill:#e8f5e9,stroke:#2e7d32
    style B fill:#e8f5e9,stroke:#2e7d32
    style C fill:#fff3e0,stroke:#f57c00
```

**Insight:** Domain metadata (age, robots.txt, responsiveness) stronger than content features (images, popups)

---

# Model Selection Rationale

### Logistic Regression
**Why chosen:**
- ✅ Coefficient interpretability
- ✅ Fast inference (~1ms)
- ✅ Regulatory explainability

**Trade-off:**
- ❌ Linear boundary may miss complex patterns

**Expected:** ROC AUC 0.75-0.78

### K-Nearest Neighbors
**Why chosen:**
- ✅ Non-parametric (local patterns)
- ✅ No training needed (lazy)
- ✅ Baseline comparison

**Trade-off:**
- ❌ Slow inference (distance calculations)

**Expected:** ROC AUC 0.78-0.82

### XGBoost
**Why chosen:**
- ✅ Industry standard for fraud
- ✅ Handles imbalance natively
- ✅ Feature importance via SHAP

**Trade-off:**
- ❌ Black-box (needs SHAP)

**Expected:** ROC AUC 0.83-0.87

**Why NOT Neural Networks?** Dataset too small (11,430 rows); tree ensembles outperform on structured data

---

# Model Performance Results

| Model | Recall | FPR | ROC AUC | Meets KPIs? | Key Insight |
|-------|--------|-----|---------|-------------|-------------|
| **XGBoost** | 86.51% | 18.22% | 0.8880 | ✅ Recall<br>❌ FPR | Best discriminator |
| **Logistic** | 81.20% | 21.89% | 0.8252 | ✅ Recall<br>❌ FPR | Most interpretable |
| **KNN** | 82.35% | 29.10% | 0.8091 | ✅ Recall<br>❌ FPR | Baseline for comparison |

**Honest Assessment:**
- ✅ **Strengths:** All achieve Recall ≥ 70%; XGBoost reaches 86.51%
- ❌ **Gap:** FPR constraint (≤3%) not met with default threshold 0.5
- 📈 **Solution:** Threshold tuning or advanced feature engineering required

---

# Threshold Tuning: Trade-off Analysis

```mermaid
graph TD
    A[Default Threshold: 0.5] --> B[XGBoost Performance:<br/>Recall=86.51%, FPR=18.22%]
    
    B --> C{Tune Threshold<br/>for FPR ≤ 3%?}
    
    C -->|Increase to 0.88| D[Tuned Performance:<br/>Recall=7.61%, FPR=2.26%]
    
    D --> E{Business Decision}
    
    E -->|Prioritize User Trust| F[✅ Use FPR ≤ 3%<br/>Accept lower recall]
    E -->|Prioritize Security| G[✅ Use default 0.5<br/>Accept higher FPR]
    
    style D fill:#ffebee,stroke:#c62828
    style F fill:#fff3e0,stroke:#f57c00
    style G fill:#e3f2fd,stroke:#1976d2
```

**Key Learning:** Achieving FPR ≤ 3% tanks recall to 7.61% → **violates 70% KPI**  
**Recommendation:** Need better features OR ensemble methods OR accept 5% FPR

---

# What I'd Do Differently (Growth Areas)

## Advanced Feature Engineering
**URL-Based:**
- Subdomain depth (phishing uses many levels)
- Suspicious TLDs (`.tk`, `.ml` common)
- URL entropy (random strings → phishing)

**HTML-Based:**
- Script-to-content ratio
- Hidden iframes count
- DOM tree complexity

**Time-Based:**
- Domain registration vs first seen
- SSL certificate age

## Hyperparameter Optimization
- Bayesian optimization (Optuna) vs grid search
- Early stopping with validation monitoring
- Ensemble methods (stacking, blending)

## Production Readiness
- Model monitoring dashboard (drift detection)
- A/B testing framework
- SHAP explainability for predictions

**Philosophy:** I built a solid foundation—ready to learn advanced techniques

---

# Reproducibility Guarantees

```mermaid
graph TD
    A[Reproducibility Framework] --> B[Environment Control]
    A --> C[Data Versioning]
    A --> D[Pipeline Determinism]
    
    B --> B1[requirements.txt:<br/>Pinned versions]
    B --> B2[Python 3.8-3.11 tested]
    B --> B3[Ubuntu 20.04, macOS 13+]
    
    C --> C1[SHA256 hash of phishing.db]
    C --> C2[Stratified splits:<br/>random_state=42]
    
    D --> D1[config.yaml version-controlled]
    D --> D2[Timestamped experiments:<br/>run_YYYYMMDD_HHMMSS/]
    D --> D3[All artifacts serialized:<br/>models/*.pkl, results/*.json]
    
    style A fill:#e3f2fd,stroke:#1976d2
    style B fill:#fff3e0,stroke:#f57c00
    style C fill:#f3e5f5,stroke:#7b1fa2
    style D fill:#e8f5e9,stroke:#2e7d32
```

**Verification:** GitHub Actions CI/CD runs `bash run.sh` → generates identical `baseline_metrics.json`

---

# Deployment Architecture (Production-Ready)

```mermaid
graph LR
    A[Browser Extension] -->|Extract URL metadata| B[API Gateway]
    B -->|HTTPS POST| C[Lambda Function<br/>Model Serving]
    
    C -->|Load artifacts| D[(S3 Bucket:<br/>model.pkl<br/>preprocessor.pkl)]
    
    D --> C
    C -->|Preprocess| E[Pipeline Transform]
    E -->|Predict| F[XGBoost Model]
    
    F -->|probability| G{Threshold<br/>Decision}
    
    G -->|prob > 0.7| H[Response:<br/>is_phishing: true<br/>confidence: 0.92]
    G -->|prob ≤ 0.7| I[Response:<br/>is_phishing: false<br/>confidence: 0.31]
    
    C -->|Metrics| J[CloudWatch:<br/>Latency, Error Rate,<br/>Feature Drift]
    
    style C fill:#fff3e0,stroke:#f57c00
    style H fill:#ffebee,stroke:#c62828
    style I fill:#e8f5e9,stroke:#2e7d32
    style J fill:#e3f2fd,stroke:#1976d2
```

**Latency Budget:** <100ms total (50ms extraction + 30ms inference + 20ms network)

---

# Key Learnings

### 1. Structured Thinking
- Systematic EDA → evidence-based decisions
- Every preprocessing choice justified
- Reproducible pipeline via `run.sh`

**Artifact:** 
`README.md` → EDA Findings table

### 2. Production Focus
- Automated end-to-end pipeline
- Serialized artifacts ready for deployment
- GitHub Actions CI/CD tested

**Artifact:**  
`models/*.pkl`, `results/baseline_metrics.json`

### 3. Growth Mindset
- Documented learnings honestly
- Clear about gaps (FPR, advanced features)
- Eager to learn from team

**Commitment:**  
Turn every project into learning opportunity

---

# Closing

**I'm not the most experienced candidate—but I'm the one who will:**

✅ **Ask the right questions** → Learn domain knowledge from security analysts  
✅ **Document everything** → Knowledge transfer for team (wiki, model cards)  
✅ **Learn rapidly** → First 30 days: feature engineering sprint, production readiness

**Core Philosophy:**  
"Build solid foundations through systematic work, then scale up with advanced techniques learned from experts."

**Evidence of Readiness:**
- ✅ End-to-end pipeline functional (`bash run.sh` works)
- ✅ All artifacts documented and reproducible
- ✅ Honest assessment of gaps and next steps

**Thank you. I'm ready for your questions.**

---

# Backup: Retraining Strategy

| Trigger | Frequency | Rationale |
|---------|-----------|-----------|
| **Scheduled** | Quarterly | Phishing tactics evolve every 3-6 months |
| **Performance Decay** | Ad-hoc | Weekly validation; retrain if recall < 65% |
| **Feature Drift** | Ad-hoc | Monitor top 3 features; retrain if KL divergence > 10% |
| **Major Event** | Immediate | New campaign (e.g., COVID-19 scams) |

**Pipeline:**
1. Query last 90 days labeled data
2. Merge with original (70% new, 30% old)
3. Run `bash run.sh` with updated DB
4. A/B test (shadow mode 7 days)
5. Rollout if improved; rollback if degraded