# Lesson 6: Supplementary Practice Questions

[Return to the lesson](lesson-guide.md) | [All lessons](../README.md)

These 15 original GH-100-style questions cover runners, networking, and secret
boundaries. They are not official or recalled exam items and do not predict
exam content or scores. All scenarios are fictional Cloud paper exercises.
Do not register runners, connect private networks, or retrieve secret values.
Choose the stated number of answers before opening the answer key.

## Questions

### 1. Self-Hosted Does Not Mean GHES

**Choose one.** A GHEC organization wants to run Actions jobs on a machine it manages. Which statement is correct?

- A. Self-hosted runners require migrating the organization to GHES.
- B. GitHub becomes responsible for every patch on that machine.
- C. A self-hosted runner can serve GHEC; customer machine administration remains necessary.
- D. Registering a runner converts personal accounts to EMU.

### 2. Matching Labels

**Choose one.** A job requests `self-hosted`, `linux`, and `gpu`. The only idle permitted runner has `self-hosted`, `linux`, and `x64`, but not `gpu`. What is the immediate mismatch?

- A. The runner does not match all requested labels.
- B. An idle runner ignores all label requirements.
- C. `x64` automatically implies `gpu`.
- D. Any Linux runner can run every GPU workload without checking capabilities.

### 3. Restricted Group

**Choose one.** A job's labels match an idle runner, but the runner group allows only another repository. What must the diagnosis include?

- A. A successful label match proves the repository is eligible.
- B. Increasing CPU size removes group restrictions.
- C. A secret input grants group access.
- D. Repository eligibility is independently restricted by the group's access policy.

### 4. Workflow-Level Runner Access

**Choose two.** A group restricts both repositories and workflows. Which checks belong in an eligibility investigation?

- A. Only the repository's number of stars.
- B. Whether the requesting repository is allowed.
- C. Whether the requesting workflow matches the configured workflow restriction.
- D. Only whether the organization has unused seats.

### 5. Eligible but Busy

**Choose one.** All requested labels and group permissions match, but the only eligible runner is executing another job. What is a plausible explanation of queue wait?

- A. A busy runner proves the repository is unauthorized.
- B. Temporary lack of available execution capacity, subject to further status/concurrency checks.
- C. The organization must have leaked a secret.
- D. The job's tests must already have failed.

### 6. Queue Time Versus Run Time

**Choose one.** Jobs wait 20 minutes but execute in 2 minutes after starting. Which investigation should come first?

- A. Rewrite application tests without examining scheduling.
- B. Increase test timeouts only.
- C. Delete logs because the execution is fast.
- D. Examine eligibility, availability, concurrency, and queue patterns before attributing the delay to test execution.

### 7. Organization Secret Scope

**Choose one.** An organization secret is needed by one deployment repository. Which repository-access policy is the narrowest match?

- A. Selected repositories containing only the approved deployment repository, with workflow protections reviewed separately.
- B. Every repository in the organization.
- C. All future repositories, regardless of purpose.
- D. A runner label with no secret access policy.

### 8. Secret Precedence

**Choose one.** A job references environment `production`. The same secret name exists at organization, repository, and that environment scope. Which value takes precedence for the job once access requirements are satisfied?

- A. Organization value, because it has the broadest scope.
- B. A random value selected by the runner.
- C. Environment value.
- D. Whichever value was created earliest.

### 9. Protected Environment

**Choose one.** A job uses an environment requiring approval. What should be expected before the required approval is granted?

- A. The job receives environment secrets immediately while waiting.
- B. The protection gate must be satisfied before the job proceeds and accesses environment secrets.
- C. Every organization member becomes an eligible reviewer automatically.
- D. The environment disables all inherited enterprise policy.

### 10. External Vault Integration

**Choose two.** Which elements support a secure integration with a compatible third-party vault?

- A. Printing the vault credential in the workflow log.
- B. Assuming the vault trusts every GitHub job by default.
- C. Configured authentication/trust for the approved workflow identity and a narrow vault policy.
- D. Retrieving only necessary secrets or short-lived credentials and controlling their exposure/lifetime.

### 11. IP Allow Lists

**Choose one.** An administrator adds an approved source IP to an allow list. Which statement is accurate?

- A. This alone creates a network route to every private service.
- B. This replaces repository authorization and secret scope.
- C. This automatically gives every hosted runner that source IP.
- D. An allow list permits defined sources; routing, actual egress IP, authentication, and authorization still need configuration.

### 12. Private Connectivity Options

**Choose one.** A trusted Cloud job needs a private service. What is the best runner-design approach?

- A. Evaluate supported hosted private-network options, including applicable Azure networking, and self-hosted options against plan, trust, and connectivity requirements.
- B. Assume GHEC jobs can never connect to private networks.
- C. Choose any runner label and assume network connectivity exists.
- D. Expose the private service publicly without reviewing the requirement.

### 13. Customer-Operated Runner Duties

**Choose two.** Which responsibilities remain important for self-hosted infrastructure?

