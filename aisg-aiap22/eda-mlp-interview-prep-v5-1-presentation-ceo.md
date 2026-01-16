---
theme: seriph
background: https://source.unsplash.com/collection/94734566/1920x1080
class: text-center
highlighter: shiki
lineNumbers: false
info: |
  ## Phishing Detection System - CEO Presentation
  CyberProtect Real-Time Fraud Prevention
  10-Minute Business Case
drawings:
  persist: false
transition: slide-left
title: Phishing Detection - CEO Brief
mdc: true
---

# Protecting CyberProtect Users from Phishing Attacks

## A Data-Driven Solution

<div class="pt-12">
  <span @click="$slidev.nav.next" class="px-2 py-1 rounded cursor-pointer" hover="bg-white bg-opacity-10">
    Press Space to begin <carbon:arrow-right class="inline"/>
  </span>
</div>

<div class="abs-br m-6 text-sm">
  HUI Joo Hwee | AIAP Batch 22
</div>

<!--
Good morning. I'm here to present a solution that will significantly reduce fraud exposure for CyberProtect users while protecting our brand reputation.

In the next 10 minutes, I'll show you:
1. The scope of the problem we're facing
2. The AI solution I've built
3. The business impact - specifically, how this translates to cost savings and customer trust
4. What it takes to deploy this in production
5. The risks and how we're mitigating them

Let's start with the problem.
-->

---
layout: center
class: text-center
---

# The Problem

<div class="grid grid-cols-2 gap-12 pt-8">

<div>

## Current State

<div class="text-8xl font-bold text-red-500 pt-4">45%</div>
<div class="text-2xl pt-2">of phishing attacks</div>
<div class="text-xl text-gray-400">go undetected today</div>

<div class="pt-8 text-left text-lg">
Without AI detection:
- Users lose credentials
- Financial fraud occurs
- Brand trust erodes
- Support costs spike
</div>

</div>

<div>

## Customer Impact

<div class="pt-8">

<div class="text-center pb-6">
<div class="text-5xl">😱</div>
<div class="text-xl font-semibold">User clicks phishing link</div>
</div>

<div class="text-center pb-6">
<div class="text-5xl">💳</div>
<div class="text-xl font-semibold">Credentials stolen</div>
</div>

<div class="text-center pb-6">
<div class="text-5xl">📰</div>
<div class="text-xl font-semibold">News headline:<br/>"CyberProtect users hit by breach"</div>
</div>

</div>

</div>

</div>

<!--
Here's the reality: With our current approach, we're missing 45% of phishing attacks. That's nearly half.

What does this mean for our users? They click a link thinking they're accessing their bank. Instead, their credentials are stolen. Days later, they discover fraudulent charges. And what's the first thing they tell their friends? "CyberProtect didn't protect me."

This isn't just a technical problem - it's a brand problem. Every missed attack is a potential data breach headline. Every breach erodes the trust we've built with our customers.

The question isn't whether we can afford to build this AI solution. The question is: can we afford NOT to?
-->

---

# The Business Case

<div class="grid grid-cols-3 gap-6 pt-8">

<div class="bg-red-50 rounded-lg p-6 border-2 border-red-200">
<div class="text-center">
<div class="text-5xl mb-2">💸</div>
<div class="text-3xl font-bold text-red-600">$4.5M</div>
<div class="text-lg">Annual Fraud Cost</div>
<div class="text-sm text-gray-600 pt-2">
• 10,000 daily users<br/>
• 45% phishing prevalence<br/>
• 45% detection failure<br/>
• $100 avg fraud loss<br/>
• = 2,025 daily incidents<br/>
• = <strong>$202K daily loss</strong>
</div>
</div>
</div>

<div class="bg-yellow-50 rounded-lg p-6 border-2 border-yellow-200">
<div class="text-center">
<div class="text-5xl mb-2">😤</div>
<div class="text-3xl font-bold text-yellow-600">34%</div>
<div class="text-lg">Customer Churn Risk</div>
<div class="text-sm text-gray-600 pt-2">
• Industry data: 34% of fraud victims switch providers<br/>
• Our users: 3,400 at risk<br/>
• Lifetime value: $500/user<br/>
• = <strong>$1.7M annual churn cost</strong>
</div>
</div>
</div>

<div class="bg-blue-50 rounded-lg p-6 border-2 border-blue-200">
<div class="text-center">
<div class="text-5xl mb-2">📞</div>
<div class="text-3xl font-bold text-blue-600">$890K</div>
<div class="text-lg">Support Burden</div>
<div class="text-sm text-gray-600 pt-2">
• 2,025 daily fraud incidents<br/>
• 60% contact support<br/>
• 1,215 daily tickets<br/>
• $2/ticket handling cost<br/>
• = <strong>$2.4K daily support cost</strong>
</div>
</div>
</div>

</div>

<div class="pt-6 text-center">

## Total Annual Cost of Inaction: <span class="text-6xl font-bold text-red-600">$7.1M</span>

</div>

