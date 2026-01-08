# AIAP Batch 22 Interview Session - Panel Lead Guide

**Document Purpose**: Real-time assessment framework for 1-hour interview + 2-hour group exercise  
**Target Audience**: Interview panel leads and technical reviewers  
**Candidate Context**: Post-submission evaluation (README + EDA already reviewed)

---

## Executive Summary: Interview Session Structure

**Total Time**: 3 hours  
**Format**: Individual interview (1 hour) → Group exercise (2 hours)

### Interview Breakdown (60 minutes)
1. **Presentation** (10 min): Candidate presents submission
2. **Q&A Session** (50 min): Panel probes technical depth, business reasoning, problem-solving

### Group Exercise (120 minutes)
1. **Case Study** (disclosed on-site): Real-world ML problem
2. **Collaborative Coding**: 2-3 candidates work together
3. **Assessment Dimensions**: Technical skills, teamwork, communication, time management

---

## Part 1: 10-Minute Presentation Assessment

### Section A: Presentation Evaluation Framework

#### **What to Observe During Presentation**

**Content Selection (30% of presentation score)**
- Does candidate choose high-impact content or get lost in details?
- Is there a clear narrative arc (problem → approach → results → insights)?
- Do they prioritize business outcomes over technical minutiae?

**Communication Effectiveness (40% of presentation score)**
- Can they explain complex concepts to mixed-technical audience?
- Do they use visual aids effectively (README, notebook, or slides)?
- Is pacing appropriate (not rushed, not slow)?
- Do they make eye contact and engage panel vs reading text?

**Technical Depth Signals (30% of presentation score)**
- Do they demonstrate understanding or just recite documentation?
- Can they defend design decisions when questioned mid-presentation?
- Do they acknowledge limitations and gaps proactively?

---

#### **Scoring Rubric: 10-Minute Presentation**

| Criterion | Poor (0-3) | Qualified (4-6) | Excellent (7-10) | Weight |
|-----------|-----------|----------------|------------------|--------|
| **Narrative Structure** | Disorganized: jumps between topics, no clear flow | Sequential: EDA → Pipeline → Results, but flat narrative | Compelling: Problem framing → Evidence-based decisions → Business impact with story arc | 20% |
| **Content Prioritization** | Gets stuck on implementation details (code walkthrough, hyperparameter grids) | Covers all sections (EDA, preprocessing, models, results) but surface-level | Focuses on high-impact insights: KPI gap, top 3 EDA findings → pipeline decisions, model trade-offs | 20% |
| **Visual Communication** | Reads walls of text from README/notebook, no visual aids | Uses diagrams/charts but doesn't explain them clearly | Strategic visuals: EDA findings table, model comparison, threshold tuning curves with clear callouts | 15% |
| **Business Framing** | Pure technical description ("I trained XGBoost with max_depth=6") | Mentions business goals ("detect phishing") but doesn't quantify impact | Every decision tied to business: "55:45 imbalance → $90M fraud exposure → stratified splits critical" | 15% |
| **Audience Engagement** | Monotone, no eye contact, reads slides | Presents to panel, occasional eye contact | Conversational tone, eye contact, invites questions, uses "you" language ("imagine you're deploying this...") | 10% |
| **Time Management** | Runs over (>12 min) or way under (<7 min) | Finishes at 9-11 minutes | Exactly 10 minutes, reserves last 30 seconds for "happy to dive deeper on any aspect" | 10% |
| **Gap Acknowledgment** | Ignores weaknesses (KPI failure, optimization validation) | Mentions gaps briefly at end if asked | Proactively addresses upfront: "XGBoost doesn't meet KPIs—here's why and next steps" | 10% |

**Total Presentation Score**: Sum of weighted scores (max 10 points)

---

#### **Candidate-Specific Assessment: HUI Joo Hwee**

**Expected Strengths in Presentation**:
- Exceptional documentation suggests strong communication skills
- EDA → Pipeline traceability table is presentation-ready visual
- Business impact framing throughout submission → likely translates to presentation

**Potential Weaknesses to Watch**:
- May over-prepare and sound rehearsed vs authentic
- Might avoid discussing KPI failure (no model meets recall≥70% AND FPR≤5%)
- Could get too technical (gradient descent derivation) instead of strategic

**Red Flags During Presentation**:
- If spends >3 minutes on EDA details → signals poor prioritization
- If doesn't mention business KPIs (recall, FPR) in first 2 minutes → misses framing
- If can't answer simple clarifying questions mid-presentation → memorized vs understood

**Green Flags During Presentation**:
- Opens with: "CyberProtect faces $90M fraud exposure—here's how I built a detection system..."
- Shows EDA findings → Pipeline decisions table → says "every transformation justified by evidence"
- Closes with: "Model doesn't meet KPIs yet, but I have a 6-week iteration plan—happy to discuss"

---

### Section B: Presentation Content Recommendations (For Panel Guidance)

#### **Ideal 10-Minute Presentation Structure**

**Minutes 0-1: Problem Framing (Business Hook)**
- "CyberProtect users risk credential theft from phishing sites"
- "Baseline: 55% accuracy → 45% attacks missed → $90M annual fraud exposure"
- "Goal: Build browser extension to warn users—KPIs: Recall≥70%, FPR≤5%, ROC AUC≥0.80"

