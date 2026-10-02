# GitHub Copilot (GH-300)

<p align="center"><img src="../../assets/copilot-splash.png" alt="GitHub Copilot certification path" width="100%"></p>

GH-300 is about using Copilot effectively and responsibly across the developer
workflow. Learn the features, but spend equal time on context, verification,
privacy, policy, and the limits of generated output. The best answer is rarely
"accept the suggestion"; it is "use the right context, then inspect the result."

## Start Here

- [Official certification page](https://learn.microsoft.com/en-us/credentials/certifications/github-copilot/): current exam details, policies, and registration.
- [GH-300 study guide](https://aka.ms/GH300-StudyGuide): skills measured and preparation references.
- [GitHub Learn catalog](https://learn.github.com/certification/COPILOT): official GitHub learning catalog; sign-in may be required.
- [GitHub Copilot Fundamentals](https://learn.microsoft.com/en-us/training/paths/copilot/): Microsoft Learn modules covering responsible use, prompting, environments, management, and productivity.
- [GitHub Copilot Fundamentals Part 2](https://learn.microsoft.com/en-us/training/paths/gh-copilot-2/): continuation of the official Microsoft Learn preparation path.
- [GitHub Copilot documentation](https://docs.github.com/en/copilot): current features, concepts, administration, and responsible-use guidance.
- [Official practice assessment](https://learn.microsoft.com/en-us/credentials/certifications/github-copilot/): open the practice assessment from the certification page after studying.

## What to Know

The official GH-300 study guide lists these six weighted skill areas. The single
features domain includes distinct subsections for IDE and CLI use, broader
Copilot capabilities, and organization-wide settings and policies:

1. **Use GitHub Copilot responsibly (15-20%):** verify output, understand limitations, protect data, and apply human judgment.
2. **Use GitHub Copilot features (25-30%):** IDE and CLI use, inline suggestions, Chat, agent mode, sessions, code review, Spaces, Spark, pull request summaries, customization, sub-agents, audit logs, subscriptions, and organization-wide feature policies.
3. **Understand GitHub Copilot data and architecture (10-15%):** data usage, flow and sharing, input processing, prompt building, suggestion lifecycle, and limitations.
4. **Apply prompt engineering and context crafting (10-15%):** clear goals, relevant files, constraints, examples, zero-shot and few-shot prompting, and iterative task decomposition.
5. **Improve developer productivity with GitHub Copilot (10-15%):** generation, refactoring, documentation, testing, learning, modernization, quality, and security workflows.
6. **Configure privacy, content exclusions, and safeguards (10-15%):** privacy settings, exclusions, public-code matching controls, ownership, and troubleshooting.

Read [prompt engineering](https://docs.github.com/en/copilot/concepts/prompting/prompt-engineering),
[best practices](https://docs.github.com/en/copilot/get-started/best-practices),
[code referencing](https://docs.github.com/en/copilot/concepts/completions/code-referencing),
and [content exclusion](https://docs.github.com/en/copilot/concepts/context/content-exclusion)
as one connected topic: better context improves usefulness, while governance
defines what context Copilot may access.

## Hands-On Missions

### Mission 1: Prompt Lab

Ask Copilot to explain, test, and refactor the same small function three ways:
with a vague prompt, a prompt containing constraints, and a prompt that names
the relevant files and acceptance criteria. Compare correctness, omissions, and
follow-up questions.

### Mission 2: Verify the Pair Programmer

Generate a change and a test. Inspect the diff, run the test, check dependencies
and security assumptions, and look for code references. Practice explaining why
human review remains necessary even when the output looks polished.

### Mission 3: Set the Boundary

Read [repository custom instructions](https://docs.github.com/en/copilot/how-tos/copilot-on-github/customize-copilot/add-custom-instructions/add-repository-instructions)
and content exclusion guidance. Draft a small policy describing allowed data,
excluded content, review expectations, and what users should do when Copilot's
answer conflicts with project rules.

## Quick Self-Check

- How do inline suggestions, Chat, CLI, code review, and agentic features differ?
- What context can improve a response, and what context should be excluded?
- Why can a generated answer be plausible yet still unsafe or incorrect?
- What is code referencing, and why does it matter during review?
- Which controls are personal settings, repository instructions, organization policies, or enterprise governance?

## Keep Current

Copilot plans, models, features, and policies move quickly. Confirm the current
domains, exam duration, languages, and practice assessment on the [official
GH-300 page](https://learn.microsoft.com/en-us/credentials/certifications/github-copilot/)
before exam day.
