# Lesson 3: Supplementary Practice Questions

[Return to the lesson](lesson-guide.md) | [All lessons](../README.md)

These 15 original GH-100-style questions cover policy, rulesets, and audit
evidence. They are not official or recalled exam items and do not predict exam
content or scores. All scenarios are fictional Cloud paper exercises.
Choose the stated number of answers before opening the answer key.

## Questions

### 1. Inherited Policy

**Choose one.** An enterprise prohibits a capability. An organization owner wants to allow it through a less restrictive organization setting. What should they expect?

- A. Organization ownership always overrides enterprise policy.
- B. Renaming the organization removes the restriction.
- C. The applicable enterprise restriction remains a constraint on the organization.
- D. Repository write permission is sufficient to override it.

### 2. Ruleset Scope

**Choose one.** A rule protects `main`, but an unwanted direct push succeeds on `release`. What should be checked first?

- A. Whether the intended branch is included in the ruleset's target scope and enforcement.
- B. Whether the contributor has changed their profile picture.
- C. Whether the organization has unused license seats.
- D. Whether all repository secrets have been rotated.

### 3. Required Check

**Choose one.** A pull request has approval, but its required `test` check failed. Under enforced rules with no bypass, what should happen?

- A. Approval automatically substitutes for a successful check.
- B. The author can merge because the check started.
- C. Renaming the pull request satisfies the requirement.
- D. Merge remains blocked until the applicable check requirement is satisfied.

### 4. Evaluation Mode

**Choose one.** A supported ruleset is in evaluation mode. Which interpretation is correct?

- A. Evaluation guarantees noncompliant pushes are blocked.
- B. It can report would-be violations without enforcing the rule; verify mode before claiming protection.
- C. Evaluation transfers repository ownership to the auditor.
- D. Evaluation turns every actor into a bypass actor.

### 5. Emergency Exceptions

**Choose two.** Which properties make an emergency bypass process more accountable?

- A. A narrow authorized actor/scope and a recorded reason/approver.
- B. A permanent organization-wide bypass for every contributor.
- C. A restoration or expiry plan with a subsequent verification/review.
- D. Deleting the evidence after the emergency merge.

### 6. Overlapping Controls

**Choose one.** A repository is targeted by multiple applicable rulesets. What should an administrator do when diagnosing a blocked change?

- A. Inspect only whichever ruleset was created most recently.
- B. Assume the shortest ruleset name wins.
- C. Assume the repository-level rule nullifies every inherited rule.
- D. Inspect all applicable rulesets and requirements rather than assuming one replaces the others.

### 7. Audit Evidence

**Choose one.** An audit record attributes a setting change to Morgan. What does the record alone prove?

- A. The change had security approval.
- B. Morgan intended to weaken security.
- C. The recorded event occurred; authorization, context, and impact need further evidence.
- D. Every repository now has the same effective rules.

### 8. Positive and Negative Tests

**Choose two.** Which sandbox tests directly examine a required-review control?

- A. A merge attempt lacking required approval, using a non-bypass actor.
- B. A merge attempt satisfying all applicable requirements, using an authorized non-bypass actor.
- C. Viewing the repository logo.
- D. Counting enterprise seats without examining the pull request.

### 9. Approval After Changes

**Choose one.** Policy requires reviewers to approve the current changes, not an outdated commit. Which documented control should be evaluated?

- A. Increasing organization base permissions.
- B. Dismissing stale pull request approvals when new commits are pushed.
- C. Adding every author to the bypass list.
- D. Changing the repository description.

### 10. Tag Protection

**Choose one.** Only an approved process should create release tags matching `v*`. Which design best matches the requirement?

- A. A rule targeting only branch `main`, with no tag coverage.
- B. A naming convention with no enforced tag controls.
- C. Organization ownership for every person who might release.
- D. Supported tag-targeted rules and restricted creation/bypass behavior, tested with authorized and unauthorized cases.

### 11. Check Identity

**Choose one.** Administrators want a required status check to come from the approved integration rather than any producer of the same check name. What should they evaluate?

- A. The expected source/integration setting for the required check where supported.
- B. The author's avatar color.
- C. A secret named after the check, without changing rules.
- D. Disabling all status checks to avoid name collisions.

### 12. Missing Audit Result

**Choose one.** A filtered audit search returns no matching event. What is the sound next interpretation?

