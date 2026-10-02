# Lesson 4: Repository Security and Integrations

**Exam domain:** Implement secure software development and compliance (25-30%)

## Goals

- Explain what a security alert tells you and what still needs checking.
- Plan a safe response when a credential may have been exposed.
- Decide what access an app or automation account actually needs.

## Words to Know

| Word | Plain-language meaning |
| --- | --- |
| Dependency | A software package that a project uses. |
| Dependabot alert | A warning about a known vulnerability in a dependency used by a repository. |
| Secret | A credential, such as a token or password, that must not be shared. |
| Secret scanning | Finding patterns that may indicate exposed credentials. |
| Code scanning | Analyzing code for potential security problems; CodeQL is one analysis tool. |
| Triage | Sorting findings by what is known, potential harm, and the next safe action. |
| GitHub App / OAuth app | Two integration models with different permissions and access behavior. |
| PAT | Personal access token: a credential associated with a person's account. |
| Revoke / rotate | Invalidate a credential / replace it with a new one. Deleting text from Git alone does not do this. |

## Your Starting Scenario

All records below are invented. Package names and findings are teaching inputs,
not reports of real vulnerabilities. Do not generate a real credential.

| Record | Supplied facts | Owner |
| --- | --- | --- |
| DEP-1 | `web` uses fictional package `example-parser` 1.0; an alert suggests fixed version 1.1; runtime use is unknown. | Avery, application maintainer |
| SEC-1 | A commit contains `EXAMPLE_SECRET_DO_NOT_USE`; the incident simulation asks how you would respond if it had been a real credential. No actual secret exists here. | Morgan, repository owner; credential issuer is unknown |
| CODE-1 | A scanner flags a path from request input to a database query in `search.js`; whether input is validated is unknown. | Avery |
| APP-1 | A vendor needs to read issues in `web` and create summary issues there; it requests write access to contents and issues in every repository. App type is unspecified. | Morgan reviews access; vendor owns the app |
| AUTO-1 | A scheduled tool needs to read issues in `web`; a developer proposes a long-lived personal token with broad repository access. | Platform team owns the automation |

## Investigate