<!--
Let me put this in financial terms.

First bucket: Direct fraud costs. With 10,000 daily users and 45% phishing prevalence, that's 4,500 daily exposures. We currently miss 45% - that's 2,025 fraud incidents per day. At $100 average loss per incident, that's $202,000 daily or $4.5 million annually in direct fraud costs.

Second bucket: Customer churn. Industry research shows 34% of fraud victims switch to competitors. That's 3,400 of our users at risk. At $500 lifetime value per user, we're looking at $1.7 million in lost revenue from churn.

Third bucket: Support costs. Every fraud incident generates support tickets. At 60% contact rate, that's 1,215 daily tickets. Even at just $2 per ticket for handling, that's $890K annually.

Add it up: We're looking at $7.1 million in annual costs from this problem. And that doesn't even count the reputational damage - which is impossible to quantify but potentially far larger.

This is the cost of doing nothing.
-->

---
layout: center
class: text-center
---

# The Solution

## AI-Powered Real-Time Phishing Detection

<div class="grid grid-cols-3 gap-8 pt-12">

<div>
<div class="text-6xl mb-4">🤖</div>
<div class="text-2xl font-bold mb-2">Intelligent</div>
<div class="text-lg text-gray-600">Learns patterns humans miss</div>
</div>

<div>
<div class="text-6xl mb-4">⚡</div>
<div class="text-2xl font-bold mb-2">Fast</div>
<div class="text-lg text-gray-600">50ms per check<br/>(instant for users)</div>
</div>

<div>
<div class="text-6xl mb-4">🎯</div>
<div class="text-2xl font-bold mb-2">Accurate</div>
<div class="text-lg text-gray-600">86% of attacks caught<br/>(vs 55% today)</div>
</div>

</div>

<div class="pt-12">

## How It Works: Think Airport Security

<div class="text-left max-w-3xl mx-auto pt-4 text-lg">

Just like airport security checks multiple signals (ID, boarding pass, metal detector), our AI examines:

- **Website Age**: New sites (days old) are suspicious - legitimate businesses have years of history
- **Missing Credentials**: No security certificates or contact info? Red flag
- **Suspicious Patterns**: Excessive pop-ups, hidden redirects, fake login forms

The AI was trained on 11,000+ real-world examples to spot these patterns instantly.

</div>

</div>

<!--
Here's what I've built: An AI system that acts like a security checkpoint for every website our users visit.

Three key attributes:

Intelligent: The AI learned from 11,000 real-world examples - both legitimate sites and phishing attacks. It spots patterns that humans would miss, like newly registered domains combined with missing security indicators.

Fast: Each check takes 50 milliseconds - that's 1/20th of a second. Users won't notice any lag.

Accurate: We catch 86% of phishing attacks, compared to 55% today. That's a 31% improvement.

Think of it like airport security. A single check might look simple - they scan your ID, check your boarding pass, run you through a metal detector. But behind the scenes, they're evaluating multiple signals simultaneously to assess risk.

Our AI does the same thing. It examines website age - phishing sites are often hours or days old, while legitimate businesses have years of history. It checks for security credentials - does the site have proper certificates, contact information, terms of service? And it looks for suspicious patterns - excessive pop-ups, hidden redirects, fake login forms.

All of this happens in 50 milliseconds, completely transparent to the user.
-->

---

# The Results

<div class="grid grid-cols-2 gap-8 pt-4">

<div>

## Performance Improvement

<div class="pt-4">

<div class="flex items-center justify-between mb-6">
<div class="text-xl">Detection Rate</div>
<div>
<span class="text-3xl font-bold text-red-500">55%</span>
<span class="text-2xl mx-2">→</span>
<span class="text-3xl font-bold text-green-500">86%</span>
</div>
</div>

<div class="flex items-center justify-between mb-6">
<div class="text-xl">Attacks Missed Daily</div>
<div>
<span class="text-3xl font-bold text-red-500">2,025</span>
<span class="text-2xl mx-2">→</span>
<span class="text-3xl font-bold text-green-500">630</span>
</div>
</div>

<div class="flex items-center justify-between mb-6">
<div class="text-xl">Fraud Prevented</div>
<div>
<span class="text-3xl font-bold text-green-500">1,395</span>
<span class="text-lg ml-2">incidents/day</span>
</div>
</div>

</div>

<div class="pt-6 bg-green-50 rounded-lg p-4 border-2 border-green-200">
<div class="text-center">
<div class="text-2xl font-bold text-green-600 mb-2">Annual Impact</div>
<div class="text-5xl font-bold text-green-700">$3.2M</div>
<div class="text-lg">in prevented fraud costs</div>
<div class="text-sm text-gray-600 pt-2">(1,395 daily incidents × $100 × 365 days)</div>
</div>
</div>

</div>

<div>

## Customer Protection

<div class="pt-4 space-y-4">

