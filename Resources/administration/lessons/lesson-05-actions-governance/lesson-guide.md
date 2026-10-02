# Lesson 5: GitHub Actions Governance

**Exam domain:** Manage GitHub Actions (20-25%)

## Goals

- Explain what each job does and what access it needs.
- Remove unnecessary permissions and secret requests from a workflow design.
- Check whether an action is allowed and whether code from outside the company can safely run.

## Words to Know

| Word | Plain-language meaning |
| --- | --- |
| Workflow | An automation file describing when jobs run and what they do. |
| Job / step | A group of work running in an execution environment / one action within that job. |
| Runner | The machine that executes a job. |
| `GITHUB_TOKEN` | A temporary credential GitHub provides to a workflow for repository operations. |
| Permissions | The operations a token may perform, such as reading repository contents or writing issues. |
| Action | A reusable piece of automation called by a workflow step. |
| Reusable workflow | A workflow called by another workflow, with documented inputs and secret requirements. |
| Fork | Another copy of a repository, often controlled by an outside contributor. |
| Secret scope | Which repositories or environments may use a stored credential. |
| Pinning | Selecting a specific action version; a full commit SHA identifies exact code, unlike a movable tag. |

## Your Starting Scenario

This is a static review exercise. Do not install or execute the example. The
Northstar and vendor references below are fictional, and the intentionally
broad permissions and secret requests are things to review, not instructions
to follow.

The proposed enterprise policy allows `actions/*` and Northstar's internal
reusable workflows. Organization policy may restrict further, not override an
enterprise restriction. The team proposes the following workflow in `web`:

```yaml
name: Proposed pull request checks
on: pull_request
permissions: write-all
jobs:
  build:
    runs-on: ubuntu-latest
    env:
      DEPLOY_KEY: ${{ secrets.DEPLOY_KEY }}
    steps:
      - uses: actions/checkout@v4
      - run: printf 'Placeholder for a read-only build and tests\n'
      - uses: example-vendor/summary@main
  report:
    uses: northstar-apps/automation/.github/workflows/report.yml@main
    with:
      issue_number: 42
    secrets:
      DEPLOY_KEY: ${{ secrets.DEPLOY_KEY }}
```

| Item | Supplied task or requirement |
| --- | --- |
| `build` | Reads repository code and runs tests; it does not deploy or write repository data. |
| Vendor action | Vendor says it prints a test summary; code and permissions have not been reviewed. |
| `report` | Fictional reusable workflow uses its `GITHUB_TOKEN` to comment on existing issue 42; accepts `issue_number` and an optional `DEPLOY_KEY`; it never deploys or uses that key. |
| `DEPLOY_KEY` | Deployment credential currently stored at organization level for all repositories; only `deploy` needs it. No value is supplied. |
| Contributions | Both company-branch and outside-fork pull requests are accepted. |

This sample is not a complete safe design. Use the documented reusable-workflow
permission rules, fork behavior, and action policy to assess it.

## Investigate

