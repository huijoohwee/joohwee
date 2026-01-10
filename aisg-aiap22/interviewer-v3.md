# interviewer.md

## AIAP Batch 22 Technical Assessment - Interview Panel Guide

**Document Version**: 1.0  
**Panel Lead**: Technical Assessment Evaluator  
**Session Duration**: 1 hour (10 min presentation + 50 min Q&A)

---

## Executive Summary

This guide provides the interview panel with:
1. **FAQs Framework**: Structured questions targeting critical competencies
2. **Scoring Rubric**: Objective criteria to classify candidates as Poor/Qualified/Excellent
3. **Assessment Methodology**: Real-time evaluation during the interview session
4. **Red Flags & Green Flags**: Behavioral indicators for quick screening

**Usage**: Use this document to standardize evaluation across all candidates and ensure fair, competency-based selection aligned with AIAP program requirements.

---

## Candidate Profile Analysis

### Submission Overview
- **Repository**: `aiap22-hui-joo-hwee-045B`
- **EDA Deliverable**: `eda.ipynb` - Comprehensive but verbose (business-heavy framing)
- **MLP Deliverable**: `src/*.py` - Modular, config-driven pipeline with 3 models
- **README Quality**: Excellent documentation (Mermaid diagrams, evidence-based design)

### Initial Assessment (Pre-Interview)

**Strengths**:
- ✅ Complete deliverables (all required files present)
- ✅ Evidence-based pipeline design (EDA findings → MLP decisions)
- ✅ Professional documentation (tables, diagrams, compliance checklist)
- ✅ CI/CD integration (GitHub Actions)

**Concerns**:
- ⚠️ **Overly verbose EDA** (business jargon may mask weak technical depth)
- ⚠️ **Custom implementations** (NumPy LogReg, custom KNN) - reinventing wheel vs sklearn?
- ⚠️ **Performance gaps** (all models fail KPIs: FPR 18-29%, Recall drops to 7-12% at FPR≤3%)
- ⚠️ **No hyperparameter tuning evidence** (mentions optimization.py but no grid search results)

**Interview Goal**: Determine if candidate genuinely understands ML fundamentals or merely followed templates/ChatGPT.

---

## Scoring Rubric (0-100 Points)

### Category 1: EDA Competency (25 points)

| Criteria | Poor (0-8) | Qualified (9-17) | Excellent (18-25) |
|----------|------------|------------------|-------------------|
| **Data Quality Assessment** | Cannot explain missingness patterns or outlier detection methods | Correctly identifies IQR method, missing thresholds (70%, 20-70%), but struggles with MNAR vs MAR | Articulates why MNAR matters for fraud detection, justifies threshold choices with business context |
| **Statistical Interpretation** | Confuses correlation with causation, cannot explain skewness impact | Correctly calculates skewness, correlation, but unclear on why log-transform improves convergence | Explains heavy-tail distributions → gradient instability, links to model selection (e.g., tree ensembles robust to skew) |
| **Visualization Choices** | Uses default plots without customization, no interpretations | Creates clear plots (histograms, heatmaps) but misses key insights (e.g., class imbalance in heatmap) | Designs visualizations to answer specific questions (e.g., missingness heatmap reveals MNAR pattern) |
| **Actionable Insights** | Lists EDA steps without linking to preprocessing | Identifies quality issues but vague remediation (e.g., "handle outliers") | Concrete preprocessing roadmap (e.g., "clip NoOfImage at 99th percentile because 14.47% outliers from adversarial manipulation") |

**Red Flags**:
- Cannot explain why stratified splitting is necessary
- Confuses ROC AUC calculation with accuracy
- Claims "no duplicates" without showing verification code

**Green Flags**:
- Immediately identifies class imbalance (55:45) as requiring stratified sampling
- Explains DomainAgeMonths as top predictor due to correlation (r=0.333) AND business logic (new domains = higher risk)
- Links 377 negative NoOfImage values to "synthetic/contaminated data" requirement

