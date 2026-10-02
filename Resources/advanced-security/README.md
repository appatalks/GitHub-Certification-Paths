# GitHub Advanced Security (GH-500)

<p align="center"><img src="../../assets/advsec-splash.png" alt="GitHub Advanced Security certification path" width="100%"></p>

GH-500 is a prevention-and-response certification. The strongest preparation
loop is simple: enable a feature, create or inspect a finding, triage it, fix or
defend the decision, and explain how to prevent the next one.

## Start Here

- [Official certification page](https://learn.microsoft.com/en-us/credentials/certifications/github-advanced-security/): current exam details, policies, and registration.
- [GH-500 study guide](https://aka.ms/GH500-StudyGuide): skills measured and preparation references.
- [GitHub Learn catalog](https://learn.github.com/certification/GHAS): official GitHub learning catalog; sign-in may be required.
- [GitHub Advanced Security Part 1](https://learn.microsoft.com/en-us/training/paths/github-advanced-security/): Microsoft Learn modules for the core security features.
- [GitHub security and code quality documentation](https://docs.github.com/en/code-security): current feature concepts, configuration, and operations.
- [Official practice assessment](https://learn.microsoft.com/en-us/credentials/certifications/github-advanced-security/): open the practice assessment from the certification page after studying.

## What to Know

The official GH-500 domains are:

1. **Security suites, features, and ecosystem (15-20%):** GitHub Code Security, GitHub Secret Protection, security settings, and where features fit in the lifecycle.
2. **Secret protection (15-20%):** secret scanning, push protection, custom patterns, validity signals, alert handling, and remediation.
3. **Supply-chain security (15-20%):** dependency graph, Dependabot alerts and updates, dependency review, advisories, and dependency policy.
4. **Code security and CodeQL (10-15%):** code scanning, default and advanced setup, query suites, SARIF, and analysis troubleshooting.
5. **Security operations (15-20%):** prioritization, alert triage, remediation, security overview, campaigns, and reporting.
6. **Security suites administration (10-15%):** organization and enterprise rollout, configurations, permissions, coverage, and usage.

Start with the [security quickstart](https://docs.github.com/en/code-security/getting-started/quickstart-for-securing-your-repository),
then go deeper with [secret scanning](https://docs.github.com/en/code-security/concepts/secret-security/secret-scanning),
[code scanning](https://docs.github.com/en/code-security/concepts/code-scanning/code-scanning),
and [supply-chain security](https://docs.github.com/en/code-security/concepts/supply-chain-security/supply-chain-security).

## Hands-On Missions

### Mission 1: Stop the Leak

Read the secret-scanning and push-protection flows. For a fictional token leak,
write the incident sequence: revoke or rotate the credential, investigate
exposure, remediate history where appropriate, close the alert, and prevent a
repeat.

### Mission 2: Make Dependencies Behave

Complete [Secure your repository's supply chain](https://github.com/skills/secure-repository-supply-chain).
Be able to distinguish dependency graph data, Dependabot alerts, security
updates, version updates, and dependency review.

### Mission 3: Read a CodeQL Finding

Use the [code scanning documentation](https://docs.github.com/en/code-security/how-tos/find-and-fix-code-vulnerabilities/configure-code-scanning/configure-code-scanning)
to compare default and advanced setup. Practice explaining a finding's path,
severity, remediation, dismissal rationale, and merge-protection impact.

## Quick Self-Check

- What is the difference between detecting a secret and preventing its push?
- How do Dependabot alerts, security updates, and version updates differ?
- When would a repository use default setup versus advanced setup for CodeQL?
- What information helps prioritize a security alert instead of merely counting it?
- Which controls belong at repository, organization, and enterprise scale?

## Keep Current

Feature names, licensing, and plan requirements evolve. Check the [official
certification page](https://learn.microsoft.com/en-us/credentials/certifications/github-advanced-security/)
and the current GitHub Docs before scheduling the exam or enabling a feature in
a real organization.
