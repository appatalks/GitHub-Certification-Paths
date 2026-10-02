# Lesson 7: Supplementary Practice Questions

[Return to the lesson](lesson-guide.md) | [All lessons](../README.md)

These 15 original GH-100-style questions cover usage, audit/API investigation,
and cost/performance decisions. They are not official or recalled exam items
and do not predict exam content or scores. All numbers and scenarios are
fictional. These are Cloud paper exercises, not authority to change billing,
remove users, export private logs, or generate traffic to trigger rate limits.
Choose the stated number of answers before opening the answer key.

## Questions

### 1. Seat Assignment

**Choose one.** At one snapshot, 430 of 500 available seats are assigned. What is the assignment percentage?

- A. 70%.
- B. 86%.
- C. 116.3%.
- D. 43%.

### 2. Activity Among Assigned Users

**Choose one.** Of those 430 assigned users, 290 meet a supplied 30-day activity definition. What is the active share of assigned users?

- A. 58%.
- B. 86%.
- C. 148.3%.
- D. Approximately 67.4%.

### 3. Percentage Points

**Choose one.** Usage rises from 60% to 82% of the same budget threshold. What is the increase in percentage points?

- A. 22 percentage points.
- B. 36.7 percentage points.
- C. 82 percentage points.
- D. 22% of the original value.

### 4. Relative Growth

**Choose one.** For the same change from 60% to 82%, what is the approximate relative increase?

- A. 22%.
- B. 82%.
- C. 36.7%.
- D. 26.8%.

### 5. Comparing Reports

**Choose two.** Which conditions are important for a meaningful period-to-period comparison?

- A. Consistent metric definitions, denominators/cohorts, and report scope, or an explicit adjustment for changes.
- B. Changing the activity definition without documenting it.
- C. Treating a one-day report as directly equivalent to a 30-day report.
- D. Comparable periods and awareness of changes in workloads, prices, or included products.

### 6. Inactivity Is Not No Need

**Choose one.** A licensed user has no event under a narrow 30-day activity definition. What is the most defensible next step before removal?

- A. Remove access immediately because every role must create events monthly.
- B. Verify role, access need, report limitations, and the applicable license/reclamation process.
- C. Assume the account was compromised.
- D. Grant owner access to encourage usage.

### 7. Budget Threshold

**Choose one.** Metered consumption reaches 82% of a defined internal budget threshold. What does this establish?

- A. Runners are busy 82% of the time.
- B. Every API request is near its rate limit.
- C. Exactly 82% of users are active.
- D. Consumption is at that budget ratio; capacity and activity require their own evidence.

### 8. Primary API Rate Limit

**Choose one.** A response identifies primary rate-limit exhaustion, with remaining quota zero and a reset time. Which response best fits?

- A. Respect the documented reset guidance and reduce unnecessary requests rather than retrying continuously.
- B. Retry as fast as possible until a request succeeds.
- C. Publish the token to distribute retries among strangers.
- D. Treat the reset time as proof of missing repository membership.

### 9. Secondary Limits

**Choose one.** Requests hit a documented secondary rate limit despite apparently remaining primary quota. What should be investigated?

- A. Only the organization seat count.
- B. Whether the repository's name is too short.
- C. Request concurrency/patterns, endpoint load, and the documented retry/backoff guidance.
- D. Whether a branch ruleset has one approval instead of two, without checking API behavior.

### 10. A 403 Response

**Choose two.** Which evidence sets help distinguish an API permission failure from rate limiting?

- A. The caller's terminal font and favorite editor extension.
- B. Sanitized response error/status and relevant rate-limit/retry headers.
- C. Endpoint, authentication context, token permission scope, and underlying resource access.
- D. The credential value in a shared worksheet.

### 11. PAT and App Limits

**Choose one.** How should an administrator compare API limits for a user PAT and a GitHub App installation token?

- A. Assume every authentication type has one identical universal quota.
- B. Infer the limit solely from the token's displayed name.
- C. Assume Apps have unlimited requests.
- D. Identify authentication type and applicable documented limit/account rules, then inspect the response headers.

### 12. Adoption Investigation

**Choose one.** A feature shows low use. Which analysis best supports an adoption recommendation?

- A. Review availability, eligibility, relevant workflows, and barriers with stakeholders before deciding whether higher use is valuable.
- B. Require every repository to use the feature regardless of need.
- C. Remove every license belonging to a non-user immediately.
- D. Treat low use as proof of a GitHub outage.

