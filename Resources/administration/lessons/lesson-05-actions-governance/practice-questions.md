# Lesson 5: Supplementary Practice Questions

[Return to the lesson](lesson-guide.md) | [All lessons](../README.md)

These 15 original GH-100-style questions cover workflow reuse, policy, token
permissions, and workflow trust. They are not official or recalled exam items
and do not predict exam content or scores. Scenarios are fictional Cloud paper
exercises, not permission to execute untrusted code or expose credentials.
Choose the stated number of answers before opening the answer key.

## Questions

### 1. Separate Job Permissions

**Choose one.** One job only reads code; another comments on issues. Which proposal best fits the tasks?

- A. Give both jobs `write-all` to avoid troubleshooting.
- B. Give the read job only its needed read permissions and the comment job the required issue-write permission.
- C. Supply a deployment credential to both jobs.
- D. Grant the read job organization ownership.

### 2. Unspecified Permissions

**Choose one.** A workflow explicitly sets `permissions: contents: read` using a permissions map. What happens to other available token permissions not specified in that map?

- A. They all become write permissions.
- B. They inherit organization-owner access.
- C. They depend only on the runner's labels.
- D. They are set to `none`; verify any operation that needs another permission.

### 3. Reusable Workflow Trigger

**Choose one.** Which trigger makes a workflow callable as a reusable workflow?

- A. `workflow_call`.
- B. `workflow_dispatch` alone.
- C. `schedule` alone.
- D. `pull_request` alone.

### 4. Action Versus Workflow Reuse

**Choose one.** Which structure correctly distinguishes a step action from a reusable workflow call?

- A. Both must be copied into shell commands.
- B. A reusable workflow is called only by a checkout step.
- C. A step action uses step-level `uses`; a reusable workflow is called with job-level `uses`.
- D. An action always grants more permissions than a reusable workflow.

### 5. Reusable Workflow Secrets

**Choose two.** Which statements about secrets in a reusable workflow are correct?

- A. Every organization secret is automatically passed to every called workflow.
- B. Review the called workflow's secret interface and pass only necessary secrets.
- C. A runner label substitutes for passing a secret.
- D. `secrets: inherit` is an explicit capability in supported call relationships, not proof that all inherited secrets are necessary.

### 6. Permission Elevation

**Choose one.** A caller gives a reusable workflow only read access, but the called workflow asks for broader token permissions. What is the governing principle?

- A. Called workflows can always elevate above the caller's token permissions.
- B. Permissions cannot be elevated by the called workflow above what the caller allows.
- C. Naming the workflow `trusted` grants owner access.
- D. Any secret input turns the token into an administrator token.

### 7. Enterprise Allow Policy

**Choose one.** An enterprise permits only approved actions. An organization allows all actions in its own settings. Which policy constrains the organization?

- A. The applicable enterprise restriction; a lower-level setting cannot relax it.
- B. Whichever policy has the shortest name.
- C. The least restrictive setting always wins.
- D. The workflow author's personal preference.

### 8. Action Reference Integrity

**Choose one.** Why is pinning an action to a reviewed full commit SHA stronger than using a mutable branch reference?

- A. It proves the action needs no security review.
- B. It automatically satisfies the enterprise allow policy.
- C. It removes all secret-access risk from the job.
- D. It fixes the selected code reference rather than following subsequent branch changes; review and policy still matter.

### 9. Privileged Pull Request Trigger

**Choose one.** A `pull_request_target` workflow checks out and runs code from an untrusted pull request while privileged credentials are available. What is the main concern?

- A. The repository has too few license seats.
- B. Checkout guarantees the code is trusted.
- C. Attacker-controlled code may execute in a privileged context and expose credentials or modify resources.
- D. The event prevents all network access by default.

### 10. Default Fork Behavior

**Choose one.** For a standard fork `pull_request` run using default security settings, what should be expected?

- A. All repository secrets and unrestricted writes are available.
- B. Secrets are not passed and `GITHUB_TOKEN` is read-only by default; inspect any non-default settings separately.
- C. The fork author inherits organization ownership.
- D. Review approval automatically passes every secret to the job.

### 11. Secret Logging

**Choose one.** A developer wants to print a credential to verify that masking works. What is the strongest recommendation?

- A. Avoid printing secrets; masking is not a guarantee against every transformed value or leak path.
- B. Print the value because masking makes disclosure impossible.
- C. Upload the value as an artifact instead of a log.
- D. Put the value in a pull request title for easier detection.

### 12. OIDC for Cloud Access

**Choose two.** Which elements belong in a secure OIDC-based deployment design?

- A. A long-lived broad cloud password committed to the workflow.
- B. A cloud trust rule accepting every repository and branch without review.
- C. Narrow cloud-side trust conditions for the expected repository/workflow/environment context.
- D. Permission to request an ID token, followed by an authorized short-lived cloud credential exchange.

