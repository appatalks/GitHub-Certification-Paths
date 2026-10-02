# Lesson 1: GitHub Model, Identity, and Access

**Exam domains:** Manage GitHub identities and access (15-20%); administer GitHub Enterprise environment (10-15%)

## Goals

- Draw where people, teams, and repositories belong in a company using GitHub.
- Explain how someone gets an account, signs in, and receives permission to work.
- Give each person only the access their job needs.
- Show how you would check that access was added or removed correctly.

## Words to Know

| Word | Plain-language meaning |
| --- | --- |
| Enterprise | The account that groups organizations and sets shared company policies. |
| Organization | A shared GitHub space that owns repositories and contains members and teams. |
| Repository | A place for a project's files, history, issues, and pull requests. |
| Team | A group of organization members that can receive repository access together. |
| Identity provider (IdP) | The company's system for identifying people and managing their sign-in. It is the identity source in these examples. |
| Authentication | Checking who is signing in. |
| Authorization | Deciding what that signed-in person may do. |
| SAML single sign-on (SSO) | A way for GitHub to rely on a company's IdP when checking identity for access. It is not a repository permission. |
| Two-factor authentication (2FA) | Checking a second factor as well as a password or other first factor. GitHub and IdP requirements depend on the account model. |
| Provisioning | Creating, updating, or disabling an account. |
| SCIM | A protocol an IdP can use to manage account lifecycle; here, investigate it for Enterprise Managed Users. |
| Team synchronization | Connecting an IdP group with GitHub team membership in supported configurations. This does not itself decide the team's repository role. |
| Least privilege | Giving only the permissions needed for the work, not the highest role available. |
| Evidence | Something you can inspect to check a claim, such as membership records, settings, or an access test. |

## Your Starting Scenario

Start with your real sandbox inventory from [organization setup](../sandbox-setup.md).
Its published alias is `training-org`, and its account model is personal
GitHub accounts. SAML SSO, team synchronization, enterprise ownership, and
specific permissions still need confirmation; do not assume they are enabled.

The Northstar tables below are a separate paper example if your approved
resources do not support a task. They do not describe your real organization.
In that example, Priya owns the enterprise, Morgan owns both organizations,
Builders belongs to `northstar-apps`, and Operators belongs to `northstar-ops`.
Do not assume a team spans both organizations.

| Repository | Organization | Work to support |
| --- | --- | --- |
| `web` | `northstar-apps` | Developers propose changes through pull requests. |
| `docs` | `northstar-apps` | A contractor proposes documentation changes. |
| `deploy` | `northstar-ops` | Operators maintain deployment configuration. |

| Person | Situation |
| --- | --- |
| Avery | New developer who needs to contribute to `web`. |
| Blake | Developer moving from Builders to Operators; no continuing need for `web`. |
| Casey | Contractor who needs to contribute to `docs` for two weeks only. |
| Drew | Departing employee who must no longer access any Northstar private repository. |

In the paper example, treat all repositories as private. In your sandbox,
record actual visibility, base permissions, and direct grants using aliases.
Mark unavailable settings unknown. Do not use a live IdP for either activity.

## Investigate

Use the official documentation to answer the questions below. Keep a source link beside each conclusion and note anything that depends on account type or configuration.

