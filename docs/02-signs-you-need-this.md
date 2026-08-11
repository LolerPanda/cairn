# Signs you need Cairn

Cairn is useful when a long-running project can make progress inside one session but cannot reliably explain or resume that progress in the next one. This checklist helps you distinguish an isolated documentation problem from a structural continuity problem.

Check every statement that is true today. Answer from evidence, not from what the workflow is intended to do.

## Continuity

- [ ] A new session needs a human to reconstruct context from memory.
- [ ] The most accurate project state exists in conversation history rather than a durable artifact.
- [ ] Switching tools or machines causes completed reasoning to be repeated.
- [ ] Handoffs grow longer over time but still omit decisions that later turn out to matter.

## State and authority

- [ ] More than one file can answer “what is current?” and they sometimes disagree.
- [ ] A status can say “done” even when the required output is absent.
- [ ] People use words such as “done,” “in progress,” or “blocked” without shared definitions.
- [ ] Readers cannot tell whether a value is observed, inferred, decided, or still unknown.

## Handoffs and ownership

- [ ] Different roles invent different handoff formats for the same underlying facts.
- [ ] The next action is selected from chat rather than from an inspectable queue.
- [ ] Work stops because a human owner is unavailable, even when the action was meant to be delegable.
- [ ] A role's definition of done is understood socially but not written as checkable evidence.

## Evidence and review

- [ ] An approval or rejection exists only as a message.
- [ ] A workflow completing successfully is treated as proof that its result is valid.
- [ ] Files are hashed or archived while another process may still be writing them.
- [ ] A copied path, digest, timestamp, or version has failed because of manual transcription.

## Read the result

This is a diagnostic, not a maturity score.

| Checked | Interpretation | Start here |
|---:|---|---|
| 0–3 | Mostly local friction | Fix the specific process; adopting the full framework may be unnecessary. |
| 4–7 | Continuity is at risk | Adopt one shared vocabulary and one handoff shape, then reassess. |
| 8–12 | The workflow is structurally session-bound | Establish a cold-read surface, one authority per fact, and explicit evidence tiers. |
| 13–16 | The workflow is firmly in its raft-era | Treat continuity as architecture, not documentation cleanup. |

Regardless of the total, any of these deserves immediate attention:

- an approval that exists only in chat;
- two writable authorities for the same fact;
- completion claimed without the required artifact;
- evidence captured from a tree that was still changing.

## Choose one first move

Do not redesign the whole workflow at once. Pick the row that matches the most expensive failure you checked.

| If your main problem is… | First move | Related material |
|---|---|---|
| status ambiguity | Adopt the shared status words | [Glossary](03-glossary.md) |
| declared progress without artifacts | Derive completion from evidence | [FM-01 · Phantom progress](04-failure-modes.md#fm-01--phantom-progress) |
| competing current-state files | Name one authority and make all other views derived | [FM-02 · Dual authoritative sources](04-failure-modes.md#fm-02--dual-authoritative-sources-for-the-same-fact) |
| session restart cost | Create one cold-read surface | [PS-02 · Cold-read surface](07-protocol-skeletons.md#ps-02--cold-read-surface-current-file) |
| inconsistent handoffs | Start with shared frontmatter | [Handoff template](../templates/handoff-frontmatter.md) |
| decisions waiting on a person | Create a durable owner queue | [PS-03 · Owner decision queue](07-protocol-skeletons.md#ps-03--owner-decision-queue) |

For a small worked adoption, continue to [First adoption example](../examples/first-adoption.md).

## What this checklist does not prove

A high count does not prove that every Cairn pattern fits your workflow. A low count does not prove that the workflow is safe. The checklist surfaces questions; the files, checks, and receipts in your own environment determine what is true.