**Minutes 1-3: EDA → Pipeline Design (Evidence-Based Approach)**
- Show EDA findings table (visual)
- Highlight top 3 critical issues:
  1. Class imbalance 55:45 → Stratified splits
  2. 377 negative NoOfImage values → Clip to 0
  3. 10 features |skew|>1 → Log-transform for gradient stability
- Key message: "Every preprocessing decision traces back to EDA finding"

**Minutes 3-6: Model Development & Evaluation**
- Three models trained: Logistic (baseline), KNN (non-parametric), XGBoost (performance)
- Results visual: ROC AUC comparison bar chart
- Trade-off discussion:
  - XGBoost: 0.888 AUC, 86.5% recall, but 18.2% FPR (violates constraint)
  - Logistic: 0.825 AUC, 81.2% recall, 21.9% FPR (explainable but weak)
- Threshold tuning: "Swept 1000 thresholds—FPR≤5% requires recall drop to 75%"

**Minutes 6-8: Critical Gap & Next Steps**
- Honest acknowledgment: "No model meets both KPIs simultaneously"
- Root cause: "Feature coverage insufficient—need text features from page content"
- Iteration plan:
  1. Text features (TFIDF/embeddings) → +3-5% AUC (6 weeks)
  2. SSL certificate characteristics (validity, CA type)
  3. Domain registration velocity (phishing campaigns cluster temporally)
- Interim deployment: "Warning mode (no hard block) to collect labels on borderline cases"

**Minutes 8-10: Deployment Considerations & Conclusion**
- Production requirements: <100ms latency, <100MB memory, SHAP explainability
- Monitoring: Feature drift detection (KL divergence on top 3 predictors)
- Key takeaway: "Built evidence-based baseline with clear roadmap to production-readiness"
- Invitation: "Happy to dive deeper on any aspect—EDA methodology, model architecture, deployment strategy"

---

#### **Questions to Interrupt Presentation (Panel Technique)**

**Purpose**: Test real-time thinking vs memorized script

**Timing**: Around minute 4-5 (mid-presentation)

**Example Interruptions**:
1. "You mentioned log-transform—why does that help gradient descent specifically?" (Tests theory depth)
2. "Show me the EDA finding that led to stratified splits." (Tests evidence linkage)
3. "What's your biggest regret about this submission?" (Tests self-awareness)

**Scoring**:
- **Poor**: Flustered, loses train of thought, can't resume smoothly
- **Qualified**: Answers briefly, returns to script
- **Excellent**: Answers confidently, uses interruption to strengthen point, seamlessly continues

---

## Part 2: 50-Minute Q&A Session Assessment

### Section A: Question Bank by Assessment Dimension

#### **Dimension 1: Technical Depth (20 minutes, 40% of Q&A score)**

**Question Set 1: ML Theory Foundations**

**Q1.1: Gradient Descent Derivation**
> "Walk me through your logistic regression implementation. Derive the gradient descent update rule from cross-entropy loss. Include L2 regularization."

**Assessment Criteria**:
- **Poor**: Cannot write update rule, confuses gradient descent/ascent
- **Qualified**: Correct update θ := θ - α*[(1/m)X^T(σ(Xθ) - y) + (λ/m)θ], explains components
- **Excellent**: Full derivation from L(θ) → ∂L/∂θ via chain rule → update with weight decay. Bayesian interpretation: L2 ≡ MAP with Gaussian prior θ ~ N(0, 1/λ)

**Follow-up Probes**:
- "What happens if you don't scale features before gradient descent?"
- "Why does L2 prevent overfitting? Give me the intuition."
- "When would you use L1 instead of L2 regularization?"

**Scoring Notes**:
- Candidate (HUI) mentions NumPy gradient descent but no derivation in README → critical test
- If cannot derive: theoretical foundation weak (tutorial-following)
- If derives fluently: strong ML theory mastery

---

**Q1.2: XGBoost vs Simpler Models**
> "You trained three models. Why not just use logistic regression if it's 10× faster? Justify XGBoost's complexity."

**Assessment Criteria**:
- **Poor**: "XGBoost is industry standard" without specific justification
- **Qualified**: Mentions non-linearity, feature interactions, better AUC
- **Excellent**: Quantified trade-off analysis: "0.06 AUC gain (0.888 vs 0.825) = 600 fewer missed attacks per 10K samples → $1.2M annual fraud prevention. Worth 10× latency cost (10ms vs 1ms) for fraud detection. If latency critical, would deploy hybrid: Logistic for 90% easy cases + XGBoost for 10% borderline → 1.9ms average."

**Follow-up Probes**:
- "Could you achieve XGBoost's performance with feature engineering + logistic regression?"
- "Show me one feature interaction XGBoost captures that logistic misses."
- "If legal requires coefficient-based explainability, can you deploy XGBoost?"

---

**Q1.3: Preprocessing Justification**
> "You applied log-transform to 10 features. Why does that help specifically? Walk me through the math."

**Assessment Criteria**:
- **Poor**: "Makes data more normal" without connecting to model
- **Qualified**: "Gradient descent converges faster on Gaussian-like distributions"
- **Excellent**: "Logistic gradient: ∇L = (1/m)X^T(σ(Xθ) - y). If X has extreme values (e.g., NoOfPopup ranges 0-1000), gradients explode → learning rate must be tiny → 500+ epochs. Log-transform compresses to [0, 6.9] → stable gradients → converged in 120 epochs. Also reduces outlier leverage on coefficient estimates."