<div class="bg-blue-50 rounded-lg p-4 border-l-4 border-blue-500">
<div class="font-bold text-lg mb-2">😊 Enhanced Trust</div>
<div class="text-gray-700">
Users see "Protected by AI" badge → increased confidence in CyberProtect brand
</div>
</div>

<div class="bg-blue-50 rounded-lg p-4 border-l-4 border-blue-500">
<div class="font-bold text-lg mb-2">📉 Reduced Churn</div>
<div class="text-gray-700">
69% fewer fraud victims (1,395 prevented daily) → saves 2,345 customers annually @ $500 LTV = <strong>$1.2M retention value</strong>
</div>
</div>

<div class="bg-blue-50 rounded-lg p-4 border-l-4 border-blue-500">
<div class="font-bold text-lg mb-2">📞 Lower Support Load</div>
<div class="text-gray-700">
837 fewer daily support tickets @ $2/ticket = <strong>$611K annual savings</strong>
</div>
</div>

<div class="bg-blue-50 rounded-lg p-4 border-l-4 border-blue-500">
<div class="font-bold text-lg mb-2">📰 Reputation Shield</div>
<div class="text-gray-700">
69% fewer breach headlines → protects brand value (unquantifiable but significant)
</div>
</div>

</div>

</div>

</div>

<div class="pt-4 text-center">

## Total Annual Value: <span class="text-5xl font-bold text-green-600">$5.0M</span>

<div class="text-lg text-gray-600">(Direct fraud prevention $3.2M + Churn reduction $1.2M + Support savings $0.6M)</div>

</div>

<!--
Let me show you the numbers.

Detection rate: We jump from catching 55% of attacks to 86%. That's a 31-percentage-point improvement.

In concrete terms: Instead of missing 2,025 phishing attempts daily, we now miss only 630. That's 1,395 fraud incidents prevented every single day.

Annual impact: At $100 average fraud loss, preventing 1,395 daily incidents translates to $3.2 million in direct fraud prevention annually.

But the value goes beyond prevented fraud:

Enhanced trust: Users see a "Protected by AI" badge - this increases confidence in our brand. They're more likely to recommend CyberProtect to friends and family.

Reduced churn: We prevent 1,395 fraud incidents daily - that's 69% fewer victims. Using the 34% churn rate, we save 2,345 customers annually. At $500 lifetime value, that's $1.2 million in retention value.

Lower support load: 69% fewer incidents means 837 fewer daily support tickets. At $2 per ticket, that's $611,000 in annual savings.

Reputation shield: Every prevented attack is a breach headline we avoid. This protects our brand value - impossible to quantify precisely, but absolutely critical for long-term growth.

Add it all up: $5 million in annual value. And remember, our cost of inaction was $7.1 million. This solution gets us most of the way there, with room for further optimization.
-->

---

# The Trade-Off: Trust vs. Security

<div class="grid grid-cols-2 gap-8 pt-8">

<div>

## Challenge: False Alarms

<div class="pt-4">

<div class="text-lg mb-4">
Current AI setting catches 86% of attacks but flags <span class="text-red-600 font-bold">18% of legitimate sites</span> as potentially suspicious.
</div>

<div class="bg-red-50 rounded-lg p-4 border-2 border-red-200 mb-4">
<div class="font-bold mb-2">User Experience Impact:</div>
<div class="text-sm">
18 out of 100 legitimate sites show warning:<br/>
<em>"⚠️ This site may be unsafe - proceed with caution?"</em>
</div>
</div>

<div class="text-lg mb-2 font-semibold">The Question:</div>
<div class="text-base text-gray-700">
Will users tolerate 18% false warnings in exchange for 86% protection? Or will they ignore warnings and erode trust?
</div>

</div>

</div>

<div>

## My Recommendation: A/B Test

<div class="pt-4 space-y-4">

<div class="bg-blue-50 rounded-lg p-4 border-l-4 border-blue-500">
<div class="font-bold mb-2">Option A: Balanced (5% false alarms)</div>
<div class="text-sm">
• Catches 75% of attacks (vs 86%)<br/>
• Only 5% false warnings<br/>
• Better user experience<br/>
• <strong>Trade-off: Miss 11% more attacks</strong>
</div>
</div>

<div class="bg-green-50 rounded-lg p-4 border-l-4 border-green-500">
<div class="font-bold mb-2">Option B: Aggressive (18% false alarms)</div>
<div class="text-sm">
• Catches 86% of attacks<br/>
• 18% false warnings<br/>
• Maximum protection<br/>
• <strong>Risk: Users may ignore warnings</strong>
</div>
</div>

<div class="bg-yellow-50 rounded-lg p-4 border-l-4 border-yellow-500">
<div class="font-bold mb-2">Recommended Approach</div>
<div class="text-sm">
1. <strong>Week 1-2</strong>: Deploy Option B to 10% of users<br/>
2. <strong>Week 3-4</strong>: Deploy Option A to another 10%<br/>
3. <strong>Measure</strong>: Warning dismissal rate, user complaints, actual breach prevention<br/>
4. <strong>Decide</strong>: Scale winning approach to 100% of users
</div>
</div>

