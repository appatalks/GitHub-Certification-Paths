# GH-100 Weekly Tutoring Plan

This eight-lesson sequence is designed for weekly tutoring and self-directed
study. The learner drives each lesson: follow the documentation links, answer
the investigation questions, make and test a recommendation, then teach the
reasoning back to the tutor. There are no prescribed session lengths or time
allocations; take the time needed to understand and verify the material.

The tutor is an observer. Let the learner research, make decisions, and explain
them before offering a solution. Ask which source supports a claim or what
evidence would change a decision; give a hint only when requested or when the
learner is stuck.

There are no fixed calendar dates. Use the current [GH-100 study guide](https://aka.ms/GH100-StudyGuide)
as the source of truth for exam objectives, and confirm current details on the
[certification page](https://learn.microsoft.com/en-us/credentials/certifications/github-administration/).

These lesson plans focus on GitHub Enterprise Cloud (GHEC), including its
enterprise account types and data residency options. They are not a GitHub
Enterprise Server (GHES) administration course. Check the current exam guide
for all measured topics and supplement any GHES coverage it requires.

## Lesson Sequence

First complete [organization setup and sanitization](sandbox-setup.md). Use
your approved sandbox's sanitized inventory for real observations; keep the
supplied fictional records separate from findings about your organization.

| Lesson | Focus | Learner guide | Between-lesson practice | Question supplement |
| --- | --- | --- | --- | --- |
| 1 | GitHub model, identity, and access | [Lesson guide](lesson-01-identity-and-access/lesson-guide.md) | [Practice](lesson-01-identity-and-access/homework.md) | [15 questions](lesson-01-identity-and-access/practice-questions.md) |
| 2 | Enterprise environments | [Lesson guide](lesson-02-enterprise-environment/lesson-guide.md) | [Practice](lesson-02-enterprise-environment/homework.md) | [15 questions](lesson-02-enterprise-environment/practice-questions.md) |
| 3 | Governance and auditability | [Lesson guide](lesson-03-governance-and-auditability/lesson-guide.md) | [Practice](lesson-03-governance-and-auditability/homework.md) | [15 questions](lesson-03-governance-and-auditability/practice-questions.md) |
| 4 | Repository security and integrations | [Lesson guide](lesson-04-repository-security/lesson-guide.md) | [Practice](lesson-04-repository-security/homework.md) | [15 questions](lesson-04-repository-security/practice-questions.md) |
| 5 | GitHub Actions governance | [Lesson guide](lesson-05-actions-governance/lesson-guide.md) | [Practice](lesson-05-actions-governance/homework.md) | [15 questions](lesson-05-actions-governance/practice-questions.md) |
| 6 | Runners and secrets | [Lesson guide](lesson-06-runners-and-secrets/lesson-guide.md) | [Practice](lesson-06-runners-and-secrets/homework.md) | [15 questions](lesson-06-runners-and-secrets/practice-questions.md) |
| 7 | Monitoring and optimization | [Lesson guide](lesson-07-monitoring-and-optimization/lesson-guide.md) | [Practice](lesson-07-monitoring-and-optimization/homework.md) | [15 questions](lesson-07-monitoring-and-optimization/practice-questions.md) |
| 8 | Integrated capstone and exam readiness | [Lesson guide](lesson-08-capstone-and-exam-readiness/lesson-guide.md) | [Practice](lesson-08-capstone-and-exam-readiness/homework.md) | [15 questions](lesson-08-capstone-and-exam-readiness/practice-questions.md) |

## How to Use the Materials

### Exam Alignment

Reviewed against Microsoft's [official GH-100 study guide](https://learn.microsoft.com/en-us/credentials/certifications/resources/study-guides/gh-100)
on October 2, 2026. The guide identifies skills measured as of July 2026.
It is an exam skills outline, not an official rubric for grading these lessons.
Our completion checklists and questions are learning aids, not an exam score
prediction or a claim of complete exam preparation.

| Official domain | Weight | Lessons | Coverage and remaining study |
| --- | --- | --- | --- |
| Manage GitHub identities and access | 15-20% | 1, 3, 8 | Account models, organization/repository access, identity concepts, and access review. Supplement IdP selection/configuration, SAML/2FA enforcement, SCIM implementation, and enterprise teams; organization teams are not the full enterprise-team objective. |
| Administer GitHub Enterprise environment | 10-15% | 2, 3, 5, 7, 8 | Cloud account types, support triage, licensing questions, and development standards. Supplement GHES deployment comparison, support bundles/diagnostics, and deeper licensing/billing practice. |
| Implement secure software development and compliance | 25-30% | 3, 4, 7, 8 | Policy design, audit evidence, security response, app/PAT review, and API investigation. Supplement hands-on security configuration, security advisories, enterprise-wide data protection, and PAT/GitHub App rate-limit differences. |
| Manage GitHub Actions | 20-25% | 5, 6, 8 | Reuse and policy review, token permissions, runner selection/access, and secret scope. Supplement runner networking/IP allow lists, Azure private networking, external vault integration, and feature-specific administration. |
| Monitor and optimize GitHub usage | 10-15% | 2, 7, 8 | Synthetic audit/usage interpretation and evidence-based cost/capacity decisions. Supplement adoption/underused-feature analysis, diagnostic generation, and real metered-product reports in an authorized environment. |

The five domains are represented, but coverage is partial. The deliberate
Cloud-only scope excludes GHES administration practice; the official outline
does include GHES. Use the linked outline to track every individual objective
and plan additional study rather than treating eight completed lessons as full
coverage.

### Multiple-Choice Checkpoints

Each lesson also has a separate **15-question supplement**, for 120 additional
questions across the sequence. These mix concept recognition, scenario-based
decisions, troubleshooting, and choose-two questions. Answer keys are collapsed
below the questions, with explanations and source IDs that refer to the linked
official documentation in each file. Explain your choice and reject the
alternatives before opening the key; revisit sources for missed concepts.
These original practice sets do not reproduce exam weighting or guarantee
actual exam similarity, and do not replace the remaining objective/configuration
study identified above.

Each guide contains three original practice checkpoints interleaved with the
activities. They are not official exam questions, recalled live questions, or
copies of the practice assessment. Their count does not reproduce exam-domain
weighting or predict the exam's question formats.

1. Choose the stated number of answers before opening **Check your answer**.
2. Explain why your choice fits the facts and why the other options do not.
3. Read the answer explanation and follow its documentation reference.
4. If you missed it, record the concept and source to revisit, then explain the corrected reasoning in your teach-back.

- Each lesson guide supplies plain-language goals, a small glossary, fictional records to work with, numbered instructions, and a completion checklist. You do not need to invent your own company, workflow, or evidence.
- The homework file contains optional between-lesson study, practical work, spaced retrieval, and questions to carry forward.
- Recheck objective wording, feature availability, and plan-specific behavior in official sources while preparing each lesson.

### Start Each Lesson Here

1. Read **Goals** to see what you will learn. Read **Words to Know** before opening the documentation.
2. Copy **Your Starting Scenario** into your notes. These are the exercise facts; label anything else as an assumption or unanswered question.
3. Open the linked documentation. Look for the topic named in the question rather than trying to memorize the whole page. Record the section and link supporting your answer.
4. Follow **Work Through the Problem**, one numbered substep at a time. At each **Save** instruction, keep the requested diagram, table, or note.
5. Use **You Are Finished When** to check your work. If an item is missing, return to that step. Say what you tried before requesting a hint.
6. Explain your work in **Teach It Back**. The tutor listens first; use the sources and your evidence to answer follow-up questions.

The organization-based path uses an approved disposable Cloud sandbox with
personal GitHub accounts. Perform live tests only within the confirmed scope
and follow the [setup and cleanup instructions](sandbox-setup.md). A paper
exercise remains available where a feature, permission, or safe test identity
is missing. The EMU material is a comparison exercise, not a direction to change
the sandbox's account model or connect an identity provider. Expected test
results are predictions, not proof of a working configuration.

## Lab Safety

Use fictional organizations, identities, repositories, and data. Confirm the lab
platform, version, feature support, reset method, and cleanup before any hands-on
exercise. If the environment does not support a control, use the scenario or
worksheet in the lesson plan. Never use production credentials or real secrets.

## Certification Guide

Start with the [GitHub Administration (GH-100) study guide](../README.md) for
official references, exam domains, hands-on missions, and self-check questions.