**Red Flag**: If candidate cannot explain why log-transform mathematically helps → doesn't understand theory

---

#### **Dimension 2: Business Reasoning (15 minutes, 30% of Q&A score)**

**Q2.1: KPI Trade-off Scenario**
> "Your XGBoost has 86.5% recall but 18.2% FPR. Product demands FPR≤3% by next week. Engineering reports current inference takes 200ms (requirement: <100ms). Legal needs explainability reports. You have 2 weeks total. What do you do?"

**Assessment Criteria**:
- **Poor**: Picks one dimension ("just lower threshold") without acknowledging trade-offs
- **Qualified**: Lists multiple options (threshold tuning, switch to logistic, optimize inference) but no prioritization
- **Excellent**: Structured triage:
  1. **Critical Path**: Legal explainability (regulatory blocker) → Deploy Logistic Regression (coefficient-based, no SHAP needed) for 90% of traffic immediately
  2. **FPR Mitigation**: Tune Logistic threshold to FPR≤3% (accept recall drop to ~70-75% per validation curve)
  3. **Latency Fix**: Logistic inference <1ms → 100× under budget → immediate compliance
  4. **Parallel Track**: Optimize XGBoost via ONNX conversion → deploy for 10% high-risk cases in Week 2
  5. **Stakeholder Communication**: Daily standups with product/legal/engineering → transparent on trade-offs

**Follow-up Probes**:
- "Product says 70% recall is too low—customers are getting hacked. Now what?"
- "How do you decide which stakeholder's constraint is most critical?"
- "If you could only fix one issue (FPR, latency, or explainability), which and why?"

---

**Q2.2: Cost-Benefit Analysis**
> "Marketing says false positives cost $500 per user in churn. Fraud costs average $2000 per incident. Your model has 75% recall and 5% FPR. Is this profitable? Show me the math."