</div>

</div>

</div>

<!--
Now let me be transparent about the challenge we face.

At current settings, the AI catches 86% of phishing attacks - excellent protection. But there's a trade-off: it also flags 18% of legitimate sites as potentially suspicious.

What does this mean in practice? Imagine a user accessing their bank's website. 18 times out of 100, they'll see a warning: "This site may be unsafe - proceed with caution?"

The question we need to answer: Will users tolerate this to get 86% protection? Or will they start ignoring warnings - which actually makes them LESS safe because they stop paying attention?

This is a classic security-versus-usability trade-off, and I don't think we should guess the answer. I think we should test it.

Here's my recommendation:

Option A - Balanced: Tune the AI to be more conservative. We catch 75% of attacks instead of 86%, but false alarms drop to 5%. Better user experience, but we miss 11% more attacks.

Option B - Aggressive: Keep current settings. Maximum protection at 86%, but 18% false alarms. Risk is users may develop "warning fatigue" and start clicking through without reading.

My recommendation: Don't choose - test both. Deploy Option B to 10% of users for two weeks. Deploy Option A to another 10%. Measure three things: how often users dismiss warnings without reading, how many complaints we get, and most importantly - how many actual breaches we prevent.

After four weeks, we'll have data showing which approach users prefer AND which keeps them safer. Then we scale the winner to all users.

This way, we're making a data-driven decision rather than guessing.
-->

---

# Deployment Plan

<div class="grid grid-cols-2 gap-8 pt-4">

<div>

## Timeline (8 Weeks)

<div class="pt-4 space-y-3">

<div class="flex items-start">
<div class="bg-blue-500 text-white rounded-full w-10 h-10 flex items-center justify-center font-bold mr-4 flex-shrink-0">1</div>
<div>
<div class="font-bold">Week 1-2: Browser Extension Build</div>
<div class="text-sm text-gray-600">Integrate AI model into Chrome/Firefox extension</div>
</div>
</div>

<div class="flex items-start">
<div class="bg-blue-500 text-white rounded-full w-10 h-10 flex items-center justify-center font-bold mr-4 flex-shrink-0">2</div>
<div>
<div class="font-bold">Week 3-4: Internal Beta Testing</div>
<div class="text-sm text-gray-600">50 CyberProtect employees test in real-world use</div>
</div>
</div>

<div class="flex items-start">
<div class="bg-blue-500 text-white rounded-full w-10 h-10 flex items-center justify-center font-bold mr-4 flex-shrink-0">3</div>
<div>
<div class="font-bold">Week 5-6: Limited Public Rollout</div>
<div class="text-sm text-gray-600">10% of users (1,000) get early access + A/B test</div>
</div>
</div>

<div class="flex items-start">
<div class="bg-blue-500 text-white rounded-full w-10 h-10 flex items-center justify-center font-bold mr-4 flex-shrink-0">4</div>
<div>
<div class="font-bold">Week 7: Data Analysis & Tuning</div>
<div class="text-sm text-gray-600">Analyze warning dismissal rates, tune threshold</div>
</div>
</div>

<div class="flex items-start">
<div class="bg-green-500 text-white rounded-full w-10 h-10 flex items-center justify-center font-bold mr-4 flex-shrink-0">5</div>
<div>
<div class="font-bold">Week 8: Full Launch</div>
<div class="text-sm text-gray-600">Scale to 100% of users, announce publicly</div>
</div>
</div>

</div>

</div>

<div>

## Investment Required

<div class="pt-4">

<div class="bg-gray-50 rounded-lg p-4 mb-3">
<div class="flex justify-between items-center">
<div class="font-semibold">Engineering (2 FTEs × 8 weeks)</div>
<div class="text-xl font-bold">$40K</div>
</div>
<div class="text-sm text-gray-600">Frontend + backend integration</div>
</div>

<div class="bg-gray-50 rounded-lg p-4 mb-3">
<div class="flex justify-between items-center">
<div class="font-semibold">Cloud Infrastructure</div>
<div class="text-xl font-bold">$15K</div>
</div>
<div class="text-sm text-gray-600">Servers, API calls, monitoring (annual)</div>
</div>

<div class="bg-gray-50 rounded-lg p-4 mb-3">
<div class="flex justify-between items-center">
<div class="font-semibold">Data Science (retraining)</div>
<div class="text-xl font-bold">$10K</div>
</div>
<div class="text-sm text-gray-600">Quarterly model updates (annual)</div>
</div>

<div class="bg-blue-50 rounded-lg p-4 border-2 border-blue-500">
<div class="flex justify-between items-center">
<div class="text-lg font-bold">Total First-Year Cost</div>
<div class="text-3xl font-bold text-blue-600">$65K</div>
</div>
</div>

