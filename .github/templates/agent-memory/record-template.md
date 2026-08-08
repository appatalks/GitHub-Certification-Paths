---
id: <stable-record-id>
kind: fact | decision | handoff | research
status: active | superseded | disputed
created: <YYYY-MM-DD>
updated: <YYYY-MM-DD>
confidence: <0-100>
tags: []
relations:
  - id: <globally-unique-relation-id>
    predicate: <supports | contradicts | supersedes | implements | depends-on>
    target: <record-id>
sources:
  - id: source-1
    type: repository | test | command | url
    reference: <path and symbol/lines, command, or URL>
    retrieved: <YYYY-MM-DD or ISO-8601 timestamp>
    freshness: <current | dated | unknown>
    revision: <commit SHA, dirty-worktree description, content hash, or N/A>
    execution:
      command: <full command or N/A>
      cwd: <working directory or N/A>
      inputs: <relevant versions, arguments, or environment constraints>
      exit_status: <integer or N/A>
      result: <observed result or durable output path>
retrieval:
  - id: <retrieval-id>
    mode: direct | full-text | vector | graph
    query: <query or retrieval scope>
    retrieved: <ISO-8601 timestamp>
    record_ids: []
    relation_ids: []
    freshness: <current | dated | unknown>
    limitations: <access limits, omissions, conflicts, or failures>
---

# <Record Title>

## Claims

- **Fact | Summary | Inference**: <claim> (primary source: `source-1`; retrieval: `<retrieval-id or none>`; confidence: <0-100>)

## Scope And Gaps

- **Scope**: <what this record covers>
- **Gaps**: <unknowns, omitted context, conflicts, or `none known`>

## Supersession Notes

<What would make this record stale, and which record replaces it when applicable.>
