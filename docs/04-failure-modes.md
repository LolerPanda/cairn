# Failure modes

Twelve failure classes observed across independent raft-era suites. Each is presented at pattern level: trigger, symptom, root cause, direction of repair. Concrete code, tools, or project names are **deliberately absent**; the reader picks their own instrument.

Reading order matters: the earlier classes are more common and cheaper to fix; the later classes are structural and require design work.

---

## FM-01 · Phantom progress

**Trigger**: A machine-writable state file records the transition to a later stage, but the artifacts that stage was defined to produce are not on disk.

**Symptom**: State says "in progress" or "done"; filesystem says "never started". Later stages depend on the earlier stage's artifacts and fail without an obvious cause.

**Root cause**: The state file is treated as authoritative for stage transitions, and no mechanism computes stage state from disk.

**Repair direction**: Stage state must be derived from filesystem evidence, not from the state file. The state file may record dispatches; it must not be trusted for completions. A check surface computes effective stage from disk existence + acknowledgment file presence, and flags divergence.

---

## FM-02 · Dual authoritative sources for the same fact

**Trigger**: Two files, symlinks, or fields claim to answer the same question ("what version is current?", "what is the latest ledger row?").

**Symptom**: Readers pick one, actors update the other, and drift accumulates silently until a specific operation fails on the mismatch.

**Root cause**: No governance decision picked exactly one authority. Both are updateable; both are read.

**Repair direction**: For every fact, pick exactly one authoritative source. Declare all others as `derived-never-authoritative`. A check surface asserts that any assertion about the fact matches the one authority.

---

## FM-03 · Hash-then-write drift

**Trigger**: A manifest is computed over files that a process is still writing.

**Symptom**: The manifest and the archive disagree; independent verification fails. Attempts to "update the expected hash" resolve the symptom but hide the cause.

**Root cause**: Order of operations. Correct order is: complete writes → snapshot to immutable staging → hash the staging → archive the staging. Incorrect order is: hash the active tree → keep running → archive.

**Repair direction**: Snapshot before hash. A run-complete sentinel (a file the process writes only after it stops writing outputs) gates the hasher. Never update expected hashes to match drifted evidence.

---

## FM-04 · Silent scope creep in archives

**Trigger**: An archive is built by a rule like "everything under this path" or "everything matching this pattern".

**Symptom**: The archive is orders of magnitude larger than intended. Investigation shows the selector was interpreted more broadly than the author expected; large weights, logs, or caches were swept in.

**Root cause**: Selection by keyword or path membership, without file-type allowlist, per-file size limit, or total budget.

**Repair direction**: Allowlist file types; cap per-file size; declare a total budget; dry-run before archiving; refuse to archive if the dry-run exceeds budget.

---

## FM-05 · Manual value transcription

**Trigger**: A hash, path, package name, timestamp, or commit hash is copied by a human from one document, chat, or terminal into another.

**Symptom**: A single-character transcription error cascades; downstream verification fails on a value that "looks right".

**Root cause**: Any human-in-the-loop for machine-produced values.

**Repair direction**: Ban hand-transcription as a discipline. Machine-produced values travel in machine-readable manifests that are automatically discovered by receivers. Chat and prose carry pointers to those manifests, never values.

---

## FM-06 · Verdicts living only in chat

**Trigger**: An external audit or approval is delivered as a message in a chat session.

**Symptom**: When the chat session ends or is compacted, the verdict text is unrecoverable. The state file may record a summary, but the reasoning is gone.

**Root cause**: No discipline that verdicts must exist as files with content-addressed identity before they count.

**Repair direction**: Adopt "a verdict is not a verdict until it exists as a file with a hash". Chat and paste remain the *transport*; a file is the *record*. Check surfaces refuse to accept "approved" or "rejected" in logs without a companion file path.

---

## FM-07 · Cold-start context loss

**Trigger**: A session ends. A new session (same or different framework/tool) tries to continue.

