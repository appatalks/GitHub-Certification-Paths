# Lesson 6: Runners and Secrets

**Exam domain:** Manage GitHub Actions (20-25%)

## Goals

- Choose where each job should run and explain why.
- Check why a job is waiting before buying or adding more machines.
- Decide which jobs should receive each secret, without using secret values.

## Words to Know

| Word | Plain-language meaning |
| --- | --- |
| GitHub-hosted runner | A job execution environment provided by GitHub. |
| Self-hosted runner | A machine the customer operates for Actions jobs; it can be used with GHEC and does not mean GHES. |
| Label | A name describing a runner; requested labels help select eligible machines. |
| Runner group | A collection of runners with access rules for repositories or workflows. |
| Queued | Waiting to start, not necessarily slow while executing. |
| Capacity | How much work available machines can handle. |
| Private network | A network that is not openly reachable from the internet. |
| Environment | A named workflow target, such as `production`, that can have secrets and protection rules. |

## Your Starting Scenario

| Workload | Known needs | Secret need |
| --- | --- | --- |
| `web` tests | Linux, 2 CPUs, outside-fork contributions, no private network. | None |
| `deploy` release | Linux, 4 CPUs, trusted approved workflow, access to an internal service. | `DEPLOY_KEY` |
| `web` sensitive build | Linux, 8 CPUs, private signing service, trusted release code only. | `SIGNING_KEY` |

Synthetic runner snapshot at the time job Q-1 was queued:

| Runner | Group | Labels | State | Group repository access | Resources |
| --- | --- | --- | --- | --- | --- |
| `runner-a` | `production` | `self-hosted`, `linux`, `x64`, `deploy` | Online, idle | `northstar-ops/deploy` only | 4 CPUs, internal-service network |
| `runner-b` | `builds` | `self-hosted`, `linux`, `x64`, `build` | Online, busy | `northstar-apps/web` only | 8 CPUs, signing-service network |

Q-1 comes from `northstar-apps/web`, requests group `production` and all labels
`self-hosted`, `linux`, `x64`, `deploy`, and is queued. No group workflow
restriction is configured. The snapshot does not include service connectivity
tests or a later runner status; do not infer those results.

Secret metadata: `DEPLOY_KEY` is currently available to all repositories in
`northstar-ops`; `SIGNING_KEY` is available to all repositories in
`northstar-apps`. Both are organization-scoped. Operations owns `DEPLOY_KEY`
for approved production deployment; Security owns `SIGNING_KEY` for approved
signing. Values are never provided.

## Investigate

