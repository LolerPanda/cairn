# Contributing to Cairn

Thank you for helping make long-running, multi-session work easier to recover and verify.

Cairn is a pattern language, not a runtime or orchestration product. Contributions should improve the clarity, portability, or practical use of its patterns without turning the repository into one particular implementation.

## Useful contributions

- Clarify a pattern that a new reader could misapply.
- Add a fictional, non-identifying example that works across tools.
- Improve a checklist or template while keeping its representation reader-defined.
- Fix broken links, rendering, accessibility, or translation drift.
- Propose a new failure class backed by more than one plausible instance.
- Report a collision between two terms or rules.

## Before opening an issue

Please check the [failure-mode catalog](docs/04-failure-modes.md) and [protocol skeletons](docs/07-protocol-skeletons.md) first. Describe the class of problem, not private details from the environment where you observed it.

A useful issue answers:

1. What repeatable failure or ambiguity did you observe?
2. Why is it not already covered?
3. What is the smallest pattern-level change that would help?
4. How could a reader in a different domain apply it?

## Privacy and provenance

Public examples must be synthetic or explicitly cleared for publication. Do not include:

- private names, organizations, project identifiers, or internal role names;
- local infrastructure paths, hostnames, credentials, or access tokens;
- real incident digests, private repository history, or unpublished measurements;
- text copied from a private workspace with identifiers removed.

When in doubt, reduce the example to placeholders and describe the class of failure. Sanitization is not permission to publish someone else's material.

## Pull request workflow

1. Fork the repository and create a focused branch.
2. Keep one conceptual change per pull request.
3. Update links or examples affected by the change.
4. Run the checks below.
5. Explain the problem, the pattern-level change, and any trade-offs in the pull request.

```sh
git diff --check

# Inspect changed Markdown links and placeholders.
git diff -- '*.md'
```

If a change adds a prescribed field, fixed status value, exact section count, or mandatory transport, explain why it is part of the pattern rather than one implementation choice.

## Writing style

- Lead with the failure or decision the reader faces.
- Prefer concrete, fictional examples over abstract claims.
- Use requirement language only when the distinction is load-bearing.
- Keep implementation choices as placeholders or clearly labeled examples.
- Use the terms defined in the [glossary](docs/03-glossary.md) consistently.
- Link to one authoritative explanation instead of repeating it in several files.

## Review criteria

A contribution is ready to merge when it is:

- pattern-level rather than project-specific;
- independently understandable without private context;
- consistent with the glossary and existing protocol skeletons;
- honest about what is required and what remains reader-defined;
- free of sensitive or identifying source material;
- linked from the appropriate public navigation surface.

Maintainers may ask for a narrower change, a more portable example, or evidence that a proposed rule addresses a recurring class rather than one incident.

## License

By contributing, you agree that your contribution will be licensed under the repository's [MIT License](LICENSE).
