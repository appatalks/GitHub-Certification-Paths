# Lesson 8: Supplementary Practice Questions

[Return to the lesson](lesson-guide.md) | [All lessons](../README.md)

These 15 original mixed-domain GH-100-style questions practice choosing
controls and interpreting incomplete evidence. They are not official or
recalled exam items, do not reproduce exam weighting, and do not predict exam
content or scores. All scenarios are fictional Cloud paper exercises.
Choose the stated number of answers before opening the answer key. Use missed
concepts to guide study, not to infer a certification pass mark.

## Questions

### 1. Two Independent Access Problems

**Choose one.** An employee passes SAML authentication. Their classic PAT has the required scope but is not authorized for the SSO organization. Their GitHub account also lacks repository access. What is required for an authorized API request?

- A. Only changing the PAT's display name.
- B. Only successful SAML sign-in, which assigns repository roles.
- C. Both appropriate token SSO/policy authorization and approved underlying repository access.
- D. An idle Actions runner instead of either access condition.

### 2. Immediate Credential Exposure

**Choose one.** A public leak contains a credential the issuer confirms is still valid. A separate dependency alert has no confirmed exposure path yet. Which immediate containment action is most directly justified?

- A. Coordinate issuer-side revocation/rotation of the exposed credential while separately triaging the dependency.
- B. Delete the latest file and assume the credential stops working.
- C. Delay all credential response until dependency exploitability is proven.
- D. Close both alerts because neither proves data theft.

### 3. Access After Team Removal

**Choose two.** A contractor is removed from a team but still has direct repository write access and an organization base read grant. Which statements are accurate?

- A. Team removal automatically cancels every independent grant.
- B. The direct write grant remains an access path until appropriately removed.
- C. Base read automatically reduces direct write to read.
- D. Offboarding must account for membership/base access as well as direct/team grants.

### 4. Federation Is Not Account Ownership

**Choose one.** A stakeholder proposes "make our personal accounts managed by enabling organization SAML." What is the correct response?

- A. SAML always transfers ownership of existing personal accounts to the company.
- B. SAML immediately provisions an EMU enterprise without a design decision.
- C. Team synchronization is the account-model migration mechanism.
- D. Organization SAML and EMU account ownership are different; evaluate the supported enterprise model and transition requirements separately.

### 5. Usage and Incomplete Billing Facts

**Choose one.** One employee belongs to several organizations, and a manager wants to sum every membership row as a separately billable user. Which response is strongest?

- A. Every membership row always represents another paid seat.
- B. Verify the actual license metric, unique-user treatment, enterprise scope, and agreement rather than equating raw memberships with billed seats.
- C. Organization membership proves all metered products are unlimited.
- D. Remove the employee from all organizations before investigating billing.

### 6. Approvals and Checks

**Choose one.** A release pull request has one approval but a failing required check. Multiple enforced rules apply and the actor has no bypass. Which conclusion follows?

- A. Approval satisfies every rule automatically.
- B. Repository ownership is unnecessary if the check has started.
- C. The applicable required check must also be satisfied; examine all effective requirements before allowing merge.
- D. Renaming the release tag bypasses the branch requirements.

### 7. App Scope and Approval

**Choose one.** A GitHub App only summarizes issues from one repository, but requests contents write and access to all repositories. What is the best approval decision?

- A. Request a justified repository/permission scope and review policy before approving the installation.
- B. Approve all requested access because installation tokens are short-lived.
- C. Treat a recognizable vendor name as proof of least privilege.
- D. Replace the app with an unrestricted permanent PAT without reviewing access.

### 8. Security Closure

**Choose two.** Which evidence supports closing a dependency-remediation finding?

- A. A screenshot showing only that an update pull request was opened.
- B. The affected branch now has the approved fixed dependency state.
- C. Relevant review/test and alert-state evidence, with any remaining deployment/exposure questions tracked.
- D. A renamed alert with no dependency change or justified dismissal.

