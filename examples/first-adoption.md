# First adoption: recover one interrupted workflow

This fictional example shows a small Cairn adoption. It does not attempt to implement the whole framework.

## Starting condition

A three-role project runs across many sessions. Its current state is spread across conversation history, two editable progress files, and a folder of outputs.

After a session ends:

- the next operator asks which progress file is current;
- “done” sometimes means “assigned” and sometimes means “verified”;
- a reviewer approval cannot be found outside chat;
- the owner writes a fresh summary from memory.

The team checks 10 items in [Signs you need Cairn](../docs/02-signs-you-need-this.md). It chooses one goal for the first adoption:

> A cold-starting session should recover current state and verify the last completed stage without asking a person.

## Step 1 · Pick one authority

The team chooses one generated file as the cold-read surface:

```text
sample-suite/
├── state/
│   └── CURRENT.md          # generated view; never hand-edited
├── records/
│   └── events.ndjson       # append-only history
├── outputs/
│   └── stage-02/
├── handoffs/
└── checks/
    └── verify-current.sh
```

The event record and output directory are ground truth. `CURRENT.md` is a projection generated from them.

## Step 2 · Replace ambiguous status

The old summary said:

```text
Stage 2: done
Review: in progress
```

The new surface says:

```markdown
## Current stage

- FACT: `outputs/stage-02/result.json` exists.
- FACT: its digest matches the stage receipt.
- PENDING: independent review has been requested; no verdict receipt exists.
- UNKNOWN: whether the result satisfies the external comparison rule.
```

The workflow has not changed yet. Its claims have become inspectable.

## Step 3 · Add a handoff

The outgoing session copies [the handoff template](../templates/handoff-frontmatter.md) and records:

- the exact scope of the transfer;
- the generated `CURRENT.md` as the cold-read entry point;
- the stage receipt as completion evidence;
- the missing review verdict as `PENDING`;
- one next action: verify the stage and write a verdict artifact.

The handoff points to evidence instead of reproducing the whole project history.

## Step 4 · Make verification fail closed

The check compares claims rather than printing values for a human to inspect:

```sh
#!/bin/sh
set -eu

test -f outputs/stage-02/result.json
test -f outputs/stage-02/receipt.sha256

cd outputs/stage-02
shasum -a 256 -c receipt.sha256
```

If the output or receipt is missing, or the digest differs, the command exits non-zero. The effective state cannot remain “complete” merely because a progress file says so.

## Step 5 · Test the cold start

A new session receives only two instructions:

1. Read `state/CURRENT.md`.
2. Run `checks/verify-current.sh`.

It can now recover:

- what is directly evidenced;
- what is still pending;
- which source is authoritative;
- what action comes next;
- how to detect drift without asking a person.

## What this example did not add

The team did not adopt every Cairn artifact. It did not create a new platform, rename its roles, or standardize every document. It introduced one authority, one vocabulary, one handoff shape, and one check around the most expensive continuity failure.

That is enough for a first adoption. Re-run the diagnostic after the workflow has used the new surface in real session transitions, then add another pattern only if an observed failure justifies it.
