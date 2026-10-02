# Lesson 8: Integrated Capstone and Exam Readiness

**Exam domains:** All GH-100 domains

## Goals

- Use the earlier lessons to investigate a release-day problem.
- Explain what you know, what you still need to check, and what you would do next.
- Present your recommendations and identify what you need to study further.

## Words to Know

| Word | Plain-language meaning |
| --- | --- |
| Capstone | A final exercise combining skills from earlier lessons. |
| Incident | A problem that may need investigation and a controlled response. |
| Priority | The order in which you address problems, based on impact and urgency. |
| Stakeholder briefing | A short explanation to people affected by your decisions. |
| Recovery plan | How you would restore a working, safe state if a proposed change fails. |

## Capstone Scenario: Northstar Release Week

Northstar uses GHEC with personal accounts and organization SAML SSO. It has
`northstar-apps` and `northstar-ops`. A release is planned, but the team has
reported access, policy, security, automation, and usage concerns. All evidence
below is invented and simplified, not actual GitHub audit-event syntax. No
production system is connected to this exercise.

## Your Starting Scenario

| Record | Supplied evidence | Owner or contact |
| --- | --- | --- |
| ACCESS-1 | Casey's contractor assignment has ended. IdP access is disabled. Casey's personal GitHub account still appears as a member of `northstar-apps` and has direct write access to `docs`. SSO enforcement and active-session details are not supplied. | Morgan, organization owner; IT owns IdP settings |
| RULE-1 | A change note says Morgan changed `web` required approvals from one to zero yesterday. No exception approval record is attached. Current inherited rules and enforcement tests are missing. | Morgan; Riley owns release approval |
| DEP-1 | `web` has an open alert for fictional `example-parser` 1.0 with proposed fixed version 1.1. Runtime use, compatibility tests, and remediation status are unknown. | Avery, application maintainer |
| TOKEN-1 | Proposed release workflow runs only on an approved same-repository manual trigger. Its sole job reads code and publishes a GitHub Release using `GITHUB_TOKEN`; it requests `write-all`. It does not deploy or need external secrets. | Platform team |
| RUN-1 | A job from `northstar-apps/web` requests group `production` and labels `self-hosted`, `linux`, `x64`, `deploy`. Matching runner `runner-a` is online and idle, but the group permits only `northstar-ops/deploy`. No workflow restriction is set. | Operations |
| USAGE-1 | Internal summaries for two consecutive 30-day periods report Actions consumption at 60% then 82% of the same unchanged budget threshold. Queue time, job mix, and unit costs are not supplied. | Billing owner |

The release manager requests two immediate changes: bypass normal review and
grant write permissions to every workflow in the organization. These are
requests to evaluate, not instructions to carry out.

