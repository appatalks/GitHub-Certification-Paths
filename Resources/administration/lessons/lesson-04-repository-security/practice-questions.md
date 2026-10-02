# Lesson 4: Supplementary Practice Questions

[Return to the lesson](lesson-guide.md) | [All lessons](../README.md)

These 15 original GH-100-style questions cover repository security, response,
tokens, and integrations. They are not official or recalled exam items and do
not predict exam content or scores. All scenarios are fictional Cloud paper
exercises. Never plant credentials or introduce vulnerable code for practice.
Choose the stated number of answers before opening the answer key.

## Questions

### 1. Vulnerability Alerts

**Choose one.** Which capability warns about known vulnerabilities affecting dependencies identified for a repository?

- A. An organization audit search alone.
- B. A runner-group restriction.
- C. Dependabot alerts.
- D. A pull request title convention.

### 2. Two Dependabot Update Types

**Choose one.** Which statement distinguishes Dependabot security updates from version updates?

- A. Security updates address known vulnerable dependencies; version updates help keep dependencies current under configured update rules.
- B. Version updates only rotate leaked credentials.
- C. Security updates always upgrade every dependency to its newest release, regardless of vulnerability.
- D. Both features replace testing and code review.

### 3. A Proposed Fix

**Choose one.** An alert has an associated dependency-update pull request. What is still needed before claiming the vulnerability is remediated in the affected branch?

- A. Assume opening the pull request deployed the fix.
- B. Remove the alert without checking the dependency state.
- C. Count the repository's open issues.
- D. Review/test the change and verify the affected dependency state after the approved update is applied.

### 4. Exposed Credential

**Choose two.** A hypothetical live credential is found in history. Which actions address containment and verification?

- A. Delete the current file and declare the credential invalid.
- B. Coordinate authorized revocation/rotation at the credential issuer.
- C. Update approved dependents and verify the old credential no longer authenticates.
- D. Publish the value so other developers recognize it.

### 5. Push Protection

**Choose one.** What is a sound expectation of secret-scanning push protection where supported and enabled?

- A. It revokes all credentials at their external issuers.
- B. It guarantees no sensitive data can ever enter the repository.
- C. It can block pushes containing supported detected secrets; it does not replace response to existing exposures.
- D. It makes repository authorization unnecessary.

### 6. CodeQL's Role

**Choose one.** Which description best fits CodeQL code scanning?

- A. A billing report for runner utilization.
- B. Analysis of code to identify potential security issues in supported languages/configurations.
- C. A universal runtime firewall for every application.
- D. An IdP account-provisioning service.

### 7. Code-Scanning Triage

**Choose one.** An alert suggests untrusted input reaches a database query. Which next investigation best supports a response decision?

- A. Examine the reported data flow, sanitization, reachability, and affected code context.
- B. Assume the alert proves data was stolen.
- C. Dismiss it because a pull request has an approval.
- D. Grant the scanner organization ownership.

### 8. GitHub App Design

**Choose two.** Which properties can support a least-privilege GitHub App integration?

- A. Installation access limited to selected repositories where appropriate.
- B. Automatic organization ownership for every installation.
- C. An assumption that app branding proves safe code.
- D. Task-appropriate permissions and short-lived installation access tokens.

### 9. Fine-Grained PAT Proposal

**Choose one.** A supported API task only reads issues in one repository. Which proposed credential scope best fits that need, subject to approval and API support?

- A. A classic PAT with every available scope and no expiry.
- B. Organization ownership for the automation account.
- C. A fine-grained PAT limited to the intended resource owner/repository, required read permission, and an appropriate expiry.
- D. A signing credential intended for production deployments.

### 10. Underlying User Access

**Choose one.** A PAT has a permission relevant to an endpoint, but its owner lacks access to the private repository. Which statement is correct?

- A. Token permissions create repository membership automatically.
- B. Token permissions do not independently grant the owner's missing underlying repository access.
- C. Renaming the token grants the missing access.
- D. Every expired token becomes an organization-owner credential.

### 11. App Model Matters

**Choose one.** A vendor requests access, but you do not know whether it uses a GitHub App or OAuth App. What should precede approval?

- A. Approve because the two models have identical authorization behavior.
- B. Give it a broad PAT without determining the model.
- C. Assume every OAuth App supports GitHub App installation-token scoping.
- D. Identify the model, requested permissions/scopes, repositories, and applicable organization policy.

### 12. Coordinating a Vulnerability

**Choose one.** Maintainers need to coordinate a sensitive vulnerability fix before public disclosure. Which repository feature should they evaluate?

- A. A repository security advisory and its supported private collaboration process.
- B. A public issue containing an unreviewed exploit and production secrets.
- C. Organization base write permissions for all users.
- D. Deleting the dependency graph.

### 13. Dependabot Registry Credentials

**Choose one.** Dependabot must access an approved private package registry for updates. Which configuration should be investigated?