---

### Category 2: Preprocessing & Feature Engineering (20 points)

| Criteria | Poor (0-6) | Qualified (7-13) | Excellent (14-20) |
|----------|------------|------------------|-------------------|
| **Imputation Strategy** | Uses mean/mode without justification | Correctly applies median for numeric, mode for categorical, but cannot explain why median > mean | Justifies median (robust to outliers) and explains why missing-value flags preserve MNAR signal for fraud detection |
| **Scaling Rationale** | Applies StandardScaler without knowing when to use RobustScaler | Knows StandardScaler assumes normality, RobustScaler uses median/IQR | Explains config.yaml choice based on EDA (RobustScaler if outliers >10%, else StandardScaler for faster convergence) |
| **Feature Engineering Depth** | No engineered features beyond one-hot encoding | Creates basic bins/ratios but cannot explain predictive value | Designs domain-age bins aligned with fraud lifecycle (e.g., <6mo = fresh phishing campaigns), explains External/Self-Ref ratio captures link manipulation |
| **Transformation Justification** | Applies log-transform to all skewed features blindly | Correctly identifies \|skew\|>1 threshold but unclear on why log vs Box-Cox | Explains log-transform stabilizes variance for gradient descent, avoids Box-Cox due to zero-value handling complexity |

**Red Flags**:
- Cannot explain difference between StandardScaler and MinMaxScaler
- Encodes categorical variables as integers (ordinal encoding) without one-hot
- Applies PCA without checking feature interpretability requirements

**Green Flags**:
- Walks through `preprocessing.py` ColumnTransformer pipeline step-by-step
- Explains why clipping NoOfImage negatives to 0 (impossible values) before log-transform
- Justifies rare-category grouping (<1% → "Other") as noise reduction for regularization

---

### Category 3: Model Selection & Training (25 points)

| Criteria | Poor (0-8) | Qualified (9-17) | Excellent (18-25) |
|----------|------------|------------------|-------------------|
| **Algorithm Justification** | Chooses models randomly or because "everyone uses XGBoost" | Correctly identifies Logistic Regression (interpretable), KNN (non-parametric), XGBoost (handles imbalance) but shallow rationale | Explains trade-offs: LogReg (fast inference, coefficients for compliance) vs XGBoost (SHAP for post-hoc explainability, better performance but black-box) |
| **Hyperparameter Understanding** | Cannot explain learning rate, max_depth, or k in KNN | Knows parameter definitions but unclear on tuning impact (e.g., higher k → smoother boundaries) | Articulates learning_rate=0.2 → faster convergence but overfitting risk, max_depth=6 → balance complexity vs generalization, validates via cross-validation |
| **Training Process** | Trains on full dataset without validation set | Uses train/val/test split but unclear on stratification necessity | Implements stratified 70/15/15 split, uses validation set for threshold tuning, explains why test set untouched until final evaluation |
| **Custom Implementations** | Cannot explain NumPy gradient descent logic or KNN distance calculation | Correctly implements algorithms but inefficient (e.g., no vectorization) | Justifies custom LogReg (educational, avoids sklearn dependency), optimizes with NumPy broadcasting, explains when to use sklearn instead |

**Red Flags**:
- Claims "XGBoost always best" without comparing to baselines
- Trains models on imbalanced data without class weights or stratified sampling
- Cannot explain why validation set needed (confuses with cross-validation)

**Green Flags**:
- Immediately identifies class imbalance → scale_pos_weight in XGBoost config
- Explains early_stopping_rounds=20 prevents overfitting by monitoring validation loss
- Justifies custom KNN (learning exercise) but acknowledges sklearn KNeighborsClassifier for production

---

### Category 4: Evaluation & Threshold Tuning (20 points)

