# Lesson 4 Homework: Security Triage and App Review

**Suggested preparation for:** Lesson 5

## Study

- Review the repository security, security response, API access, GitHub Apps, OAuth Apps, and PAT objectives in the [current GH-100 study guide](https://aka.ms/GH100-StudyGuide).
- Work through the security and sensitive-data learning material linked from the guide.
- Note the difference between a detection signal, confirmed exposure, remediation, and evidence of closure.

## Practice

1. Open the [lesson guide](lesson-guide.md) and reuse DEP-1, SEC-1, CODE-1, APP-1, and AUTO-1.
2. Revisit Step 1's triage table. Add one source-backed question you had not considered for each detection finding.
3. Check the Step 2 simulated secret-response checklist. Explain why the placeholder needs no actual revocation, and what issuer evidence would matter in a real incident.
4. Revisit Step 3's integration review. Compare requested access with the supplied tasks and record any remaining app-model or policy unknowns.
5. Revisit Step 4's closure checks. Explain how you would distinguish an alert being closed from the underlying problem being fixed.

Use only `EXAMPLE_SECRET_DO_NOT_USE` as a placeholder if a sample value is needed. Never enter a real secret, PAT, or token into notes, chat, or a lab.

## Retrieval Practice

On three different days, explain the difference among dependency alerts, secret scanning, CodeQL, and security advisories. Then explain how you would narrow an app's permissions.

## Bring to Class

- The triage sheet.
- One case where more information is needed before declaring a finding true or resolved.