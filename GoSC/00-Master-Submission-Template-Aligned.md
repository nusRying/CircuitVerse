# GSoC 2026 Proposal (Template-Aligned Draft)

## 1) Personal Information
- Name: Umair
- Email: engr.umairejaz@gmail.com
- Timezone: PKT (UTC+5)
- GitHub: https://github.com/nusRying
- Resume/Portfolio: https://github.com/nusRying/CircuitVerse/blob/docs/proposal-final-links/GoSC/assets/Umair_Ejaz_Resume.pdf
- University/Current Status: Graduated

## 2) Organization and Project
- Organization: CircuitVerse
- Project Title: FSM to Circuit Synthesizer
- Project Idea: Project 3 (GSoC 2026 list)
- Preferred Project Size: 175 hours

## 3) Abstract / Synopsis
Finite State Machines (FSMs) are a core topic in digital logic, but students often struggle to convert state behavior into gate-level circuits correctly. CircuitVerse currently offers strong circuit design and simulation capabilities, but lacks an end-to-end FSM synthesis workflow.

This proposal adds an FSM-to-circuit synthesizer inside CircuitVerse. Users will define Moore or Mealy machines using a guided input workflow, and the system will generate equivalent, editable sequential circuits. The implementation prioritizes correctness, testability, incremental delivery, and compatibility with existing simulator data flow.

## 4) Problem Statement
- Manual FSM-to-circuit conversion is error-prone and time-consuming in educational workflows.
- Typical failure points include incorrect state encoding, transition mapping, and output logic.
- There is no built-in guided workflow in CircuitVerse for FSM definition and synthesis.

## 5) Why This Project Matters to CircuitVerse
- Improves educational value by bridging automata concepts to practical sequential circuit design.
- Reduces friction for educators creating FSM-based learning material.
- Produces editable generated circuits, preserving CircuitVerse’s learn-by-building philosophy.

## 6) Proposed Objectives
1. Implement a guided FSM definition workflow (MVP: structured/tabular input).
2. Support synthesis for Moore and Mealy machine models.
3. Generate CircuitVerse-compatible sequential circuits (flip-flops + combinational logic).
4. Add robust validation, tests, and documentation for maintainability.

## 7) Scope
### In Scope
- FSM schema/model for states, transitions, inputs, and outputs.
- Validation and normalization for deterministic FSM definitions.
- State encoding and truth-table derivation.
- Boolean equation generation (next-state and output logic).
- Mapping equations to CircuitVerse-compatible circuit structure.
- UI integration for define → validate → synthesize workflow.
- Unit/integration tests and developer/user documentation.

### Out of Scope (MVP)
- Full advanced graphical FSM editor with complex interactions.
- Heavy formal minimization for very large variable/state spaces.
- Non-FSM automata support (NFA/PDA/TM).

## 8) Technical Approach
### A. FSM Data Contract
Define a normalized model containing:
- machine type (`moore` or `mealy`),
- input alphabet and output symbols,
- states (including initial state metadata),
- transitions (with output semantics where applicable).

### B. Validation and Normalization Layer
- Enforce deterministic transitions and consistency constraints.
- Validate transition completeness for selected symbols.
- Return actionable validation errors before synthesis.

### C. State Encoding and Derivation
- Assign deterministic binary state codes.
- Derive truth tables for flip-flop input functions and output functions.

### D. Logic Generation
- Produce Boolean equations for next-state and output logic.
- Reuse existing combinational logic conventions/patterns where practical.

### E. Circuit Mapping and Integration
- Convert equations into gates + sequential elements.
- Ensure synthesized output is compatible with simulator load/edit flow.
- Keep generated circuits user-editable after synthesis.

## 9) Deliverables and Acceptance Criteria
1. **Synthesis MVP (Moore + Mealy)**
   - Acceptance: two benchmark FSMs (one Moore, one Mealy) synthesize and run correctly.
2. **Core Engine Modules**
   - Acceptance: parser, validator, encoder, generator, and mapper have test coverage for happy/edge cases.