### 13. Environment Protection

**Choose one.** A release job must wait for an authorized human approval before accessing its production environment secrets. Which feature should be evaluated where supported?

- A. Renaming the workflow file to `production`.
- B. Giving every job all organization secrets.
- C. Protected environments with required reviewers and appropriately scoped secrets.
- D. Increasing the job's CPU count.

### 14. Publishing a GitHub Release

**Choose one.** An approved same-repository job publishes a GitHub Release. Which `GITHUB_TOKEN` permission is relevant to that operation?

- A. `issues: read` only.
- B. `contents: write`, subject to the workflow's other needs and applicable controls.
- C. `id-token: write` alone, without contents access.
- D. Every write permission, including unrelated packages and issues.

### 15. Troubleshooting a Comment Failure

**Choose one.** After reducing permissions, an authorized issue-comment step fails. What is the best scoped investigation?

- A. Restore `write-all` everywhere before reading the error.
- B. Add a deployment secret to the read-only job.
- C. Disable enterprise Actions policy.
- D. Check the failing operation, token context, event restrictions, and required issue permission, then test the smallest justified change.

## Answer Key

<details>
<summary>Answers and explanations</summary>

| Question | Answer | Explanation | Source |
| --- | --- | --- | --- |
| 1 | B | Job-level permissions can match distinct tasks. Blanket writes, unrelated credentials, and owner roles exceed those tasks. | S1 |
| 2 | D | An explicit permission map sets unspecified permissions to none. Runner labels and organization roles do not fill them in. | S1 |
| 3 | A | `workflow_call` defines reusable-workflow invocation. Manual, scheduled, or pull request triggers alone do not provide that interface. | S2 |
| 4 | C | Actions are used within steps; reusable workflows are invoked as jobs. Neither syntax determines whether broad permissions are appropriate. | S1, S2 |
| 5 | B, D | Secrets require deliberate interface/passing review. Supported inheritance is explicit and can overexpose; labels do not supply secret authorization. | S2 |
| 6 | B | A called workflow cannot elevate the caller's token permission ceiling. Names and secret inputs are not elevation mechanisms. | S2 |
| 7 | A | Enterprise restrictions constrain lower-level settings. Policy names, permissiveness, and author preference do not reverse inheritance. | S3 |
| 8 | D | A full SHA fixes the selected reference. It does not prove safety, replace approval, or remove credential risk. | S4 |
| 9 | C | Untrusted code in a privileged trigger context can abuse credentials. Checkout does not establish trust or guarantee network isolation. | S4, S5 |
| 10 | B | Default fork restrictions withhold secrets and limit token writes. Non-default settings need separate review; approval is not blanket secret access. | S5 |
| 11 | A | Redaction is not a universal confidentiality boundary. Logs, artifacts, and titles are all inappropriate places for credential values. | S4, S6 |
| 12 | C, D | OIDC requires appropriate token-request permission and narrow cloud trust. Broad trust and stored long-lived passwords undermine the design. | S7 |
| 13 | C | Environment protection can gate jobs and environment-secret access. File names, broad secrets, and CPU size do not enforce review. | S8 |
| 14 | B | Publishing releases uses contents write permission. Issue read or OIDC token issuance does not substitute; unrelated writes are unnecessary. | S1 |
| 15 | D | Diagnose the actual permission/event boundary and test narrowly. Blanket writes, secrets, and policy removal conceal or broaden the problem. | S1, S5 |

</details>

## Sources

Check the [official GH-100 outline](https://learn.microsoft.com/en-us/credentials/certifications/resources/study-guides/gh-100) and current Actions policy/feature support.

- **S1:** [Workflow syntax and permissions](https://docs.github.com/en/actions/reference/workflows-and-actions/workflow-syntax).
- **S2:** [Reusing workflows](https://docs.github.com/en/actions/sharing-automations/reusing-workflows).
- **S3:** [Enterprise Actions policies](https://docs.github.com/en/enterprise-cloud@latest/admin/enforcing-policies/enforcing-policies-for-your-enterprise/enforcing-policies-for-github-actions-in-your-enterprise).
- **S4:** [Secure use of Actions](https://docs.github.com/en/actions/reference/security/secure-use).
- **S5:** [Workflow events](https://docs.github.com/en/actions/reference/workflows-and-actions/events-that-trigger-workflows).
- **S6:** [Using secrets](https://docs.github.com/en/actions/security-for-github-actions/security-guides/using-secrets-in-github-actions).
- **S7:** [OpenID Connect](https://docs.github.com/en/actions/security-for-github-actions/security-hardening-your-deployments/about-security-hardening-with-openid-connect).
- **S8:** [Deployment environments](https://docs.github.com/en/actions/deployment/targeting-different-environments/using-environments-for-deployment).