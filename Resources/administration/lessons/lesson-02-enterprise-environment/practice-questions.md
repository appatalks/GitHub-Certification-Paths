# Lesson 2: Supplementary Practice Questions

[Return to the lesson](lesson-guide.md) | [All lessons](../README.md)

These 15 original GH-100-style questions cover enterprise environments,
licensing, and support. They are not official or recalled exam items and do
not predict exam content or scores. Scenarios are fictional; no changes are
authorized. GHES appears only as a deployment comparison, not a hands-on lab.
Choose the stated number of answers before opening the answer key.

## Questions

### 1. Public Collaboration Requirements

**Choose one.** Employees must use the same accounts for work and contributions to unrelated public projects. Which Cloud account model should be evaluated first?

- A. EMU, assuming unrestricted collaboration outside the enterprise.
- B. GHEC with personal accounts, alongside company access controls.
- C. A runner group instead of an account model.
- D. A data residency setting instead of account ownership requirements.

### 2. Data Residency

**Choose one.** Legal requires specified data categories to reside in a specified region. What must precede a compliance claim?

- A. Select any region mentioned in a product announcement.
- B. Make repositories private and treat location as resolved.
- C. Enable 2FA and treat location as resolved.
- D. Compare the precise legal scope with current residency capabilities, regions, exclusions, and account-model requirements.

### 3. Hosting Responsibility

**Choose one.** Which deployment involves the customer operating a GitHub Enterprise Server instance rather than GitHub operating the Cloud service?

- A. GHES.
- B. GHEC with personal accounts.
- C. GHEC with EMU.
- D. GHEC with data residency.

### 4. Managed-Account Tradeoffs

**Choose two.** Before recommending EMU, which requirements warrant explicit compatibility review?

- A. Whether the company likes the repository names.
- B. How accounts will be provisioned and maintained through a supported IdP.
- C. Whether required external collaboration fits managed-account restrictions.
- D. Whether the default branch is named `main`.

### 5. Local Access Issue

**Choose one.** One user cannot access one repository. Other authorized users can. The user's team lacks the required grant. What is the most appropriate first response?

- A. Open a service-outage incident without investigating authorization.
- B. Purchase additional Actions minutes.
- C. Verify the intended access and correct the authorized local grant, then retest.
- D. Change the enterprise account model.

### 6. Support Ticket Quality

**Choose one.** Which ticket gives Support the most useful safe starting evidence?

- A. Sanitized symptom, expected/actual result, timestamp, affected scope, reproduction steps, and checks already made.
- B. Only "GitHub does not work."
- C. A PAT value and no description of the request.
- D. A conclusion of global outage based on a single error.

### 7. Diagnostic Boundaries

**Choose one.** A GHES troubleshooting article requests a server support bundle, but your environment is GHEC. What should you do?

- A. Assume GHEC gives you shell access to its underlying server.
- B. Install GHES in production just to generate the bundle.
- C. Send unrelated local workstation files as the server bundle.
- D. Identify appropriate Cloud diagnostics and clarify the environment with Support rather than applying server-only steps.

### 8. Exact Billing Estimate

**Choose two.** Which inputs are necessary to support an estimate rather than guessing from headcount?

- A. Relevant subscription/agreement, license assignments, and billing rules.
- B. Product consumption, applicable rates/allowances, and the measurement period.
- C. The number of repository stars alone.
- D. The number of open issues alone.

### 9. Assigned and Purchased

**Choose one.** A report lists 500 available seats and 430 assigned. Which statement is justified by those fields alone?

- A. Exactly 70 employees should be removed.
- B. All 430 assigned users were active this month.
- C. There are 70 unassigned seats in this snapshot; activity and billing implications need separate evidence.
- D. Metered Actions consumption is zero.

### 10. Metered Products

**Choose one.** An enterprise has paid user licenses and sees additional product-usage charges. What is the best interpretation?

- A. A paid user license guarantees every metered product is unlimited.
- B. License assignment and product consumption are separate inputs governed by the applicable billing model.
- C. Product usage proves duplicate user accounts exist.
- D. Removing a repository collaborator always erases historical consumption charges.

### 11. Enterprise Structure

**Choose one.** Why might a company use multiple organizations within a Cloud enterprise?

- A. To separate administration/collaboration boundaries while applying relevant enterprise-wide policies.
- B. To ensure organization settings override every enterprise restriction.
- C. To make every organization member an enterprise owner.
- D. To avoid all licensing and billing obligations.

### 12. Development Standards

**Choose one.** A company wants consistent reviews and releases. Which recommendation is most actionable?

- A. Ask each repository to infer what "high quality" means.
- B. Require organization ownership for every author.
- C. Use repository visibility as the only release control.
- D. Define branching, review, check, release, and exception standards, then map them to supported controls.

### 13. Unresolved Authentication

**Choose one.** Users have personal GitHub accounts. Does that alone establish whether organization SAML SSO is enabled?