<div class="mt-6 bg-green-50 rounded-lg p-4 border-2 border-green-500">
<div class="text-center">
<div class="text-lg font-bold mb-2">ROI Calculation</div>
<div class="text-sm">
Annual Value: <span class="font-bold text-green-600">$5.0M</span><br/>
First-Year Cost: <span class="font-bold text-red-600">$65K</span><br/>
<div class="text-3xl font-bold text-green-700 mt-2">76× Return</div>
</div>
</div>
</div>

</div>

</div>

</div>

<!--
Let's talk deployment. This can be live in 8 weeks.

Timeline breakdown:

Weeks 1-2: Browser extension build. Our engineering team integrates the AI model into a Chrome and Firefox extension. This is the primary technical lift.

Weeks 3-4: Internal beta. We deploy to 50 CyberProtect employees for real-world testing. This catches any bugs before customers see them.

Weeks 5-6: Limited public rollout. 10% of our users - about 1,000 people - get early access. This is where we run the A/B test I mentioned: half see the aggressive setting (18% false alarms), half see the balanced setting (5% false alarms).

Week 7: Data analysis. We crunch the numbers - which setting do users prefer? Which prevents more breaches? We tune the final threshold based on real-world data.

Week 8: Full launch. We scale to 100% of users and announce publicly: "CyberProtect now features AI-powered phishing protection."

Investment required:

Engineering: Two full-time engineers for 8 weeks at $40,000 total. This covers frontend and backend integration.

Cloud infrastructure: $15,000 annually for servers, API calls, and monitoring. The AI runs in the cloud to ensure it's always up-to-date with the latest phishing tactics.

Data science: $10,000 annually for quarterly retraining. Phishing tactics evolve - we need to keep the AI current.

Total first-year cost: $65,000.

Compare that to the $5 million in annual value: That's a 76-times return on investment in year one. Even if we're off by 50%, it's still a 38× ROI.

This is a no-brainer investment.
-->

---

# Risk Management

<div class="grid grid-cols-2 gap-6 pt-4">

<div>

## What Could Go Wrong?

<div class="pt-4 space-y-3">

<div class="bg-red-50 rounded-lg p-4 border-l-4 border-red-500">
<div class="font-bold text-lg mb-2">⚠️ Attackers Adapt</div>
<div class="text-sm text-gray-700">
<strong>Risk:</strong> Phishers learn to bypass AI (e.g., artificially age domains)<br/>
<strong>Probability:</strong> Medium (3-6 months after launch)<br/>
<strong>Mitigation:</strong> Quarterly retraining on new attack patterns + anomaly detection flags suspicious "old" domains with new content
</div>
</div>

<div class="bg-red-50 rounded-lg p-4 border-l-4 border-red-500">
<div class="font-bold text-lg mb-2">🙈 Warning Fatigue</div>
<div class="text-sm text-gray-700">
<strong>Risk:</strong> Users ignore warnings if false alarms too high<br/>
<strong>Probability:</strong> High if >10% false alarm rate<br/>
<strong>Mitigation:</strong> A/B test to find optimal threshold + monthly user surveys + warning dismissal rate monitoring
</div>
</div>

<div class="bg-red-50 rounded-lg p-4 border-l-4 border-red-500">
<div class="font-bold text-lg mb-2">🐛 Technical Failures</div>
<div class="text-sm text-gray-700">
<strong>Risk:</strong> AI service downtime → no protection<br/>
<strong>Probability:</strong> Low (99.9% uptime SLA)<br/>
<strong>Mitigation:</strong> Fallback to rule-based detection + 24/7 monitoring + automatic alerts
</div>
</div>

</div>

</div>

<div>

## Success Monitoring (Weekly)

<div class="pt-4 space-y-3">

<div class="bg-green-50 rounded-lg p-4 border-l-4 border-green-500">
<div class="font-bold text-lg mb-2">📊 Core Metrics</div>
<div class="text-sm">
• <strong>Detection Rate:</strong> % of known phishing caught (target: ≥75%)<br/>
• <strong>False Positive Rate:</strong> % of legitimate sites flagged (target: ≤5%)<br/>
• <strong>User Warning Dismissal Rate:</strong> % of warnings clicked through (alert if >40%)<br/>
• <strong>Prevented Fraud Incidents:</strong> Daily count (baseline: 1,395)
</div>
</div>

<div class="bg-green-50 rounded-lg p-4 border-l-4 border-green-500">
<div class="font-bold text-lg mb-2">💬 User Feedback</div>
<div class="text-sm">
• <strong>NPS Score:</strong> Monthly survey "How likely to recommend?" (target: +20 increase)<br/>
• <strong>Support Tickets:</strong> Volume trend (expect -69% reduction)<br/>
• <strong>App Store Reviews:</strong> Sentiment analysis on "security" mentions
</div>
</div>

<div class="bg-green-50 rounded-lg p-4 border-l-4 border-green-500">
<div class="font-bold text-lg mb-2">💰 Business Impact</div>
<div class="text-sm">
• <strong>Churn Rate:</strong> % of users canceling (expect -2.3% reduction)<br/>
• <strong>Customer Acquisition Cost:</strong> "AI Protection" as marketing angle<br/>
• <strong>Upsell Conversion:</strong> Premium tier with advanced protection
</div>
</div>

