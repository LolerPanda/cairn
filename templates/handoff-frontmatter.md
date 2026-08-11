# Handoff frontmatter

Use this template when work must cross a session, tool, machine, or audience boundary. It gives the receiver five facts before asking them to trust the body.

The field names and serialization format are adaptable. The semantics are not: identity, scope, time, shape, and verification must all be present.

## Copyable template

````markdown
---
anchor_sha: <detached SHA-256 of this file; exclude this anchor_sha line>
scope: <one sentence describing exactly what this handoff transfers>
date: <ISO-8601 date or timestamp, including timezone>
format_id: <stable handoff shape name and version>
verify_status: <independent verification instructions, or "author statement only">
---

# <handoff title>

## Current outcome

<What is true now? Use FACT, DECISION, OBSERVATION, INFERENCE, PENDING,
BLOCKED, DIAGNOSTIC_ONLY, NOT_AUTHORIZED, or UNKNOWN deliberately.>

## Evidence

| artifact | identity | proves | verification |
|---|---|---|---|
| `<path-or-id>` | `<full digest, version, or receipt>` | `<claim>` | `<command or method>` |

## Decisions and boundaries

- DECISION: <binding choice and its authority>
- NOT_AUTHORIZED: <actions the receiver must not take>
- UNKNOWN: <important question that remains unresolved>

## Next action

<One checkable next action, or an honest statement that several actions remain.>

## Verification

```sh
<commands that fail with a non-zero exit status when a load-bearing claim is false>
```
````

## Detached anchor

Placing a file's final digest inside the bytes covered by that digest creates a self-reference. A detached anchor avoids the loop by excluding only the first `anchor_sha:` line from the digest.

One POSIX-oriented verification shape is:

```sh
handoff=<path-to-handoff>

expected=$(awk '/^anchor_sha:/{print $2; exit}' "$handoff")
actual=$(
  awk 'BEGIN{removed=0} /^anchor_sha:/ && !removed {removed=1; next} {print}' "$handoff" \
    | shasum -a 256 \
    | awk '{print $1}'
)

test "$actual" = "$expected"
```

On systems with `sha256sum`, replace `shasum -a 256` with `sha256sum`.

## Quality checks

Before sending a handoff, verify that:

- every load-bearing claim has a file, receipt, or reproducible check;
- commands compare actual values with expected values rather than merely printing them;
- a failed check exits non-zero;
- paths, identifiers, and digests required for verification are complete;
- facts, decisions, inferences, and unknowns are not blended together;
- the receiver's authority and stop conditions are explicit;
- the handoff points to sources of truth instead of copying their full contents.

See [PS-01 · Handoff frontmatter](../docs/07-protocol-skeletons.md#ps-01--handoff-frontmatter) for the underlying pattern.