- Read [About GitHub for enterprises](https://docs.github.com/en/enterprise-cloud@latest/admin/overview/about-github-for-enterprises). What objects and administrative boundaries does it describe?
- Read [Roles in an organization](https://docs.github.com/en/enterprise-cloud@latest/organizations/managing-peoples-access-to-your-organization-with-roles/roles-in-an-organization). Which roles grant access at the organization, team, or repository level?
- Compare [authentication to GitHub](https://docs.github.com/en/enterprise-cloud@latest/authentication/keeping-your-account-and-data-secure/about-authentication-to-github), [SCIM provisioning for Enterprise Managed Users](https://docs.github.com/en/enterprise-cloud@latest/admin/managing-iam/provisioning-user-accounts-with-scim/configuring-scim-provisioning-for-users), and [team synchronization](https://docs.github.com/en/enterprise-cloud@latest/admin/managing-iam/using-saml-for-enterprise-iam/managing-team-synchronization-for-organizations-in-your-enterprise). What does each process change, and what does it not change?

## Work Through the Problem

### Step 1: Draw the Company Map

1. Open your sandbox organization from the private address map. Draw a box labelled `training-org`; record its owner as an alias, not a real handle.
2. Add an enterprise box only if an authorized owner confirms the relationship. Otherwise write "enterprise relationship not verified". Do not invent a second organization.
3. Open **Repositories** and **Teams** where permitted. Put your approved repository and team aliases inside `training-org`. Use the paper tables only if this observation is unavailable.
4. Open each selected team's repository-access view. Draw connections for observed roles and mark any proposed connection with a different label.
5. Use the roles documentation to explain what each role permits. Explain why contribution access differs from organization ownership; list additional access paths you cannot inspect.

**Save:** One labelled diagram. It should distinguish ownership of an organization from permission to contribute to a repository.

### Checkpoint 1: Team Boundaries

**Objective focus:** Organization roles and access. **Choose one answer.**

A developer needs to contribute to one repository. Which proposal best limits access to the stated work?

- A. Make the developer an organization owner so they can manage their own access.
- B. Give a team an appropriate role on that repository, add the developer, and inspect other access paths.
- C. Enable SAML SSO and assume repository permission is automatically granted.
- D. Give write access to every repository so the same policy applies everywhere.

<details>
<summary>Check your answer</summary>

**Answer: B.** A task-based team grant can limit the proposed access, but base permissions and other grants still need review. A and D grant more than the task requires. C checks identity, not the repository role. Review [organization roles](https://docs.github.com/en/enterprise-cloud@latest/organizations/managing-peoples-access-to-your-organization-with-roles/roles-in-an-organization).

</details>

### Step 2: Explain Avery's Access in Two Different Account Models

Both diagrams below are comparisons using a fictional Avery, not instructions
to reconfigure the sandbox. For your real organization, separately note which
personal-account authentication settings you could confirm. Ordinary personal
accounts do not imply SAML SSO is configured.

This means answering two separate questions: "How does Avery prove who they
are?" and "What allows Avery to change `web`?" Do not put every acronym in one
universal sign-in chain.

1. Create a page titled **Personal accounts with SAML SSO**. Draw four boxes: Avery's personal GitHub account, company IdP, GitHub organization, and `web`.
2. Read the authentication and team synchronization links above. Add labelled connections for identity verification, organization membership, team membership, and repository role. Mark team synchronization as optional and configuration-dependent.
3. Next to the GitHub account and IdP, write where you would check their separate 2FA requirements. Do not assume GitHub 2FA and IdP authentication are the same setting.
4. Create a second page titled **Enterprise Managed Users (EMU)**. Draw boxes for the company IdP, Avery's managed GitHub account, a team, and `web`.
5. Read the SCIM documentation. Label which connection creates or updates the managed account. Label IdP sign-in separately from provisioning.
6. Find the managed-user group/team guidance from the linked SCIM documentation or the GitHub admin documentation. Record what controls group membership and what still controls the team's repository permission. Do not reuse personal-account team synchronization rules without checking.
7. Under both diagrams, answer: "Would successful sign-in alone prove Avery can change `web`? What else must I inspect?" Cite the source for your answer.

**Save:** Two account-model diagrams and a short explanation of the difference. Write "not verified yet" wherever the documentation has not resolved a question.

### Checkpoint 2: Sign-In Is Not Access

**Objective focus:** Authentication versus authorization. **Choose one answer.**

Avery successfully completes company SSO but cannot open a private repository. What should you investigate next?

- A. Whether SCIM has assigned the repository's required check.
- B. Whether enabling a second factor would automatically grant write permission.
- C. Whether every organization member must be promoted to owner to use SSO.
- D. Whether Avery has the required organization/repository access and has met applicable SSO access requirements.

<details>
<summary>Check your answer</summary>

**Answer: D.** Successful authentication does not establish repository authorization, and the applicable SSO access conditions still matter. A confuses provisioning with code controls. B confuses authentication with permission. C proposes unnecessary ownership. Review [authentication to GitHub](https://docs.github.com/en/enterprise-cloud@latest/authentication/keeping-your-account-and-data-secure/about-authentication-to-github) and the role references above.

</details>

### Step 3: Plan the Access Changes

1. Create a table with columns: person, required work, proposed membership/role, access to remove, person responsible, and verification.
2. Add Avery, Blake, Casey, and Drew using the scenario table.
3. For Blake, check both the new access needed and old access that should end. Include direct grants and other team memberships as questions to inspect.
4. For Casey, record the task end date as a removal reminder, not an automatic expiry feature you assume exists. Compare the appropriate membership options in the docs for each account model.
5. For Drew, list every route you would inspect: organization membership, teams, direct repository access, and account-model-specific IdP/account lifecycle controls.
6. For each proposed change, describe an allowed action and an action that should be denied. State how you would test them safely with synthetic accounts in an authorized sandbox, or mark them as expected results if working on paper.

**Save:** The access-change table. Clearly label proposed settings and expected tests; a paper plan is not proof that access was actually removed.

### Optional Sandbox Practice: Observe a Temporary Team Grant

1. Ask the owner to approve an empty disposable repository, one test team, and an existing authorized training account. Confirm who will restore access. Do not invite a real contractor or remove an employee.
2. Record the repository's base permissions, the test account's direct grants, and existing team access before the exercise.
3. Follow the roles documentation to grant the test team the agreed repository role and add the approved training account. Record only aliases in shared notes.
4. Have the training account perform the agreed harmless action, such as a dummy pull request. Do not share its credentials or impersonate the account.
5. Remove only the temporary grant or membership you added. Repeat the agreed access check; if another route still grants access, record that instead of claiming total removal.
6. Restore the original state, check it with the owner, and label your results "observed in sandbox". Use expected paper results if permissions or training accounts are unavailable.

### Step 4: Research an Unclear Request

Morgan asks for "one contribution policy for the whole company."

1. Write three questions that clarify the request: which repositories, which people, and which action should be allowed or blocked?
2. Find a relevant enterprise or organization policy in GitHub Docs.
3. Record the documented scope, any plan requirement, and why it might meet the request. Explain what information is still missing before changing it.

### Checkpoint 3: Removing One Route

**Objective focus:** Auditing access. **Choose two answers.**

You remove an approved test account from a team, but it can still access the disposable private repository. Which two checks directly help explain the remaining access?

- A. Inspect direct repository grants and other team memberships.
- B. Assume team removal failed because all access must come through that team.
- C. Inspect organization base permissions and any higher role the account holds.
- D. Delete the repository to prove the user cannot access it anymore.

<details>
<summary>Check your answer</summary>

**Answers: A and C.** Access can arrive through more than one route. B assumes a single route without evidence; D destroys the resource rather than checking permission. Review [organization roles](https://docs.github.com/en/enterprise-cloud@latest/organizations/managing-peoples-access-to-your-organization-with-roles/roles-in-an-organization) and your Step 3 access table.

</details>

## You Are Finished When

- [ ] Your company map places each team and repository in the correct organization.
- [ ] Your two identity diagrams label sign-in, account creation, and repository permission separately.
- [ ] Every access-change row has an owner and a verification plan.
- [ ] You can explain SAML SSO, 2FA, SCIM, and team membership in ordinary language without treating them as interchangeable.
- [ ] You have source links for decisions and a visible list of unresolved questions.

## Supplementary Practice

Use the [15-question practice set and answer key](practice-questions.md) for additional exam-style retrieval practice.

## Teach It Back

Use your diagram and checklist to teach the end-to-end access lifecycle to your tutor. Explain authentication versus authorization, SAML SSO versus 2FA, and SCIM versus team synchronization. When you cannot support a claim with a source or evidence, mark it as an open question and look it up.

## Carry Forward

Keep your object map and lifecycle checklist. In Lesson 2, use them to reason about how enterprise account type changes identity ownership and administration.