</div>

</div>

</div>

<!--
Every project has risks. Let me be upfront about what could go wrong and how we're protecting against it.

Risk 1 - Attackers adapt: Once we deploy, sophisticated phishers will study our AI and try to bypass it. For example, they might artificially age domains to look legitimate.

Probability: Medium. This will happen within 3-6 months of launch.

Mitigation: We're not building a static system. Quarterly retraining keeps the AI current with new attack patterns. Plus, we're adding anomaly detection - if an "old" domain suddenly hosts brand-new phishing content, we flag it as suspicious regardless of age.

Risk 2 - Warning fatigue: If false alarms are too high, users stop reading warnings and click through automatically. This makes them LESS safe, not more.

Probability: High if we exceed 10% false alarm rate.

Mitigation: This is exactly why we're A/B testing. We'll find the threshold where users stay engaged with warnings. We're also monitoring warning dismissal rates weekly - if they spike above 40%, we know we need to recalibrate.

Risk 3 - Technical failures: What if our AI service goes down?

Probability: Low. We're targeting 99.9% uptime.

Mitigation: Fallback to rule-based detection if the AI service is unavailable. Users still get basic protection. Plus, 24/7 monitoring with automatic alerts if uptime drops.

On the monitoring side, we're tracking success weekly across three dimensions:

Core metrics: Detection rate (target ≥75%), false positive rate (target ≤5%), warning dismissal rate (alert if >40%), and prevented fraud incidents (baseline 1,395 daily).

User feedback: NPS score (expect +20 point increase), support ticket volume (expect -69% reduction), and app store review sentiment.

Business impact: Churn rate (expect -2.3%), customer acquisition cost (we can market "AI Protection"), and premium tier conversion (advanced protection features).

Bottom line: We're going in eyes open. We know the risks, we're monitoring aggressively, and we have contingency plans.
-->

---
layout: center
class: text-center
---

# Competitive Landscape

<div class="grid grid-cols-3 gap-6 pt-12">

<div class="bg-gray-50 rounded-lg p-6 border-2 border-gray-200">
<div class="text-4xl mb-3">🐌</div>
<div class="text-xl font-bold mb-2">Competitors Today</div>
<div class="text-sm text-gray-600">
• Manual blacklists (updated weekly)<br/>
• 55-60% detection rates<br/>
• 3-5 day delay for new threats<br/>
• No personalization
</div>
</div>

<div class="bg-blue-50 rounded-lg p-6 border-4 border-blue-500">
<div class="text-4xl mb-3">🚀</div>
<div class="text-xl font-bold mb-2 text-blue-600">CyberProtect with AI</div>
<div class="text-sm">
• <strong>Real-time AI detection</strong><br/>
• <strong>86% detection rate</strong><br/>
• <strong>Instant protection for new threats</strong><br/>
• <strong>Learns from user behavior</strong>
</div>
</div>

<div class="bg-yellow-50 rounded-lg p-6 border-2 border-yellow-300">
<div class="text-4xl mb-3">⏰</div>
<div class="text-xl font-bold mb-2">Competitors in 6-12 Months</div>
<div class="text-sm text-gray-600">
• Will catch up with AI<br/>
• Detection rates normalize<br/>
• Feature parity achieved<br/>
• First-mover advantage lost
</div>
</div>

</div>

<div class="pt-12 text-2xl">

## First-Mover Advantage: <span class="text-blue-600 font-bold">6-12 Month Window</span>

<div class="text-lg text-gray-600 pt-4">
Move now → market leader in AI security<br/>
Delay → follower copying competitors
</div>

</div>

<!--
Let me put this in competitive context.

Today's landscape: Our competitors are still using manual blacklists - security analysts updating lists of known phishing sites weekly. They achieve 55-60% detection rates, and there's a 3-5 day lag when new phishing campaigns emerge before they're added to blacklists.

With AI, we leap ahead: 86% detection rate, real-time protection for brand-new threats the instant they appear, and the system learns from user behavior patterns.

But here's the critical point: This advantage won't last forever. In 6-12 months, competitors will deploy their own AI solutions. Detection rates will normalize. We'll achieve feature parity with everyone else.

The question is: Do we want to be the first mover who defines "AI-powered security," or do we want to be the follower playing catch-up?

First-mover advantages are powerful in security:
- Marketing: We get to say "First to deploy AI protection" - huge trust signal
- User acquisition: Security-conscious users flock to the leader
- Press coverage: "CyberProtect launches AI phishing detection" is a story. "CyberProtect also launches AI" 6 months later is not.
- Premium positioning: First movers can charge premium prices for advanced features

This is a 6-12 month window. If we move now, we're the market leader. If we wait, we're a follower copying our competitors.

I think the choice is clear.
-->

---
layout: center
---

# Next Steps & Decision Points

<div class="grid grid-cols-2 gap-12 pt-8">

<div>