**Assessment Criteria**:
- **Poor**: "Yes, 75% recall is good" without quantifying
- **Qualified**: Calculates: Prevented fraud = 0.75 * (# phishing attacks) * $2000, Cost = 0.05 * (# legitimate) * $500, doesn't compare
- **Excellent**: 
  - Assumptions: 100K users/month, 10% encounter phishing (10K attacks), 90% legitimate (90K)
  - Without model: 10K attacks * $2000 = $20M fraud losses
  - With model: 
    - Prevented: 7.5K attacks * $2000 = $15M saved
    - False positives: 90K * 0.05 = 4.5K users * $500 = $2.25M churn cost
    - Net benefit: $15M - $2.25M = $12.75M positive ROI
  - Conclusion: "Profitable at 75% recall / 5% FPR, but optimizing toward 85% recall / 3% FPR increases ROI to $15.6M"

**Red Flag**: If candidate cannot do back-of-envelope calculation → weak business acumen

---

**Q2.3: Bias & Fairness**
> "Your top predictor is DomainAgeMonths. A compliance officer asks: 'Could this unfairly harm legitimate startups with new domains?' How do you respond?"

**Assessment Criteria**:
- **Poor**: Defensive ("It's the data's fault") or dismissive ("Startups are rare")
- **Qualified**: Acknowledges concern, mentions feature combination reduces bias
- **Excellent**: Comprehensive response:
  1. **Acknowledge validity**: "Legitimate concern—young domains ≠ phishing universally"
  2. **Mitigation in model**: "XGBoost combines DomainAge with content features (IsResponsive, NoOfExternalRef, Industry). Example: 'DomainAge <6mo AND NoOfExternalRef >50 AND Industry=Unknown' → high risk, but 'DomainAge <6mo AND Industry=E-commerce AND IsResponsive=True' → low risk"
  3. **Propose fairness audit**: "Stratify FPR by industry and domain age. If e-commerce startups have 10% FPR vs financial services 2%, that's bias. Solution: Retrain with synthetic minority oversampling or adjust decision thresholds per segment"
  4. **Explainability**: "For every blocked site, generate SHAP report: 'DomainAge contributed +0.3 phishing score, but IsResponsive -0.2 → net: borderline.' Helps users understand why flagged"

---

#### **Dimension 3: Problem-Solving & Iteration (10 minutes, 20% of Q&A score)**

**Q3.1: Post-Deployment Scenario**
> "Your model's been in production 3 months. Recall has dropped from 85% to 68%. What's your debugging process?"

**Assessment Criteria**:
- **Poor**: "Retrain immediately" without investigation
- **Qualified**: Checks feature drift, collects recent labels, retrains
- **Excellent**: Systematic debugging:
  1. **Feature Drift Analysis**: Compare production vs training distributions (KL divergence on DomainAgeMonths, IsResponsive, Robots). If DomainAge shifted from mean=18mo to 28mo → adversaries using older domains
  2. **Concept Drift Check**: Evaluate model on recent labeled samples (last 2 weeks). If AUC stable but recall dropped → distribution shift (more phishing resembles legitimate). If AUC dropped → concept drift (attacker tactics changed)
  3. **Error Analysis**: Sample 100 recent false negatives. Pattern: All have HTTPS + verified SSL certs (new attacker strategy). Previous model didn't have SSL features → blind spot
  4. **Feature Engineering**: Add SSL certificate characteristics (CA type, validity period)
  5. **Retrain**: On combined dataset (historical + recent 3 months with new features)
  6. **A/B Test**: Deploy new model to 10% traffic (shadow mode) for 1 week, compare metrics
  7. **Root Cause Report**: Document why drift occurred (adversarial adaptation) → update monitoring to detect SSL-based attacks

**Follow-up**: "What if you don't have labeled data from recent production traffic?"

---

**Q3.2: Resource Constraints**
> "Your manager says you can only work on this project 1 more week before moving to another team. You have KPI gaps and optimization work undone. What do you prioritize?"

**Assessment Criteria**:
- **Poor**: Tries to do everything (optimization + features + deployment) → spreads too thin
- **Qualified**: Picks feature engineering to close KPI gap
- **Excellent**: Strategic prioritization with handoff plan:
  1. **This Week**: 
     - Document current baseline thoroughly (README already done ✓)
     - Run hyperparameter optimization (validate infrastructure works)
     - Implement ONE high-impact feature: text features from page titles (3 days of work)
     - Retrain XGBoost with text features → validate if AUC improves +0.03-0.05
     - Update README with results + next steps documentation
  2. **Handoff Package**:
     - `HANDOFF.md`: Detailed next steps (SSL features, ensemble methods, A/B test plan)
     - `config.yaml`: Pre-configured experiments for next engineer
     - `scripts/quick_start.sh`: One-command pipeline run for new team member
  3. **Rationale**: "Feature engineering moves needle on KPIs. Optimization yields diminishing returns (+1-2% AUC max). Proper documentation enables next engineer to continue without ramp-up time."

---

#### **Dimension 4: Communication & Collaboration (5 minutes, 10% of Q&A score)**

**Q4.1: Explaining to Non-Technical Stakeholder**
> "Explain threshold tuning to a product manager who doesn't know statistics. You have 2 minutes."

**Assessment Criteria**:
- **Poor**: Uses jargon ("precision-recall curve," "ROC AUC," "decision boundary")
- **Qualified**: Uses analogy but doesn't connect to business outcome
- **Excellent**: Stakeholder-friendly explanation:
  > "Think of the model as a security guard with a suspicion meter (0-100%). Right now, if suspicion ≥50%, we block the site. But 50% is arbitrary—we can adjust it.
  >
  > If we set the bar higher (e.g., 80%), the guard only blocks when VERY suspicious → fewer false alarms (legitimate sites blocked) but also misses some real attacks (false negatives).
  >
  > If we set it lower (e.g., 30%), guard blocks more aggressively → catches more attacks but annoys users with false alarms.
  >
  > Threshold tuning finds the sweet spot: What suspicion level gives us ≤5 false alarms per 100 legitimate sites while still catching ≥70% of attacks? For XGBoost, that's around 65% suspicion threshold, which catches 75% of attacks at 5% false alarm rate.
  >
  > This is why we can't hit 85% recall at 3% FPR yet—the model's 'discrimination ability' isn't good enough. We need better features (like text analysis) to improve its judgment, not just adjust the threshold."

**Scoring**: Judge clarity, analogy quality, and connection to business impact

---

### Section B: Real-Time Assessment Techniques

#### **Technique 1: The "Explain Like I'm 5" Test**

**Purpose**: Distinguish deep understanding from memorization

**Execution**: Pick any technical concept candidate mentioned (e.g., "You said 'L2 regularization'—explain it like I'm a 5-year-old")

**Scoring**:
- **Poor**: Reverts to jargon or says "It's complicated"
- **Qualified**: Attempts analogy but it's confusing
- **Excellent**: Clean metaphor: "L2 is like a penalty for using big numbers. If your model wants to say 'this feature is 1000× more important,' it gets punished. This forces the model to spread importance across many features instead of memorizing specific examples."

---

#### **Technique 2: The "What Would You Do Differently?" Probe**

**Purpose**: Assess self-awareness and growth mindset

**Execution**: Around minute 40 of Q&A, ask: "If you restarted this assessment today, what's ONE thing you'd change?"

**Scoring**:
- **Poor**: "Nothing, I'm happy with it" (arrogance) or "Everything" (no prioritization)
- **Qualified**: Names one thing (e.g., "Run hyperparameter optimization") but doesn't explain impact
- **Excellent**: Specific improvement with reasoning:
  > "I'd add text features from the start. My EDA showed metadata features (domain age, hosting, link counts) yield 0.888 AUC max. Literature on phishing detection reports text features (page titles, TFIDF on content) add 5-10% F1 improvement. If I had text features, I likely hit 0.92-0.93 AUC → enough to achieve 80% recall at 3% FPR. I didn't do this because assessment provided SQLite with structured data only—but in real project, I'd web-scrape page content as priority."

**Red Flags**: Defensive about gaps, blames constraints, no concrete improvement

---

#### **Technique 3: The "Pressure Test" Scenario**

**Purpose**: Evaluate composure and decision-making under constraints

**Execution**: Around minute 45, present multi-constraint scenario (Q2.1 above: FPR, latency, explainability all violated, 2-week deadline)

**Observation Points**:
- Does candidate panic or stay calm?
- Do they ask clarifying questions ("What's the regulatory deadline for explainability?")?
- Do they prioritize or try to solve everything?
- Do they communicate trade-offs transparently?

**Scoring**:
- **Poor**: Overwhelmed, no clear plan, focuses on one dimension
- **Qualified**: Lists options, struggles with prioritization
- **Excellent**: Structured triage (see Q2.1), asks for constraints to inform priorities, proposes interim solutions

---

### Section C: Candidate-Specific Assessment (HUI Joo Hwee)

#### **Predicted Strengths in Q&A**

Based on submission review:

1. **Business Framing**: Consistently links technical → business in README → expect strong Q2 performance
2. **Evidence-Based Reasoning**: EDA → Pipeline traceability → should excel at "Why this preprocessing?" questions
3. **Stakeholder Communication**: Tutorial-grade documentation suggests strong Q4 (explaining to non-technical)
4. **Problem-Solving**: Acknowledges gaps (KPI failure implicit) → likely proposes concrete iteration plans

#### **Predicted Weaknesses in Q&A**

1. **Mathematical Depth**: No gradient descent derivation in README → uncertain Q1.1 performance (critical test)
2. **Real-World Experience**: Deployment considerations mentioned but unclear if implemented → Q3 scenarios may expose theory-practice gap
3. **Optimization Validation**: Hyperparameter grids exist but results not shown → Q1.2 follow-ups may reveal incomplete work

#### **High-Priority Questions for This Candidate**

**Must Ask** (non-negotiable):
1. Q1.1: Gradient descent derivation (validates theory foundation)
2. Q2.1: Multi-constraint scenario (tests prioritization under pressure)
3. Custom: "Your models don't meet KPIs. Walk me through your 6-week iteration plan in detail." (Tests if gap acknowledgment is superficial or substantive)

**Should Ask** (time permitting):
1. Q1.3: Preprocessing justification with math (validates evidence-based claims)
2. Q2.3: Bias & fairness (tests ethical reasoning)
3. Q3.2: Resource constraint prioritization (tests strategic thinking)

**Nice to Have** (if time remains):
1. Q4.1: Explain to product manager (already strong communicator, likely performs well)
2. Q3.1: Post-deployment debugging (tests operational awareness)

---

## Part 3: Group Exercise Assessment (2 Hours)

### Section A: Group Exercise Structure & Observation Framework

#### **Exercise Format**

**Setup**:
- 2-3 candidates work together on ML case study
- Case disclosed on-site (no preparation possible)
- Candidates bring personal laptops
- Internet and resources allowed (libraries, documentation, Google)

**Typical Case Study Structure**:
1. **Business Problem** (15 min): Read case, understand requirements
2. **Exploratory Analysis** (30 min): Load data, profile, identify issues
3. **Model Development** (45 min): Feature engineering, train baseline models
4. **Evaluation & Presentation** (30 min): Assess performance, prepare summary

**Panel Role**:
- Observe collaboration dynamics (don't interrupt unless stuck >20 min)
- Take notes on individual contributions vs group dynamic
- Ask clarifying questions if candidates misunderstand problem

---

#### **Assessment Dimensions for Group Exercise**

**Dimension 1: Technical Execution (30% of group score)**

**Observe**:
- Code quality: Modular functions or spaghetti scripts?
- Debugging: How do they handle errors (Stack Overflow immediately or reason through)?
- Tool proficiency: Comfortable with pandas, sklearn, matplotlib?
- Best practices: Version control, comments, reproducibility?

**Scoring Rubric**:
- **Poor (0-3)**: Copy-paste code from web, errors not resolved, hardcoded values everywhere
- **Qualified (4-6)**: Functional pipeline (load → clean → train → evaluate), basic error handling, some comments
- **Excellent (7-10)**: Modular design (separate functions), config-driven, error handling with logging, Git commits, reproducible (seeds set)

---

**Dimension 2: Problem-Solving Approach (25% of group score)**

**Observe**:
- Do they jump to modeling or start with EDA?
- How do they handle ambiguity ("case says 'improve accuracy'—what metric?")?
- Do they validate assumptions or make blind choices?

**Scoring Rubric**:
- **Poor**: Immediately trains model without EDA, ignores data quality issues
- **Qualified**: Does basic EDA (df.describe(), value counts), trains baseline, evaluates
- **Excellent**: Systematic approach:
  1. Clarify requirements (asks panel: "By 'accuracy,' do you mean overall or per-class?")
  2. EDA with documented findings (missingness, imbalance, outliers)
  3. Baseline (logistic regression, no feature engineering)
  4. Iterate (feature engineering → retrain → compare)
  5. Validate (holdout set, not just training metrics)

---

**Dimension 3: Collaboration & Communication (25% of group score)**

**Observe**:
- Does one candidate dominate or do they distribute tasks?
- How do they resolve disagreements (vote, defer to "expert," discuss trade-offs)?
- Do they explain approaches to each other or work in silos?

**Scoring Rubric**:
- **Poor**: One person codes while others watch, no discussion, passive team members
- **Qualified**: Task division (A does EDA, B trains model, C evaluates), minimal coordination
- **Excellent**: Active collaboration:
  - Explicit task allocation: "I'll profile the data, you set up the pipeline, let's sync in 15 min"
  - Pair programming on complex parts (feature engineering together)
  - Knowledge sharing: "I've done text classification—let me show you TFIDF"
  - Conflict resolution: "We have two approaches—let's test both and compare metrics"

**Red Flags**:
- Candidate dismisses others' ideas without discussion
- Candidate sits back and contributes minimally ("I don't know this library")
- No communication for >30 minutes (working in parallel without alignment)

---

**Dimension 4: Time Management & Prioritization (20% of group score)**

**Observe**:
- Do they track time ("We have 45 minutes left—need to start modeling")?
- Do they get stuck on non-critical details (perfect plot formatting, hyperparameter tuning for hours)?
- Do they deliver something vs nothing (working model at end vs incomplete)?

**Scoring Rubric**:
- **Poor**: Runs out of time, no model trained or can't present results
- **Qualified**: Finishes all tasks but rushed presentation, no time for polishing
- **Excellent**: Strategic time allocation:
  - First 30 min: EDA and quick baseline (even if crude)
  - Next 45 min: Iterate on features and models
  - Last 30 min: Finalize best model + prepare concise presentation (3 slides max)
  - Leaves 15-min buffer for unexpected issues

---

### Section B: Common Group Exercise Case Study Types

#### **Case Study Type 1: Binary Classification with Imbalanced Data**

**Example**: "Predict customer churn (10% churn rate). Provided: customer_data.csv with 15 features."

**Key Challenges**:
- Class imbalance → naive model predicts "no churn" for all → 90% accuracy but useless
- Missing values, categorical features (encoding required)
- Evaluation metric ambiguity (accuracy vs recall vs F1?)

**What Panel Looks For**:
- Do candidates identify imbalance immediately (EDA)?
- Do they use stratified splits?
- Do they use appropriate metrics (precision-recall vs accuracy)?
- Do they try SMOTE, class weights, or threshold tuning?

---

#### **Case Study Type 2: Regression with Temporal Data**

**Example**: "Predict next month's sales. Provided: sales_history.csv (5 years of monthly data)."

**Key Challenges**:
- Temporal leakage (can't use future to predict past)
- Train/test split must respect time order (not random shuffle)
- Seasonality, trends (need feature engineering: month, lagged values)

**What Panel Looks For**:
- Do candidates recognize time-series nature?
- Do they avoid data leakage (split at time T, train on <T, test on >T)?
- Do they engineer time-based features (moving averages, lag, trend)?
- Do they validate with time-aware metrics (walk-forward validation)?

---

#### **Case Study Type 3: Multi-Class Classification with Text**

**Example**: "Classify customer reviews into 5 sentiment categories. Provided: reviews.csv (text + rating)."

**Key Challenges**:
- Text preprocessing (tokenization, stopwords, stemming)
- Feature extraction (TFIDF, word embeddings, or count vectors)
- Multi-class evaluation (confusion matrix, per-class metrics)

**What Panel Looks For**:
- Do candidates have NLP basics (TFIDF, tokenization)?
- Do they handle text cleaning (lowercase, remove punctuation)?
- Do they try multiple approaches (simple count vectors → TFIDF → word2vec if time)?
- Do they evaluate per-class (not just overall accuracy)?

---

### Section C: Candidate-Specific Predictions (HUI Joo Hwee)

#### **Expected Performance in Group Exercise**

**Strong Areas**:
1. **Problem Structuring**: Submission shows systematic approach (EDA → Pipeline → Evaluation) → likely replicates in group setting
2. **Communication**: Documentation quality suggests can explain approaches clearly to teammates
3. **Code Organization**: Modular pipeline in submission → likely writes clean code during exercise
4. **Time Management**: Completed comprehensive assessment → shows planning ability

**Potential Challenges**:
1. **Collaboration Style**: Solo submission doesn't reveal teamwork skills → uncertain if dominant, passive, or balanced
2. **Real-Time Coding**: Polished submission may mask live-coding speed → could struggle with time pressure
3. **Handling Ambiguity**: Detailed documentation suggests preference for structure → may be uncomfortable with vague case requirements

**Observation Focus**:
- **First 15 minutes**: Does candidate take lead in problem clarification or defer to others?
- **Middle 60 minutes**: Does candidate pair-program or work independently? How do they handle disagreements?
- **Last 30 minutes**: Does candidate help teammates or focus only on own code? Who presents results?

**Red Flags**:
- Takes over entire exercise (codes everything, doesn't delegate) → poor teamwork
- Spends too much time documenting/commenting during exercise → misses time pressure
- Perfectionism (tweaking plots, optimizing hyperparameters for minor gains) → loses sight of deliverable

**Green Flags**:
- Proactively suggests task allocation: "I'll handle EDA, you set up the pipeline?"
- Shares knowledge: "I've dealt with class imbalance before—let's try stratified CV"
- Tracks time: "We're at minute 90—need to finalize model and prep presentation"
- Helps debug teammates' code without taking over

---

## Part 4: Integrated Scoring & Decision Framework

### Section A: Overall Interview Score Calculation

**Component Weights**:
- 10-Minute Presentation: 20%
- 50-Minute Q&A: 50%
- Group Exercise: 30%

**Q&A Dimension Weights** (within 50%):
- Technical Depth: 40% of Q&A → 20% of overall
- Business Reasoning: 30% of Q&A → 15% of overall
- Problem-Solving: 20% of Q&A → 10% of overall
- Communication: 10% of Q&A → 5% of overall

**Total Score Calculation**:
```
Overall Score = (Presentation * 0.20) + 
                (Q&A_TechDepth * 0.20) + 
                (Q&A_Business * 0.15) + 
                (Q&A_ProblemSolving * 0.10) + 
                (Q&A_Communication * 0.05) + 
                (GroupExercise * 0.30)
```

---

### Section B: Hiring Decision Thresholds

| Overall Score | Recommendation | Rationale | Next Steps |
|--------------|----------------|-----------|------------|
| **90-100** | **STRONG HIRE** | Top 5% candidate: exceptional technical depth + business acumen + collaboration | Offer with Senior IC track, fast-track promotion eligibility |
| **80-89** | **HIRE** | Strong candidate: solid fundamentals with growth potential | Standard offer, pair with mentor for 6 months |
| **70-79** | **BORDERLINE** | Competent but gaps in key areas (theory, collaboration, or business reasoning) | Panel discussion: Does candidate fit specific role? Offer if domain expertise critical |
| **60-69** | **NO HIRE** | Insufficient depth or collaboration issues | Decline with constructive feedback (if requested) |
| **<60** | **STRONG NO HIRE** | Critical gaps in multiple dimensions | Decline immediately |

---

### Section C: Tie-Breaker Criteria (For Borderline Cases)

When candidate scores 75-80 (borderline), use these tie-breakers:

**Tier 1 (Highest Priority)**:
1. **Growth Mindset**: Did candidate acknowledge gaps honestly and propose concrete improvements? (Green flag: "If I restarted, I'd add text features because...") vs defensiveness (Red flag: "My submission is perfect")
2. **Communication Skills**: Can they explain to non-technical stakeholders? (Critical for cross-functional teams)
3. **Collaboration**: Did they enable teammates or dominate/disappear? (Predicts team fit)

**Tier 2 (Secondary)**:
1. **Domain Knowledge**: Specific expertise in relevant areas (e.g., fraud detection, NLP, CV)
2. **Deployment Awareness**: Understands production constraints (latency, monitoring, compliance)
3. **Problem-Solving Creativity**: Proposes novel solutions vs textbook approaches

**Tie-Breaker Example**:
- **Candidate A**: 78 score, weak collaboration (dominated group exercise), strong technical depth
- **Candidate B**: 77 score, excellent collaboration (enabled teammates), moderate technical depth
- **Decision**: Hire Candidate B → collaboration skills harder to teach, technical depth grows with mentorship

---

### Section D: Post-Interview Debrief Template

**Immediately After Interview** (Panel completes within 15 minutes)

**Candidate Name**: HUI Joo Hwee  
**Interview Date**: [Date]  
**Panel Members**: [Names]

#### **1. Presentation Score** (/10)
- Narrative Structure: ___ /10
- Content Prioritization: ___ /10
- Visual Communication: ___ /10
- Business Framing: ___ /10
- Audience Engagement: ___ /10
- Time Management: ___ /10
- Gap Acknowledgment: ___ /10
- **Weighted Total**: ___ /10 (weight: 20%)

**Key Observations**:
- Strengths: _______________
- Weaknesses: _______________
- Notable moments: _______________

---

#### **2. Q&A Session Scores**

**Technical Depth** (/10, weight: 20% overall)
- ML Theory (Q1.1 Gradient Descent): ___ /10
- Model Justification (Q1.2 XGBoost): ___ /10
- Preprocessing Math (Q1.3 Log-Transform): ___ /10
- **Average**: ___ /10

**Business Reasoning** (/10, weight: 15% overall)
- KPI Trade-off (Q2.1): ___ /10
- Cost-Benefit (Q2.2): ___ /10
- Bias & Fairness (Q2.3): ___ /10
- **Average**: ___ /10

**Problem-Solving** (/10, weight: 10% overall)
- Post-Deployment Debug (Q3.1): ___ /10
- Resource Constraints (Q3.2): ___ /10
- **Average**: ___ /10

**Communication** (/10, weight: 5% overall)
- Explain to PM (Q4.1): ___ /10

**Key Observations**:
- Technical strengths: _______________
- Business reasoning quality: _______________
- Red flags: _______________
- Green flags: _______________

---

#### **3. Group Exercise Score** (/10, weight: 30%)
- Technical Execution: ___ /10 (weight: 30%)
- Problem-Solving Approach: ___ /10 (weight: 25%)
- Collaboration & Communication: ___ /10 (weight: 25%)
- Time Management: ___ /10 (weight: 20%)
- **Weighted Total**: ___ /10

**Key Observations**:
- Role in team (leader/contributor/passive): _______________
- Code quality: _______________
- Collaboration style: _______________
- Unique contributions: _______________

---

#### **4. Overall Assessment**

**Total Score**: ___ /100  
**Recommendation**: ☐ Strong Hire  ☐ Hire  ☐ Borderline  ☐ No Hire  

**Strengths (Top 3)**:
1. _______________
2. _______________
3. _______________

**Development Areas (Top 3)**:
1. _______________
2. _______________
3. _______________

**Concerns/Red Flags**:
- _______________

**Tie-Breaker Factors** (if borderline):
- Growth mindset: _______________
- Communication: _______________
- Collaboration: _______________

**Final Decision Rationale**:
_______________________________________________
_______________________________________________

**Interviewer Signatures**: _______________

---

## Part 5: Candidate-Specific Interview Plan (HUI Joo Hwee)

### Pre-Interview Briefing (5 minutes before candidate arrives)

**Panel Alignment**:
- "This is a strong submission (A-, 92%) with exceptional documentation. Key question: Does depth match documentation quality?"
- "Critical tests: (1) Gradient descent derivation (theory depth), (2) KPI gap discussion (self-awareness), (3) Group collaboration (unknown)"
- "Expected strengths: Business framing, communication. Potential weaknesses: Mathematical proofs, real-world deployment experience."

---

### Presentation Phase (10 minutes)

**Observation Checklist**:
- ☐ Does candidate open with business framing (fraud exposure, KPIs)?
- ☐ Does candidate show EDA → Pipeline traceability table?
- ☐ Does candidate acknowledge KPI failure proactively?
- ☐ Does candidate engage panel (eye contact, invites questions)?
- ☐ Does candidate finish within 10 minutes (±1 min)?

**Panel Member Roles**:
- **Lead**: Interrupt at minute 5 with: "Quick clarification—why log-transform specifically for gradient descent?"
- **Technical Reviewer**: Assess if answers are deep vs superficial
- **Business Reviewer**: Track if candidate quantifies business impact

---

### Q&A Phase (50 minutes)

**Must-Ask Questions** (30 minutes):
1. **Q1.1**: Gradient descent derivation (10 min) → validates theory foundation
2. **Q2.1**: Multi-constraint scenario (10 min) → validates prioritization under pressure
3. **Custom KPI Question** (10 min): "Your models don't meet KPIs. Walk through your 6-week plan."

**Should-Ask Questions** (15 minutes):
1. **Q1.3**: Preprocessing math (5 min)
2. **Q2.3**: Bias & fairness (5 min)
3. **Q3.2**: Resource constraints (5 min)

**Buffer** (5 minutes):
- Candidate questions for panel
- Clarifications on AIAP program

**Interviewer Rotation**:
- Lead asks Q1.1, Q2.1
- Technical Reviewer asks Q1.3, follow-ups on theory
- Business Reviewer asks Q2.3, Q3.2

---

### Group Exercise (2 hours)

**Observer Assignment**:
- **Lead**: Focus on candidate's collaboration style (dominant/balanced/passive)
- **Technical Reviewer**: Focus on code quality and problem-solving approach
- **Business Reviewer**: Focus on time management and communication

**Observation Intervals**:
- **Minute 0-15**: How does candidate contribute to problem understanding?
- **Minute 15-30**: Task allocation—does candidate lead, follow, or collaborate?
- **Minute 30-90**: Coding phase—pair programming or independent work?
- **Minute 90-120**: Presentation prep—who presents, who supports?

**Key Moments to Note**:
- First 5 minutes: Who speaks first? Who suggests approach?
- Conflict resolution: If disagreement arises, how does candidate respond?
- Debugging: If error occurs, does candidate help teammates or focus on own code?

---

### Post-Interview Panel Discussion (30 minutes)

**Agenda**:
1. **Round-Robin Initial Impressions** (5 min): Each panel member shares 1-sentence take
2. **Score Calibration** (10 min): Discuss scoring for presentation, Q&A, group exercise
3. **Debate Borderline Areas** (10 min): If scores conflict, discuss evidence
4. **Final Decision** (5 min): Vote (Strong Hire / Hire / Borderline / No Hire)

**Decision Criteria**:
- If score ≥85: Strong Hire (unanimous required)
- If score 80-84: Hire (2/3 agreement)
- If score 75-79: Borderline → Discuss tie-breakers
- If score <75: No Hire

**Expected Outcome for HUI Joo Hwee**:
- If gradient descent derivation strong: 85+ (Strong Hire)
- If gradient descent weak but collaboration strong: 80-84 (Hire)
- If both weak: 75-79 (Borderline) → Tie-breaker: Growth mindset + communication skills likely push to Hire

---

## Appendix: Quick Reference Checklists

### Red Flags (Immediate Concern)

**Presentation**:
- ☐ Cannot finish in 10 minutes (runs to 15+ or stops at 5)
- ☐ No business framing (launches into technical details)
- ☐ Defensive when interrupted ("Let me finish first")

**Q&A**:
- ☐ Cannot derive gradient descent update rule
- ☐ Blames submission gaps on time/data constraints (not taking ownership)
- ☐ Talks over panel or dismisses questions ("That's not important")

**Group Exercise**:
- ☐ Dominates entire exercise (doesn't let others contribute)
- ☐ Passive (contributes minimally, waits for others)
- ☐ Conflict-averse (agrees with everything, no critical thinking)

### Green Flags (Strong Positive)

**Presentation**:
- ☐ Opens with compelling business hook (fraud exposure, customer impact)
- ☐ Proactively acknowledges gaps with iteration plan
- ☐ Invites panel questions ("Happy to dive deeper on any aspect")

**Q&A**:
- ☐ Derives gradient descent fluently with Bayesian interpretation
- ☐ Uses "Explain Like I'm 5" effectively (analogies, no jargon)
- ☐ Asks clarifying questions before answering multi-constraint scenarios

**Group Exercise**:
- ☐ Facilitates collaboration ("Let's divide tasks: I'll do EDA, you set up pipeline")
- ☐ Shares knowledge generously ("I've used SMOTE before—let me show you")
- ☐ Tracks time and keeps team on schedule

---

**End of Interview Panel Guide**