### 13. Correlation in Audit Data

**Choose one.** API errors occurred the day after an audit event changed a policy. What is the strongest interpretation?

- A. The event proves the cause without examining affected requests.
- B. The actor must have intended an outage.
- C. The timing is a hypothesis lead; compare affected scope and response evidence to test causation.
- D. No investigation is possible because audit data exists.

### 14. Cost and Performance Optimization

**Choose two.** Which actions support a measured optimization decision?

- A. Buy capacity solely because spending rose.
- B. Change licenses, runner size, and every workflow simultaneously.
- C. Break down product/workload consumption and separate queue delay from execution time.
- D. Test a narrow reversible change with success, cost, and security criteria.

### 15. Escalation Evidence

**Choose one.** After reasonable local checks, unexplained failures persist. Which escalation record is most useful?

- A. Only a cost percentage without symptoms.
- B. Sanitized timestamps, request IDs/errors, affected scope, expected results, and checks already performed, through an approved channel.
- C. A raw credential and an unfiltered directory export.
- D. A statement that all GitHub services are down without testing scope.

## Answer Key

<details>
<summary>Answers and explanations</summary>

| Question | Answer | Explanation | Source |
| --- | --- | --- | --- |
| 1 | B | `430 / 500 * 100 = 86%`. The other options use an incorrect ratio or scale. | S1 |
| 2 | D | `290 / 430 * 100` is about `67.4%`. `58%` uses available seats, not assigned users; the other ratios do not answer the question. | S1 |
| 3 | A | Subtract the percentages: `82 - 60 = 22` points. Relative change is a different measure. | S1 |
| 4 | C | Relative growth is `(82 - 60) / 60 * 100`, approximately `36.7%`. The denominator is the original value. | S1 |
| 5 | A, D | Consistent definitions/scope and comparable periods make differences interpretable. Undocumented changes and unequal periods can mislead. | S1 |
| 6 | B | A narrow activity metric does not establish business need or license treatment. Removal, compromise claims, and privilege increases require other evidence. | S1 |
| 7 | D | Budget consumption is not runner utilization, API quota, or user activity. Inspect each metric's own source and definition. | S1 |
| 8 | A | Documented reset handling and request reduction address primary exhaustion. Aggressive retries and credential exposure worsen risk. | S2 |
| 9 | C | Secondary restrictions concern request behavior as well as primary quota. Seats, names, and unrelated review settings do not diagnose them. | S2 |
| 10 | B, C | Error/headers and access context distinguish competing causes. A 403 alone does not settle the diagnosis, and token values should not be shared. | S2, S3 |
| 11 | D | Applicable rate rules depend on authentication/account context. Names, universal-quota assumptions, and unlimited-App claims are unreliable. | S2 |
| 12 | A | Low use may reflect lack of need, entitlement, or workflow barriers. Investigate before forcing adoption, removing licenses, or alleging outages. | S1, S4 |
| 13 | C | Temporal sequence is not causal proof. Match scope and response evidence before assigning cause or intent. | S3, S4 |
| 14 | C, D | Breakdowns and reversible experiments test optimization while retaining attribution. Broad simultaneous changes and spend-only capacity guesses do not. | S1, S5 |
| 15 | B | Scoped, reproducible sanitized diagnostics enable Support investigation. Credentials, unrelated percentages, and unsupported outage claims do not. | S6 |

</details>

## Sources

Check the [official GH-100 outline](https://learn.microsoft.com/en-us/credentials/certifications/resources/study-guides/gh-100). Ratios above use the supplied synthetic definitions, not a promise about a product report's fields.

- **S1:** [Billing and usage documentation](https://docs.github.com/en/billing).
- **S2:** [REST API rate limits](https://docs.github.com/en/rest/using-the-rest-api/rate-limits-for-the-rest-api).
- **S3:** [Troubleshooting the REST API](https://docs.github.com/en/rest/using-the-rest-api/troubleshooting-the-rest-api).
- **S4:** [Enterprise audit log](https://docs.github.com/en/enterprise-cloud@latest/admin/monitoring-activity-in-your-enterprise/reviewing-audit-logs-for-your-enterprise/about-the-audit-log-for-your-enterprise).
- **S5:** [Self-hosted runner workflow routing](https://docs.github.com/en/actions/hosting-your-own-runners/managing-self-hosted-runners/using-self-hosted-runners-in-a-workflow).
- **S6:** [Creating a support ticket](https://docs.github.com/en/support/contacting-github-support/creating-a-support-ticket).