| Criteria | Poor (0-6) | Qualified (7-13) | Excellent (14-20) |
|----------|------------|------------------|-------------------|
| **Metric Selection** | Uses only accuracy or F1-score | Correctly calculates ROC AUC, precision, recall but unclear on business relevance | Explains Recall≥70% (customer fraud exposure), FPR≤3% (user trust), ROC AUC (regulatory compliance), links metrics to business KPIs |
| **Threshold Tuning Logic** | Uses default 0.5 threshold without justification | Tunes threshold on validation set but unclear on FPR constraint | Explains threshold sweep (0.0→1.0, step=0.01), maximizes recall subject to FPR≤3%, validates on test set for unbiased estimate |
| **Confusion Matrix Interpretation** | Confuses TP/FP/TN/FN or cannot calculate FPR from matrix | Correctly calculates FPR=FP/(FP+TN) but struggles with business impact | Interprets confusion matrix as "at threshold=0.97, XGBoost catches 12% of phishing (too low) but only 2.82% false alarms on legitimate sites" |
| **Trade-off Analysis** | Cannot explain precision-recall trade-off | Knows increasing threshold → higher precision, lower recall but vague on decision | Articulates "FPR≤3% constraint forces threshold=0.97 → recall drops to 12% → violates Recall≥70% KPI → need ensemble methods or SMOTE to balance" |

**Red Flags**:
- Claims "ROC AUC=0.88 is excellent" without comparing to baseline (55% majority class)
- Cannot explain why FPR matters more than precision for phishing detection
- Applies threshold tuning to test set directly (data leakage)

**Green Flags**:
- Explains ROC curve as "TP Rate vs FP Rate across all thresholds → area measures discrimination"
- Justifies PR curve for imbalanced data (focuses on minority class performance)
- Links tuned threshold to deployment (e.g., "threshold=0.88 → 7.61% recall too low → retrain with SMOTE")

---

### Category 5: Code Quality & Reproducibility (10 points)

| Criteria | Poor (0-3) | Qualified (4-6) | Excellent (7-10) |
|----------|------------|------------------|-------------------|
| **Modularity** | Monolithic scripts, no functions/classes | Modular structure but tight coupling (e.g., hard-coded paths) | Loosely coupled modules, dependency injection via config.yaml, clear separation of concerns |
| **Documentation** | No docstrings or comments | Basic docstrings but unclear on parameter types/return values | Google-style docstrings with type hints, README with Mermaid diagrams, inline comments for complex logic |
| **Reproducibility** | No random seeds or version pinning | Fixed random seeds but requirements.txt missing versions | Pinned dependencies (xgboost==2.1.1), random seeds (42), experiment metadata (Git commit hash), validation JSON |

**Red Flags**:
- `run.sh` installs dependencies (violates assessment requirement)
- Hard-coded paths (`/Users/candidate/data/phishing.db`)
- No error handling (crashes on missing database)

**Green Flags**:
- Config-driven architecture (all hyperparameters in config.yaml)
- Experiment logging with timestamps (`experiments/run_20251201_143022/`)
- GitHub Actions CI/CD validates reproducibility

---

## FAQs Framework (Structured Q&A)

### Opening Questions (Warm-Up, 5 minutes)

**Q1**: Walk us through your 10-minute presentation structure. What are the 3 key points you want us to remember?

**Purpose**: Assess communication skills and prioritization.

**Scoring**:
- **Poor**: Rambles through README/notebook without structure
- **Qualified**: Highlights EDA findings → MLP design → Results
- **Excellent**: Crisp narrative: "1) Class imbalance drove stratified splits, 2) DomainAge top predictor informed feature engineering, 3) All models fail KPIs → need SMOTE/ensemble"

---

**Q2**: If you had to delete one section from your README, which would it be and why?

**Purpose**: Test understanding of essential vs superficial content.

**Scoring**:
- **Poor**: "None, everything is important" (lacks critical thinking)
- **Qualified**: "Business Impact Summary redundant with EDA findings"
- **Excellent**: "Deployment Considerations premature without meeting KPIs first → focus should be model improvement roadmap"

---

### EDA Deep Dive (10 minutes)

