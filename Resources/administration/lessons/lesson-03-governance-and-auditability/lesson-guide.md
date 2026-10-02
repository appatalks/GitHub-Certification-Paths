# Lesson 3: Governance and Auditability

**Exam domain:** Implement secure software development and compliance (25-30%)

## Goals

- Turn a team's request into rules about how code can change.
- Explain where each rule belongs and who can make an exception.
- Plan tests that show a rule allows good changes and blocks unwanted changes.

## Words to Know

| Word | Plain-language meaning |
| --- | --- |
| Branch | A line of work in a repository; `main` is the default branch in this exercise. |
| Pull request | A proposal to merge changes into another branch. |
| Required check | An automated result that must meet the rule's requirements before a change is accepted. |
| Tag | A name pointing to a version of the code, often used to mark releases. |
| Ruleset | A collection of rules controlling specified branches or tags. |
| Scope | Where a rule applies: for example, one repository or selected repositories in an organization. |
| Bypass | A permitted exception to normal enforcement for specified actors. |
| Audit log | A record of administrative activity; it is not a record of every possible user action. |

## Your Starting Scenario

In `northstar-apps/web`, developers submit pull requests to `main`. Morgan owns
the organization; Avery contributes code; Riley approves releases. No active
ruleset is recorded in the supplied inventory. Whether other controls exist is unknown.

| Requirement | Requested behavior |
| --- | --- |
| Changes to `main` | Use a pull request, require one approval, and require the `test` check to succeed. |
| Release tags | Only the approved release process should create tags matching `v*`. |
| Emergency fixes | Record an authorized, narrowly scoped exception and review it afterward. |

These are requested controls, not proof that they are already working.

## Investigate