**Symptom**: The new session cannot recover working state without a human writing a multi-page handoff document from memory. Handoffs proliferate, drift from truth, and take hours to author.

**Root cause**: State lives in conversation history, not in files. There is no single cold-read surface that summarizes the situation.

**Repair direction**: One file per suite acts as the cold-read surface, machine-regenerated from ground truth. The new session reads exactly that file plus whatever the file explicitly points to. Nothing else.

---

## FM-08 · Handoff format babel

**Trigger**: Multiple audiences (auditors, operators, orchestrators, human overseers) each get a differently-shaped handoff.

**Symptom**: Every new audience produces a new format. Cross-referencing across handoffs requires human translation. New authors reinvent the format each time.

**Root cause**: Attempting to unify presentation format across audiences with genuinely different needs.

**Repair direction**: Do not unify format; unify **fact base**. A single fact-base document is authoritative; every handoff, in whatever format its audience needs, begins by citing the fact-base path and its content-hash. Machine frontmatter carries the citation.

---

## FM-09 · Same-name skill drift

**Trigger**: A skill, playbook, or template is copied to serve a second framework/environment, then diverges over time.

**Symptom**: Same-named artifact runs different logic under different frameworks. Behavior depends on which framework loaded first.

**Root cause**: No source of truth; both trees are edited independently.

**Repair direction**: Declare one authoritative tree. Other trees are symlinks or generated copies. A check surface asserts that same-named artifacts have identical content across trees, or that non-authoritative trees carry a "generated from X" header.

---

## FM-10 · Circular hash

**Trigger**: A frozen "final" document is defined to record hashes that include the document's own final hash.

**Symptom**: `H = SHA256(prefix || body_that_contains(H))` has no solution. The document cannot be closed.

**Root cause**: Coupling a finalization record's identity to its own hash.

**Repair direction**: Detached finalization. The finalization record contains only append-before-self hashes. A separate, independently-signed document (or an out-of-band checksum file) records post-append hashes. Neither self-signs.

---

## FM-11 · Frozen document with stale citation

**Trigger**: A frozen document cites the hash of an append-only log at some moment; the log is later legitimately appended to.

**Symptom**: A reader comparing the cited hash against the current log sees mismatch and suspects tampering. Every future append renews the alarm.

**Root cause**: Treating "cited hash matches current hash" as an integrity criterion for an append-only log.

**Repair direction**: The integrity criterion for an append-only log is **chain continuity** (each row's prior hash matches the previous row's post hash, and the newest post matches the file's current bytes), not equality with any frozen document's citation. Written adjudications should carry a rule stating "frozen citations record a moment; appends are expected".

---

## FM-12 · Selection bias in own audit

**Trigger**: A design is evaluated only by its author or originating session, without independent review.

**Symptom**: The self-audit accepts patterns whose only justification is that the designer built them. Convergence appears where it is really author bias.

**Root cause**: Author and auditor are the same session.

**Repair direction**: The methodology called *failure-mode census* (see `docs/08-methodology.md`) is the honest form: enumerate concrete recorded incidents, then ask, for each candidate rule or interface, whether it mechanically prevents that incident. If an incident was caused by *absence* of the rule, the rule earns its place. Rules that appear in the design without an incident to justify them are marked speculative and demoted.

---

## What to do with this catalog

- **Read all twelve** before designing. Half the effort of a raft→next-iteration migration is recognizing which failures your suite currently exhibits.
- **Grade each against your own suite**. For each: present (Y/N), severity, whether an existing check catches it. Absent classes are candidates to guard against preemptively; present classes are your migration priority.
- **Do not repair speculatively**. Repair fires an incident cost you observed; guarding against imagined incidents is the exact pattern FM-12 warns against.
- **Add to the catalog as you observe**. This is v0.1. Every class here was distilled from an observed instance somewhere; new classes are welcome, provided each carries at least one non-hypothetical trigger.