- A. Printing the registry password in a pull request comment.
- B. Assuming all Actions secrets are automatically available to Dependabot update operations.
- C. Dependabot's encrypted secrets and private-registry configuration, with narrow access.
- D. Replacing the registry password with the repository's description.

### 14. Response Records

**Choose two.** Which fields make a security-response record useful for follow-up and closure?

- A. A copied live secret so reviewers can recognize it.
- B. The affected resource, confirmed facts, owner, containment action, and unresolved questions.
- C. Verification evidence and a documented closure or dismissal reason.
- D. A severity label with no investigation or action history.

### 15. Configuring Code Scanning

**Choose one.** A repository owner wants to enable CodeQL. What should be checked before promising a working configuration?

- A. Only the number of repository stars.
- B. That SAML automatically analyzes application code.
- C. That every language is supported by every setup mode.
- D. Feature entitlement, supported languages/build needs, and the requirements of the selected setup mode.

## Answer Key

<details>
<summary>Answers and explanations</summary>

| Question | Answer | Explanation | Source |
| --- | --- | --- | --- |
| 1 | C | Dependabot alerts identify known vulnerable dependencies. Audit searches, runner restrictions, and naming conventions do not provide that alerting function. | S1 |
| 2 | A | Security updates remediate known vulnerabilities; version updates follow configured maintenance rules. Neither eliminates review/testing or rotates credentials. | S2, S3 |
| 3 | D | A proposed update is not an applied, verified fix. Check review/test results and actual dependency state rather than deleting evidence. | S1, S2 |
| 4 | B, C | Issuer-side invalidation and dependent-service verification address credential validity. File deletion alone and publication do not contain exposure. | S4 |
| 5 | C | Push protection detects supported secret patterns at push time. It is neither universal detection nor issuer-side revocation. | S5 |
| 6 | B | CodeQL performs code security analysis within supported configurations. It is not billing, runtime firewalling, or identity provisioning. | S6 |
| 7 | A | Code context and data flow inform exploitability and remediation. The alert does not itself prove exploitation, and unrelated approvals do not resolve it. | S6 |
| 8 | A, D | Repository selection and scoped installation permissions/tokens reduce access. Ownership and branding are not substitutes for review. | S7 |
| 9 | C | Selected resources, limited permissions, and expiry fit the task where supported. Broad scopes and unrelated credentials overgrant or serve another purpose. | S8 |
| 10 | B | A token acts within its owner's access and applicable restrictions. A token permission, name, or expiry does not create missing membership. | S8 |
| 11 | D | GitHub Apps and OAuth Apps differ in authorization. Approval needs the actual model and requested access, not assumptions or a broad replacement token. | S7 |
| 12 | A | Security advisories support coordinated handling and private collaboration. Broad write grants and public sensitive material are not that process. | S9 |
| 13 | C | Dependabot has its own secret/configuration mechanism. Actions secrets are not automatically a replacement; plaintext disclosure is unsafe. | S10 |
| 14 | B, C | Facts, ownership, actions, and verification enable accountable closure. Credential values and unsupported labels do not. | S1, S4, S6 |
| 15 | D | Entitlement, language/build support, and setup requirements affect availability and operation. Popularity and authentication do not establish scanning support. | S6 |

</details>

## Sources

Check the [official GH-100 outline](https://learn.microsoft.com/en-us/credentials/certifications/resources/study-guides/gh-100) and current plan-specific security features.

- **S1:** [Dependabot alerts](https://docs.github.com/en/code-security/dependabot/dependabot-alerts/about-dependabot-alerts).
- **S2:** [Dependabot security updates](https://docs.github.com/en/code-security/dependabot/dependabot-security-updates/about-dependabot-security-updates).
- **S3:** [Dependabot version updates](https://docs.github.com/en/code-security/dependabot/dependabot-version-updates/about-dependabot-version-updates).
- **S4:** [Secret-scanning alerts](https://docs.github.com/en/code-security/secret-scanning/managing-alerts-from-secret-scanning).
- **S5:** [Push protection](https://docs.github.com/en/code-security/secret-scanning/introduction/about-push-protection).
- **S6:** [Code scanning](https://docs.github.com/en/code-security/code-scanning/introduction-to-code-scanning/about-code-scanning).
- **S7:** [GitHub Apps and OAuth Apps](https://docs.github.com/en/apps/oauth-apps/building-oauth-apps/differences-between-github-apps-and-oauth-apps).
- **S8:** [Personal access tokens](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/managing-your-personal-access-tokens).
- **S9:** [Repository security advisories](https://docs.github.com/en/code-security/security-advisories/working-with-repository-security-advisories/about-repository-security-advisories).
- **S10:** [Dependabot encrypted secrets](https://docs.github.com/en/code-security/dependabot/working-with-dependabot/managing-encrypted-secrets-for-dependabot).