# Glossary

The vocabulary a raft-era suite's state descriptions must use. This is not a suggestion — it is a discipline. Ambiguity in status words is one of the mechanisms by which raft-era suites lose track of what is true.

## Nine status words

Use exactly these when describing the state of anything. Mixing categories is a defect, not a stylistic choice.

| Word | Means | What it excludes |
|---|---|---|
| `FACT` | Directly evidenced by a file, a check output, or a first-party confirmation | Interpretation; hearsay; consensus |
| `DECISION` | A binding choice made by an authorized party, recorded verbatim | Opinion; suggestion; proposal |
| `OBSERVATION` | The output of a read-only inspection this session | Historical claims; prior sessions' inspections |
| `INFERENCE` | A derivation that requires review before being acted upon | Fact; direct evidence |
| `PENDING` | Action started, final receipt missing | Complete; blocked; unknown |
| `BLOCKED` | Evidence or precondition is insufficient; work cannot proceed to next state | Pending; unauthorized |
| `DIAGNOSTIC_ONLY` | May be examined for troubleshooting; must not be cited as a formal result | Stable; releasable |
| `NOT_AUTHORIZED` | Explicitly refused by governance, regardless of technical readiness | Blocked; pending |
| `UNKNOWN` | The current session lacks evidence to classify | Any of the above |

**Prohibited compressions**: single words like "done", "in progress", "issue", "problem", "wip", "ok" — they collapse two or more of the above categories and let raft-era suites move on with unresolved state.

## Six one-vote-vetoes

These pairs get conflated. Every conflation observed has produced a real defect in a raft-era suite. Enforce the distinction mechanically wherever possible.

1. **Dispatched ≠ implemented.** A task assigned is not a task done, even if the state file says otherwise. Implementation is proven only by artifacts on disk that the dispatch demanded.

2. **Installed ≠ current.** A version present in the tree is not the version in use. Authority for "what version is current" belongs to exactly one source, and that source is not the same as "is this version present?"

3. **Workflow completed ≠ result valid.** That a pipeline ran end-to-end without erroring says nothing about whether its output is trustworthy. Result validity is a separate check.

4. **Delivery composed ≠ delivery integrated.** A package built and passing internal audit is not a package landed in the target. Integration is a separate gate.

5. **Internally reproducible ≠ externally comparable.** That two implementations of your scorer agree bit-for-bit says nothing about whether your protocol matches the external standard you claim to align with.

6. **Numbers match ≠ upstream verified.** That a table matches a source workbook says nothing about whether that workbook was itself produced by a trustworthy run.

Any status description that couples one side of these pairs with the other, without explicit adjudication, is by convention a defect. A raft-era suite that adopts this vocabulary immediately makes many of its previously-invisible ambiguities visible; several will refuse to remain both un-adjudicated and unspoken.

## Four evidence tiers

Every reference to evidence should carry a tier tag. Tiers exist because the same *shape* of artifact can be safe or unsafe depending on how it was produced.

| Tier | Definition | Permitted use |
|---|---|---|
| `STABLE` | Bytes in the archive match a manifest computed before the snapshot; independent verification passes | Formal recomputation, comparison, external reference |
| `RUNTIME_DRIFT_SNAPSHOT` | Bytes captured at archive time, differ from an earlier declared manifest (typically because a process was still writing) | Diagnostic only. Never as a formal result. Never mixable with STABLE in a summary |
| `UNVERIFIED` | Provenance or check missing; includes anything living in an ephemeral location such as a downloads folder, a temp directory, or a chat paste | Hint only. Must be promoted to a higher tier before citation |
| `SUPERSEDED` | Replaced by a later protocol or authority decision; retained for history | Historical trace only. Citations must name the replacement |

**Discipline**: a summary that mixes STABLE and RUNTIME_DRIFT_SNAPSHOT numbers is by convention a defect. UNVERIFIED can never be laundered into STABLE by an act of citation; it must be re-produced under the STABLE tier's conditions.

## Why this glossary is at layer 03

Because everything downstream — failure modes, protocol skeletons, discipline rules — assumes readers speak this vocabulary. A raft-era suite that skips glossary adoption will find failure modes look like isolated incidents rather than instances of a class.

## What this glossary does not do

- It does not name your roles, systems, or artifacts. `<system>`, `<role>`, `<suite>` remain placeholders.
- It does not tell you what tier tag your evidence deserves — that is your judgment against the tier definitions above.
- It does not enforce itself. A check script that refuses status descriptions outside this vocabulary is the reader's implementation choice; the framework provides only the vocabulary.