- Read [About rulesets](https://docs.github.com/en/enterprise-cloud@latest/repositories/configuring-branches-and-merges-in-your-repository/managing-rulesets/about-rulesets). How do rulesets compare with branch protection, and how can rules layer?
- Read [Creating rulesets for repositories in your organization](https://docs.github.com/en/enterprise-cloud@latest/organizations/managing-organization-settings/creating-rulesets-for-repositories-in-your-organization). Which scopes and bypass options are available?
- Read [Reviewing audit logs for your enterprise](https://docs.github.com/en/enterprise-cloud@latest/admin/monitoring-activity-in-your-enterprise/reviewing-audit-logs-for-your-enterprise). What can audit records establish, and what would you still need to verify?

## Work Through the Problem

### Start with Your Sandbox

1. Complete [organization setup](../sandbox-setup.md). Choose an owner-approved disposable repository and record its alias and default branch.
2. Open the repository's **Settings** and inspect **Rules** / **Rulesets** where available. Record existing and inherited controls before creating anything.
3. Use the ruleset documentation to compare the actual controls with the fictional requirements below. Missing visibility does not prove no protection exists.
4. If the owner approves a live test, record a restoration plan and apply only the selected rule to the disposable target using the linked documentation. Use dummy pull requests or tags for Step 3's tests; do not alter the organization's shared protections.
5. Restore the starting state and record observed results separately from the paper design. If the plan or permissions do not support a rule, complete the paper exercise instead.

### Step 1: Write the Rules in Ordinary Language

1. Copy the requirement table into your notes.
2. Split the first row into three rules: use a pull request, require approval, and require a successful check.
3. Beside each rule, write one unwanted action it should prevent. Example format: "Without this rule, someone could ...".
4. Name the branch or tag pattern each rule targets. Keep `main` and `v*` separate.

**Save:** A requirement-to-risk list.

### Step 2: Choose Documented Controls

1. Open the ruleset documentation above and find branch and tag rules.
2. Make a table with columns: requirement, target, proposed rule, scope, owner, and source.
3. Fill each row using a documented rule. Check availability for the intended Cloud plan and repository visibility.
4. For release tags, investigate how creation restrictions and permitted actors can satisfy the request. Do not assume a branch rule also protects tags.
5. Record the current controls you would inspect before adding another ruleset, including inherited rules and branch protection.

**Save:** A proposed control map, not a claim that settings have been applied.

### Checkpoint 1: A Narrow Exception

**Objective focus:** Policies and rulesets. **Choose one answer.**

An urgent fix needs an exception to normal review. Which proposal best preserves the lesson's governance requirements?

- A. Give every developer permanent bypass access for future emergencies.
- B. Disable all rules until someone remembers to restore them.
- C. Treat the word "urgent" as sufficient approval to bypass any control.
- D. Use a documented, narrowly scoped exception with an approver, evidence, and an explicit restoration check.

<details>
<summary>Check your answer</summary>

**Answer: D.** An exception should have a controlled boundary and an accountable review trail. A broadens standing access; B leaves restoration uncertain; C substitutes a label for authorization. Verify the available bypass behavior using [rulesets](https://docs.github.com/en/enterprise-cloud@latest/repositories/configuring-branches-and-merges-in-your-repository/managing-rulesets/about-rulesets).

</details>

### Step 3: Plan the Tests

1. Create a table with columns: attempted action, actor, expected result, evidence to collect, and actual result.
2. Add a pull request with approval and a passing `test` check.
3. Add a pull request missing the check, one missing approval, a direct push to `main`, and a release-tag attempt by an unauthorized actor.
4. Predict allowed or blocked behavior from your proposed rules. Explain each prediction.
5. Leave actual result as "not run" unless you have an authorized disposable Cloud sandbox. In a sandbox, first record its plan, permissions, starting controls, reset method, and cleanup; then record observations separately from predictions.

**Save:** The test table. A settings screenshot alone does not prove a test passed.

### Checkpoint 2: Evidence of Enforcement

**Objective focus:** Verifying security controls. **Choose one answer.**

You have a screenshot showing that a rule requires one approval. What additional evidence most directly tests its enforcement?

- A. A signed statement that the rule's name sounds correct.
- B. Approved sandbox tests showing the expected rejection without approval and expected allowed behavior when requirements are satisfied.
- C. An audit entry proving only that someone opened Settings.
- D. A successful merge performed by an unrestricted bypass actor, with no other test.

<details>
<summary>Check your answer</summary>

**Answer: B.** Allowed and denied cases test behavior, with actor, scope, and applicable controls recorded. A is an opinion; C does not test merging; D may demonstrate bypass rather than normal enforcement. Review [rulesets](https://docs.github.com/en/enterprise-cloud@latest/repositories/configuring-branches-and-merges-in-your-repository/managing-rulesets/about-rulesets) and your Step 3 test table. Label unperformed tests as predictions.

</details>

### Step 4: Design the Emergency Process

1. Riley asks to skip a review for an urgent fix. Write what fact would justify urgency and who can approve an exception.
2. Look up ruleset bypass options. Propose the smallest permitted exception instead of disabling all rules.
3. Record the approval, action, owner, reason, verification, and follow-up review you would retain.
4. Read the audit documentation and identify what administrative events could support the record. List other evidence you would need, such as the pull request and check results.
5. Describe how to end any temporary exception and check that normal protection works again.

**Save:** An exception checklist and one risk your design still needs to address.

### Checkpoint 3: An Audit Entry Is Not Approval

**Objective focus:** Audit logging and reporting. **Choose one answer.**

An audit record says Morgan changed a review requirement. What does that fact alone establish?

- A. The recorded change occurred; its authorization and the effective resulting controls still need investigation.
- B. Security approved the change because GitHub recorded it.
- C. Every repository is now unprotected, regardless of scope or inherited rules.
- D. The actor's intent was malicious.

<details>
<summary>Check your answer</summary>

**Answer: A.** An audit event supports the recorded action, not the approval, intent, or every resulting access condition. B treats logging as authorization; C ignores scope and inherited controls; D infers intent. Review [organization audit logs](https://docs.github.com/en/enterprise-cloud@latest/organizations/keeping-your-organization-secure/managing-security-settings-for-your-organization/reviewing-the-audit-log-for-your-organization).

</details>

## You Are Finished When

- [ ] Every requirement maps to a target, documented control, and owner.
- [ ] Tests include both allowed and blocked actions.
- [ ] Expected results and observed results are labelled separately.
- [ ] Your exception process includes approval, evidence, and a return to normal protection.

Use an isolated repository only if you can confirm feature availability, reset, and cleanup. Otherwise, document the configuration and expected test results without changing a live repository.

## Supplementary Practice

Use the [15-question practice set and answer key](practice-questions.md) for additional exam-style retrieval practice.

## Teach It Back

Walk your tutor through the requirement-to-control map. Explain why each control belongs at its chosen scope and how your tests would distinguish configuration from enforcement. Keep a list of assumptions you could not verify.

## Carry Forward

Save the control map and test cases. Lesson 4 will use the same evidence-first approach to investigate security findings and integration requests.