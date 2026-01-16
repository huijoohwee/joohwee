---
theme: default
author: "joohwee"
tags: [EDA, MLP]
date: 2026-01-16
class: text-center
highlighter: shiki
lineNumbers: false
drawings:
  persist: false
transition: none
title: Phishing Detection ML Pipeline - Technical Assessment
mdc: true
mermaidAnchorsOnly: true
mermaid: |
  graph TD
    Start([🎬 START<br/>10-Minute Presentation]) --> Intro[📍 Slide 1-2: Agenda & Opening<br/>⏱️ 0:00-1:00<br/>🎯 Set tone: Systematic learner]
    
    Intro --> Problem[📍 Slide 3-5: Business Problem<br/>⏱️ 1:00-3:00<br/>🎯 Frame impact: 44.96% attacks missed]
    
    Problem --> ProblemDecision{⏳ Time Check:<br/>Running behind?}
    ProblemDecision -->|Yes: Skip KPI details| EDA
    ProblemDecision -->|No: Full KPI slide| KPIDetail[📍 Slide 5: Business KPIs<br/>⏱️ 2:30-3:00<br/>🎯 Hard constraints: Recall, FPR, AUC]
    
    KPIDetail --> EDA
    
    EDA[📍 Slide 6-8: EDA-Driven Pipeline<br/>⏱️ 3:00-6:00<br/>🎯 Evidence-based decisions]
    
    EDA --> EDADetail1[📍 Slide 6: EDA Findings Table<br/>⏱️ 3:00-4:00<br/>💡 6 critical issues → 6 solutions<br/>🗣️ Point to specific examples]
    
    EDADetail1 --> EDADetail2[📍 Slide 7: Pipeline Architecture<br/>⏱️ 4:00-5:00<br/>💡 Data flow: Load → Validate → Transform<br/>🗣️ Emphasize quality gates]
    
    EDADetail2 --> EDADetail3[📍 Slide 8: Preprocessing Order<br/>⏱️ 5:00-5:30<br/>💡 Why this sequence matters<br/>🗣️ Impute → Engineer → Encode → Scale]
    
    EDADetail3 --> Features[📍 Slide 9: Top 10 Features<br/>⏱️ 5:30-6:00<br/>💡 Domain metadata > content<br/>🗣️ DomainAge r=0.333 strongest]
    
    Features --> Models[📍 Slide 10-12: Model Performance<br/>⏱️ 6:00-8:00<br/>🎯 Results + honest assessment]
    
    Models --> ModelChoice[📍 Slide 10: Model Selection<br/>⏱️ 6:00-6:45<br/>💡 Why 3 diverse models<br/>🗣️ Logistic, KNN, XGBoost rationale]
    
    ModelChoice --> ModelResults[📍 Slide 11: Performance Table<br/>⏱️ 6:45-7:30<br/>💡 All meet Recall ≥ 70%<br/>🗣️ FPR gap: 18-29% vs target 3%]
    
    ModelResults --> Threshold[📍 Slide 12: Threshold Trade-off<br/>⏱️ 7:30-8:00<br/>💡 FPR ≤ 3% → Recall tanks to 7.61%<br/>🗣️ Business decision required]
    
    Threshold --> TimeCheck{⏳ Time Check:<br/>2 min left?}
    
    TimeCheck -->|Yes: Skip growth| Closing
    TimeCheck -->|No: Include growth| Growth
    
    Growth[📍 Slide 13: Growth Areas<br/>⏱️ 8:00-9:00<br/>🎯 Show self-awareness]
    
    Growth --> GrowthDetail[💡 Advanced features:<br/>URL parsing, HTML structure<br/>💡 Hyperparameter optimization<br/>💡 Production readiness<br/>🗣️ Solid foundation → ready to learn]
    
    GrowthDetail --> Closing
    
    Closing[📍 Slide 14-15: Reproducibility + Deployment<br/>⏱️ 9:00-9:30<br/>🎯 Production-ready artifacts]
    
    Closing --> ClosingDetail[💡 CI/CD tested via GitHub Actions<br/>💡 <100ms latency budget<br/>🗣️ Show run.sh execution if demo allowed]
    
    ClosingDetail --> Takeaways[📍 Slide 16: Key Takeaways<br/>⏱️ 9:30-9:50<br/>🎯 Why select me?]
    
    Takeaways --> TakeawayDetail[💡 1. Structured thinking<br/>💡 2. Production focus<br/>💡 3. Growth mindset<br/>🗣️ I'm the one who will learn & document]
    
    TakeawayDetail --> Final[📍 Slide 17: Closing<br/>⏱️ 9:50-10:00<br/>🎯 Strong finish]
    
    Final --> FinalDetail[💡 Not most experienced<br/>💡 But will ask right questions<br/>💡 Turn every project into learning<br/>🗣️ Thank you. Ready for questions.]
    
    FinalDetail --> End([✅ END<br/>Transition to Q&A<br/>50 minutes])
    
    %% Emergency paths if running over time
    TimeCheck -.->|>8:30: ABORT growth| EmergencyClosing[⚠️ Emergency Skip:<br/>Jump to Slide 16]
    EmergencyClosing -.-> Takeaways
    
    ProblemDecision -.->|>2:30: ABORT KPIs| EmergencyEDA[⚠️ Emergency Skip:<br/>Jump to Slide 6]
    EmergencyEDA -.-> EDA
    
    %% Backup slides (if time permits or Q&A)
    End -.-> Backup[📦 Backup Slides 18-21<br/>Repository structure<br/>Error analysis example<br/>Retraining strategy]
    
    %% Styling
    classDef introStyle fill:#e3f2fd,stroke:#1976d2,stroke-width:3px
    classDef problemStyle fill:#fff3e0,stroke:#f57c00,stroke-width:3px
    classDef edaStyle fill:#f3e5f5,stroke:#7b1fa2,stroke-width:3px
    classDef modelStyle fill:#fce4ec,stroke:#c2185b,stroke-width:3px
    classDef closingStyle fill:#e8f5e9,stroke:#2e7d32,stroke-width:3px
    classDef decisionStyle fill:#ffebee,stroke:#c62828,stroke-width:2px
    classDef emergencyStyle fill:#fff9c4,stroke:#f57f17,stroke-width:2px,stroke-dasharray: 5 5
    
    class Start,Intro,Takeaways,Final,FinalDetail,End introStyle
    class Problem,ProblemDecision,KPIDetail problemStyle
    class EDA,EDADetail1,EDADetail2,EDADetail3,Features edaStyle
    class Models,ModelChoice,ModelResults,Threshold,Growth,GrowthDetail modelStyle
    class Closing,ClosingDetail closingStyle
    class TimeCheck decisionStyle
    class EmergencyClosing,EmergencyEDA,Backup emergencyStyle
    
    %% Notes for presenter
    classDef noteStyle fill:#fffde7,stroke:#f9a825,stroke-width:1px
    
    Note1[📝 PRESENTER NOTES<br/>──────────────────<br/>Slide 1-2: Smile, confident posture<br/>Slide 6: Point to printed README<br/>Slide 11: Pause for impact on FPR gap<br/>Slide 17: Eye contact, thank panel]
    
    Note2[🎤 KEY PHRASES<br/>──────────────────<br/>Evidence-based decisions<br/>Production-ready artifacts<br/>Growth mindset<br/>I'm the one who will learn]
    
    Note3[⏱️ TIME MANAGEMENT<br/>──────────────────<br/>0:00-1:00: Intro 1 min<br/>1:00-3:00: Problem 2 min<br/>3:00-6:00: EDA 3 min<br/>6:00-8:00: Models 2 min<br/>8:00-9:00: Growth 1 min<br/>9:00-10:00: Close 1 min]
    
    Note4[🚨 EMERGENCY PROTOCOL<br/>──────────────────<br/>@2:30 behind → Skip KPI details<br/>@6:00 behind → Skip Top 10 Features<br/>@8:30 behind → Skip Growth Areas<br/>Always keep: Takeaways + Closing]
    
    class Note1,Note2,Note3,Note4 noteStyle
---

# Phishing Detection ML Pipeline
## AIAP Batch 22 Technical Assessment

**Hui Joo Hwee**  
huijoohwee@live.com

---

# Agenda (10 Minutes)

<div class="grid grid-cols-2 gap-4">
<div>

## Coverage
1. Business Problem Framing
2. EDA-Driven Pipeline Design  
3. Model Performance & Learnings
4. Growth Areas & Next Steps

</div>
<div>

## Core Message
**Systematic approach:**  
EDA → Evidence-based decisions → Production-ready pipeline

**Three competencies demonstrated:**
- Data quality remediation
- End-to-end automation
- Reproducible artifacts

</div>
</div>

---

# Opening: Three Core Competencies

<div class="grid grid-cols-3 gap-4">
<div>

### 1. Systematic EDA
- 6 critical quality issues identified
- 377 impossible values fixed
- Top predictors ranked

</div>
<div>

### 2. Production Pipeline
- Automated via `run.sh`
- Stratified data splits (70/15/15)
- Serialized artifacts ready

</div>
<div>

### 3. Evidence-Based
- Every preprocessing choice linked to EDA
- Decision logic documented
- Assumptions stated clearly

</div>
</div>

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

<div class="grid grid-cols-2 gap-4">
<div>

## Hard Constraints
| Metric | Target | Rationale |
|--------|--------|-----------|
| **Recall** | ≥ 70% | Catch 7/10 phishing attacks |
| **FPR** | ≤ 3% | Minimize false alarms |
| **ROC AUC** | ≥ 0.80 | Strong discrimination |

</div>
<div>

## Deployment Requirements
- **Latency:** <100ms (browser extension)
- **Memory:** <100MB (client-side)
- **Explainability:** Regulatory compliance

**Solution:** 3 diverse models evaluated against all KPIs

</div>
</div>

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

<div class="grid grid-cols-3 gap-4">
<div>

### Logistic Regression
**Why chosen:**
- ✅ Coefficient interpretability
- ✅ Fast inference (~1ms)
- ✅ Regulatory explainability

**Trade-off:**
- ❌ Linear boundary may miss complex patterns

**Expected:** ROC AUC 0.75-0.78

</div>
<div>

### K-Nearest Neighbors
**Why chosen:**
- ✅ Non-parametric (local patterns)
- ✅ No training needed (lazy)
- ✅ Baseline comparison

**Trade-off:**
- ❌ Slow inference (distance calculations)

**Expected:** ROC AUC 0.78-0.82

</div>
<div>

### XGBoost
**Why chosen:**
- ✅ Industry standard for fraud
- ✅ Handles imbalance natively
- ✅ Feature importance via SHAP

**Trade-off:**
- ❌ Black-box (needs SHAP)

**Expected:** ROC AUC 0.83-0.87

</div>
</div>

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

<div class="grid grid-cols-2 gap-4">
<div>

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

</div>
<div>

## Hyperparameter Optimization
- Bayesian optimization (Optuna) vs grid search
- Early stopping with validation monitoring
- Ensemble methods (stacking, blending)

## Production Readiness
- Model monitoring dashboard (drift detection)
- A/B testing framework
- SHAP explainability for predictions

**Philosophy:** I built a solid foundation—ready to learn advanced techniques

</div>
</div>

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

# Key Takeaways: Why Select Me?

<div class="grid grid-cols-3 gap-4">
<div>

### 1. Structured Thinking
- Systematic EDA → evidence-based decisions
- Every preprocessing choice justified
- Reproducible pipeline via `run.sh`

**Artifact:** 
`README.md` → EDA Findings table

</div>
<div>

### 2. Production Focus
- Automated end-to-end pipeline
- Serialized artifacts ready for deployment
- GitHub Actions CI/CD tested

**Artifact:**  
`models/*.pkl`, `results/baseline_metrics.json`

</div>
<div>

### 3. Growth Mindset
- Documented learnings honestly
- Clear about gaps (FPR, advanced features)
- Eager to learn from team

**Commitment:**  
Turn every project into learning opportunity

</div>
</div>

---

# Closing: What I Bring to Your Team

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

# Backup: Repository Structure

```
├── .github/workflows/     # CI/CD automation
├── src/                   # Pipeline modules
│   ├── data_loader.py          # SQLite → DataFrame
│   ├── preprocessing.py        # Cleaning, scaling, encoding
│   ├── feature_engineering.py  # Missing flags, bins, ratios
│   ├── data_splitter.py        # Stratified 70/15/15
│   ├── evaluation.py           # Metrics + threshold tuning
│   └── models/                 # Logistic, KNN, XGBoost
├── data/                  # phishing.db (not committed)
├── models/                # Serialized artifacts (created at runtime)
├── results/               # baseline_metrics.json (created at runtime)
├── eda.ipynb              # Task 1: Exploratory Data Analysis
├── README.md              # Full documentation
├── requirements.txt       # Pinned dependencies
├── config.yaml            # Hyperparameters
└── run.sh                 # Automated pipeline execution
```

**Design Principle:** Modular, reusable, config-driven architecture

---

# Backup: Error Analysis Example

**Scenario:** False positive on legitimate banking site

**Investigation Process:**

1. **Reproduce:**
   ```bash
   python scripts/predict.py --input suspect_url.csv
   ```

2. **Feature Inspection:**
   - High `NoOfExternalRef`? (Banks link to many partners)
   - Low `DomainAgeMonths`? (New legitimate site)

3. **SHAP Explainability:**
   ```python
   shap.TreeExplainer(model).shap_values(X)
   # Identify top 3 contributing features
   ```

4. **Corrective Actions:**
   - Immediate: Whitelist domain
   - Short-term: Retrain with hard negative
   - Long-term: Engineer context feature (Alexa Top 10K override)

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