- A. The action definitely never occurred.
- B. The search proves all actors are authorized.
- C. Check filters, scope, retention, event coverage, and collection before drawing a conclusion.
- D. A repository owner must have deleted every enterprise record.

### 13. Governance Artifacts

**Choose two.** Which artifacts help another administrator verify a control decision?

- A. Only an unsupported claim that the settings are secure.
- B. A requirement-to-control map with applicable scope and exception rules.
- C. A list of credential values used in production.
- D. A test record distinguishing predicted results from observed allowed/denied behavior.

### 14. Bypass-Limited Access

**Choose one.** An actor's bypass is configured for pull requests only, not all interactions. What should a direct-push test assume?

- A. The actor has unrestricted direct-push bypass because they can bypass on a pull request.
- B. Pull-request bypass does not itself authorize direct-push bypass; evaluate the applicable rules and actor grants.
- C. Any repository member inherits the actor's bypass.
- D. The rule automatically switches to evaluation mode for direct pushes.

### 15. Closing a Governance Finding

**Choose one.** A misconfiguration was edited in Settings. What is still needed before declaring the finding resolved?

- A. Verify effective scope/enforcement with appropriate tests and retain the change/approval evidence.
- B. Treat the settings edit as proof of every expected behavior.
- C. Remove the original requirement from the report.
- D. Give all users bypass so future tests succeed.

## Answer Key

<details>
<summary>Answers and explanations</summary>

| Question | Answer | Explanation | Source |
| --- | --- | --- | --- |
| 1 | C | Lower-level ownership cannot relax the applicable enterprise restriction. Names and repository roles do not change policy inheritance. | S1 |
| 2 | A | Protection of one branch does not establish protection of another. Check target matching and enforcement before unrelated settings. | S2 |
| 3 | D | Approval and required checks are separate requirements. Starting a check or changing the title does not satisfy a failed check. | S3 |
| 4 | B | Evaluation measures prospective violations without active blocking. It is not proof of enforced protection or an ownership change. | S2 |
| 5 | A, C | Narrow authorization and restoration/review preserve accountability. Broad permanent bypass and erased evidence undermine it. | S2, S4 |
| 6 | D | Multiple rulesets can apply together. Do not infer last-created, name-based, or repository-precedence replacement. | S2 |
| 7 | C | Logging records an action, not approval or intent. Effective repository impact also depends on scope and other controls. | S4 |
| 8 | A, B | Non-bypass denied and allowed cases test enforcement. Branding and seat counts do not test a merge requirement. | S2, S3 |
| 9 | B | Stale-approval dismissal addresses changes after review. Broad permissions, bypasses, and descriptions do not ensure current-change approval. | S3 |
| 10 | D | Tag-targeted controls must match the tag namespace and intended creation path. Branch-only rules and conventions are not tag enforcement. | S3 |
| 11 | A | Binding a required check to its expected integration addresses producer identity. Cosmetic settings or disabling checks do not. | S3 |
| 12 | C | Search limitations can explain missing results. Absence in a filtered view is not conclusive evidence of absence or authorization. | S4 |
| 13 | B, D | The mapping and behavioral evidence make the decision inspectable. Unsupported claims and credential disclosure do not. | S2, S4 |
| 14 | B | Pull-request-only bypass has a narrower interaction scope than always-available bypass. It does not propagate to everyone or change enforcement mode. | S2 |
| 15 | A | A saved setting is not a behavior test. Preserve evidence and check the effective boundary rather than weakening it or deleting requirements. | S2, S4 |

</details>

## Sources

Check the [official GH-100 outline](https://learn.microsoft.com/en-us/credentials/certifications/resources/study-guides/gh-100) and current feature availability.

- **S1:** [Enterprise policies](https://docs.github.com/en/enterprise-cloud@latest/admin/enforcing-policies/enforcing-policies-for-your-enterprise/about-enterprise-policies).
- **S2:** [Rulesets](https://docs.github.com/en/enterprise-cloud@latest/repositories/configuring-branches-and-merges-in-your-repository/managing-rulesets/about-rulesets).
- **S3:** [Available rules for rulesets](https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/managing-rulesets/available-rules-for-rulesets).
- **S4:** [Organization audit log](https://docs.github.com/en/enterprise-cloud@latest/organizations/keeping-your-organization-secure/managing-security-settings-for-your-organization/reviewing-the-audit-log-for-your-organization).