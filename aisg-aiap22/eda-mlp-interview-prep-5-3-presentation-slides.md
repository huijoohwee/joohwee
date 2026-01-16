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
    %% ============================================================================
    %% MASTER INTEGRATED MERMAID: PHISHING DETECTION ML PIPELINE PRESENTATION
    %% Consolidates all diagrams from interview-presentation-slides.md
    %% ============================================================================
    
    PresentationStart([🎯 PRESENTATION START<br/>Phishing Detection ML Pipeline<br/>10 Minutes])
    
    %% ============================================================================
    %% SECTION 1: BUSINESS PROBLEM (Slide 4)
    %% ============================================================================
    
    PresentationStart --> BusinessProblem
    
    subgraph BusinessProblem["📊 BUSINESS PROBLEM FRAMING"]
        BP_User[User visits website] --> BP_Model{ML Model<br/>Prediction}
        BP_Model -->|Phishing<br/>prob > 0.7| BP_Block[⚠️ Warning:<br/>Block access]
        BP_Model -->|Legitimate<br/>prob ≤ 0.7| BP_Allow[✅ Allow:<br/>Safe to proceed]
        
        BP_Data[Data: 11,430 websites] --> BP_Features[Features:<br/>DomainAge, Robots,<br/>NoOfExternalRef]
        BP_Features --> BP_Model
        
        BP_Challenge[❌ Critical Challenge:<br/>55.04% baseline accuracy<br/>→ 44.96% attacks missed]
        BP_Impact[💰 Business Impact:<br/>Customer fraud exposure<br/>Trust erosion<br/>Regulatory scrutiny]
        
        BP_KPIs[🎯 Hard Constraints:<br/>Recall ≥ 70%<br/>FPR ≤ 3%<br/>ROC AUC ≥ 0.80]
        BP_Deploy[⚙️ Deployment:<br/>Latency <100ms<br/>Memory <100MB<br/>Explainability required]
    end
    
    %% ============================================================================
    %% SECTION 2: EDA FINDINGS → PIPELINE DECISIONS (Slide 6)
    %% ============================================================================
    
    BusinessProblem --> EDAFindings
    
    subgraph EDAFindings["🔍 EDA-DRIVEN PIPELINE DESIGN"]
        EDA_Issue1[Issue 1:<br/>55:45 class imbalance] --> EDA_Sol1[Solution:<br/>Stratified sampling]
        EDA_Issue2[Issue 2:<br/>DomainAge r=0.333<br/>top predictor] --> EDA_Sol2[Solution:<br/>Median imputation<br/>+ bins]
        EDA_Issue3[Issue 3:<br/>377 negative<br/>NoOfImage] --> EDA_Sol3[Solution:<br/>Clip to 0]
        EDA_Issue4[Issue 4:<br/>10 features<br/>|skew| > 1] --> EDA_Sol4[Solution:<br/>Log-transform<br/>+ clip 99th]
        EDA_Issue5[Issue 5:<br/>NoOfiFrame<br/>14.47% outliers] --> EDA_Sol5[Solution:<br/>Clip at 99th<br/>percentile]
        EDA_Issue6[Issue 6:<br/>1 feature<br/>20-70% missing] --> EDA_Sol6[Solution:<br/>*_missing<br/>binary flags]
        
        EDA_Principle[✅ Key Principle:<br/>Every transformation<br/>evidence-based &<br/>traceable to EDA]
    end
    
    %% ============================================================================
    %% SECTION 3: PIPELINE ARCHITECTURE (Slide 7)
    %% ============================================================================
    
    EDAFindings --> PipelineArch
    
    subgraph PipelineArch["🏗️ PIPELINE ARCHITECTURE"]
        PA_DB[(SQLite DB<br/>phishing.db)] -->|load_data| PA_Validate[Validate Schema<br/>11,430 × 15 cols]
        PA_Validate -->|check_quality| PA_Quality{Data Quality<br/>Pass?}
        
        PA_Quality -->|❌ Fail| PA_Error[❌ DataQualityError:<br/>Log & Exit]
        PA_Quality -->|✅ Pass| PA_Engineer[Feature Engineering<br/>Missing flags, bins, ratios]
        
        PA_Engineer --> PA_Preprocess[Preprocessing Pipeline<br/>Impute → Transform<br/>→ Encode → Scale]
        PA_Preprocess --> PA_Split[Stratified Split<br/>70% Train<br/>15% Val<br/>15% Test]
        
        PA_Split --> PA_Train[Train 3 Models<br/>Logistic, KNN, XGBoost]
        PA_Train --> PA_EvalVal[Evaluate on Val Set<br/>Tune thresholds<br/>for FPR ≤ 3%]
        PA_EvalVal --> PA_EvalTest[Test Set Evaluation<br/>Final unbiased metrics]
        
        PA_EvalTest --> PA_Select[Select Best Model<br/>Highest ROC AUC]
        PA_Select --> PA_Persist[Persist Artifacts<br/>model.pkl<br/>preprocessor.pkl<br/>metrics.json]
    end
    
    %% ============================================================================
    %% SECTION 4: PREPROCESSING PIPELINE ORDER (Slide 8)
    %% ============================================================================
    
    PipelineArch --> PreprocOrder
    
    subgraph PreprocOrder["⚙️ PREPROCESSING PIPELINE: EVIDENCE-BASED ORDER"]
        PP_Raw[Raw Features] -->|1. Imputation| PP_Impute[Fill Missing:<br/>Median/Mode]
        PP_Impute -->|2. Engineering| PP_Engineer[Create Features:<br/>Ratios, Bins, Flags]
        PP_Engineer -->|3. Encoding| PP_Encode[Categorical → Numeric:<br/>OneHot, Frequency]
        PP_Encode -->|4. Scaling| PP_Scale[Standardize:<br/>Z-score/Robust]
        
        PP_Scale --> PP_Final[Transformed Features<br/>Ready for Training]
        
        PP_Reason1[Why 1st: Imputation<br/>→ Missing breaks<br/>downstream ops]
        PP_Reason2[Why 2nd: Engineering<br/>→ Create domain features<br/>from clean data]
        PP_Reason3[Why 3rd: Encoding<br/>→ Categorical → numeric<br/>before scaling]
        PP_Reason4[Why 4th: Scaling<br/>→ Standardize final<br/>numeric features]
        
        PP_Save[Saved as<br/>preprocessor.pkl<br/>→ Test data undergoes<br/>identical transformations]
    end
    
    %% ============================================================================
    %% SECTION 5: TOP 10 PREDICTIVE FEATURES (Slide 9)
    %% ============================================================================
    
    PreprocOrder --> TopFeatures
    
    subgraph TopFeatures["⭐ TOP 10 PREDICTIVE FEATURES"]
        TF_Rank1[1. DomainAgeMonths<br/>r=0.333<br/>Younger = higher risk]
        TF_Rank2[2. IsResponsive<br/>r=0.330<br/>Non-responsive = suspicious]
        TF_Rank3[3. Robots<br/>r=0.242<br/>Missing robots.txt = fraud]
        TF_Rank4[4. NoOfiFrame<br/>r=0.150<br/>Excessive = obfuscation]
        TF_Rank5[5. NoOfExternalRef<br/>r=0.128<br/>Link pattern differs]
        
        TF_FE1[Feature Engineering:<br/>DomainAge → Bins<br/><6mo, 6-12mo,<br/>12-24mo, >24mo]
        TF_FE2[Feature Engineering:<br/>Missing flags<br/>Robots_missing<br/>IsResponsive_missing]
        TF_FE3[Feature Engineering:<br/>External/Self Ratio<br/>NoOfExternalRef /<br/>NoOfSelfRef + 1]
        
        TF_Insight[💡 Key Insight:<br/>Domain metadata<br/>stronger than<br/>content features]
        
        TF_Rank1 --> TF_FE1
        TF_Rank2 --> TF_FE2
        TF_Rank3 --> TF_FE2
        TF_Rank5 --> TF_FE3
    end
    
    %% ============================================================================
    %% SECTION 6: MODEL SELECTION RATIONALE (Slide 10)
    %% ============================================================================
    
    TopFeatures --> ModelSelection
    
    subgraph ModelSelection["🤖 MODEL SELECTION RATIONALE"]
        MS_Logistic[Logistic Regression<br/>──────────────<br/>✅ Coefficient interpretability<br/>✅ Fast inference ~1ms<br/>✅ Regulatory explainability<br/>❌ Linear boundary<br/>Expected: ROC AUC 0.75-0.78]
        
        MS_KNN[K-Nearest Neighbors<br/>──────────────<br/>✅ Non-parametric local patterns<br/>✅ No training needed lazy<br/>✅ Baseline comparison<br/>❌ Slow inference<br/>Expected: ROC AUC 0.78-0.82]
        
        MS_XGBoost[XGBoost<br/>──────────────<br/>✅ Industry standard for fraud<br/>✅ Handles imbalance natively<br/>✅ Feature importance via SHAP<br/>❌ Black-box needs SHAP<br/>Expected: ROC AUC 0.83-0.87]
        
        MS_WhyNot[❌ Why NOT Neural Networks?<br/>──────────────<br/>Dataset too small 11,430 rows<br/>Tree ensembles outperform<br/>on structured data]
    end
    
    %% ============================================================================
    %% SECTION 7: MODEL PERFORMANCE RESULTS (Slide 11)
    %% ============================================================================
    
    ModelSelection --> ModelPerformance
    
    subgraph ModelPerformance["📈 MODEL PERFORMANCE RESULTS"]
        MP_XGB[XGBoost<br/>──────────────<br/>Recall: 86.51%<br/>FPR: 18.22%<br/>ROC AUC: 0.8880<br/>✅ Recall ≥ 70%<br/>❌ FPR > 3%]
        
        MP_Logistic[Logistic Regression<br/>──────────────<br/>Recall: 81.20%<br/>FPR: 21.89%<br/>ROC AUC: 0.8252<br/>✅ Recall ≥ 70%<br/>❌ FPR > 3%]
        
        MP_KNN[K-Nearest Neighbors<br/>──────────────<br/>Recall: 82.35%<br/>FPR: 29.10%<br/>ROC AUC: 0.8091<br/>✅ Recall ≥ 70%<br/>❌ FPR > 3%]
        
        MP_Strength[✅ Strengths:<br/>All achieve Recall ≥ 70%<br/>XGBoost reaches 86.51%]
        
        MP_Gap[❌ Gap:<br/>FPR constraint ≤3%<br/>not met with<br/>default threshold 0.5]
        
        MP_Solution[📈 Solution:<br/>Threshold tuning OR<br/>advanced feature<br/>engineering required]
    end
    
    %% ============================================================================
    %% SECTION 8: THRESHOLD TUNING TRADE-OFF (Slide 12)
    %% ============================================================================
    
    ModelPerformance --> ThresholdTuning
    
    subgraph ThresholdTuning["⚖️ THRESHOLD TUNING: TRADE-OFF ANALYSIS"]
        TT_Default[Default Threshold: 0.5] --> TT_DefaultPerf[XGBoost Performance:<br/>Recall=86.51%<br/>FPR=18.22%]
        
        TT_DefaultPerf --> TT_Tune{Tune Threshold<br/>for FPR ≤ 3%?}
        
        TT_Tune -->|Increase to 0.88| TT_Tuned[Tuned Performance:<br/>Recall=7.61%<br/>FPR=2.26%]
        
        TT_Tuned --> TT_Decision{Business Decision}
        
        TT_Decision -->|Prioritize<br/>User Trust| TT_LowFPR[✅ Use FPR ≤ 3%<br/>Accept lower recall]
        TT_Decision -->|Prioritize<br/>Security| TT_HighRecall[✅ Use default 0.5<br/>Accept higher FPR]
        
        TT_Learning[💡 Key Learning:<br/>FPR ≤ 3% tanks recall to 7.61%<br/>→ violates 70% KPI<br/>Need better features OR<br/>ensemble methods OR<br/>accept 5% FPR]
    end
    
    %% ============================================================================
    %% SECTION 9: GROWTH AREAS (Slide 13)
    %% ============================================================================
    
    ThresholdTuning --> GrowthAreas
    
    subgraph GrowthAreas["🌱 WHAT I'D DO DIFFERENTLY - GROWTH AREAS"]
        GA_URLFeatures[Advanced Features: URL-Based<br/>──────────────<br/>• Subdomain depth<br/>• Suspicious TLDs .tk .ml<br/>• URL entropy random strings]
        
        GA_HTMLFeatures[Advanced Features: HTML-Based<br/>──────────────<br/>• Script-to-content ratio<br/>• Hidden iframes count<br/>• DOM tree complexity]
        
        GA_TimeFeatures[Advanced Features: Time-Based<br/>──────────────<br/>• Domain registration vs first seen<br/>• SSL certificate age]
        
        GA_HyperOpt[Hyperparameter Optimization<br/>──────────────<br/>• Bayesian optimization Optuna<br/>• Early stopping validation<br/>• Ensemble methods stacking]
        
        GA_Production[Production Readiness<br/>──────────────<br/>• Model monitoring dashboard<br/>• A/B testing framework<br/>• SHAP explainability]
        
        GA_Philosophy[💡 Philosophy:<br/>Built solid foundation<br/>→ Ready to learn<br/>advanced techniques]
    end
    
    %% ============================================================================
    %% SECTION 10: REPRODUCIBILITY GUARANTEES (Slide 14)
    %% ============================================================================
    
    GrowthAreas --> Reproducibility
    
    subgraph Reproducibility["🔄 REPRODUCIBILITY GUARANTEES"]
        Rep_Framework[Reproducibility Framework]
        
        Rep_Framework --> Rep_Env[Environment Control]
        Rep_Framework --> Rep_Data[Data Versioning]
        Rep_Framework --> Rep_Pipeline[Pipeline Determinism]
        
        Rep_Env --> Rep_Env1[requirements.txt:<br/>Pinned versions<br/>xgboost==2.1.1]
        Rep_Env --> Rep_Env2[Python 3.8-3.11<br/>tested]
        Rep_Env --> Rep_Env3[Ubuntu 20.04<br/>macOS 13+]
        
        Rep_Data --> Rep_Data1[SHA256 hash of<br/>phishing.db]
        Rep_Data --> Rep_Data2[Stratified splits:<br/>random_state=42]
        
        Rep_Pipeline --> Rep_Pipeline1[config.yaml<br/>version-controlled]
        Rep_Pipeline --> Rep_Pipeline2[Timestamped experiments:<br/>run_YYYYMMDD_HHMMSS/]
        Rep_Pipeline --> Rep_Pipeline3[All artifacts serialized:<br/>models/*.pkl<br/>results/*.json]
        
        Rep_Verify[✅ Verification:<br/>GitHub Actions CI/CD<br/>runs bash run.sh<br/>→ generates identical<br/>baseline_metrics.json]
    end
    
    %% ============================================================================
    %% SECTION 11: DEPLOYMENT ARCHITECTURE (Slide 15)
    %% ============================================================================
    
    Reproducibility --> Deployment
    
    subgraph Deployment["🚀 DEPLOYMENT ARCHITECTURE - PRODUCTION-READY"]
        Deploy_Browser[Browser Extension] -->|Extract URL<br/>metadata| Deploy_Gateway[API Gateway]
        Deploy_Gateway -->|HTTPS POST| Deploy_Lambda[Lambda Function<br/>Model Serving]
        
        Deploy_Lambda -->|Load artifacts| Deploy_S3[(S3 Bucket:<br/>model.pkl<br/>preprocessor.pkl)]
        
        Deploy_S3 --> Deploy_Lambda
        Deploy_Lambda -->|Preprocess| Deploy_Pipeline[Pipeline Transform]
        Deploy_Pipeline -->|Predict| Deploy_Model[XGBoost Model]
        
        Deploy_Model -->|probability| Deploy_Decision{Threshold<br/>Decision}
        
        Deploy_Decision -->|prob > 0.7| Deploy_Block[Response:<br/>is_phishing: true<br/>confidence: 0.92]
        Deploy_Decision -->|prob ≤ 0.7| Deploy_Allow[Response:<br/>is_phishing: false<br/>confidence: 0.31]
        
        Deploy_Lambda -->|Metrics| Deploy_Monitor[CloudWatch:<br/>Latency p50/p99<br/>Error Rate<br/>Feature Drift]
        
        Deploy_Latency[⏱️ Latency Budget:<br/><100ms total<br/>50ms extraction<br/>30ms inference<br/>20ms network]
    end
    
    %% ============================================================================
    %% SECTION 12: KEY TAKEAWAYS (Slide 16)
    %% ============================================================================
    
    Deployment --> Takeaways
    
    subgraph Takeaways["🎯 KEY TAKEAWAYS: WHY SELECT ME?"]
        TA_Structured[1. Structured Thinking<br/>──────────────<br/>✅ Systematic EDA<br/>✅ Evidence-based decisions<br/>✅ Reproducible pipeline<br/>Artifact: README.md]
        
        TA_Production[2. Production Focus<br/>──────────────<br/>✅ Automated end-to-end<br/>✅ Serialized artifacts<br/>✅ CI/CD tested<br/>Artifact: models/*.pkl]
        
        TA_Growth[3. Growth Mindset<br/>──────────────<br/>✅ Documented learnings<br/>✅ Clear about gaps<br/>✅ Eager to learn<br/>Commitment: Learn & document]
    end
    
    %% ============================================================================
    %% SECTION 13: CLOSING (Slide 17)
    %% ============================================================================
    
    Takeaways --> Closing
    
    subgraph Closing["✨ CLOSING: WHAT I BRING TO YOUR TEAM"]
        Close_NotMost[I'm not the most experienced candidate]
        
        Close_ButIAm[But I'm the one who will:]
        Close_ButIAm --> Close_Ask[✅ Ask the right questions<br/>Learn domain from analysts]
        Close_ButIAm --> Close_Document[✅ Document everything<br/>Knowledge transfer for team]
        Close_ButIAm --> Close_Learn[✅ Learn rapidly<br/>First 30 days: feature sprint]
        
        Close_Philosophy[Core Philosophy:<br/>Build solid foundations<br/>through systematic work,<br/>then scale up with<br/>advanced techniques]
        
        Close_Evidence[Evidence of Readiness:<br/>✅ Pipeline functional<br/>✅ Artifacts documented<br/>✅ Honest about gaps]
        
        Close_Thanks[Thank you.<br/>Ready for questions.]
    end
    
    %% ============================================================================
    %% BACKUP SLIDES: ADDITIONAL TECHNICAL DETAILS
    %% ============================================================================
    
    Closing --> BackupSlides
    
    subgraph BackupSlides["📦 BACKUP SLIDES - FOR Q&A"]
        Backup_Repo[Repository Structure<br/>──────────────<br/>├── .github/workflows/<br/>├── src/<br/>│   ├── data_loader.py<br/>│   ├── preprocessing.py<br/>│   └── models/<br/>├── eda.ipynb<br/>├── README.md<br/>└── run.sh]
        
        Backup_Error[Error Analysis Example<br/>──────────────<br/>Scenario: False positive<br/>on banking site<br/><br/>1. Reproduce with predict.py<br/>2. Feature inspection<br/>3. SHAP explainability<br/>4. Corrective actions]
        
        Backup_Retrain[Retraining Strategy<br/>──────────────<br/>Scheduled: Quarterly<br/>Performance Decay: Ad-hoc<br/>Feature Drift: Ad-hoc<br/>Major Event: Immediate<br/><br/>Pipeline: Query → Merge<br/>→ Run → A/B test → Rollout]
    end
    
    BackupSlides --> PresentationEnd([✅ PRESENTATION END<br/>Transition to Q&A<br/>50 Minutes])
    
    %% ============================================================================
    %% STYLING DEFINITIONS
    %% ============================================================================
    
    classDef problemStyle fill:#fff3e0,stroke:#f57c00,stroke-width:3px
    classDef edaStyle fill:#f3e5f5,stroke:#7b1fa2,stroke-width:3px
    classDef pipelineStyle fill:#e3f2fd,stroke:#1976d2,stroke-width:3px
    classDef modelStyle fill:#fce4ec,stroke:#c2185b,stroke-width:3px
    classDef successStyle fill:#e8f5e9,stroke:#2e7d32,stroke-width:3px
    classDef errorStyle fill:#ffebee,stroke:#c62828,stroke-width:3px
    classDef warningStyle fill:#fff9c4,stroke:#f57f17,stroke-width:2px
    classDef infoStyle fill:#e0f2f1,stroke:#00695c,stroke-width:2px
    
    %% Apply styles to nodes
    class BP_Model,BP_Challenge,BP_Impact,BP_KPIs,BP_Deploy problemStyle
    class EDA_Issue1,EDA_Issue2,EDA_Issue3,EDA_Issue4,EDA_Issue5,EDA_Issue6,EDA_Principle edaStyle
    class PA_DB,PA_Validate,PA_Quality,PA_Engineer,PA_Preprocess,PA_Split,PA_Train pipelineStyle
    class MS_Logistic,MS_KNN,MS_XGBoost,MP_XGB,MP_Logistic,MP_KNN modelStyle
    class BP_Allow,EDA_Sol1,EDA_Sol2,EDA_Sol3,EDA_Sol4,EDA_Sol5,EDA_Sol6,PA_Persist,Deploy_Allow,Close_Thanks successStyle
    class BP_Block,PA_Error,MP_Gap,TT_Tuned,Deploy_Block errorStyle
    class TT_Learning,GA_Philosophy,Rep_Verify warningStyle
    class TF_Insight,Close_Philosophy,Close_Evidence infoStyle
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