**Q3**: You reported 0 duplicates and 0 features with >70% missingness. Walk me through the code that validates this. What if I claimed there ARE duplicates—how would you verify?

**Purpose**: Test if candidate actually ran the analysis or copied templates.

**Expected Answer**:
```python
# Duplicates
dup_count = df.duplicated().sum()  # Returns 0
# Verification: df[df.duplicated(keep=False)] shows all duplicate rows

# Missingness >70%
mv_pct = df.isna().mean() * 100
high_missing = mv_pct[mv_pct >= 70]  # Returns empty Series
```

**Scoring**:
- **Poor**: Cannot recall code or method
- **Qualified**: Describes `.duplicated()` but unclear on `keep=False` parameter
- **Excellent**: Explains `keep=False` shows all duplicates (not just first), validates with `df.shape` before/after drop

---

**Q4**: Your heatmap shows "systematic missingness" in phishing sites. What does MNAR (Missing Not At Random) mean, and why does it matter for fraud detection?

**Purpose**: Distinguish statistical knowledge from business intuition.

**Expected Answer**:
- **MNAR**: Missingness depends on unobserved value itself (e.g., phishing sites deliberately omit DomainAge to hide newness)
- **Impact**: Simple imputation (median) loses signal → create binary flags (`DomainAge_missing`) as predictive feature
- **Alternative**: MAR (Missing At Random) = missingness depends on observed variables, MCAR (Missing Completely At Random) = random missingness

**Scoring**:
- **Poor**: "MNAR means missing data" (tautology)
- **Qualified**: Correctly defines MNAR but unclear on fraud relevance
- **Excellent**: "Phishing sites hide metadata to evade detection → missingness itself is fraud signal → `*_missing` flags capture adversarial behavior"

---

**Q5**: You applied log-transform to 10 features with |skew| > 1. Why log instead of square root or Box-Cox? When would log-transform FAIL?

**Purpose**: Test transformation rationale beyond cookbook rules.

**Expected Answer**:
- **Why log**: Stabilizes variance for multiplicative processes, simple to interpret (log(x+1) handles zeros), computationally cheap
- **vs sqrt**: Less aggressive (sqrt compresses less than log), used when skew moderate
- **vs Box-Cox**: Requires parameter search (λ), complex for zero-values, overkill for this dataset
- **Failure cases**: Negative values (need shift), zero-inflation (log(0) undefined), already normal distribution

**Scoring**:
- **Poor**: "Log-transform always works for skewed data"
- **Qualified**: Knows log handles heavy tails but unclear on alternatives
- **Excellent**: "Used log(x+1) for zero-safe transform, considered Box-Cox but interpretability cost not worth performance gain for baseline models"

---

### Preprocessing Deep Dive (10 minutes)

**Q6**: Your `preprocessing.py` has a ColumnTransformer. Explain the difference between `fit_transform(X_train)` and `transform(X_test)`. What happens if you `fit_transform(X_test)`?

**Purpose**: Fundamental sklearn pipeline understanding.

**Expected Answer**:
- **fit_transform(X_train)**: Learns parameters (mean/std for scaler, categories for encoder) from training data, applies transformation
- **transform(X_test)**: Applies learned parameters to test data WITHOUT re-learning
- **Danger of fit_transform(X_test)**: Data leakage → test statistics contaminate model → overly optimistic performance

**Scoring**:
- **Poor**: "Both transform data, no difference"
- **Qualified**: Knows fit learns parameters but unclear on leakage impact
- **Excellent**: "fit_transform on test = data leakage → test mean/std differ from train → model sees future information → invalid evaluation"

---

**Q7**: You created `External_to_Self_Ratio = NoOfExternalRef / (NoOfSelfRef + 1)`. Why add 1 to denominator? What if both are 0?

**Purpose**: Test feature engineering edge case handling.