- A. Relying on repository names to patch the operating system.
- B. Maintaining the host/software and monitoring its health.
- C. Restricting untrusted workloads and limiting host/network credential exposure.
- D. Assuming GitHub removes every persistent file between jobs.

### 14. Ephemeral Runner Design

**Choose one.** Why might a team choose ephemeral self-hosted runners and disposable machines?

- A. To remove the need for any trust or patching review.
- B. To make all workflows eligible for production secrets.
- C. To reduce cross-job persistence, with actual teardown and log retention designed separately.
- D. To bypass enterprise action restrictions.

### 15. Verifying Secret Scope

**Choose one.** Which evidence best supports a secret-boundary review without exposing the secret?

- A. A pasted credential value and its owner's password.
- B. Only an online runner status.
- C. A successful login by an unrelated organization owner.
- D. Approved metadata/configuration and sanitized allowed/denied checks with a safe test credential where separately authorized.

## Answer Key

<details>
<summary>Answers and explanations</summary>

| Question | Answer | Explanation | Source |
| --- | --- | --- | --- |
| 1 | C | Self-hosted runner infrastructure can be used with GHEC. It does not change the GitHub deployment/account model or remove host-maintenance duties. | S1 |
| 2 | A | Requested labels must all match an eligible runner. Idle state and architecture labels do not create a missing GPU label/capability. | S2 |
| 3 | D | Group authorization is separate from labels and CPU resources. A secret cannot confer runner-group eligibility. | S3 |
| 4 | B, C | Both repository and workflow restrictions can constrain access. Stars and seats do not establish scheduling eligibility. | S3 |
| 5 | B | A matching busy runner can cause waiting. Inspect status and concurrency before inferring authorization failure or completed execution results. | S2, S3 |
| 6 | D | Queue delay precedes execution and needs scheduling evidence. Longer test timeouts or rewritten tests do not necessarily address it. | S2, S3 |
| 7 | A | Selected-repository scope matches the stated need. Broad grants overexpose; labels are not a secret-access policy. | S4 |
| 8 | C | For a job using the environment, its secret takes precedence over repository and organization secrets of the same name. Creation time is irrelevant. | S4 |
| 9 | B | Required environment protection gates execution and environment-secret access. It does not confer reviewer eligibility or relax enterprise policy. | S5 |
| 10 | C, D | Vault access needs explicit trust/authentication and scoped retrieval/lifetime controls. Default universal trust and credential logging are unsafe assumptions. | S6 |
| 11 | D | Source filtering does not build routes, assign all runner IPs, or grant GitHub permission. These are distinct controls. | S7, S8 |
| 12 | A | Private connectivity can have hosted or self-hosted designs with requirements to verify. Labels alone and blanket impossibility claims are insufficient. | S8 |
| 13 | B, C | Host maintenance and workload isolation remain customer concerns. Names do not patch systems, and persistent hosts are not guaranteed clean between jobs. | S1, S9 |
| 14 | C | Disposable execution reduces persistence only with real lifecycle cleanup. It does not eliminate trust, policy, or patching requirements. | S10, S9 |
| 15 | D | Metadata and safely authorized behavioral checks support scope without publishing values. Runner state or unrelated login success does not test secret authorization. | S4, S9 |

</details>

## Sources

Check the [official GH-100 outline](https://learn.microsoft.com/en-us/credentials/certifications/resources/study-guides/gh-100). Networking and vault questions introduce additional study; they do not substitute for authorized configuration practice.

- **S1:** [Self-hosted runners](https://docs.github.com/en/actions/hosting-your-own-runners/managing-self-hosted-runners/about-self-hosted-runners).
- **S2:** [Using self-hosted runners in workflows](https://docs.github.com/en/actions/hosting-your-own-runners/managing-self-hosted-runners/using-self-hosted-runners-in-a-workflow).
- **S3:** [Runner-group access](https://docs.github.com/en/actions/how-tos/manage-runners/self-hosted-runners/manage-access).
- **S4:** [Using secrets](https://docs.github.com/en/actions/security-for-github-actions/security-guides/using-secrets-in-github-actions).
- **S5:** [Deployment environments](https://docs.github.com/en/actions/deployment/targeting-different-environments/using-environments-for-deployment).
- **S6:** [OIDC with HashiCorp Vault](https://docs.github.com/en/actions/security-for-github-actions/security-hardening-your-deployments/configuring-openid-connect-in-hashicorp-vault).
- **S7:** [Organization IP allow lists](https://docs.github.com/en/enterprise-cloud@latest/organizations/keeping-your-organization-secure/managing-security-settings-for-your-organization/managing-allowed-ip-addresses-for-your-organization).
- **S8:** [Hosted-runner private networking](https://docs.github.com/en/actions/using-github-hosted-runners/connecting-to-a-private-network).
- **S9:** [Secure use of Actions](https://docs.github.com/en/actions/reference/security/secure-use).
- **S10:** [Self-hosted runner autoscaling](https://docs.github.com/en/actions/hosting-your-own-runners/managing-self-hosted-runners/autoscaling-with-self-hosted-runners).