3. **UI Workflow Integration**
   - Acceptance: user can define and synthesize FSM without manual JSON editing.
4. **Documentation**
   - Acceptance: contributor and user docs are complete and review-ready.

## 10) Measurable Success Metrics
- Moore/Mealy synthesis parity for MVP flows.
- CI green for all newly added tests.
- Reproducible correctness on benchmark FSM fixtures.
- Mentor sign-off at milestone demos.

## 11) Timeline (12 Weeks)
### Community Bonding (Weeks 1-2)
- Week 1: setup, architecture mapping, integration touchpoints, onboarding contribution.
- Week 2: design freeze for schema/module boundaries and UI interaction model.

### Coding Phase 1 (Weeks 3-6)
- Week 3: parser and validator.
- Week 4: state encoding and truth-table derivation.
- Week 5: equation generation for Moore/Mealy.
- Week 6: circuit mapping compatible with simulator flow.

### Midterm (Week 7)
- End-to-end MVP demo: define FSM → synthesize → run circuit.

### Coding Phase 2 (Weeks 8-11)
- Week 8: UI integration and validation UX.
- Week 9: integration hardening + baseline readability improvements.
- Week 10: parity stabilization, optional one-hot encoding.
- Week 11: test/reliability hardening and guardrails.

### Finalization (Week 12)
- Documentation, cleanup, final review iteration, handoff.

## 12) 175-Hour Budget Breakdown
| Workstream | Hours |
|---|---:|
| Setup, architecture mapping, design freeze | 15 |
| Parser and validator | 25 |
| State encoding and truth-table generation | 20 |
| Equation generation (Moore + Mealy) | 30 |
| Circuit mapping and simulator compatibility | 30 |
| UI integration and workflow polish | 25 |
| Testing and reliability hardening | 20 |
| Documentation and final handoff | 10 |
| **Total** | **175** |

## 13) Pre-proposal Contributions Plan
### Targets Before Final Review
- 3-5 high-quality PRs submitted.
- 1-2 PRs merged.
- At least 1 PR with meaningful tests.
- At least 1 PR directly relevant to Project 3 groundwork.

### Submitted PRs
- https://github.com/CircuitVerse/CircuitVerse/pull/7110
- https://github.com/CircuitVerse/CircuitVerse/pull/7111

### Contribution Themes
- Simulator/project data-flow test improvements.
- FSM-adjacent utilities (normalization/validation scaffolding).
- Documentation improvements for contributor onboarding and architecture clarity.

## 14) Risks and Mitigation
1. **Scope creep (UI + core engine):** lock MVP to tabular input + synthesis core; defer advanced editor.
2. **Algorithmic blow-up for larger FSMs:** enforce practical limits and complexity guardrails.
3. **Simulator integration mismatch:** use existing serialization patterns and fixture-based end-to-end checks.
4. **Late product decisions:** freeze schema/UX by Week 2 with mentor checkpoints.
5. **Test brittleness in graphical flows:** concentrate correctness in deterministic logic-layer tests.
6. **Upstream migration changes:** keep synthesis core modular and adapter-driven.
7. **Review delays:** submit small milestone-scoped PRs with clear validation evidence.

## 15) Contingency Plan
If schedule risk appears:
1. Preserve core deliverable: functionally correct Moore/Mealy synthesis pipeline.
2. Defer non-essential UX enhancements to stretch scope.
3. Prioritize tests and docs for all completed modules.
4. Publish revised timeline early with mentor agreement.

## 16) Communication Plan
- Weekly mentor update: completed work, blockers, next goals.
- Demo checkpoints at milestone boundaries.
- Immediate escalation when assumptions/dependencies change.

## 17) Why I Am a Good Fit
- Strong alignment with digital logic learning outcomes and product goals.
- Execution plan emphasizes incremental delivery, maintainability, and testability.
- Pre-proposal strategy demonstrates initiative through relevant, measurable contributions.

## 18) References
- CircuitVerse GSoC 2026 Project List (Project 3)
- CircuitVerse setup and contribution documentation