- A. Yes; personal accounts cannot use organization SAML.
- B. Yes; personal accounts always require organization SAML.
- C. No; account ownership and configured authentication requirements must be checked separately.
- D. No; only the Actions runner operating system can establish SAML status.

### 14. Escalation Without Secrets

**Choose two.** Which practices fit a safe support escalation?

- A. Include live credentials to speed up reproduction.
- B. Minimize/sanitize identifying data and share necessary diagnostics through approved support channels.
- C. Publish all internal logs in a public issue before triage.
- D. State unresolved facts and the checks that distinguish a local configuration issue from a service issue.

### 15. Conditional Architecture

**Choose one.** A proposed Cloud account model meets lifecycle needs, but vendor collaboration requirements remain unknown. What is the strongest recommendation?

- A. Recommend conditionally, naming the missing requirement and what finding would change the choice.
- B. Declare suitability for every vendor collaboration pattern.
- C. Convert the sandbox immediately to prove suitability.
- D. Ignore collaboration because lifecycle control is the only exam objective.

## Answer Key

<details>
<summary>Answers and explanations</summary>

| Question | Answer | Explanation | Source |
| --- | --- | --- | --- |
| 1 | B | Personal accounts fit this combined work/public-identity requirement. Managed accounts have external-collaboration restrictions; runner and residency settings are not account models. | S1, S2 |
| 2 | D | Compliance depends on precise requirements and documented capabilities. Privacy and authentication controls do not establish data location. | S1, S3 |
| 3 | A | GHES is customer-operated. The listed GHEC variants remain Cloud service deployments. | S4 |
| 4 | B, C | IdP lifecycle support and external collaboration are account-model constraints. Naming preferences do not resolve either. | S1, S2 |
| 5 | C | The supplied evidence points to a local grant gap. Correct only approved access and retest; billing, outage declarations, and migration do not address that gap. | S5 |
| 6 | A | Reproducible symptoms and prior checks support triage. Vague reports, credentials, and unsupported diagnoses do not. | S6 |
| 7 | D | Server-only diagnostics do not imply access to Cloud infrastructure. Clarify product-specific evidence instead of manufacturing a bundle. | S4, S6 |
| 8 | A, B | Agreements, assignments, usage, rates, and periods inform cost. Stars and issue counts are not sufficient billing inputs. | S7 |
| 9 | C | The difference is 70 seats. Neither activity, billing treatment, nor metered usage follows from this subtraction alone. | S7 |
| 10 | B | Entitlements and metered consumption require their actual product rules. Universal unlimited-use or automatic charge-erasure claims are unsupported. | S7 |
| 11 | A | Organizations provide boundaries within an enterprise. They do not automatically relax inherited policy, confer ownership, or eliminate costs. | S4 |
| 12 | D | Explicit process standards can be implemented and tested. Vague goals, broad ownership, and visibility alone do not specify review/release behavior. | S8 |
| 13 | C | Personal accounts can coexist with organization SAML requirements. Inspect approved settings rather than inferring them from account ownership. | S9 |
| 14 | B, D | Safe evidence and clearly stated unknowns support escalation. Public logs and live credentials create avoidable exposure. | S6 |
| 15 | A | A conditional decision exposes the unresolved constraint. An immediate conversion or universal suitability claim hides it. | S1, S2 |

</details>

## Sources

Check the [official GH-100 outline](https://learn.microsoft.com/en-us/credentials/certifications/resources/study-guides/gh-100) for full coverage; this is not a complete deployment/licensing syllabus.

- **S1:** [Choose a Cloud enterprise type](https://docs.github.com/en/enterprise-cloud@latest/admin/concepts/enterprise-fundamentals/choose-an-enterprise-type).
- **S2:** [Enterprise Managed Users](https://docs.github.com/en/enterprise-cloud@latest/admin/managing-iam/understanding-iam-for-enterprises/about-enterprise-managed-users).
- **S3:** [Data residency](https://docs.github.com/en/enterprise-cloud@latest/admin/data-residency/about-github-enterprise-cloud-with-data-residency).
- **S4:** [GitHub Enterprise overview](https://docs.github.com/en/enterprise-cloud@latest/admin/overview/about-github-for-enterprises).
- **S5:** [Organization roles](https://docs.github.com/en/enterprise-cloud@latest/organizations/managing-peoples-access-to-your-organization-with-roles/roles-in-an-organization).
- **S6:** [Creating a support ticket](https://docs.github.com/en/support/contacting-github-support/creating-a-support-ticket).
- **S7:** [Billing documentation](https://docs.github.com/en/billing).
- **S8:** [Rulesets](https://docs.github.com/en/enterprise-cloud@latest/repositories/configuring-branches-and-merges-in-your-repository/managing-rulesets/about-rulesets).
- **S9:** [SAML SSO](https://docs.github.com/en/enterprise-cloud@latest/authentication/authenticating-with-saml-single-sign-on/about-authentication-with-saml-single-sign-on).