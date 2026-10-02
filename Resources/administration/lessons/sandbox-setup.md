# Set Up Your Organization-Based Lessons

Use your approved disposable GitHub Enterprise Cloud organization for these
lessons. Published notes call it `training-org` and use personal GitHub
accounts. Do not interpret the made-up incident records in later lessons as
findings about your organization.

## Step 1: Confirm the Sandbox Boundary

1. Open the organization address supplied privately by your tutor. Confirm with the tutor that this is the disposable sandbox approved for these lessons, not a production organization.
2. Sign in with your own authorized training account. Never share passwords, tokens, recovery codes, or browser sessions.
3. Ask the owner which repositories and test accounts you may use, which settings you may change, and who can restore them. Sandbox approval does not grant enterprise or identity-provider administration rights.
4. Write down the approved scope privately. Stop if the scope is unclear or you cannot restore a proposed change.
5. Confirm the Cloud plan and available features through the owner or permitted settings. Record unavailable features as limitations; do not upgrade the plan or enable billable services for a lesson without separate approval.

## Step 2: Create a Private Alias Map

1. Keep the actual organization address and alias-to-real-name mapping in local ignored notes under `tmp/lesson-planning/`. Never commit this mapping.
2. Label the organization `training-org`. Label its enterprise, if confirmed, `training-enterprise`; do not invent an enterprise relationship you cannot see.
3. Choose aliases for approved lesson repositories, such as `app-repo`, `docs-repo`, and `release-repo`. Record each real repository's purpose and visibility privately. These are suggested aliases, not claims that three repositories already exist.
4. Label teams `team-a`, `team-b`, and so on. Label approved test accounts `student-a`, `student-b`, and so on. Keep actual handles out of published diagrams.
5. If a required example resource is missing, mark it missing. Ask for approval before creating an empty training repository, team, or test identity. Otherwise, use the supplied paper exercise.

## Step 3: Record the Organization You Can Actually See

1. Open the organization's **Repositories** tab. For each approved lesson repository, record its alias, purpose, visibility, and your permission level.
2. Open **Teams** if you have access. Record each selected team's alias and organization. Open the team and inspect its repository access and membership where permitted.
3. Open **People** if permitted. Record training-account aliases and their organization roles, not a full employee directory.
4. Ask the owner to show or confirm relevant **Settings**: base repository permissions, authentication requirements, rulesets, Actions policy, and runner access. Do not change settings during this inventory.
5. Mark any unavailable page or setting "not visible to this account". Lack of visibility is not evidence that a feature, team, or repository does not exist.
6. Create the following sanitized table for your lesson notes. Fill the observations from the sandbox; do not copy fictional values from the later incident packets.

| Resource alias | Purpose or role | Observed access or setting | Evidence type | Unanswered question |
| --- | --- | --- | --- | --- |
| `training-org` | Organization | To inspect | Owner confirmation or permitted settings | Enterprise relationship and features |
| Your chosen repository alias | Training work | To inspect | Repository settings or role confirmation | Who may change it? |
| Your chosen team alias | Grouped access | To inspect | Team repository access | Are there other access paths? |

## Step 4: Separate Observation, Simulation, and Live Practice

1. Label each exercise result **observed in sandbox**, **supplied simulation**, or **proposed / not tested**.
2. Use your actual sanitized inventory for organization maps and settings comparisons. Use the supplied fictional records when the real sandbox does not contain that exact example or incident.
3. Before a live change, write the target alias, starting value, proposed value, expected allowed/denied result, owner approval, and restoration steps.
4. Make only the approved change on disposable resources. Use the feature-specific GitHub documentation linked in that lesson for the current interface and requirements.
5. Test using approved dummy content and training identities. Never expose real secrets, broaden production access, connect a real IdP, or run the intentionally unsafe sample workflow.
6. Record what happened, restore the starting state or perform the agreed cleanup, and check that temporary access is gone. Stop and ask the owner if restoration fails.

## Step 5: Sanitize Before Sharing

1. Replace organization, enterprise, repository, team, person, and workflow names with aliases. Remove real URLs, handles, emails, numeric IDs, machine names, network addresses, and unnecessary timestamps.
2. Prefer a recreated table or diagram to a raw screenshot, log, workflow file, or audit export. Removing a displayed name alone does not sanitize hidden metadata or link targets.
3. Include only the minimum non-sensitive facts needed to explain the exercise. Access settings and network details can be sensitive even when names are changed.
4. Check both visible text and link destinations. Keep the mapping, raw evidence, and unredacted screenshots local; do not attach them to issues or pull requests.
5. Ask the tutor to review the sanitized output before publishing it. Verify that files under `tmp/` are ignored with `git check-ignore -v tmp/lesson-planning/sandbox-context.md`.

**Finished when:** Your private mapping exists, your sanitized inventory is
filled or marks missing visibility, and every planned live action has an
approved target and restoration procedure. Continue with [Lesson 1](lesson-01-identity-and-access/lesson-guide.md).