**Expected Answer**:
- **Why +1**: Avoid division by zero when NoOfSelfRef=0
- **Edge case**: If both=0, ratio=0/1=0 (interpretable as "no links at all")
- **Alternative**: Could use log((External+1)/(Self+1)) for symmetry, or flag zero-case separately

**Scoring**:
- **Poor**: "To avoid errors" (no mathematical understanding)
- **Qualified**: Correctly identifies division-by-zero but unclear on 0/0 case
- **Excellent**: "Added 1 as Laplace smoothing → 0/1=0 interpretable as 'no external links', considered log-ratio but kept simple for baseline"

---

**Q8**: Your README states "Group rare categories (<1%) as Other". How do you determine this 1% threshold? What if a rare category is highly predictive?

**Purpose**: Challenge blind application of heuristics.

**Expected Answer**:
- **Threshold justification**: Balance noise reduction vs information loss → 1% empirical rule (too rare = sparse one-hot columns)
- **Predictive rare category**: Check correlation with target BEFORE grouping → if r>0.2, keep separate
- **Alternative**: Use frequency encoding (preserve rarity signal) or target encoding (supervised)

**Scoring**:
- **Poor**: "1% is standard practice" (no critical thinking)
- **Qualified**: Acknowledges trade-off but unclear on validation
- **Excellent**: "1% threshold configurable in config.yaml, validated via ablation study (compare model performance with/without grouping), willing to adjust if rare category has high target correlation"

---

### Model Selection Deep Dive (10 minutes)

**Q9**: You implemented custom Logistic Regression in NumPy. Walk me through gradient descent. What's the update rule? How do you know it converged?

**Purpose**: Verify genuine implementation vs copy-paste.

**Expected Answer**:
- **Update rule**: `θ = θ - α * ∇L(θ)` where ∇L = (1/m) * X^T * (σ(Xθ) - y)
- **Convergence**: Monitor loss decrease per epoch, stop if change < tolerance (e.g., 1e-6) or max epochs reached
- **Sigmoid**: σ(z) = 1 / (1 + e^(-z))

**Scoring**:
- **Poor**: Cannot recall gradient formula
- **Qualified**: Knows gradient involves X^T*(pred-actual) but unclear on vectorization
- **Excellent**: "Used NumPy broadcasting for efficiency, added L2 penalty (θ^T θ) for regularization, monitored log-loss convergence, typical ~100 epochs at lr=0.1"

---

**Q10**: Your XGBoost achieved ROC AUC=0.888 but FPR=18.22%. Why did XGBoost outperform Logistic Regression (0.825) but still fail the FPR≤5% KPI?

**Purpose**: Test diagnostic reasoning.

**Expected Answer**:
- **Why XGBoost > LogReg**: Captures non-linear interactions (tree splits), handles class imbalance better (scale_pos_weight), ensemble reduces variance
- **Why FPR high**: Default threshold=0.5 optimizes F1/accuracy, not FPR → need threshold tuning
- **Root cause**: Class imbalance (55:45) → model biased toward majority class → higher false alarm rate

**Scoring**:
- **Poor**: "XGBoost always better" (no analysis)
- **Qualified**: Identifies threshold issue but unclear on class imbalance impact
- **Excellent**: "FPR=18% means 1 in 5 legitimate sites flagged → threshold=0.5 too lenient → tuned to 0.97 (FPR=2.82%) but recall collapsed to 12% → need SMOTE or class weights to rebalance"

---

**Q11**: Your KNN uses k=5. How did you choose 5? What happens if k=1 or k=100?

**Purpose**: Test hyperparameter intuition.

**Expected Answer**:
- **k=5**: Empirical starting point, validated via cross-validation (should show grid search results)
- **k=1**: Overfitting (memorizes training noise), high variance, sensitive to outliers
- **k=100**: Underfitting (overly smooth boundaries), high bias, loses local patterns
- **Optimal k**: Depends on dataset size and noise level (typically √n as heuristic)