- Compare [secret scanning](https://docs.github.com/en/enterprise-cloud@latest/code-security/secret-scanning/introduction/about-secret-scanning), [code scanning](https://docs.github.com/en/enterprise-cloud@latest/code-security/code-scanning/introduction-to-code-scanning/about-code-scanning), and [Dependabot alerts](https://docs.github.com/en/enterprise-cloud@latest/code-security/dependabot/dependabot-alerts/about-dependabot-alerts). What does each detect, and what does an alert not prove?
- Read [Differences between GitHub Apps and OAuth apps](https://docs.github.com/en/apps/oauth-apps/building-oauth-apps/differences-between-github-apps-and-oauth-apps) and [Choosing permissions for a GitHub App](https://docs.github.com/en/apps/creating-github-apps/setting-up-a-github-app/choosing-permissions-for-a-github-app). Which permissions does the stated task actually need?
- Review [Managing personal access tokens](https://docs.github.com/en/enterprise-cloud@latest/authentication/keeping-your-account-and-data-secure/managing-your-personal-access-tokens). What policies, scope limits, and lifecycle questions apply?

## Work Through the Problem

### Start with Your Sandbox

1. Complete [organization setup](../sandbox-setup.md). Open an approved repository's **Security** tab and permitted security settings.
2. Record which features are visible, enabled, disabled, or unavailable under aliases. Do not assume an absent tab proves a feature is disabled.
3. Use the supplied fictional findings for response practice. Do not export real alerts, install a vulnerable dependency, expose a credential, or change real integration approvals to recreate them.
4. If separately approved, use harmless dummy files to explore an available feature in the disposable repository, record the starting state, and clean up afterward. A placeholder that does not trigger an alert is not proof of secret-scanning coverage.

### Step 1: Sort the Findings

1. Create a table with columns: record, detection tool, known facts, unanswered questions, owner, and next action.
2. Add DEP-1, SEC-1, and CODE-1. Match each to the relevant documentation above.
3. For DEP-1, list what you would check about package use, affected versions, upgrade compatibility, and a test of the proposed fix.
4. For CODE-1, list what code and input-validation evidence you would examine before deciding it is a real vulnerability.
5. Keep potential harm separate from confirmed harm. Use "unknown" where facts are absent.

**Save:** The triage table with a source for each next action.

### Checkpoint 1: Dependency Triage

**Objective focus:** Vulnerability alerts and security response. **Choose one answer.**

DEP-1 reports a vulnerable dependency and a proposed fixed version, but runtime use is unknown. Which next action is best supported?

- A. Close the finding because a fixed version exists.
- B. Declare exploitation proven without reviewing the application.
- C. Assess exposure, ownership, and the upgrade's test results before deciding priority and closure.
- D. Delete the alert so it no longer affects the dashboard.

<details>
<summary>Check your answer</summary>

**Answer: C.** A remediation decision needs impact and verification evidence. A mistakes an available fix for an applied fix; B mistakes a vulnerability for proof of exploitation; D hides the finding without addressing it. Review [Dependabot alerts](https://docs.github.com/en/code-security/dependabot/dependabot-alerts/about-dependabot-alerts).

</details>

### Step 2: Plan the Secret Response

1. For SEC-1, write "simulation only: placeholder is not a credential" at the top of the response note.
2. Use the secret scanning documentation to locate response/remediation guidance. Record the link you followed.
3. Write who you would contact to identify the credential issuer and affected systems in a real incident.
4. Put containment, revoke/rotate responsibility, exposure review, and safe repository cleanup in an ordered plan. Explain why editing a file would not invalidate a real token.
5. For each planned action, name the evidence that would verify it. Never test whether a real credential works as part of this exercise.

**Save:** A simulated response checklist, with owners and closure evidence.

### Checkpoint 2: Credential Containment

**Objective focus:** Secret scanning and response planning. **Choose two answers.**

In a hypothetical incident, a real credential was exposed in a repository. Which two actions belong in a coordinated containment and recovery plan?

- A. Delete the current file and assume the credential is invalid everywhere.
- B. Have the authorized credential owner revoke or rotate the exposed credential at its issuer.
- C. Paste the credential into a public issue to ask whether it still works.
- D. Update authorized dependents as needed and verify the old credential no longer works.

<details>
<summary>Check your answer</summary>

**Answers: B and D.** Containment must address the issuer and dependent services. A leaves copies/history and credential validity unresolved; C creates another exposure. Review [secret scanning alerts](https://docs.github.com/en/code-security/secret-scanning/managing-alerts-from-secret-scanning). SEC-1 in this lesson is only a placeholder; do not perform real revocation or plant a secret for this exercise.

</details>

### Step 3: Review App and Token Requests

1. Copy APP-1 and AUTO-1 into a table with columns: task, requested access, access to investigate, model, owner, and open questions.
2. Open the GitHub App/OAuth comparison. For APP-1, ask which app model the vendor uses before assuming installation-level permissions apply.
3. Use the GitHub App permission documentation to find permissions needed to read and create issues. Compare those with the requested contents access and all-repository scope.
4. For AUTO-1, compare a suitable GitHub App approach with a PAT approach. Record differences in ownership, selected repository access, expiry/rotation, and organization approval requirements.
5. Write a provisional approve/change/reject decision for each request. Name the documented conditions you would verify before approval.

**Save:** The integration review table and two short decisions.

### Step 4: Define What "Resolved" Means

1. Add a closure-evidence column to your triage table.
2. For each finding, describe a check of the underlying problem, not just an alert-status change.
3. Include follow-up tests for a dependency upgrade or code fix, and issuer-confirmed invalidation in the hypothetical secret incident.
4. Write one example of a dismissed alert that would not prove a fix occurred.

### Checkpoint 3: App Approval

**Objective focus:** API integrations and least privilege. **Choose one answer.**

APP-1 only needs to read issues in one repository, but requests contents and issues write across all repositories. The app model is not supplied. What is the best decision now?

- A. Approve because an app's requested permissions always match its needs.
- B. Pause approval, identify the app model and policy constraints, and request a scope justified by the read-only task.
- C. Replace it with a long-lived broad PAT without reviewing the new access.
- D. Approve the broad grant, since vendor branding proves safety.

<details>
<summary>Check your answer</summary>

**Answer: B.** The task does not justify the proposed grant, and app type affects available permission controls. A and D replace review with assumptions; C does not reduce the unjustified access. Review [GitHub Apps versus OAuth Apps](https://docs.github.com/en/apps/oauth-apps/building-oauth-apps/differences-between-github-apps-and-oauth-apps) and the integration sources in Investigate.

</details>

## You Are Finished When

- [ ] Each finding has known facts, open questions, an owner, and a next action.
- [ ] Your secret response distinguishes the placeholder exercise from a real incident.
- [ ] App/token access is tied to the task, not granted broadly by default.
- [ ] Closure evidence checks the problem rather than only changing its status.

Use only the placeholder `EXAMPLE_SECRET_DO_NOT_USE` if a sample value is required. Never enter or record a real secret, PAT, or token. Use an isolated repository only after checking its feature support and cleanup process.

## Supplementary Practice

Use the [15-question practice set and answer key](practice-questions.md) for additional exam-style retrieval practice.

## Teach It Back

Teach your tutor how you classified each finding and chose next actions. For every recommendation, point to the documentation and evidence you used. Mark any product-specific behavior that still needs verification.

## Carry Forward

Keep your triage sheet and app/PAT review notes. Lesson 5 applies least privilege and policy decisions to GitHub Actions workflows.