### 9. Trusted Release and Untrusted Tests

**Choose one.** A repository has fork tests and a trusted production release. Which design best separates the trust boundaries?

- A. Run both on the same persistent internal-network runner with every secret.
- B. Use `pull_request_target` to execute arbitrary fork code with release credentials.
- C. Grant every contributor the production environment's approval role.
- D. Keep untrusted tests in suitably isolated execution without production credentials; gate the trusted release and its restricted runner/secret access separately.

### 10. Reusable Workflow Ceiling

**Choose one.** A reusable release workflow needs contents write, but its caller permits contents read only. What is the appropriate response?

- A. Assume the called workflow can elevate its token independently.
- B. Review the trusted publishing need and authorize the minimal caller/callee permission chain; the callee cannot exceed the caller's ceiling.
- C. Put `write-all` on every unrelated test job.
- D. Change the runner label to `write` to grant contents write.

### 11. Labels, Groups, and Secrets

**Choose two.** A release job is queued despite a matching runner label, and a secret is scoped to a different repository. Which controls must be investigated independently?

- A. Runner-group repository/workflow eligibility and actual availability.
- B. The repository's displayed description only.
- C. Whether the label name contains the secret name.
- D. Organization-secret repository scope and any relevant workflow/environment protections.

### 12. API Rate-Limit Evidence

**Choose one.** The failing response explicitly identifies primary rate-limit exhaustion and quota remaining is zero. Permission checks show the caller has the necessary access. What should be addressed first?

- A. Make the caller an organization owner without reviewing the limit.
- B. Change repository visibility to public.
- C. Follow reset/retry guidance and reduce unnecessary request volume, retaining the sanitized evidence.
- D. Publish the token so more people can try it.

### 13. Spend Versus Capacity

**Choose one.** Spend rises while queue wait remains low and execution durations are stable. A manager proposes more runners. What is the best evidence-based response?

- A. More spending proves a capacity shortage.
- B. Stable durations prove billing is wrong.
- C. Disable every workflow without examining product use.
- D. Inspect volume, runner/product choices, rates, and cost drivers; the supplied performance data does not establish capacity shortage.

### 14. Support or Local Administration

**Choose one.** A reproduced error remains unexplained after scoped access, policy, and rate-limit checks. What is the strongest escalation?

- A. A safe Support ticket with product/account context, timestamps, errors/request IDs, reproduction, and completed checks.
- B. A public issue containing tokens and raw private logs.
- C. A claim of global outage with no scope evidence.
- D. A GHES server-bundle procedure applied blindly to GHEC.

### 15. Exam Readiness

**Choose one.** A learner answers most Cloud practice questions correctly. What should determine their remaining study plan?

- A. Treat this question set's score as the official exam result.
- B. Compare every current official objective with evidence of understanding/practice, including remaining GHES and configuration gaps.
- C. Skip all objectives not mentioned in this supplement.
- D. Memorize answer letters instead of the documented reasoning.

## Answer Key

<details>
<summary>Answers and explanations</summary>

