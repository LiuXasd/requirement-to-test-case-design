# Requirement-to-Test-Case Design

An engineering-focused Codex skill for turning requirements into structured, traceable, executable test cases.

It is designed for teams that need more than a happy-path test list: it analyses requirement quality, asks targeted clarification questions, identifies observable verification evidence, and highlights coverage gaps before producing cases in an Excel template.

## Capabilities

- Analyse requirements, supporting documentation, and DNG links.
- Preserve source authority, conflicts, assumptions, and TBD items.
- Use adaptive batch clarification ("Grill-Me") without repeatedly asking known-unavailable questions.
- Design positive, negative, failure, boundary, and risk-based corner/combination cases.
- Assign `Priority` (`Low`, `Med`, `High`, `Critical`) and independent test complexity (`XS`, `S`, `M`, `L`).
- Maintain requirement → objective → test-case traceability.
- Use configured DNG authentication without exposing tokens.
- Populate an existing Excel (`.xlsx`) template while preserving its structure, formulas, validation, and formatting; request one when missing, or generate a usable default template if none exists.
- Produce a coverage summary and a visible list of potential omissions, conflicts, and TBDs.

## Installation

Copy the `requirement-to-test-case-design` directory into your Codex skills directory:

```text
~/.codex/skills/requirement-to-test-case-design/
```

Restart or begin a new Codex turn after installing the skill.

## Example prompt

```text
Use $requirement-to-test-case-design to design test cases for this DNG requirement.
Use my Excel test-case template and make sure to cover positive, negative,
failure, boundary, and relevant corner cases.
```

## Repository layout

```text
.
├── README.md
└── requirement-to-test-case-design/
    ├── SKILL.md
    └── agents/openai.yaml
```

## Requirements

- Codex with custom skill support.
- DNG access configured in the environment when using DNG links.
- A user-provided `.xlsx` template when Excel output is requested.

## License

This project is available under the [MIT License](LICENSE).