**Scoring**:
- **Poor**: "k=5 is default" (no justification)
- **Qualified**: Knows k controls bias-variance but unclear on validation
- **Excellent**: "Tested k=[3,5,7,9] via stratified 5-fold CV, k=5 balanced validation ROC AUC (0.81) and inference speed, k=7 similar performance but slower"

---

### Evaluation Deep Dive (10 minutes)

**Q12**: Explain ROC AUC calculation WITHOUT using sklearn. How would you compute it manually from prediction scores?

**Purpose**: Distinguish conceptual understanding from API usage.

**Expected Answer**:
- **ROC curve**: Sort predictions descending, sweep thresholds, calculate TPR=TP/(TP+FN) and FPR=FP/(FP+TN) at each threshold
- **AUC**: Trapezoidal integration under ROC curve OR rank-based: AUC = P(score(positive) > score(negative))
- **Implementation**: Count pairs where positive scored higher than negative, divide by total pairs

**Scoring**:
- **Poor**: "ROC AUC is sklearn.metrics.roc_auc_score" (no understanding)
- **Qualified**: Knows ROC plots TPR vs FPR but unclear on AUC calculation
- **Excellent**: "Implemented rank-based AUC: sort scores, count concordant pairs (pos>neg), divide by n_pos*n_neg, matches sklearn output"

---

**Q13**: Your tuned threshold for XGBoost is 0.97 (Recall=12%, FPR=2.82%). Is this production-ready? How would you convince CyberProtect's CEO to deploy it?

**Purpose**: Test business judgment and stakeholder communication.

**Expected Answer**:
- **Production-ready**: NO → Recall=12% means missing 88% of phishing attacks → unacceptable fraud exposure
- **Trade-off**: FPR=2.82% excellent (low false alarms) but Recall too low
- **Solution**: Ensemble with rule-based system (e.g., blacklist known phishing domains), use model as secondary check
- **CEO pitch**: "Model catches 12% with high confidence (2.82% false alarm) → deploy for warnings, not blocking → iterate to Recall≥70%"

**Scoring**:
- **Poor**: "Yes, FPR<3% meets KPI" (ignores Recall failure)
- **Qualified**: Identifies Recall issue but unclear on remediation
- **Excellent**: "Current model unsuitable for autonomous blocking → deploy as 'soft warning' with human review → parallel track: retrain with SMOTE, cost-sensitive learning, or ensemble to hit Recall≥70%"

---