- Compare [GitHub-hosted runners](https://docs.github.com/en/enterprise-cloud@latest/actions/using-github-hosted-runners/about-github-hosted-runners) and [self-hosted runners](https://docs.github.com/en/enterprise-cloud@latest/actions/hosting-your-own-runners/about-self-hosted-runners). What ownership, maintenance, isolation, and network needs does each imply?
- Read [Managing access to self-hosted runners using groups](https://docs.github.com/en/enterprise-cloud@latest/actions/hosting-your-own-runners/managing-access-to-self-hosted-runners-using-groups). How can group access affect which jobs can use a runner?
- Read [Using secrets in GitHub Actions](https://docs.github.com/en/enterprise-cloud@latest/actions/security-for-github-actions/security-guides/using-secrets-in-github-actions). Which scopes and protections are relevant to the scenarios below?

## Work Through the Problem

### Start with Your Sandbox

1. Complete [organization setup](../sandbox-setup.md). Inspect permitted **Settings** > **Actions** runner pages and approved repository access.
2. Record selected runner and group aliases, labels, access, and state locally. Publish only minimal sanitized facts; omit real machine names and network details.
3. Inspect secret names and access scope only where approved. Do not retrieve, display, export, or rotate values for this lesson.
4. Compare the actual inventory with the synthetic Q-1 packet below. A missing self-hosted runner does not prevent completing the paper diagnosis.
5. Do not register machines, broaden runner-group access, connect internal networks, or expose existing runners to test code without separate owner approval and a safe cleanup plan.

### Step 1: Choose a Runner for Each Workload

1. Copy the workload table. Add columns for runner approach, operating owner, risk, and documentation link.
2. Open the hosted and self-hosted documentation. Compare the CPU, network, trust, and maintenance requirements one workload at a time.
3. Write a provisional choice and explain the tradeoff. Consider supported hosted options too; do not assume private networking always demands a self-hosted runner.
4. List facts requiring confirmation, such as available runner sizes, networking support, isolation, and plan requirements.
5. For outside-fork tests, explain how you would keep untrusted code away from the internal service and signing credential.

**Save:** Three workload recommendations, with known requirements separated from unknown product details.

### Checkpoint 1: Untrusted Code and Private Networks

**Objective focus:** Runner options and trust boundaries. **Choose one answer.**

The public-fork test workload needs no private network or secret. A production self-hosted runner can reach an internal service. What is the best recommendation?

- A. Use the production runner because it is currently idle.
- B. Add a production secret to every fork test so it can authenticate.
- C. Treat a runner label as proof that the job is safe to run there.
- D. Evaluate a suitably isolated hosted option for the test workload and keep untrusted code away from the production runner's trusted boundary.

<details>
<summary>Check your answer</summary>

**Answer: D.** A runner choice must consider trust and network reach, not just available CPU time. A exposes the production boundary; B adds an unnecessary credential; C mistakes scheduling metadata for isolation. Hosted options also require a security and capability review. Review [secure use of Actions](https://docs.github.com/en/actions/reference/security/secure-use).

</details>

### Step 2: Investigate Q-1

1. Create a table: check, requested value, observed value, match or mismatch, and next evidence.
2. Copy Q-1's repository, group, and labels into separate rows.
3. Compare all requested labels with each runner's labels. Then check group repository access; an idle machine is not automatically eligible.
4. Record each runner's online/busy status. Keep this check separate from permissions and label matching.
5. Record the group-access mismatch. Q-1's intended workload is not supplied: ask whether it is a web build or an approved deployment before proposing a correction. Do not broaden group access or change selectors until you have confirmed the workload and who may run it.
6. Add a follow-up check that would show the corrected job can be assigned. If it starts but cannot reach a service, record that as a separate network investigation.

**Save:** The match table and a short diagnosis supported by the snapshot, not a guess about all possible queue causes.

### Checkpoint 2: An Idle Runner Is Not Always Eligible

**Objective focus:** Runner groups and troubleshooting. **Choose one answer.**

Q-1 comes from `northstar-apps/web` and targets the production group. Runner-a is idle but that group allows only `northstar-ops/deploy`. What does the packet support?

- A. A repository/group eligibility mismatch; confirm the intended workload and trust before proposing a selector or access change.
- B. A CPU shortage that will be fixed by buying more of the same restricted runners.
- C. Proof that runner-a is offline, despite the supplied snapshot.
- D. An immediate need to allow all repositories into the production group.

<details>
<summary>Check your answer</summary>

**Answer: A.** The group restriction excludes the requesting repository. B does not address eligibility; C contradicts the supplied status; D widens a sensitive boundary without establishing need. Other queue causes can exist, but the packet supports this mismatch. Review [self-hosted runner groups](https://docs.github.com/en/actions/how-tos/manage-runners/self-hosted-runners/manage-access).

</details>

### Step 3: Limit Secret Access

1. Make a table with columns: secret name, owner, intended consumer, current scope, proposed scope, and verification.
2. Add both keys from the supplied metadata. Do not create credentials.
3. Read the secret-scope documentation. Compare repository, selected-repository organization, and environment options.
4. Choose a scope that fits each consumer and any required approvals. Explain both storage scope and how a workflow actually receives the secret.
5. Write an allowed case and a denied case for each key. Check denial using metadata or an approved dummy value in a separate sandbox, never by printing a real secret.

**Save:** The secret-boundary table.

### Step 4: Check Whether More Capacity Would Help

1. Separate wait time before a job starts from execution time after it starts.
2. List reports you would need: queue history, eligible runner status, job durations, and concurrent workload.
3. Write one observation supporting a capacity problem and one that would instead support a label or access problem.
4. Recommend what to measure before adding machines. Explain what result would make you change that recommendation.

### Checkpoint 3: Secret Scope Is a Separate Control

**Objective focus:** Encrypted secret access. **Choose one answer.**

Only the approved deployment workflow in one repository needs `DEPLOY_KEY`. What should the organization-secret proposal aim to do?

- A. Make it available to every repository because a runner group already exists.
- B. Restrict repository access to the documented deployment need, review workflow/environment protections separately, and verify with authorized checks.
- C. Put the credential value in the artifact so the tutor can verify the scope.
- D. Assume selecting a runner label automatically removes secret access from every other repository.

<details>
<summary>Check your answer</summary>

**Answer: B.** Organization secret scope, workflow trust, and runner access are separate boundaries. A overexposes the secret; C leaks its value; D assigns secret authorization to a scheduling label. Review [using secrets](https://docs.github.com/en/actions/security-for-github-actions/security-guides/using-secrets-in-github-actions). This exercise records metadata and a proposal, not secret values or unauthorized changes.

</details>

## You Are Finished When

- [ ] Every runner choice addresses network needs, trust, and operating responsibility.
- [ ] Your Q-1 diagnosis compares labels, group access, and state separately.
- [ ] Both secrets have named consumers and allowed/denied verification cases.
- [ ] You distinguish queue wait from execution time before proposing capacity changes.

Do not expose a self-hosted runner to untrusted workloads. Use synthetic job and secret metadata only; never place secret values in notes, logs, or test output.

## Supplementary Practice

Use the [15-question practice set and answer key](practice-questions.md) for additional exam-style retrieval practice.

## Teach It Back

Walk your tutor through one runner recommendation and your Q-1 comparison table. Explain which assumptions could change your decision and show where the documentation supports it.

## Carry Forward

Keep your workload recommendations, Q-1 comparison table, and secret-boundary table. Lesson 7 uses evidence and measurements to reason about platform usage and optimization.