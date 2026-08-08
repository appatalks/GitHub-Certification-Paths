# Project Memory Starter

This files-only starter gives CESAR and reviewer a durable, portable format for
repository facts, decisions, handoffs, and certification research. It is
intentionally lightweight for this small Markdown study repository.

## Layout

```text
.agent-memory/
  records/
    <record-id>.md
  local/
```

Keep one durable fact, decision, handoff, or research result per record. Markdown
records are the authoritative source. Keep generated indexes, caches, and other
machine-local retrieval artifacts in `local/`.

The project should remain files-only until direct reading becomes slow or
unreliable. SQLite FTS5, vector retrieval, and graph retrieval are optional
derived layers and are not enabled by this starter.

## Record Contract

Start every record from [`record-template.md`](record-template.md). Record IDs
must be stable and unique, for example
`fact-certification-gh-600-20260807` or
`decision-milestone-numbering-20260807`.

Every material claim needs at least one primary source. For repository evidence,
record a file path and symbol or line reference together with the commit SHA or
explicit dirty-worktree state. For commands and checks, preserve the full
command, working directory, relevant versions or inputs, exit status, and
observed result. For external evidence, record the URL and retrieval date.
Label summaries and inferences explicitly; they are not primary evidence.

Relationships use globally unique IDs, stable target record IDs, and simple
predicates such as `supports`, `contradicts`, `supersedes`, `implements`, and
`depends-on`.

## Retrieval Contract

Any retrieval layer must return the evidence needed by the Context Integrity
Protocol: record and relationship IDs, primary sources, query and retrieval
mode, retrieval time, freshness, access limits, conflicts, omissions, failures,
and the exact claims returned with their confidence and classification.

Agents must read the primary record and verify its primary sources before relying
on a material claim. Retrieval narrows the search; it does not replace evidence
verification.

## Adoption Stages

1. **Files only**: Read records directly and link them in handoffs. This is the
   default for this project.
2. **SQLite FTS5**: Add a local lexical index only when the record volume makes
   direct reading slow. Keep Markdown authoritative.
3. **Semantic retrieval**: Add vectors only for demonstrated vocabulary mismatch,
   returning record IDs and source links with every result.
4. **Graph retrieval**: Add a graph store only for recurring multi-hop or
   entity-centric questions, derived from the same records and relationships.

Do not advance stages because the technology is available. Advance only when the
current stage cannot answer recurring questions accurately, quickly, or with
sufficient provenance.
