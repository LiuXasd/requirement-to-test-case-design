---
name: requirement-to-test-case-design
description: Design structured, traceable, executable test cases from requirements and supporting documentation. Use when Codex needs to analyse requirements or DNG links, identify testability gaps and risks, ask focused clarification questions, define verification evidence, produce test objectives or test cases, classify test-case complexity as XS/S/M/L, or populate a user-provided Excel (.xlsx) test-case template. Apply across software, hardware, embedded, API, web, mobile, cloud, and system testing.
---

# Requirement-to-Test-Case Design

Transform supplied requirements and evidence into test cases that a tester can execute and assess. Do not merely restate requirements.

## Source authority and epistemic rules

Treat the explicit requirement as the highest authority. Use this order when sources disagree:

1. Requirement
2. Authoritative specification
3. Design or architecture documentation
4. Interface specification
5. User clarification
6. Existing test cases
7. Logs, examples, or observations
8. AI inference

Keep a concise fact register while working:

- **Known**: supported by an authoritative source.
- **Clarified**: supplied by the user and not in conflict with a higher source.
- **Inferred**: useful interpretation or risk; never treat it as required behaviour.
- **TBD**: unavailable information.
- **Conflict**: values that disagree, their sources, the authority decision, and impact.

Never silently invent required behaviour, timing, thresholds, state transitions, retries, error handling, logs, signal values, API responses, database values, or verification evidence. Mark unsupported items as `TBD`; ask only when the gap blocks a reliable test objective, action, expected behaviour, or pass/fail criterion.

When a lower-authority source conflicts with a requirement, retain the requirement for expected behaviour and record the conflict. Do not reinterpret a conflict as a requirement change.

## Intake and analysis

1. If no requirement is present, request it. Accept requirement IDs, user stories, feature descriptions, specification excerpts, or DNG links.
2. Access each supplied DNG link with the DNG authentication already configured in the environment. Do not request, reveal, copy, or store authentication tokens. Extract the item ID, title, requirement text, linked artifacts, and revision/baseline when visible. Keep the DNG URL and item ID in traceability. If access or retrieval fails, report the failure concisely and ask for an export or the relevant text; do not infer link content.
3. Once requirements are present, ask once whether supporting material should be considered before analysis. Accept DNG links/exports, documents, existing cases, interfaces, state/sequence diagrams, APIs, database schemas, logs, traces, signal definitions, configuration material, and defect history.
4. Analyse all supplied material before asking design questions. If later evidence arrives, assess its authority and impact on facts, conflicts, objectives, questions, coverage, and affected cases.
5. Extract a context model where supported: requirement ID/text, feature or module, actor, trigger, preconditions, inputs, outputs, constraints, states, interfaces, dependencies, configurations, failures, recovery, observability, and ambiguities. Label facts as known, inferred, ambiguous, conflicting, or TBD.
6. Assess testability: observable outcome, pass/fail rule, inputs, boundaries, timing, state transitions, failures, recovery, dependencies, interfaces, and configuration variants.
7. Select only relevant test dimensions: nominal, negative, boundary, state transition, sequence, timing, retry/recovery, error handling, interruption, interface, configuration, dependency, persistence/restart, concurrency, load/performance, compatibility, security, data integrity, diagnostics, end-to-end, fault injection, or degraded operation. Do not assume a domain, protocol, tool, or interface.

## Clarification protocol

Maintain a question history. Do not re-ask a question resolved by a source or explicitly answered as `Unknown`, `TBD`, `N/A`, or `Not Available`, unless new evidence changes its relevance.

Classify open questions:

- **Blocking** when a reliable objective, scenario, action, expected behaviour, or pass/fail criterion cannot be defined without the answer.
- **Non-blocking** when useful cases can proceed with a visible TBD.

Ask known blocking questions in one concise, grouped batch. Group by relevant headings, such as Preconditions, Trigger/Input, Expected Behaviour, Boundary/Timing, Failure/Recovery, Configuration, Interface/Dependency, or Known Risks. Tell the user they may answer `Unknown`, `TBD`, `N/A`, or `Not Available`.

