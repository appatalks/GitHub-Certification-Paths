# Lesson 1: Supplementary Practice Questions

[Return to the lesson](lesson-guide.md) | [All lessons](../README.md)

These 15 original questions practice GH-100 identity and access objectives.
They are not official, recalled, or copied exam questions, and do not predict
exam content or scores. All scenarios are fictional and Cloud-focused.
Choose the stated number of answers and explain your reasoning before opening
the answer key. These are paper exercises, not instructions to change access.

## Questions

### 1. Successful Sign-In

**Choose one.** A user signs in successfully but cannot open a private repository. Which distinction best explains why more investigation is needed?

- A. Authentication and authorization are interchangeable.
- B. Authentication establishes identity; authorization determines permitted access.
- C. Successful authentication grants organization ownership.
- D. Private repositories require every contributor to be an enterprise owner.

### 2. Company-Controlled Accounts

**Choose one.** An enterprise requires its IdP to provision and control the lifecycle of employees' work accounts. Which model should it evaluate?

- A. Personal accounts with optional organization membership.
- B. Outside collaborators using personal accounts without federation.
- C. Enterprise Managed Users.
- D. Repository teams with no identity-provider integration.

### 3. SCIM's Purpose

**Choose one.** What is the primary role of SCIM in a supported identity integration?

- A. Automating identity provisioning and lifecycle changes.
- B. Enforcing pull request approval counts.
- C. Replacing all repository roles with administrator access.
- D. Encrypting Actions secret values inside a workflow file.

### 4. Personal Accounts with SAML

**Choose one.** A company uses personal GitHub accounts with organization SAML SSO. Which statement is accurate?

- A. The company owns and can delete each personal GitHub account through SAML.
- B. SAML automatically creates repository write grants for authenticated users.
- C. Personal accounts become managed accounts when a team is created.
- D. Organization SSO requirements and GitHub account ownership are distinct.

### 5. Remaining Access

**Choose two.** A developer loses one team membership but still accesses a repository. Which checks could identify another authorization path?

- A. Direct repository grants and other teams.
- B. The developer's preferred editor theme.
- C. Organization base permissions and higher organization roles.
- D. The repository's default branch name alone.

### 6. Base Permissions

**Choose one.** Organization base permissions grant members write access. A member's team has read access to a repository. What should the administrator expect from those grants alone?

- A. The base write grant still applies; team read access does not subtract it.
- B. Team read access always overrides and reduces the base grant.
- C. The two grants cancel, leaving no access.
- D. A repository must be public for base permissions to apply.

### 7. Broad Administration

**Choose one.** Which standard organization role is appropriate for someone authorized to manage organization-wide settings and membership, rather than just maintain a repository?

- A. Repository triage.
- B. Repository write.
- C. Organization owner.
- D. Outside collaborator with read access.

### 8. Narrow Contractor Access

**Choose one.** In a personal-account organization, a contractor needs write access to one repository and no organization-wide role. Which approach best matches that requirement, subject to policy?

- A. Enterprise ownership.
- B. Outside-collaborator access to the specified repository.
- C. Organization ownership.
- D. Organization-wide base write permissions for all members.

### 9. Authentication Controls

**Choose two.** Which statements distinguish SAML SSO and two-factor authentication correctly?

- A. SAML federation can require a company identity-provider authentication flow for organization access.
- B. Enabling 2FA alone assigns repository write roles.
- C. A team synchronization mapping is itself a second authentication factor.
- D. 2FA adds another factor to account authentication; it is not a repository permission grant.

### 10. Team Synchronization

**Choose one.** A personal-account organization wants membership of a supported GitHub team to follow a connected IdP group. Which capability should it investigate?

- A. Required status checks.
- B. Repository secret scanning.
- C. Team synchronization, with its supported IdP and plan prerequisites.
- D. An Actions runner label.

### 11. Offboarding Personal Accounts

**Choose one.** An employee's IdP identity is disabled, but their personal GitHub account remains an organization member. What is the most defensible next step?

- A. Assume the personal GitHub account was deleted.
- B. Review membership, grants, and SSO/session conditions, and perform authorized offboarding.
- C. Re-enable the IdP identity to avoid investigating GitHub access.
- D. Make the account an owner so its remaining grants are easier to find.

### 12. Proving Least Privilege

**Choose one.** What evidence best supports a proposed least-privilege access change?

- A. A screenshot of the user's profile only.
- B. A statement that the repository name looks sensitive.
- C. Successful sign-in, without testing repository authorization.
- D. Authorized allowed/denied checks, with the actor, grants, and resource scope recorded.

### 13. Choosing an IdP

**Choose two.** Which requirements should inform an identity-provider integration decision?

- A. Supported federation/provisioning features for the chosen account model.
- B. Whether repository names contain the company brand.
- C. Required account lifecycle, recovery, and authentication-policy behavior.
- D. Whether every developer uses the same terminal font.

