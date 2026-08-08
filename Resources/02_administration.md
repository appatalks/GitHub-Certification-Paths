# GitHub Administration (GH-100)

GH-100 is for people who make GitHub usable, governed, and secure for teams.
Study it as an administrator making policy decisions, not as a tour of every
settings page. The recurring question is: *who can do what, where, and how do we
know it is working?*

## Start Here

- [Official certification page](https://learn.microsoft.com/en-us/credentials/certifications/github-administration/): current exam details, policies, and registration.
- [GH-100 study guide](https://aka.ms/GH100-StudyGuide): skills measured and preparation references.
- [GitHub Learn catalog](https://learn.github.com/certification/ADMIN): official GitHub learning catalog; sign-in may be required.
- [GitHub for enterprises](https://docs.github.com/en/enterprise-cloud@latest/admin/overview/about-github-for-enterprises): enterprise concepts and deployment options.
- [GitHub administration documentation](https://docs.github.com/en/enterprise-cloud@latest/admin): the administrator's reference hub.
- [Official practice assessment](https://learn.microsoft.com/en-us/credentials/certifications/github-administration/): open the practice assessment from the certification page after studying.

## What to Know

The official GH-100 domains are:

1. **Identity and access management (15-20%):** authentication, authorization, teams, roles, external identity, and access lifecycle decisions.
2. **Enterprise environment (10-15%):** enterprise, organization, and repository boundaries; policies; settings; and deployment choices.
3. **Secure development and compliance (25-30%):** rulesets, branch protection, auditability, security policies, data protection, and compliance controls.
4. **GitHub Actions administration (20-25%):** Actions policies, runner choices, secrets, permissions, reusable automation, and governance.
5. **Monitoring and optimization (10-15%):** audit logs, usage, limits, billing signals, reliability, and improving the platform over time.

Review the [GitHub account and permission concepts](https://docs.github.com/en/get-started/learning-about-github/access-permissions-on-github),
then use the [Actions documentation](https://docs.github.com/en/actions) and
[security documentation](https://docs.github.com/en/code-security) to connect
policy decisions to the developer experience.

## Hands-On Missions

### Mission 1: Design the Boundary

Sketch an enterprise containing two organizations and several repositories.
Assign owners, teams, repository roles, and a ruleset. Explain which decision
belongs at the enterprise, organization, repository, or team level.

### Mission 2: Govern a Workflow

Take a simple Actions workflow and write an administration checklist: allowed
actions, `GITHUB_TOKEN` permissions, secret scope, runner type, fork behavior,
environment protection, and audit evidence.

### Mission 3: Investigate the Signal

Choose a hypothetical access or policy change. Describe which audit or usage
signal you would inspect, what evidence you would collect, and which control you
would adjust. The goal is a defensible operating decision, not memorizing a menu.

## Quick Self-Check

- How do enterprise, organization, repository, team, and individual permissions relate?
- When should a rule be enforced with a ruleset rather than documented as guidance?
- How do authentication and authorization solve different problems?
- What can administrators control for Actions without blocking useful automation?
- Which logs or metrics help distinguish a policy problem from a usage or reliability problem?

## Keep Current

Administration features and plan requirements change frequently. Confirm the
current domain weights, exam language, duration, and practice assessment on the
[official certification page](https://learn.microsoft.com/en-us/credentials/certifications/github-administration/)
before exam day.