After each answer, update the fact register and question history. Ask another batch only for newly discovered blocking questions. Stop when all blocking gaps are resolved, the user cannot provide the information, or only non-blocking gaps remain. Do not use clarification as a gate for progress.

## Design objectives and coverage

Generate objectives automatically once blocking questions are resolved or explicitly unavailable. Do not request approval solely to proceed.

Each objective must be meaningful, traceable to one or more requirements, and cover a distinct behaviour, condition, or risk. Merge semantic duplicates; retain separate objectives when setup, condition, expected behaviour, or verification purpose differs materially.

Aim for comprehensive, risk-based coverage rather than a minimal happy-path suite. For every applicable requirement clause, explicitly assess whether it needs:

- a positive/nominal case;
- a negative or invalid-input case;
- a failure case, including dependency, interface, resource, timeout, interruption, or error-handling failures when applicable;
- boundary cases at minimum/maximum values, just inside/outside a permitted range, empty/missing values, and capacity limits when applicable;
- corner cases created by meaningful combinations of states, inputs, configurations, timing, dependencies, or recovery paths.

Do not mechanically create every theoretical combination. Prioritise combinations with supported risk, a distinct outcome, a known defect pattern, an interface/state boundary, or a realistic misuse/failure mode. Do not invent unsupported limits, error responses, recovery behaviour, or expected results.

Maintain a compact coverage matrix per requirement or feature with `Positive`, `Negative`, `Failure`, `Boundary`, and `Corner/Combination` columns, marked `Covered`, `Not applicable`, `TBD`, or `Gap`. Check each relevant requirement clause and selected test dimension for coverage. Add an objective when the evidence supports it. Ask only if a missing dimension requires blocking information; otherwise record the limitation as TBD.

Before generating detailed cases, issue a **Potential omissions** reminder whenever a relevant dimension is not covered or cannot be assessed. State what appears missing, why it may matter, what information would enable coverage, and whether it is a confirmed gap or an evidence-limited TBD. Examples include unavailable boundary values, unspecified invalid inputs, absent timeout/retry rules, unclear failure handling, untested state combinations, dependency loss, persistence/restart behaviour, concurrency, permissions/security, or unsupported configurations. Do not label a dimension as missing merely because it is not relevant to the supplied context.

## Verification design

For each objective, separate:

- **Expected behaviour**: what the system is required to do, derived from authoritative information.
- **Expected result/evidence**: what the tester observes to establish that the behaviour occurred.

Identify meaningful verification points: output or state changes, interface transmissions, error detection, retry/recovery events, persistent data updates, timing boundaries, diagnostic state, UI changes, or measurements. Do not add expected results to setup-only steps without an observable requirement.

Ask a single grouped evidence question for objectives sharing the same observation. Possible sources include user-provided logs, traces, signals, network captures, API responses, database values, files, UI indications, diagnostic responses, hardware measurements, simulators, or tool outputs. Never invent an evidence source. When it remains unknown, use `Verification Source: TBD` and `Expected Evidence: TBD`; continue generating cases.

## Positive-flow reference, naming, and Excel template handling

Before generating detailed test cases, ask once whether the user can provide a positive/nominal flow for the feature as a reference. Explain that this may be a DNG link, existing positive test case, user journey, sequence diagram, API trace, or numbered process.

- If supplied, analyse it as supporting evidence, record its authority, and use it to clarify preconditions, action order, observable checkpoints, and terminology.
- Do not treat it as a replacement for the requirement or infer unmentioned required behaviour from it.
- If unavailable, continue with the authoritative requirements and mark any resulting non-blocking uncertainty as TBD.
- Do not repeat this request later unless newly supplied evidence makes the reference materially necessary.

Use a naming convention provided by the user. If none is provided and identifiers are needed, propose a readable provisional convention and label it `TBD naming convention`; do not block the design.

Before producing the final workbook, request the user's Excel (`.xlsx`) test-case template if one has not been supplied. If the user confirms that no template exists, generate a default, editable `.xlsx` template before populating it. The default template must include the applicable internal-schema fields as column headers, a clear title, readable formatting, frozen headers, filters, and a dedicated `Open Items` worksheet for TBDs, assumptions, conflicts, and potential omissions. Do not delay test-case design while waiting for the template; generate the internal cases first and then render them into the supplied or generated workbook.