- Compare [enterprise Actions policies](https://docs.github.com/en/enterprise-cloud@latest/admin/enforcing-policies/enforcing-policies-for-your-enterprise/enforcing-policies-for-github-actions-in-your-enterprise) with [organization Actions settings](https://docs.github.com/en/enterprise-cloud@latest/organizations/managing-organization-settings/disabling-or-limiting-github-actions-for-your-organization). Where can each policy apply?
- Read [GITHUB_TOKEN authentication](https://docs.github.com/en/enterprise-cloud@latest/actions/security-for-github-actions/security-guides/automatic-token-authentication). How do you determine the permissions a job needs?
- Read [Reusing workflows](https://docs.github.com/en/enterprise-cloud@latest/actions/sharing-automations/reusing-workflows). What should you inspect about a called workflow, its inputs, and secrets?

## Work Through the Problem

### Start with Your Sandbox

1. Complete [organization setup](../sandbox-setup.md). Open permitted organization **Settings** > **Actions** pages and an approved repository's Actions settings.
2. Record actual allowed-action policy and workflow-token defaults using aliases; ask the owner about inherited restrictions you cannot inspect.
3. Compare that snapshot with the fictional policy and workflow below. Do not copy actual workflows or secrets into published notes, and never install the unsafe example.
4. For an approved live exercise, use a separate owner-reviewed harmless workflow with no secrets or untrusted code. Record its token permissions and expected behavior before running it. Clean up the test workflow and any test artifacts afterward; check possible usage charges first.

### Step 1: Read the Workflow Without Running It

1. Copy the YAML into your notes as plain text; do not place it in `.github/workflows`.
2. Find `on`, `permissions`, `jobs`, `uses`, and `secrets`. Beside each, write what the field controls using the glossary and docs.
3. Make a table with columns: job, stated task, token access needed, secret needed, and source.
4. Fill the task column from the supplied table. Do not assume "build" means "deploy".

**Save:** An annotated workflow and the two-row job table.

### Checkpoint 1: Different Jobs, Different Permissions

**Objective focus:** Workflow permissions. **Choose two answers.**

The supplied `build` job only reads code and tests it. The `report` job comments on an issue with `GITHUB_TOKEN` and does not deploy. Which two changes fit these stated tasks?

- A. Keep workflow-wide `write-all` because one job writes a comment.
- B. Propose only the read permissions needed by `build`, then verify its checks.
- C. Give `report` the required issue-comment permission and remove its unneeded deployment-secret input.
- D. Give both jobs every organization secret to avoid future failures.

<details>
<summary>Check your answer</summary>

**Answers: B and C.** Permission and secret scope should match each job's actual task. A gives unrelated write access; D exposes unrelated secrets. Inspect the reusable workflow before finalizing its exact permissions and inputs. Review [automatic token authentication](https://docs.github.com/en/actions/security-for-github-actions/security-guides/automatic-token-authentication) and the reusable-workflow source above.

</details>

### Step 2: Propose Permission and Policy Changes

1. Open the token documentation. Find the syntax for job permissions and the named permission needed for each task.
2. Replace `write-all` in a written change proposal with a restrictive default and task-specific job permissions. Check how the caller limits a reusable workflow's token.
3. Check each `uses` reference against the proposed enterprise policy. List any source that needs removal, review, or a policy exception before use.
4. Find GitHub's [secure use guidance for actions](https://docs.github.com/en/actions/security-for-github-actions/security-guides/security-hardening-for-github-actions). Explain why `@main`, a version tag, and a verified full commit SHA are different choices. Do not invent a SHA.
5. Create a change table: original field, proposed change, reason, and documentation link. A change table is sufficient; you do not need to produce runnable YAML.

**Save:** The permission and action-policy review.

### Checkpoint 2: Policy Inheritance

**Objective focus:** Enterprise and organization Actions policies. **Choose one answer.**

The fictional enterprise permits only `actions/*` and approved internal workflows. A repository maintainer wants the unapproved vendor action. Which statement is correct?

- A. A repository policy can always override an enterprise restriction.
- B. Pinning any vendor action automatically makes it enterprise-approved.
- C. An organization can make policy more restrictive, but cannot use a lower-level setting to allow what the enterprise forbids.
- D. Granting the workflow a write token overrides action allow-list restrictions.

<details>
<summary>Check your answer</summary>

**Answer: C.** Lower-level settings cannot relax the applicable enterprise restriction. A reverses that relationship; B confuses reference integrity with approval; D confuses token permissions with action policy. Review [enterprise Actions policies](https://docs.github.com/en/enterprise-cloud@latest/admin/enforcing-policies/enforcing-policies-for-your-enterprise/enforcing-policies-for-github-actions-in-your-enterprise).

</details>

### Step 3: Review Secrets and Outside Contributions

1. Locate every `DEPLOY_KEY` reference. Compare it with the declared work of that job or called workflow.
2. Use [Using secrets in GitHub Actions](https://docs.github.com/en/enterprise-cloud@latest/actions/security-for-github-actions/security-guides/using-secrets-in-github-actions) to propose which consumer should retain access and which should not.
3. Make two rows: same-repository pull request and outside-fork pull request. Record documented token and secret behavior for each, including settings you would need to inspect.
4. Explain whether the reporting job can comment in each case under your design. Do not grant broad write access simply to make an outside contribution succeed.
5. Record why switching to a more privileged event is not a simple fix for running untrusted contribution code. Find the relevant trust-boundary warning in the secure use guidance.

**Save:** A secret-access map and two contribution-case notes.

### Step 4: Write Test Cases

1. Make a table: case, input, expected result, evidence to inspect, and actual result.
2. Add a company pull request, an outside-fork pull request, an action outside the allowlist, and a build attempting a write or deployment-secret access it does not need.
3. Predict results from the documented settings in your proposal, not from the insecure starting example.
4. Keep actual results as "not run". Explain what an authorized Cloud sandbox would need before safely testing a revised design.

### Checkpoint 3: Fork Contributions

**Objective focus:** Secret access and untrusted workflows. **Choose one answer.**

A standard `pull_request` workflow runs for a fork contribution using GitHub's default fork security behavior. Which expectation should guide your review?

- A. Every organization secret is automatically passed to the job.
- B. Approval to run the job automatically grants the contributor all deployment credentials.
- C. A checkout action gives the job a write token regardless of event or settings.
- D. Repository secrets are not passed to the fork-triggered job, and `GITHUB_TOKEN` is read-only by default; verify any non-default policy settings separately.

<details>
<summary>Check your answer</summary>

**Answer: D.** Default fork behavior restricts credentials. A and B invent automatic secret access; C assigns token control to checkout rather than the trigger and applicable settings. Do not switch to a privileged trigger just to make this example work. Review [events that trigger workflows](https://docs.github.com/en/actions/reference/workflows-and-actions/events-that-trigger-workflows#pull_request) and the security-hardening source in Investigate.

</details>

## You Are Finished When

- [ ] Every job has a task-based permission choice and a reason.
- [ ] Your change table addresses action sources, version references, and unnecessary secret access.
- [ ] You distinguish outside-fork behavior from same-repository behavior.
- [ ] Your tests include expected allowed and denied cases without executing the unsafe sample.

## Supplementary Practice

Use the [15-question practice set and answer key](practice-questions.md) for additional exam-style retrieval practice.

## Teach It Back

Present your workflow review to your tutor. Explain each permission and secret decision, what could go wrong, and how your tests would reveal it. The tutor observes; you lead the review and consult the docs to resolve disagreements.

## Carry Forward

Save the reviewed workflow and test cases. Lesson 6 builds on them to choose runner types and investigate queued jobs.