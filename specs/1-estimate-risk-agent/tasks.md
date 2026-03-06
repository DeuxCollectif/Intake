# Tasks: Chief Estimator Risk Agent

**Input**: Design documents from `/specs/1-estimate-risk-agent/`
**Prerequisites**: `plan.md` (required), `spec.md` (required for user stories), `research.md`, `data-model.md`, `contracts/`

**Tests**: Scenario-based prompt validation and output contract conformance review are included because they are explicitly required in `specs/1-estimate-risk-agent/plan.md`.

**Organization**: Tasks are grouped by user story to enable independent implementation and testing of each story.

## Format: `[ID] [P?] [Story] Description`

- **[P]**: Can run in parallel (different files, no dependencies)
- **[Story]**: Which user story this task belongs to (`US1`, `US2`, `US3`)
- Include exact file paths in descriptions

## Phase 1: Setup (Shared Infrastructure)

**Purpose**: Ensure repository artifacts and feature documentation structure are in place for implementation and validation.

- [ ] T001 Confirm feature artifact structure in `specs/1-estimate-risk-agent/plan.md`
- [ ] T002 Create pilot validation directory `specs/1-estimate-risk-agent/validation/`
- [ ] T003 [P] Create executive output rubric in `specs/1-estimate-risk-agent/validation/executive-rubric.md`
- [ ] T004 [P] Create comparator-fit scoring guide in `specs/1-estimate-risk-agent/validation/comparator-fit-guide.md`

---

## Phase 2: Foundational (Blocking Prerequisites)

**Purpose**: Establish shared contracts, schema assumptions, and baseline evaluation rules used by all user stories.

**⚠️ CRITICAL**: No user story work should begin until this phase is complete.

- [ ] T005 Define SharePoint historical record required metadata map in `specs/1-estimate-risk-agent/validation/sharepoint-metadata-map.md`
- [ ] T006 [P] Define value-band and geolocation normalization rules in `specs/1-estimate-risk-agent/validation/normalization-rules.md`
- [ ] T007 [P] Define confidence-level rubric (low/medium/high) in `specs/1-estimate-risk-agent/validation/confidence-rubric.md`
- [ ] T008 Align output contract fields with risk categories in `specs/1-estimate-risk-agent/contracts/risk-briefing-contract.yaml`
- [ ] T009 Establish non-fabrication and data-gap disclosure checklist in `specs/1-estimate-risk-agent/validation/data-integrity-checklist.md`
- [ ] T010 Create baseline acceptance test scenarios from quickstart in `specs/1-estimate-risk-agent/validation/scenario-tests.md`

**Checkpoint**: Foundation ready. User story implementation can begin.

---

## Phase 3: User Story 1 - Generate Risk Briefing (Priority: P1) 🎯 MVP

**Goal**: Produce a complete executive-ready five-section risk briefing using filtered historical comparables.

**Independent Test**: Run one complete project input through the prompt and verify all five required sections, evidence-backed risks, and confidence statement are present.

### Implementation for User Story 1

- [ ] T011 [US1] Refine mission, input, filtering, and output instructions in `.github/agents/chief-estimator-risk.agent.md`
- [ ] T012 [P] [US1] Add explicit required input capture placeholders in `.github/prompts/estimate-risk-from-sharepoint.prompt.md`
- [ ] T013 [P] [US1] Add risk evidence and likelihood/impact completion checks in `specs/1-estimate-risk-agent/validation/executive-rubric.md`
- [ ] T014 [US1] Add sample-size and confidence reporting rules in `.github/agents/chief-estimator-risk.agent.md`
- [ ] T015 [US1] Add contingency posture guidance criteria in `.github/agents/chief-estimator-risk.agent.md`
- [ ] T016 [US1] Document MVP run procedure and expected output shape in `specs/1-estimate-risk-agent/quickstart.md`
- [ ] T017 [US1] Execute and capture MVP pilot result notes in `specs/1-estimate-risk-agent/validation/us1-pilot-results.md`

**Checkpoint**: User Story 1 is independently functional and reviewable.

---

## Phase 4: User Story 2 - Handle Incomplete Data Gracefully (Priority: P2)

**Goal**: Ensure the workflow continues in best-effort mode with explicit assumptions and data gaps when data is partial or inaccessible.

**Independent Test**: Run a scenario with intentionally missing comparator fields and verify the output still provides ranked risks while explicitly listing assumptions/data gaps.

### Implementation for User Story 2

- [ ] T018 [US2] Add partial-access fallback logic instructions in `.github/agents/chief-estimator-risk.agent.md`
- [ ] T019 [P] [US2] Add missing-data prompt guardrails in `.github/prompts/estimate-risk-from-sharepoint.prompt.md`
- [ ] T020 [P] [US2] Add incomplete-data scenario cases in `specs/1-estimate-risk-agent/validation/scenario-tests.md`
- [ ] T021 [US2] Add data-gap disclosure acceptance criteria in `specs/1-estimate-risk-agent/validation/data-integrity-checklist.md`
- [ ] T022 [US2] Capture fallback-mode pilot run evidence in `specs/1-estimate-risk-agent/validation/us2-pilot-results.md`

