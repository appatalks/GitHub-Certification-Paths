# Lesson 2: Enterprise Environments

**Exam domain:** Administer GitHub Enterprise environment (10-15%)

## Goals

- Explain who controls employees' GitHub accounts in each Cloud account model.
- Ask the right questions about where company data must be stored.
- Make a recommendation without guessing at prices, features, or missing requirements.

## Words to Know

| Word | Plain-language meaning |
| --- | --- |
| GHEC | GitHub Enterprise Cloud, hosted by GitHub rather than on a company's own GitHub server. |
| Personal account | An account owned by an individual, who may also contribute outside the company. |
| EMU | Enterprise Managed Users: accounts managed through the company's identity provider. |
| Data residency | Requirements about the region where specified data is stored; not a promise that all data stays in one place. |
| License | A right to use a product under the company's agreement. |
| Consumption | Usage of a product, such as billable Actions execution. |
| Assumption | Something you think is true but have not confirmed. |
| Support escalation | Asking GitHub Support to help after collecting relevant facts and safe diagnostic evidence. |

## Your Starting Scenario

All three companies want GHEC. Their requirements are fictional, not claims about product availability.

| Company | Known requirements | Unanswered question |
| --- | --- | --- |
| Harbor | Employees collaborate in public projects outside work; IT supports an IdP; no specified residency requirement. | Must contractors use the same IdP? |
| Cedar | IT must control work-account creation and removal; approved region requirements are being reviewed by legal; approved network access is required. | Which data types and regions does legal mean? |
| Summit | IT already owns employee identities; external vendor collaboration is essential; a central team manages GitHub costs. | What access do vendors need, and which account model supports it? |

Support example: Avery can sign in to GitHub but receives an access error opening
`northstar-apps/web`. No error text, timestamp, or membership record has been
collected. Do not assume this is an outage.

## Investigate