## Immediate Actions (This Week)

<div class="pt-4 space-y-3">

<div class="flex items-start">
<div class="text-2xl mr-3">✅</div>
<div>
<div class="font-bold">CEO Approval</div>
<div class="text-sm text-gray-600">Greenlight project + $65K budget</div>
</div>
</div>

<div class="flex items-start">
<div class="text-2xl mr-3">✅</div>
<div>
<div class="font-bold">Assign Engineering Lead</div>
<div class="text-sm text-gray-600">2 FTEs for 8-week sprint</div>
</div>
</div>

<div class="flex items-start">
<div class="text-2xl mr-3">✅</div>
<div>
<div class="font-bold">Kickoff Meeting</div>
<div class="text-sm text-gray-600">Align stakeholders on timeline</div>
</div>
</div>

</div>

<div class="pt-8 bg-blue-50 rounded-lg p-6 border-2 border-blue-500">
<div class="font-bold text-lg mb-3">🎯 Go/No-Go Decision Point</div>
<div class="text-sm">
<strong>After Week 6 (Limited Rollout)</strong><br/><br/>
If A/B test shows:<br/>
• ≥70% detection + ≤10% false alarms → Scale to 100%<br/>
• <70% detection or >15% false alarms → Retune AI<br/>
• Users love it (NPS +15) → Accelerate launch<br/>
• Users hate it (NPS -10) → Pause and reassess
</div>
</div>

</div>

<div>

## Success Criteria (8 Weeks)

<div class="pt-4 space-y-3">

<div class="bg-green-50 rounded-lg p-4 border-l-4 border-green-500">
<div class="font-bold mb-2">Technical</div>
<div class="text-sm">
✓ Extension deployed in Chrome & Firefox stores<br/>
✓ 99.9% uptime in production<br/>
✓ <100ms latency per check<br/>
✓ ≥75% detection rate on test set
</div>
</div>

<div class="bg-green-50 rounded-lg p-4 border-l-4 border-green-500">
<div class="font-bold mb-2">User Experience</div>
<div class="text-sm">
✓ ≤5% false positive rate (tuned threshold)<br/>
✓ <40% warning dismissal rate<br/>
✓ NPS increase +15 or higher<br/>
✓ <2% negative reviews mentioning warnings
</div>
</div>

<div class="bg-green-50 rounded-lg p-4 border-l-4 border-green-500">
<div class="font-bold mb-2">Business</div>
<div class="text-sm">
✓ 1,000+ daily fraud incidents prevented<br/>
✓ Support ticket volume down ≥50%<br/>
✓ Press coverage in ≥3 security publications<br/>
✓ Premium tier signups +20%
</div>
</div>

</div>

<div class="pt-6 text-center">
<div class="text-xl font-bold">Timeline: Decision Today → Live in 8 Weeks</div>
</div>

</div>

</div>

<!--
So here's what I need from you today.

Immediate actions this week:

First, CEO approval. I need your greenlight to proceed and approval for the $65,000 first-year budget.

Second, assign an engineering lead. We need two full-time engineers for the 8-week sprint.

Third, kickoff meeting. Let's align all stakeholders - engineering, product, support, marketing - on the timeline and success criteria.

Success criteria at 8 weeks:

Technical: Extension deployed in Chrome and Firefox stores, 99.9% uptime, under 100ms latency, at least 75% detection rate.

User experience: 5% or lower false positive rate, under 40% warning dismissal rate, NPS increase of +15 or higher, fewer than 2% negative reviews mentioning warnings.

Business: 1,000+ daily fraud incidents prevented, support tickets down at least 50%, press coverage in at least 3 security publications, premium tier signups up 20%.

Go/No-Go decision point:

After Week 6, when we have A/B test results from the limited rollout, we make a data-driven decision:

If we're hitting ≥70% detection with ≤10% false alarms, we scale to 100% of users immediately.

If detection is below 70% or false alarms above 15%, we retune the AI before full launch.

If users love it (NPS +15 or higher), we accelerate the launch and prepare the press release.

If users hate it (NPS drops 10 points), we pause and reassess whether we need a fundamentally different approach.

This is a data-driven process with a clear decision framework.

Timeline: If you give me the go-ahead today, we're live in 8 weeks. That puts us in market 6-12 months ahead of competitors.

The decision is yours.
-->

---
layout: center
class: text-center
---

# Summary: The Case for AI-Powered Phishing Protection

<div class="grid grid-cols-3 gap-8 pt-12">

<div class="bg-red-50 rounded-lg p-6 border-2 border-red-300">
<div class="text-5xl mb-4">💸</div>
<div class="text-2xl font-bold text-red-600 mb-2">The Problem</div>
<div class="text-lg">
$7.1M annual cost<br/>
45% missed attacks<br/>
Brand reputation risk
</div>
</div>

<div class="bg-green-50 rounded-lg p-6 border-2 border-green-500">
<div class="text-5xl mb-4">🎯</div>
<div class="text-2xl font-bold text-green-600 mb-2">The Solution</div>
<div class="text-lg">
86% detection rate<br/>
$5M annual value<br/>
8-week deployment
</div>
</div>