**Checkpoint**: User Story 2 is independently functional and reviewable.

---

## Phase 5: User Story 3 - Executive Presentation Readiness (Priority: P3)

**Goal**: Ensure output is concise, business-focused, and ready for steering-committee presentation.

**Independent Test**: Review generated output against the executive rubric and confirm it is scannable, non-technical, and understandable in under 5 minutes.

### Implementation for User Story 3

- [ ] T023 [US3] Refine style and tone constraints for executive audience in `.github/agents/chief-estimator-risk.agent.md`
- [ ] T024 [P] [US3] Add no-table-by-default enforcement language in `.github/prompts/estimate-risk-from-sharepoint.prompt.md`
- [ ] T025 [P] [US3] Add executive readability scoring criteria in `specs/1-estimate-risk-agent/validation/executive-rubric.md`
- [ ] T026 [US3] Add sponsor-review walkthrough steps in `specs/1-estimate-risk-agent/quickstart.md`
- [ ] T027 [US3] Capture executive dry-run feedback in `specs/1-estimate-risk-agent/validation/us3-pilot-results.md`

**Checkpoint**: User Story 3 is independently functional and reviewable.

---

## Phase 6: Polish & Cross-Cutting Concerns

**Purpose**: Final consistency, traceability, and launch readiness across all stories.

- [ ] T028 [P] Reconcile agent and prompt wording with contract terms in `.github/agents/chief-estimator-risk.agent.md`
- [ ] T029 [P] Reconcile prompt wording with required output contract in `.github/prompts/estimate-risk-from-sharepoint.prompt.md`
- [ ] T030 Update risk contract examples and edge-case notes in `specs/1-estimate-risk-agent/contracts/risk-briefing-contract.yaml`
- [ ] T031 Create end-to-end validation summary across US1-US3 in `specs/1-estimate-risk-agent/validation/final-validation-summary.md`
- [ ] T032 Run quickstart verification and update runbook notes in `specs/1-estimate-risk-agent/quickstart.md`

---

## Dependencies & Execution Order

### Phase Dependencies

- **Setup (Phase 1)**: No dependencies; starts immediately.
- **Foundational (Phase 2)**: Depends on Setup; blocks all story phases.
- **User Story Phases (Phase 3-5)**: Depend on Foundational completion.
- **Polish (Phase 6)**: Depends on completion of selected user stories.

### User Story Dependencies

- **US1 (P1)**: Starts after Phase 2; no dependency on US2/US3.
- **US2 (P2)**: Starts after Phase 2; independent but reuses US1 artifacts.
- **US3 (P3)**: Starts after Phase 2; independent but reuses US1 outputs.

### Within Each User Story

- Update behavior/prompt instructions first.
- Update validation criteria second.
- Run pilot scenario and capture evidence last.

### Parallel Opportunities

- Phase 1: T003 and T004 in parallel.
- Phase 2: T006 and T007 in parallel.
- US1: T012 and T013 in parallel.
- US2: T019 and T020 in parallel.
- US3: T024 and T025 in parallel.
- Polish: T028 and T029 in parallel.

---

## Parallel Example: User Story 1

```bash
Task: "T012 [US1] Add explicit required input capture placeholders in .github/prompts/estimate-risk-from-sharepoint.prompt.md"
Task: "T013 [US1] Add risk evidence and likelihood/impact completion checks in specs/1-estimate-risk-agent/validation/executive-rubric.md"
```

---

## Implementation Strategy

### MVP First (User Story 1 Only)

1. Complete Phase 1 and Phase 2.
2. Complete Phase 3 (US1).
3. Validate output using `specs/1-estimate-risk-agent/validation/executive-rubric.md`.
4. Demo executive briefing generation.

### Incremental Delivery

1. Deliver US1 for baseline briefing generation.
2. Add US2 for resilient incomplete-data operation.
3. Add US3 for executive presentation quality.
4. Complete Phase 6 polish and final validation summary.

### Parallel Team Strategy

1. One owner updates `.github/agents/chief-estimator-risk.agent.md` tasks.
2. One owner updates `.github/prompts/estimate-risk-from-sharepoint.prompt.md` tasks.
3. One owner maintains validation docs under `specs/1-estimate-risk-agent/validation/`.

---

## Notes

- `[P]` tasks are parallelizable by file separation.
- `[US1]`, `[US2]`, `[US3]` labels provide traceability to spec stories.
- Each user story includes an independent acceptance check.
- Use pilot-result files as objective evidence before moving to next phase.