Use the official references from Lessons 1-7 as needed. In particular, consult [organization roles](https://docs.github.com/en/enterprise-cloud@latest/organizations/managing-peoples-access-to-your-organization-with-roles/roles-in-an-organization), [rulesets](https://docs.github.com/en/enterprise-cloud@latest/repositories/configuring-branches-and-merges-in-your-repository/managing-rulesets/about-rulesets), [Dependabot alerts](https://docs.github.com/en/enterprise-cloud@latest/code-security/dependabot/dependabot-alerts/about-dependabot-alerts), [`GITHUB_TOKEN` authentication](https://docs.github.com/en/enterprise-cloud@latest/actions/security-for-github-actions/security-guides/automatic-token-authentication), [runner group access](https://docs.github.com/en/enterprise-cloud@latest/actions/hosting-your-own-runners/managing-access-to-self-hosted-runners-using-groups), and [enterprise audit logs](https://docs.github.com/en/enterprise-cloud@latest/admin/monitoring-activity-in-your-enterprise/reviewing-audit-logs-for-your-enterprise).

## Work Through the Problem

### Start with Your Sandbox

1. Complete [organization setup](../sandbox-setup.md). Open your sanitized `training-org` inventory and the results you actually observed in Lessons 1-7.
2. Mark every Northstar capstone record below "supplied simulation". None is a reported incident in your organization, and SAML SSO in the story is not evidence it is enabled in the sandbox.
3. For each capstone response, identify the corresponding page or evidence source you would use in the sandbox. Use aliases and record any missing permissions.
4. Present the simulated response alongside your observed learning evidence. Do not recreate security incidents, offboard real users, disable protections, or expand workflow privileges for the capstone.

### Step 1: Build an Investigation Table

1. Make columns: record, known fact, missing fact, possible harm, owner, and first check.
2. Add the six records above. Copy facts before adding interpretations.
3. Use the earlier lesson glossaries to explain unfamiliar terms beside the table.
4. Choose an investigation order. Give a reason based on possible harm and urgency rather than simply following the table order.

**Save:** Six investigation rows and an explained priority order.

### Checkpoint 1: Personal Accounts and Offboarding

**Objective focus:** Identity lifecycle and access auditing. **Choose one answer.**

In the fictional personal-account/SAML environment, Casey's IdP identity was disabled, but the GitHub account remains an organization member with direct `docs` write access. Which statement best follows from these facts?

- A. Disabling the IdP identity deleted Casey's personal GitHub account.
- B. The recorded direct grant proves Casey can currently use it, regardless of SSO/session conditions.
- C. No GitHub access review is needed once the IdP reports a disabled account.
- D. The GitHub membership and grants still need review and authorized removal as appropriate; investigate effective access and SSO/session state rather than assuming complete offboarding.

<details>
<summary>Check your answer</summary>

**Answer: D.** Personal-account ownership, membership, grants, and SSO access conditions are distinct. A incorrectly equates disabling an IdP identity with deleting a personal GitHub account; B ignores effective authentication conditions; C ignores the remaining grants. Review [SAML SSO](https://docs.github.com/en/enterprise-cloud@latest/authentication/authenticating-with-saml-single-sign-on/about-authentication-with-saml-single-sign-on) and your Lesson 1 account-model diagrams. This is a simulation, not a finding about the actual sandbox.

</details>

### Step 2: Check Access, Rules, and the Dependency

1. For ACCESS-1, revisit Lesson 1's personal-account diagram. List remaining membership, direct-access, SSO, and credential/session questions. Do not assume disabling the IdP account removes the personal GitHub account.
2. Propose who should verify and remove unneeded company access. State an allowed/denied test and distinguish planned evidence from observed evidence.
3. For RULE-1, revisit Lesson 3's control map. List which rules, change record, approval, and allowed/blocked tests you would inspect before claiming protection is gone or restored.
4. For DEP-1, revisit Lesson 4. Write an upgrade investigation with compatibility testing and evidence of remediation; do not claim the alert alone proves exploitation.
5. For each record, record a source, the change owner, and how to recover or follow up if the proposed action fails.

**Save:** Three response plans linked to evidence and documentation.

### Step 3: Review Automation and the Queued Job

1. For TOKEN-1, open the token documentation and find the named permission for publishing a release. Propose job-specific access instead of organization-wide write access.
2. Record the manual trigger and same-repository approval assumptions. List what you would verify before using that design; do not silently extend it to untrusted pull requests.
3. For RUN-1, create requested/observed rows for labels, group access, and runner state, as in Lesson 6.
4. Explain the mismatch shown by the snapshot and propose a narrowly scoped correction only after confirming which workload should use that group.
5. Describe the safe test that would show each proposed correction worked. Leave results as "not run".

**Save:** A workflow-permission proposal and runner comparison table.

### Checkpoint 2: A Release Without Deployment Secrets

**Objective focus:** Actions token permissions and encrypted secrets. **Choose one answer.**

TOKEN-1 is an approved manual same-repository workflow that reads code and publishes a GitHub Release. It does not deploy externally. Which proposal best matches its stated task?

- A. Keep `write-all` because publishing any release needs every write permission.
- B. Propose the required `contents: write` permission for the publishing job, review any other actual job needs separately, and do not add deployment secrets.
- C. Set every job to `contents: read` and assume that also permits publishing a release.
- D. Add a broad PAT and both signing and deployment credentials as fallback authentication.

<details>
<summary>Check your answer</summary>

**Answer: B.** Publishing a release needs the relevant contents write permission, not unrelated writes or external deployment credentials. A overgrants; C omits the required write capability; D introduces unnecessary credentials. Review [workflow permission syntax](https://docs.github.com/en/actions/reference/workflows-and-actions/workflow-syntax#permissions) and verify the final proposal against the actual publishing step. This is not the default untrusted-fork case from Lesson 5.

</details>

### Step 4: Evaluate the Emergency Requests and Usage

1. Write an accept/change/reject response to each release-manager request. Explain the risk of changing more than this release needs.
2. Describe an approval and exception record that would support a narrow alternative, plus how normal controls would be checked afterward.
3. For USAGE-1, state the change in percentage points. Explain why the figures do not by themselves measure runner capacity or prove a cause.
4. List the additional cost, job, and queue evidence you would ask for. Propose a follow-up measure before increasing capacity.

**Save:** Two request decisions and a usage-investigation note.

### Step 5: Prepare Your Briefing

1. Choose your three most important next actions.
2. For each, write: "We know ...; we still need ...; I recommend ...; the owner is ...; we will verify by ...".
3. Add a recovery or follow-up step and a supporting documentation link.
4. Present your briefing before asking your tutor for feedback. Resolve questions by returning to the supplied evidence and official docs.

### Checkpoint 3: A Trend Is Not a Diagnosis

**Objective focus:** Usage trends and resource optimization. **Choose one answer.**

USAGE-1 increases from 60% to 82% of the same budget threshold over consecutive 30-day periods. Which interpretation is accurate?

- A. A 22% relative increase proves more runners are required.
- B. A 36.7-percentage-point increase proves the same users worked more.
- C. A 22-percentage-point increase (about 36.7% relative) warrants investigating consumption drivers; capacity need is still unproven.
- D. An 82-percentage-point increase proves a service outage.

<details>
<summary>Check your answer</summary>

**Answer: C.** The point difference is `82 - 60 = 22`; the relative change is `22 / 60 * 100`, about `36.7%`. A confuses the two measures and invents a cause; B swaps the measures and assumes user behavior; D misstates the change and diagnosis. Review [billing documentation](https://docs.github.com/en/billing) and compare cost, job, and queue evidence before recommending a change.

</details>

## You Are Finished When

- [ ] All six records have a fact, unanswered question, owner, and next check.
- [ ] Planned actions and observed results are not confused.
- [ ] Your runner and workflow decisions use the supplied task and access facts.
- [ ] Emergency exceptions are narrow, approved, recorded, and followed up.
- [ ] Your briefing explains the reasoning in everyday language, with sources available if questioned.

## Supplementary Practice

Use the [15-question practice set and answer key](practice-questions.md) for additional exam-style retrieval practice.

## Teach It Back

Give your tutor a concise stakeholder briefing. For each recommendation, state the evidence, assumptions, risks, owner, verification step, and recovery or follow-up plan. Use the official sources to support your reasoning; record disagreements as questions to investigate rather than guessing.

## Readiness Review

- Recheck the current [GH-100 study guide](https://aka.ms/GH100-StudyGuide) and [certification page](https://learn.microsoft.com/en-us/credentials/certifications/github-administration/) for measured objectives and exam logistics.
- Select two objectives for further review based on your practice evidence.
- Decide whether you are ready to schedule or sit the exam. Practice results and this tutoring sequence do not predict or guarantee an exam outcome.