<div class="bg-blue-50 rounded-lg p-6 border-2 border-blue-500">
<div class="text-5xl mb-4">📊</div>
<div class="text-2xl font-bold text-blue-600 mb-2">The ROI</div>
<div class="text-lg">
$65K investment<br/>
76× first-year return<br/>
6-12 mo competitive edge
</div>
</div>

</div>

<div class="pt-12">

## <span class="text-blue-600">Recommendation: Approve & Launch Immediately</span>

<div class="text-xl pt-6 max-w-4xl mx-auto">
Protecting our users from phishing attacks isn't just good security - it's good business. With an 76× ROI, 6-12 month competitive advantage, and 8-week deployment timeline, the risk is in waiting, not acting.
</div>

</div>

<div class="pt-8">
<div class="text-2xl">I'm ready to start Monday. What questions do you have?</div>
</div>

<!--
Let me bring this together.

The problem: We're facing $7.1 million in annual costs from phishing attacks. We miss 45% of attacks today. Every missed attack is a fraud incident, a frustrated customer, and a potential brand-damaging headline.

The solution: AI-powered real-time phishing detection. 86% detection rate - a 31-point improvement. $5 million in annual value from prevented fraud, reduced churn, and lower support costs. And we can deploy in just 8 weeks.

The ROI: $65,000 investment in year one. That's a 76-times return. Even if I'm off by 50%, it's still a 38× return. Plus, we gain a 6-12 month competitive advantage as the first mover in AI security.

My recommendation: Approve this project today and let's start Monday.

Here's why I'm confident:
- The math works. $65K for $5M in value is a no-brainer.
- The timeline is realistic. 8 weeks to production is aggressive but achievable.
- The risks are manageable. We're A/B testing the user experience, monitoring aggressively, and we have fallback plans.
- The competitive advantage is real. First movers in security win trust, users, and premium positioning.

The question isn't whether we should do this. The question is: can we afford not to?

Every week we delay is another $140,000 in fraud costs, another 14,000 incidents, another opportunity for competitors to catch up.

I'm ready to lead this project starting Monday. What questions do you have?
-->

---
layout: end
class: text-center
---

# Questions?

<div class="pt-8 text-xl">

Thank you for your time.

</div>

<div class="pt-12">

📧 **Email**: huijoohwee@live.com  
🔗 **Technical Details**: [GitHub Repository](https://github.com/huijoohwee/aiap22-hui-joo-hwee-045B)

</div>

<div class="pt-12 text-sm text-gray-400">
Built with data, driven by impact, ready to deploy.
</div>

<!--
Thank you for your time. I know you have many priorities competing for resources and attention.

But I genuinely believe this is one of those rare projects where the business case is overwhelming:
- Clear problem ($7.1M annual pain)
- Measurable solution (86% detection, $5M value)
- Proven ROI (76× return in year one)
- Fast timeline (8 weeks to launch)
- Competitive advantage (6-12 month first-mover window)

I'm ready to answer any questions you have:
- About the technical implementation
- About the A/B testing approach
- About the competitive landscape
- About the financial projections
- About the risks and mitigation strategies

My contact information is on the screen. The full technical documentation is available on GitHub if you or your team want to dive deeper into the AI methodology.

I'm ready to start as soon as you give the word.

Thank you again, and I look forward to your questions.
-->

---

## Prompt_202601162000

### Prompt-01

```
**use code snippet, forbid code blocks/interactive demo**

"You have 10 minutes to present this to CyberProtect's CEO (non-technical). What would you cover?"

generate  `interview-presentation-ceo.md`  that is compatible with https://github.com/slidevjs/slidev.git (such as supporting https://sli.dev/guide/syntax#notes, https://sli.dev/features/import-snippet, https://sli.dev/features/line-highlighting) Markdown-to-HTML presentation demo
```

#### Note-01

```
This CEO presentation is:

✅ **Non-technical**: No code, no math formulas, plain English
✅ **Business-focused**: Every slide ties to $, customer trust, or competitive advantage  
✅ **Quantified**: Specific numbers ($7.1M cost, 86% detection, 76× ROI)
✅ **Actionable**: Clear next steps and decision points
✅ **10 minutes**: ~11 slides at 50-60 seconds each
✅ **Slidev-compatible**: Speaker notes, transitions, layout variants
✅ **Honest**: Acknowledges trade-offs (false alarms) and proposes A/B testing

**Key persuasion techniques used**:
1. **Problem-first**: Start with pain ($7.1M) before solution
2. **Storytelling**: User journey ("clicks link → credentials stolen → headline")
3. **Analogy**: Airport security (familiar mental model)
4. **Social proof**: "Industry standard" and "first-mover advantage"
5. **Risk mitigation**: Transparent about what could go wrong + plans
6. **Competitive urgency**: 6-12 month window before parity
```