- Review the enterprise administration model in [About GitHub for enterprises](https://docs.github.com/en/enterprise-cloud@latest/admin/overview/about-github-for-enterprises). Which decisions belong to an enterprise administrator?
- Read [Choosing an enterprise type for GitHub Enterprise Cloud](https://docs.github.com/en/enterprise-cloud@latest/admin/concepts/enterprise-fundamentals/choose-an-enterprise-type). Compare identity ownership, onboarding, and account lifecycle for personal accounts and EMU.
- Read [About GitHub Enterprise Cloud with data residency](https://docs.github.com/en/enterprise-cloud@latest/admin/data-residency/about-github-enterprise-cloud-with-data-residency). What requirement does data residency address, and what constraints or details must be checked?
- Use the current [GH-100 study guide](https://aka.ms/GH100-StudyGuide) to find the licensing and consumption objectives. Record the official source you would consult rather than guessing at prices or entitlements.

## Work Through the Problem

### Start with Your Sandbox

1. Complete [organization setup](../sandbox-setup.md) and open your sanitized inventory for `training-org`.
2. Record the confirmed personal-account model. Ask the authorized owner to confirm the enterprise relationship, Cloud plan, and authentication requirements you cannot see.
3. Inspect permitted settings or an owner explanation; keep unavailable residency, licensing, and enterprise settings marked unknown.
4. Compare those observed facts with the fictional company profiles below. These profiles are decision exercises, not recommendations to migrate your sandbox to EMU or data residency.

### Step 1: Compare the Account Models

1. Create a table with columns: question, personal accounts, EMU, and documentation link.
2. Add rows for who creates accounts, who removes company access, external collaboration, and sign-in requirements.
3. Open the enterprise-type documentation above. Fill one row at a time using a sentence you can explain in your own words.
4. If a behavior depends on configuration, write the condition. If you cannot find it, write "needs verification" rather than guessing.

**Save:** The account comparison table.

### Checkpoint 1: A Conditional Recommendation

**Objective focus:** Cloud deployment/account models. **Choose one answer.**

Cedar wants IT to control work-account creation and removal, but legal has not specified which data must reside in which region. What is the best next step?

- A. Promise that EMU alone meets every residency requirement.
- B. Change the sandbox account model before gathering more requirements.
- C. Evaluate EMU for account lifecycle, clarify legal's requirements, and verify the relevant Cloud residency capabilities.
- D. Treat data residency and repository visibility as the same setting.

<details>
<summary>Check your answer</summary>

**Answer: C.** Account ownership and data-location requirements are separate decisions. A assumes compliance without facts, B changes a live design prematurely, and D confuses where data is stored with who can access it. Review [Cloud enterprise types](https://docs.github.com/en/enterprise-cloud@latest/admin/concepts/enterprise-fundamentals/choose-an-enterprise-type) and the residency reference above.

</details>

### Step 2: Make Three Conditional Recommendations

1. Create a table with columns: company, known needs, missing facts, possible account type, and reason.
2. Copy each company profile into a row. Keep its unanswered question visible.
3. Use your account comparison to suggest a type. Write "if ... then ..." where missing information could change the recommendation.
4. For Cedar, open the data residency documentation. Write which product facts to verify and which requirements only legal can define.
5. For each company, add one requirement that would cause you to reconsider. Do not claim a compliance guarantee.

**Save:** Three recommendations with assumptions and source links.

### Step 3: Find Billing Evidence

1. Open the [GitHub billing documentation](https://docs.github.com/en/billing).
2. Find guidance on viewing license and product usage. Record the page title and link.
3. Create two rows: licenses assigned and product usage. Write what report you would inspect and what time period you would ask for.
4. List the company agreement or plan details you would need before estimating a cost. Do not invent a price.

**Save:** A short billing-information checklist.

### Checkpoint 2: Licenses and Consumption

**Objective focus:** Licensing and usage. **Choose one answer.**

A manager asks for an exact cost estimate. You have an assigned-seat count but no agreement details or metered-product report. What can you responsibly provide?

- A. The seat count as one input, plus a list of missing agreement and usage information needed for an estimate.
- B. An exact total based on the seat count alone.
- C. Proof that unassigned seats are always billable at the same price.
- D. A guarantee that Actions costs nothing whenever seats are paid for.

<details>
<summary>Check your answer</summary>

**Answer: A.** License and consumption data must be interpreted under the actual agreement and product definitions. B omits needed inputs. C and D make universal billing claims the evidence does not support. Review [GitHub billing documentation](https://docs.github.com/en/billing).

</details>

### Step 4: Plan a Support Investigation

1. Copy Avery's issue into a note. List the facts you have and the facts you lack separately.
2. List safe checks: exact error and timestamp, correct repository address, membership and role, and applicable SSO requirements.
3. Read [Creating a support ticket](https://docs.github.com/en/support/contacting-github-support/creating-a-support-ticket). Build a draft ticket with symptom, expected result, actual result, and checks already made. Use placeholders for facts you do not have.
4. Explain what findings would lead you to fix access locally or seek Support help. Include no tokens, passwords, or private customer data.

**Save:** The draft ticket and investigation checklist.

### Checkpoint 3: Support Evidence

**Objective focus:** Administrator investigation versus Support. **Choose two answers.**

Avery can sign in but gets a repository access error. Which two actions help produce a useful, safe investigation record?

- A. Attach Avery's token so Support can reproduce the issue.
- B. Record the exact safe error text, time, expected result, and checks already performed.
- C. Describe which membership, role, and SSO access checks remain unresolved.
- D. State that GitHub is down because one account received an error.

<details>
<summary>Check your answer</summary>

**Answers: B and C.** These describe the symptom and investigation without guessing at a cause. A exposes a credential; D makes an unsupported service-wide diagnosis. Review [Creating a support ticket](https://docs.github.com/en/support/contacting-github-support/creating-a-support-ticket).

</details>

## You Are Finished When

- [ ] Your comparisons distinguish individual-owned and company-managed accounts.
- [ ] Each recommendation names its assumptions and a condition that could change it.
- [ ] Your residency questions distinguish legal requirements from documented product behavior.
- [ ] Your billing and support checklists say exactly which evidence is missing.

Do not attempt to change an enterprise account type in a live environment. This tutoring sequence covers GHEC design, not GHES administration; check the exam guide separately for any GHES topics it measures.

## Supplementary Practice

Use the [15-question practice set and answer key](practice-questions.md) for additional exam-style retrieval practice.

## Teach It Back

Present one account-type recommendation to your tutor. Explain the assumptions, tradeoffs, missing facts, and source material behind it. Your tutor observes and asks you to support your reasoning; you drive the investigation.

## Carry Forward

Keep the comparison table and unresolved questions. In Lesson 3, use them to decide where enterprise, organization, and repository controls belong.