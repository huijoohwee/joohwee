**forbid code blocks, interactive demo**
# context: `aisg-aiap22-technical-assessment.md`
#generate  `interviewer.md`: you're the lead for the business domain & technical interview panel,
1. FAQs, Scoring Rubric to screen & qualify poor/qualified/excellent candidates;
2. critique & assess the candidate `README.md`, `aisg-aiap22-task-1_20251201.md`

#generate  `interviewee.md`: you're the interviewee aiming to be the excellent candidate

---

I'll create comprehensive interview guides for both the panel lead and the candidate. These documents will help structure the technical and business domain interview effectively.I've created two comprehensive interview guides for the AIAP Batch 22 technical assessment:

## **For the Interview Panel** (`interviewer.md`)

This 15,000+ word guide provides:

- **Structured FAQ Bank**: 15 questions across 5 categories (Business Domain, Technical Design, Evaluation, Production, Code Quality) with 3-tier scoring rubrics (Poor 0-3, Qualified 4-6, Excellent 7-10)

- **Critical Assessment**: The candidate's submission earns **A- (92%)** - exceptional documentation and business acumen, but with gaps in mathematical depth, KPI acknowledgment, and security awareness

- **Key Findings**:
  - **Strengths**: Top 5% documentation, evidence-based design (EDA→pipeline traceability), production mindset
  - **Critical Gap**: No model meets both recall≥70% AND FPR≤5% - candidate doesn't acknowledge this failure or propose iteration plan
  - **Recommendation**: **STRONG HIRE** with caveat: probe ML theory depth to distinguish tutorial-following from deep understanding

- **Interview Strategy**: Focus on 3 areas:
  1. Gradient descent derivation (test theoretical foundations)
  2. KPI failure discussion (test problem-solving under constraints)
  3. Deployment claims (distinguish aspirational from implemented)

## **For the Candidate** (`interviewee.md`)

This 18,000+ word preparation guide includes:

- **10 Model Answers** with frameworks for anticipated questions (phishing problem framing, threshold tuning, feature drift detection, stakeholder communication)

- **Gap Mitigation**: Pre-emptive strategies to address submission weaknesses before panel probes them

- **Communication Strategies**:
  - "Evidence-Then-Recommendation" pattern
  - "Trade-off Triangle" (present 3 options, defend choice)
  - "Red Team Your Own Work" (surface weaknesses proactively)

- **Mock Scenarios**: Pressure tests (defending 18% FPR), theory deep dives (Bayesian interpretation of L2), stakeholder pitches (non-technical PM)

- **Confidence Builders**: Why this submission is top-tier despite gaps, and how to frame imperfections as growth opportunities

Both guides emphasize that the candidate demonstrates **strong potential for senior IC track** with mentorship on theoretical foundations. The submission quality (especially documentation and business framing) is exceptional—gaps are in depth, not breadth.

---

I've created two comprehensive interview session guides tailored to the AIAP format:

## **Interviewer-v2.md** (Panel Lead Guide)

**Structured around the 3-hour session**:

**1. 10-Minute Presentation Assessment**
- 7-criterion scoring rubric (narrative structure, content prioritization, visual communication, business framing, engagement, time management, gap acknowledgment)
- Ideal presentation structure template
- Mid-presentation interruption technique to test real-time thinking
- Candidate-specific predictions for HUI Joo Hwee

**2. 50-Minute Q&A Framework**
- Question bank across 4 dimensions:
  - **Technical Depth** (40%): Gradient descent derivation, XGBoost justification, preprocessing math
  - **Business Reasoning** (30%): KPI trade-offs, cost-benefit analysis, bias & fairness
  - **Problem-Solving** (20%): Post-deployment debugging, resource constraints
  - **Communication** (10%): Explaining to non-technical stakeholders
- Real-time assessment techniques: "Explain Like I'm 5" test, pressure scenarios
- High-priority questions customized for this candidate

**3. 2-Hour Group Exercise Observation**
- 4 assessment dimensions: Technical execution (30%), problem-solving (25%), collaboration (25%), time management (20%)
- Common case study types with evaluation criteria
- Observation checklist for each phase (problem understanding, task allocation, execution, presentation)

**4. Integrated Scoring System**
- Overall score calculation with component weights
- Hiring decision thresholds (Strong Hire ≥90, Hire 80-89, Borderline 70-79)
- Tie-breaker criteria for borderline cases
- Post-interview debrief template

---

## **Interviewee-v2.md** (Candidate Success Guide)

**Structured for maximum performance**:

**1. 10-Minute Presentation Mastery**
- Winning opening hook: "$90M fraud exposure problem..."
- Minute-by-minute structure (Problem → EDA → Models → Gap → Iteration → Deployment)
- How to handle mid-presentation interruptions
- Visual aid recommendations from README

**2. 50-Minute Q&A Excellence**
- Three-part answer structure: Anchor → Core → Bridge
- Model answers for high-probability questions:
  - Gradient descent derivation with Bayesian interpretation
  - XGBoost justification with quantified trade-offs
  - Multi-constraint prioritization scenario
  - Cost-benefit calculation
  - Fairness & bias mitigation
- Emergency strategies for questions you can't answer

**3. Group Exercise Dominance**
- Phase-by-phase action scripts:
  - **Phase 1 (0-15 min)**: Facilitator role—clarify requirements, build alignment
  - **Phase 2 (15-20 min)**: Coordinator role—propose task allocation, set milestones
  - **Phase 3 (20-90 min)**: Contributor role—execute + help teammates
  - **Phase 4 (90-110 min)**: Synthesizer role—create presentation
  - **Phase 5 (110-120 min)**: Presenter role—deliver confidently
- Collaboration touchpoints every 30 minutes
- How to handle teammate conflicts

**4. Preparation Checklists**
- 24-hour pre-interview checklist
- What to bring (laptop, printed README, backup materials)
- Post-interview debrief questions
- Thank-you email template

**5. The Winning Mindset**
- Your competitive advantages: exceptional documentation, business framing, production awareness
- Critical tests: gradient descent (theory depth), KPI gap (self-awareness), group work (collaboration)
- Emergency strategies for presentation freeze, unanswerable questions, time pressure

Both guides emphasize that the interview tests **depth beyond documentation**—can you explain what you built, acknowledge gaps honestly, and collaborate effectively under pressure?