When an Excel (`.xlsx`) test-case template is provided or generated:

1. Use the spreadsheet workflow to read the workbook and visually inspect each relevant worksheet before editing.
2. Identify the target worksheet, header row, tables/ranges, required columns, data validation, formulas, examples, merged cells, conditional formatting, and row/column formatting.
3. Map the internal case schema to the actual columns; do not assume a particular sheet name or column order.
4. Add cases without overwriting template formulas, validations, formatting, hidden support ranges, or example rows unless the template clearly designates them for replacement. Extend relevant formatting and validation to the added rows.
5. Save a new completed `.xlsx` output rather than overwriting the source template, unless the user explicitly asks to overwrite it.
6. Verify the finished workbook: inspect representative populated ranges, scan for formula errors where formulas exist, and visually render all populated worksheets to check clipping, wrapping, layout, and formatting.
7. Validate required cells, names, traceability, Priority, Test Level, step order, and visible TBD/conflict notes before delivering the output.

Use this internal schema as applicable, rendering only fields the template supports: Requirement ID, Test Case ID, Name, Module/Feature, Objective, Type, Preconditions, Environment, Data, Steps, Expected Behaviour, Expected Result, Verification Source, Expected Evidence, Postconditions, Priority, Test Level, Traceability, Assumptions, TBDs, and Notes.

## Case-writing rules

Write executable, ordered, reproducible cases. Include preconditions, setup, actions, expected results at meaningful verification points, evidence, and postconditions when supported. Phrase unsupported operational detail as TBD rather than fabricated instruction.

Assign a mandatory **Priority** to every test case. Use only `Low`, `Med`, `High`, or `Critical`. Assign it from the consequence of an undetected failure, user/business/safety/security impact, likelihood or change risk when evidence supports it, and the case's role in protecting essential functionality. Do not derive it from step count, execution time, or test-case complexity.

| Priority | Use for |
|---|---|
| Critical | Safety, security, data-loss, legal/compliance, system-availability, or release-blocking failures; or loss of an essential end-to-end capability with no acceptable workaround. |
| High | Core user or business functionality, high-impact interfaces, or failures likely to materially disrupt normal operation; a workaround may exist but is inadequate or costly. |
| Med | Important but non-core functionality, common error handling, or meaningful degradation with a reasonable workaround and limited impact. |
| Low | Cosmetic, infrequent, low-impact, or convenience behaviour; failure does not materially impair normal operation. |

When the impact is not supported by the requirements or supplied risk information, assign the best evidence-based priority and record `Priority rationale: TBD` rather than inventing impact. Preserve any user- or project-defined priority scheme when it is supplied; map it to these four values only when the user requests that mapping.

Assign **Test Level** independently from complexity, not elapsed duration:

| Level | Use for |
|---|---|
| XS | One simple condition, minimal setup/dependencies, one straightforward check. |
| S | A short, structured sequence with limited states and verification. |
| M | Multiple steps/states/verification points, tool coordination, dependencies, or recovery logic. |
| L | Multiple systems/interfaces, complex environment or transitions, end-to-end dependency chains, or extensive recovery/verification. |

## Final review and output

Before delivering, verify:

- Every case maps to a requirement and objective.
- Expected behaviour has authoritative support.
- Evidence is supplied or visibly marked TBD.
- Cases are executable without invented details and are not needless duplicates.
- Relevant dimensions and requirement clauses have been reviewed.
- Positive, negative, failure, boundary, and relevant corner/combination coverage has been assessed for every requirement or feature.
- Potential omissions are visible as confirmed gaps or evidence-limited TBDs, with a suggested next input where useful.
- DNG links used for source material retain their URL/item-ID traceability; inaccessible links are clearly identified.
- The user was offered one opportunity to provide a positive-flow reference before detailed cases were created.
- Naming, Priority, Test Level, and template requirements are satisfied.
- TBDs and conflicts are visible.

Provide a brief coverage and open-items summary alongside the cases, unless the supplied template is the sole requested deliverable. Include requirement IDs, coverage status, uncovered dimensions/reasons, TBDs, assumptions, and conflicts.