| Question | Answer | Explanation | Source |
| --- | --- | --- | --- |
| 1 | C | Token SSO authorization and underlying repository access are separate prerequisites. Sign-in, token names, and runner availability do not replace them. | S1, S2 |
| 2 | A | A confirmed valid exposed credential warrants containment at its issuer. File deletion or absence of proven theft does not remove that exposure. | S3 |
| 3 | B, D | Direct and base grants can survive team removal. A lower base grant does not subtract a higher direct grant. | S2 |
| 4 | D | SAML authentication requirements do not turn personal accounts into enterprise-owned managed accounts. EMU needs its own supported model/lifecycle design. | S4, S5 |
| 5 | B | Membership rows and billed-user metrics are not interchangeable. Verify applicable unique-user/license rules rather than guessing or removing access. | S6 |
| 6 | C | Approval and successful required checks are independent applicable requirements. Names and started checks do not satisfy failed-check enforcement. | S7 |
| 7 | A | Short token lifetime does not justify excessive installation permissions or repository scope. Branding and broad PAT substitution do not solve least privilege. | S8 |
| 8 | B, C | Applied state and verification evidence support remediation. A proposed update or renamed finding does not demonstrate closure. | S9 |
| 9 | D | Separate untrusted execution from production trust and credentials. Shared privileged runners, privileged untrusted triggers, and broad reviewer access weaken that boundary. | S10, S11 |
| 10 | B | The caller sets the permission ceiling. A justified trusted release can require narrowly authorized contents write, not unrelated writes or scheduling labels. | S12 |
| 11 | A, D | Runner eligibility and secret authorization are separate control paths. Matching labels, descriptions, or names do not resolve both. | S13, S14 |
| 12 | C | The response supports quota exhaustion. Broad ownership, visibility changes, and credential publication do not address request-rate handling. | S15 |
| 13 | D | Spending can change through volume, product choices, or rates without a queue-capacity problem. Stable execution also does not prove a billing fault. | S6 |
| 14 | A | Sanitized, reproducible evidence supports escalation. Credentials, unsupported service-wide claims, and wrong-deployment diagnostics do not. | S16 |
| 15 | B | The current official objectives govern study coverage. This independent set supplies neither an official pass score nor complete objective coverage. | S17 |

</details>

## Sources

- **S1:** [PAT authorization for SAML SSO](https://docs.github.com/en/enterprise-cloud@latest/authentication/authenticating-with-saml-single-sign-on/authorizing-a-personal-access-token-for-use-with-saml-single-sign-on).
- **S2:** [Organization roles](https://docs.github.com/en/enterprise-cloud@latest/organizations/managing-peoples-access-to-your-organization-with-roles/roles-in-an-organization).
- **S3:** [Secret-scanning response](https://docs.github.com/en/code-security/secret-scanning/managing-alerts-from-secret-scanning).
- **S4:** [SAML SSO](https://docs.github.com/en/enterprise-cloud@latest/authentication/authenticating-with-saml-single-sign-on/about-authentication-with-saml-single-sign-on).
- **S5:** [Enterprise Managed Users](https://docs.github.com/en/enterprise-cloud@latest/admin/managing-iam/understanding-iam-for-enterprises/about-enterprise-managed-users).
- **S6:** [Billing documentation](https://docs.github.com/en/billing).
- **S7:** [Rulesets](https://docs.github.com/en/enterprise-cloud@latest/repositories/configuring-branches-and-merges-in-your-repository/managing-rulesets/about-rulesets).
- **S8:** [GitHub Apps and OAuth Apps](https://docs.github.com/en/apps/oauth-apps/building-oauth-apps/differences-between-github-apps-and-oauth-apps).
- **S9:** [Dependabot security updates](https://docs.github.com/en/code-security/dependabot/dependabot-security-updates/about-dependabot-security-updates).
- **S10:** [Secure use of Actions](https://docs.github.com/en/actions/reference/security/secure-use).
- **S11:** [Deployment environments](https://docs.github.com/en/actions/deployment/targeting-different-environments/using-environments-for-deployment).
- **S12:** [Reusing workflows](https://docs.github.com/en/actions/sharing-automations/reusing-workflows).
- **S13:** [Runner-group access](https://docs.github.com/en/actions/how-tos/manage-runners/self-hosted-runners/manage-access).
- **S14:** [Using secrets](https://docs.github.com/en/actions/security-for-github-actions/security-guides/using-secrets-in-github-actions).
- **S15:** [REST API rate limits](https://docs.github.com/en/rest/using-the-rest-api/rate-limits-for-the-rest-api).
- **S16:** [Creating a support ticket](https://docs.github.com/en/support/contacting-github-support/creating-a-support-ticket).
- **S17:** [Official GH-100 study guide](https://learn.microsoft.com/en-us/credentials/certifications/resources/study-guides/gh-100).