# Lesson 7: Monitoring and Optimization

**Exam domain:** Monitor and optimize GitHub usage (10-15%)

## Goals

- Explain what each report tells you and what it cannot tell you.
- Calculate simple usage percentages and explain their limits.
- Suggest a small, reversible improvement and describe how you would check it helped.

## Words to Know

| Word | Plain-language meaning |
| --- | --- |
| Seat | A place assigned to a user under a licensing arrangement; actual billing definitions depend on the plan. |
| Assigned | Allocated to a user, not necessarily actively used. |
| Utilization | The share of an available amount being used according to a stated definition. |
| Time window | The period covered by a report. |
| API | An interface a program uses to ask GitHub to perform an operation or return data. |
| Rate limit | A restriction on how many or how frequently API requests may be made. |
| Hypothesis | A possible explanation to check, not a proven cause. |
| Reversible change | A change you can undo if it does not help or causes harm. |

Create a notes table with these columns before reading: observation, source,
time window, possible explanation, and next check. An observation is what the
record says; an explanation is your interpretation.

## Investigate

- Review the monitoring, API usage, licensing, and optimization objectives in the [current GH-100 study guide](https://aka.ms/GH100-StudyGuide).
- Read [Reviewing audit logs for your enterprise](https://docs.github.com/en/enterprise-cloud@latest/admin/monitoring-activity-in-your-enterprise/reviewing-audit-logs-for-your-enterprise). What activity can these records show, and what do they not establish?
- Read [Rate limits for the REST API](https://docs.github.com/en/rest/using-the-rest-api/rate-limits-for-the-rest-api). What evidence distinguishes rate limiting from other causes of API errors?
- Review [metered product and license usage](https://docs.github.com/en/enterprise-cloud@latest/billing/how-tos/products/view-productlicense-use) and [GitHub Actions billing](https://docs.github.com/en/billing/managing-billing-for-your-products/managing-billing-for-github-actions/about-billing-for-github-actions). Which definitions, plan details, and time windows matter?

## Your Starting Scenario

All values are fictional. For this exercise only, "active" means at least one event in a 30-day window. These numbers are not product benchmarks or billing guidance.

| Record | Value | Fictional source | Period |
| --- | --- | --- | --- |
| Available seats | 500 | License inventory | End-of-period snapshot |
| Assigned seats | 430 | License inventory | Same snapshot |
| Assigned users meeting the exercise activity definition | 290 | Synthetic activity report, covering the same assigned population | Previous 30 days |
| Actions budget use | 82% of an internal budget threshold | Internal cost summary, not a runner-capacity report | Same 30-day period |
| Ruleset change | Morgan changed `web` review rules | Synthetic administrative change note | Day 20 |
| API errors | Team reports failures on some requests | Team incident note; response headers/status are missing | Days 21-22 |

## Work Through the Problem

### Start with Your Sandbox

1. Complete [organization setup](../sandbox-setup.md). Ask the owner which audit or usage report you may inspect and whether it covers this organization or the whole enterprise.
2. Where permitted, inspect report names, scope, and available time windows. Do not export member activity, billing amounts, or raw audit records for publication.
3. Use only the synthetic numbers below for calculations. The supplied seat counts and budget figures are not your organization's usage.
4. Keep report access observational. Do not remove seats, change billing settings, or generate paid usage to recreate the exercise.

### Step 1: Calculate Two Ratios

1. Write the formula: assigned seats divided by available seats, multiplied by 100.
2. Substitute the two seat values from the table. Use a calculator if needed; record the calculation and percentage.
3. Write a second formula: assigned users meeting the activity definition divided by assigned seats, multiplied by 100.
4. Substitute the relevant numbers and round to one decimal place.
5. Under each result, write a sentence starting "This means ..." using the exercise's definitions. Then write "It does not show ..." to name one limitation.

**Save:** Two calculations and their explanations. Neither calculation proves whether someone's access is still required.

### Checkpoint 1: Use the Right Denominator

**Objective focus:** Interpreting usage reports. **Choose one answer.**

Using this lesson's definitions and snapshot, which pair correctly describes seat assignment and the fraction of assigned users meeting the activity definition?

- A. 67.4% assigned; 86% of assigned users active.
- B. 58% assigned; 86% of assigned users active.
- C. 86% assigned; approximately 67.4% of assigned users active.
- D. 86% assigned; 58% of assigned users active.

<details>
<summary>Check your answer</summary>

**Answer: C.** Assignment is `430 / 500 * 100 = 86%`. Activity among assigned users is `290 / 430 * 100`, approximately `67.4%`. A swaps the ratios; B uses the activity count for assignment; D divides activity by available seats rather than assigned users. These use the synthetic definition, not a universal GitHub activity metric. Review [billing documentation](https://docs.github.com/en/billing) when interpreting an actual report's definitions.

</details>

### Step 2: Separate Evidence from Explanations

1. Copy each record into your notes table, including its source and period.
2. Mark each record as a snapshot, a measurement over a period, or an incident report.
3. Write a question about scope or completeness for each record. For example, does the activity report include every relevant kind of work?
4. For the budget figure, explain what you would need to know about costs and job timing before suggesting more runners.
5. Use the billing documentation to identify which real report you would consult to validate the corresponding number. Do not query live accounts for this lesson.

**Save:** The evidence table, with interpretations clearly labelled.

### Step 3: Investigate the API Errors

1. Write two possible explanations, such as rate limiting and missing access. The supplied note does not establish either.
2. Open the rate-limit documentation. Find the response status, headers, or error details relevant to checking a limit.
3. List the missing request details you would gather: endpoint, time, status, safe error text, and relevant limit headers. Never copy credentials into the note.
4. Explain why a ruleset change before the errors is not proof it caused them.
5. For each explanation, write one result that would support it and one that would make you reconsider.

**Save:** Two hypotheses with distinguishing evidence.

### Checkpoint 2: API Errors Need Distinguishing Evidence

**Objective focus:** API activity and rate limits. **Choose two answers.**

You have intermittent API errors but no status or response headers. Which two evidence sets help distinguish a rate-limit problem from an access problem?

- A. Sanitized status/error text and relevant rate-limit or retry headers for the affected request.
- B. The raw PAT value copied into the shared investigation note.
- C. Only the date of an unrelated ruleset change, treated as proof of cause.
- D. The request's endpoint and authentication type, plus permitted checks of the relevant access and permission scope.

<details>
<summary>Check your answer</summary>

**Answers: A and D.** Response details and access context help test competing explanations. A status such as 403 alone does not settle the cause; inspect the accompanying error and headers. B exposes a credential; C relies on timing alone. Review [REST API rate limits](https://docs.github.com/en/rest/using-the-rest-api/rate-limits-for-the-rest-api).

</details>

### Step 4: Respond to the Executive

The executive asks to remove every seat without a recorded event and immediately
increase runner capacity based on the budget figure.

1. Create headings: facts, unknowns, risk of acting now, next step, and follow-up measurement.
2. Put only supplied observations under facts. Put access needs, reporting completeness, and queue/capacity evidence under unknowns.
3. Propose a limited investigation or reversible change instead of changing every account at once.
4. State who should approve it, what result would show improvement, and when you would undo it if harmful. Use a measurement condition, not a prescribed study timeline.

**Save:** A short recommendation with a source and a way to check it.

### Checkpoint 3: Budget Is Not Runner Capacity

**Objective focus:** Cost and performance optimization. **Choose one answer.**

The report says consumption reached 82% of an internal budget threshold. What conclusion is justified without queue or execution data?

- A. Consumption is close to that defined threshold; investigate what drove it before making a capacity or license decision.
- B. Runners are busy exactly 82% of the time.
- C. Increasing runner count must lower the bill.
- D. Every user outside the activity definition should immediately lose access.

<details>
<summary>Check your answer</summary>

**Answer: A.** A budget ratio is a spending signal, not a runner-utilization or access-need measure. B substitutes a different metric; C asserts an untested cost effect; D treats activity as the sole access criterion. Review [billing documentation](https://docs.github.com/en/billing) and the evidence needed in your Step 4 recommendation.

</details>

## You Are Finished When

- [ ] Both percentages show their inputs and arithmetic.
- [ ] You distinguish assigned seats, recorded activity, budget use, and runner capacity.
- [ ] Each API explanation has evidence that could support or contradict it.
- [ ] Your recommendation names missing facts, an owner, and a follow-up measurement.

## Supplementary Practice

Use the [15-question practice set and answer key](practice-questions.md) for additional exam-style retrieval practice.

## Teach It Back

Present your analysis to your tutor. Explain how you calculated the ratios and why the figures alone do or do not support the requested changes. Identify the source and follow-up measure you would use to test your recommendation.

## Carry Forward

Review your earlier work and choose two objectives to revisit in Lesson 8. Bring your analysis and a short readiness note based on your own practice evidence.