### 14. Role Boundaries

**Choose one.** A user receives repository administrator access through a team. What should you infer?

- A. The user can administer that repository within applicable constraints, but the grant does not itself make them an organization owner.
- B. The user automatically becomes an enterprise owner.
- C. The user now administers every repository in every organization.
- D. The team grant disables inherited enterprise policy.

### 15. PAT Access with SSO

**Choose one.** A classic PAT has the needed scope, but a request to an organization protected by SAML SSO fails. Which additional check is relevant?

- A. Whether the token name matches the repository name.
- B. Whether the user has a public profile picture.
- C. Whether the token is appropriately authorized for the organization and permitted by its policies, and whether the user has access.
- D. Whether a runner is currently idle.

## Answer Key

<details>
<summary>Answers and explanations</summary>

| Question | Answer | Explanation | Source |
| --- | --- | --- | --- |
| 1 | B | Identity verification and resource permission are separate. A conflates them; C and D invent ownership requirements. | S1, S2 |
| 2 | C | EMU provides enterprise-managed work accounts through an IdP. Personal accounts and teams alone do not provide that account-ownership model. | S3 |
| 3 | A | SCIM supports provisioning/lifecycle operations, not code review, blanket authorization, or workflow encryption. Account-model specifics still matter. | S3, S4 |
| 4 | D | SAML controls an authentication requirement; it does not transfer personal-account ownership or automatically create repository grants. | S5 |
| 5 | A, C | Direct, team, base, and higher-role grants can coexist. Editor theme and branch names do not establish another grant. | S2 |
| 6 | A | A lower team role does not remove a higher base grant. Review all effective grants instead of assuming the narrower one wins. | S2 |
| 7 | C | Organization ownership covers broad organization administration. Repository roles and outside-collaborator access have narrower scope. | S2 |
| 8 | B | A repository-specific outside-collaborator grant can match this personal-account scenario. A, C, and D broaden unrelated access. | S6 |
| 9 | A, D | SAML federation and 2FA concern authentication. Neither team synchronization nor 2FA alone assigns repository authorization. | S1, S5 |
| 10 | C | Team synchronization connects supported IdP groups and teams. Required checks, scanners, and runner labels serve different purposes. | S7 |
| 11 | B | IdP disablement does not prove personal-account deletion or completed GitHub offboarding. Restoring identity or increasing privileges does not fix the review gap. | S5, S2 |
| 12 | D | Scoped behavioral checks test the intended boundary. Profiles, names, and sign-in alone do not prove repository least privilege. | S2 |
| 13 | A, C | Supported capabilities and lifecycle/security requirements determine suitability. Branding and display preferences do not. | S3, S5, S7 |
| 14 | A | Repository administration is not organization or enterprise ownership and cannot override applicable inherited policy. | S2 |
| 15 | C | Classic PAT scope alone is insufficient when SSO authorization, policy, or underlying user access prevents the request. Token labels and runner state are irrelevant. | S8 |

</details>

## Sources

Use the [official GH-100 outline](https://learn.microsoft.com/en-us/credentials/certifications/resources/study-guides/gh-100) to check current objectives. These questions do not cover every identity objective.

- **S1:** [Authentication to GitHub](https://docs.github.com/en/enterprise-cloud@latest/authentication/keeping-your-account-and-data-secure/about-authentication-to-github).
- **S2:** [Organization roles](https://docs.github.com/en/enterprise-cloud@latest/organizations/managing-peoples-access-to-your-organization-with-roles/roles-in-an-organization).
- **S3:** [Enterprise Managed Users](https://docs.github.com/en/enterprise-cloud@latest/admin/managing-iam/understanding-iam-for-enterprises/about-enterprise-managed-users).
- **S4:** [SCIM for organizations](https://docs.github.com/en/enterprise-cloud@latest/organizations/managing-saml-single-sign-on-for-your-organization/about-scim-for-organizations).
- **S5:** [SAML SSO](https://docs.github.com/en/enterprise-cloud@latest/authentication/authenticating-with-saml-single-sign-on/about-authentication-with-saml-single-sign-on).
- **S6:** [Outside collaborators](https://docs.github.com/en/organizations/managing-user-access-to-your-organizations-repositories/adding-outside-collaborators-to-repositories-in-your-organization).
- **S7:** [Team synchronization](https://docs.github.com/en/enterprise-cloud@latest/organizations/organizing-members-into-teams/synchronizing-a-team-with-an-identity-provider-group).
- **S8:** [Authorizing a PAT for SAML SSO](https://docs.github.com/en/enterprise-cloud@latest/authentication/authenticating-with-saml-single-sign-on/authorizing-a-personal-access-token-for-use-with-saml-single-sign-on).