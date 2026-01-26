
## 1. Project Purpose

The purpose of this project is to **increase sales efficiency and conversion** by helping sales teams **focus only on people who match their specific requirements**.

The system must measure **how well a profile matches the user's stated intent**, not generate decorative scores.

If this tool fails to guide correct outreach, it directly impacts revenue and company stability.

---

## 2. Business Problem

Sales teams currently waste time on:

* Profiles that don't match their specific requirements
* People who look good on paper but are inactive
* Old or irrelevant profile information

This leads to:

* Low response rates
* Poor pipeline quality
* Missed high-intent opportunities

---

## 3. Primary Objective

For any LinkedIn profile and user-defined intent, the system must clearly answer:

> **How well does this profile match my requirements?**

The output must support **immediate sales decisions**.

---

## 4. User Intent Input

The user provides a **free-form paragraph** describing exactly what they are looking for.

### Examples:

* "I need decision-makers who are actively evaluating CRM tools for mid-sized teams"
* "Looking for startup founders who recently raised funding and are scaling their engineering teams"
* "Find HR leaders in tech companies who are dealing with high employee turnover"

### Requirements:

* The input must be a clear description of the target profile characteristics
* The system accepts any intent - buying, hiring, partnership, or any other objective
* The more specific the intent, the more accurate the matching

---

## 5. Scope of the Tool

### The system must:

* Analyze LinkedIn profile information
* Match profile signals against the **user's stated intent**
* Prioritize **recent activity** over old background
* Score how well the profile aligns with user requirements

### The system must not:

* Act as a resume analyzer
* Show generic or misleading scores
* Treat all profile fields equally
* Overvalue education or old experience

---

## 6. How the System Should Judge Profiles

The system must evaluate profiles based on **alignment with the user's stated intent**.

### High Importance (most impact)

* Recent posts or activity **relevant to the user's intent**
* Current role and decision authority **related to the requirement**
* Recent changes or discussions **aligned with the stated need**

### Medium Importance

* Headline relevance to intent
* Profile summary alignment
* Current business context match

### Low Importance (background only)

* Education
* Old roles
* Certifications

Recent behavior that aligns with intent must **outweigh all static information**.

---

## 7. Recency Requirement (Critical)

* Recent activity must strongly influence results
* Old information must fade in importance over time
* Profiles with no recent signals must score lower

This ensures the system reflects **what is happening now**, not history.

---

## 8. Output Requirements

For each profile, the system must provide:

* **Confidence Score (0-100)** - how well the profile matches the user's intent

### Score Interpretation:

* **80-100**: Strong match - profile highly aligned with intent
* **60-79**: Moderate match - some alignment with intent
* **40-59**: Weak match - limited alignment
* **0-39**: Poor match - profile does not match intent

---

## 9. Actionability Requirement

The score should enable a sales person to decide:

* **80+**: Reach out now
* **60-79**: Monitor for later
* **Below 60**: Ignore for now

If this decision is not clear from the score, the output is insufficient.

---

## 10. Accuracy & Trust Principles

* A wrong high score is worse than a missed opportunity
* Conservative scoring is preferred over inflated confidence
* The system must avoid false urgency

Sales teams must **trust the output** to adopt it.

---

## 11. Efficiency Goals

The tool should help:

* Reduce time spent on poor leads
* Improve outreach focus
* Increase response and conversion rates
* Align sales effort with user's specific intent

---

## 12. Success Criteria

The project is successful if:

* Sales teams rely on the tool for any type of intent
* Outreach quality improves
* Irrelevant conversations reduce
* Conversion rates increase
* Sales productivity improves measurably
* The system accurately scores profiles against diverse user intents

---

## 13. Design Philosophy

This is a **decision-support tool**, not a reporting tool.

Every feature must justify itself by answering:

> *Does this help sales act better and faster?*

If not, it should not be included.