**Q14**: You calculated Precision and Recall. Explain the difference to a non-technical stakeholder (e.g., CyberProtect's CEO).

**Purpose**: Test communication skills and business translation.

**Expected Answer**:
- **Precision**: "Of all sites we flag as phishing, what % are actually phishing?" → Accuracy of alarms
- **Recall**: "Of all actual phishing sites, what % do we catch?" → Coverage of threats
- **Analogy**: Medical test → Precision=% of positive tests that are true disease, Recall=% of diseased patients detected
- **Business**: High Precision→ user trust (low false alarms), High Recall→ fraud prevention (catch attacks)

**Scoring**:
- **Poor**: Uses formulas (TP/FP/FN) without plain language
- **Qualified**: Correct definitions but no analogy
- **Excellent**: "Precision=trustworthiness of warnings, Recall=completeness of protection → need both high for production, currently trading off via threshold"

---

### Code Quality Deep Dive (5 minutes)

**Q15**: Your `run.sh` executes the pipeline. What happens if `data/phishing.db` is missing? Show me the error handling in your code.

**Purpose**: Test defensive programming and edge case handling.

**Expected Answer**:
```python
# data_loader.py
if not os.path.exists(db_path):
    raise FileNotFoundError(f"Database not found: {db_path}")
```

**Scoring**:
- **Poor**: No error handling → cryptic crash
- **Qualified**: Try-except but generic error message
- **Excellent**: Specific FileNotFoundError with instructions ("Download from assessment URL and place at data/phishing.db")

---

**Q16**: GitHub Actions runs your pipeline automatically. How do you ensure reproducibility across different machines (Ubuntu, macOS, Windows)?

**Purpose**: Test DevOps awareness and reproducibility.

**Expected Answer**:
- **Dependencies**: Pinned versions in requirements.txt (xgboost==2.1.1)
- **Random seeds**: Fixed at 42 in all random operations
- **Paths**: Relative paths (data/phishing.db, not /Users/candidate/...)
- **OS differences**: run.sh (bash) requires WSL on Windows (documented in README)

**Scoring**:
- **Poor**: "It works on my machine" (no reproducibility consideration)
- **Qualified**: Knows requirements.txt but unclear on path/seed issues
- **Excellent**: "CI tested on Ubuntu 20.04, macOS 13+, pinned Python 3.8-3.11, documented Windows users need WSL, SHA256 hash of phishing.db logged for version control"

---

### Closing Questions (5 minutes)

**Q17**: If you could restart this assessment with current knowledge, what would you do differently?

**Purpose**: Test self-awareness and learning mindset.

**Scoring**:
- **Poor**: "Nothing, my submission is perfect"
- **Qualified**: "Use sklearn instead of custom implementations to save time"
- **Excellent**: "1) Focus on hitting KPIs first (SMOTE, cost-sensitive learning) before custom code, 2) Run ablation studies to validate feature engineering, 3) Document hyperparameter grid search results in README"

---

**Q18**: CyberProtect wants to deploy your model tomorrow. What's the biggest risk, and how would you mitigate it in 24 hours?

**Purpose**: Test prioritization under pressure.

**Expected Answer**:
- **Biggest risk**: Recall=12% at FPR≤3% → missing 88% of phishing attacks → customer fraud exposure
- **24-hour fix**: 
  1. Lower FPR constraint to 10% (threshold~0.6) → Recall~70% → meets KPI
  2. Deploy with human review for high-risk cases (score 0.5-0.6)
  3. Parallel track: Retrain with SMOTE overnight

**Scoring**:
- **Poor**: "Just deploy, it's 88% ROC AUC" (ignores KPI failure)
- **Qualified**: Identifies Recall issue but unclear on quick fix
- **Excellent**: "Emergency deployment: Relax FPR to 10% (threshold=0.6), add human-in-loop for borderline cases, commit to Recall≥70% retraining within 1 week"

---

## Real-Time Assessment Rubric (During Interview)

### Presentation Phase (10 minutes)

**Observable Behaviors**:

| Indicator | Poor | Qualified | Excellent |
|-----------|------|-----------|-----------|
| **Structure** | No agenda, random walk through README | Clear 3-part structure (EDA→MLP→Results) | Executive summary upfront, tells a story with conflict/resolution |
| **Visual Aids** | Reads README verbatim | Shows key plots (ROC curve, confusion matrix) | Custom slides with annotated diagrams, highlights trade-offs |
| **Time Management** | Runs over 10 min or finishes in 5 min | Finishes within 10 min but rushed ending | Smooth pacing, reserves 1 min for Q&A preview |
| **Confidence** | Apologizes for submission quality | Neutral delivery | Enthusiastic about design choices, acknowledges limitations proactively |

**Scoring**: Deduct 5 points for poor structure/time management, award 5 bonus points for excellent storytelling.

---

### Q&A Phase (50 minutes)

**Behavioral Red Flags** (Immediate Disqualification):
- ❌ **Plagiarism Indicators**: Cannot explain own code when asked line-by-line
- ❌ **Defensive Hostility**: Argues with panel instead of addressing feedback
- ❌ **Fabrication**: Claims results not in submission (e.g., "I ran grid search but didn't save")
- ❌ **Fundamental Gaps**: Confuses basic concepts (correlation vs causation, bias vs variance)

**Green Flags** (Bonus Points):
- ✅ **Intellectual Humility**: "I should have validated that assumption" (shows learning mindset)
- ✅ **Deep Reasoning**: Unprompted explains trade-offs (e.g., "Chose median over mean because EDA showed 10% outliers")
- ✅ **Proactive Problem-Solving**: Suggests improvements before asked (e.g., "Next iteration would use SMOTE")
- ✅ **Handles Unknowns Well**: "I don't know X but would research Y approach" (resourcefulness)

---

## Final Scoring Summary

| Category | Weight | Poor (0-59) | Qualified (60-79) | Excellent (80-100) |
|----------|--------|-------------|-------------------|-------------------|
| EDA Competency | 25% | Cannot link findings to pipeline | Correct methods, shallow insights | Evidence-based design, business context |
| Preprocessing & FE | 20% | Template application, no justification | Correct transformations, unclear edge cases | Thoughtful choices, handles exceptions |
| Model Selection | 25% | Random algorithm choices | Baseline comparisons, weak rationale | Trade-off analysis, hyperparameter validation |
| Evaluation | 20% | Metric confusion, no business link | Correct calculations, vague interpretation | KPI-driven, threshold tuning, stakeholder communication |
| Code Quality | 10% | Monolithic scripts, no docs | Modular but poorly documented | Config-driven, reproducible, CI/CD |

**Total Score**: Sum of (Category Score × Weight)

**Pass Threshold**: 60/100 (Qualified) for AIAP admission

---

## Post-Interview Calibration

### Panel Discussion Framework

After each candidate interview, panel convenes for 10-minute calibration:

1. **Score Reconciliation**: Compare individual scores, discuss discrepancies >10 points
2. **Red Flag Review**: Any disqualifying behaviors observed? Unanimous veto required
3. **Comparative Ranking**: How does this candidate compare to previous interviewees?
4. **Final Decision**: Reject (<60), Waitlist (60-74), Accept (75-89), Strong Accept (90+)

### Tiebreaker Criteria (If Multiple Candidates Score 75-80)

1. **Code Quality** (most predictive of program success)
2. **Learning Mindset** (receptiveness to feedback during Q&A)
3. **Communication Skills** (ability to explain technical concepts simply)

---

## Appendix A: Sample Candidate Profiles

### Profile 1: "The Template Follower" (Score: 45-55)
- **Strengths**: Complete deliverables, follows instructions
- **Weaknesses**: Cannot explain EDA steps, says "I used sklearn" for everything, no original insights
- **Interview**: Stumbles on Q3 (duplicate verification), Q9 (gradient descent), Q12 (ROC AUC calculation)
- **Verdict**: Reject - lacks foundational understanding

---

### Profile 2: "The Solid Engineer" (Score: 70-80)
- **Strengths**: Correct methods, modular code, reproducible pipeline
- **Weaknesses**: Surface-level EDA insights, no hyperparameter tuning evidence, fails KPIs
- **Interview**: Answers Q1-Q

------

16 correctly but mechanically, struggles with Q13 (business judgment)
- **Verdict**: Qualified/Waitlist - competent but needs mentorship

---

### Profile 3: "The ML Practitioner" (Score: 85-95)
- **Strengths**: Evidence-based design, ablation studies, exceeds requirements (PR curves, Brier score)
- **Weaknesses**: Minor—overly verbose README
- **Interview**: Anticipates Q13-Q18, proposes SMOTE before asked, explains trade-offs clearly
- **Verdict**: Strong Accept - ready for AIAP challenges

---

## Appendix B: Controversial Q&A Handling

**Scenario**: Candidate challenges FPR≤3% as "too strict for real-world deployment"

**Panel Response**:
- ✅ **Good Answer**: "You're right that 3% is aggressive. Walk me through how you'd negotiate this requirement with CyberProtect's product team. What data would you present?"
- ❌ **Bad Answer**: "The assessment specifies 3%, so you must meet it" (shuts down critical thinking)

**Scoring**: Award 5 bonus points for reasoned pushback with data (e.g., "Industry benchmark is 5-10% FPR for fraud detection")

---

**END OF INTERVIEWER GUIDE**