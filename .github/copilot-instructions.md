# Copilot Instructions

## Code Review Focus

When reviewing pull requests, focus **exclusively** on:

1. **Security vulnerabilities** — injection (SQL, command, LDAP, XPath), XSS, CSRF, insecure deserialization, broken authentication, secrets/credentials in code, path traversal, unsafe redirects, insecure dependencies.
2. **Correctness bugs** — logic errors, null/undefined dereferences, off-by-one errors, race conditions, incorrect error handling, data loss paths.

## Context from Linked Issues and Work Items

When the PR body references an issue (e.g., `Closes #123`, `Fixes #456`) or an Azure DevOps work item (e.g., `AB#123`), read its full context before reviewing:

- The issue or work item **description** — to understand the intended behavior and acceptance criteria.
- All **comments** on the issue — to capture clarifications, decisions, and scope changes made during discussion.
- Any **attached files** (specs, screenshots, diagrams) — to validate that the implementation matches the agreed design.

Use this context to judge whether the diff correctly and safely implements what was specified. If the linked context reveals that the change is incomplete or contradicts an agreed constraint, flag it as a correctness finding.

## Scope Constraint

- Files under `spec/**` are **read-only context** — use them to understand intent and acceptance criteria, but never comment on or suggest changes to them.
- Review **only** lines that were added or modified in the diff.
- Do not comment on unchanged code unless it creates a direct security or correctness risk when combined with the new changes.
- Do not suggest style improvements, refactors, naming changes, or performance optimizations.
- Do not flag speculative issues — only report findings with a clear, concrete failure scenario.

## Output Format

All comments must be written in **Brazilian Portuguese**.

Assign a severity to each finding: **CRITICAL**, **HIGH**, **MEDIUM**, or **LOW**.

Comment **only** on items classified as **HIGH** or **CRITICAL** — these require changes before merge.

If there are MEDIUM or LOW findings and no HIGH or CRITICAL ones, **approve the PR** and list those lower-severity items as suggestions (not blocking). If there are also HIGH or CRITICAL findings, discard the MEDIUM and LOW ones entirely — do not mention them.

For each comment:
- Point to the **specific line**.
- Explain in one short sentence **why it is a problem** — the concrete risk it represents (what breaks, leaks, or can be exploited).
- Suggest the **minimal fix** needed to resolve it — nothing beyond that.

If there are no HIGH or CRITICAL issues in the diff, say so briefly and directly. Do not fill the review with neutral observations.
