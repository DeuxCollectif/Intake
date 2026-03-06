# Implementation Plan: Chief Estimator Risk Agent

**Branch**: `[1-estimate-risk-agent]` | **Date**: 2026-03-06 | **Spec**: `/workspaces/Intake/specs/1-estimate-risk-agent/spec.md`
**Input**: Feature specification from `/specs/1-estimate-risk-agent/spec.md`

## Summary

Deliver a Copilot-based estimating risk workflow that accepts conceptual project inputs, queries SharePoint historical estimate spreadsheets, builds a comparable benchmark set by value/geolocation/contract type, and returns an executive-ready textual risk briefing with confidence and mitigation guidance.

## Technical Context

**Language/Version**: Markdown-defined Copilot agent and prompt files (no runtime language required in this repository)  
**Primary Dependencies**: GitHub Copilot custom agents/prompts, enterprise SharePoint data access via connected Microsoft 365 context  
**Storage**: SharePoint-hosted Excel estimate history (external)  
**Testing**: Scenario-based prompt validation and output contract conformance review  
**Target Platform**: GitHub Copilot Chat in VS Code with enterprise data connectors
**Project Type**: AI agent customization package (workspace-level)  
**Performance Goals**: Produce first complete risk briefing in under 10 minutes for pilot users; maintain full required section coverage in >=95% of complete-input runs  
**Constraints**: No fabricated records or confidence claims; always disclose missing access/data; default to textual response (no tables unless requested)  
**Scale/Scope**: Initial rollout for Chief Estimator workflow, covering one project analysis per run with historical comparables from the existing SharePoint repository

## Constitution Check

*GATE: Must pass before Phase 0 research. Re-check after Phase 1 design.*

- Constitution source expected at `/memory/constitution.md` is not present in this repository.
- Temporary gate result: **PASS WITH ASSUMPTION**.
- Assumption: No ratified constitutional constraints are currently enforceable beyond repository templates and explicit feature requirements.
- Action: If a formal constitution is later ratified, rerun this plan gate and record deviations in Complexity Tracking.

## Project Structure

### Documentation (this feature)

```text
specs/1-estimate-risk-agent/
├── plan.md
├── research.md
├── data-model.md
├── quickstart.md
├── contracts/
│   └── risk-briefing-contract.yaml
└── tasks.md
```

### Source Code (repository root)

```text
.github/
├── agents/
│   └── chief-estimator-risk.agent.md
└── prompts/
    └── estimate-risk-from-sharepoint.prompt.md

specs/
└── 1-estimate-risk-agent/
    ├── spec.md
    ├── plan.md
    ├── research.md
    ├── data-model.md
    ├── quickstart.md
    └── contracts/
        └── risk-briefing-contract.yaml
```

**Structure Decision**: Use a documentation-first structure because this feature is delivered as Copilot customization artifacts and behavior contracts, not application runtime code.

## Phase 0: Research Scope

- Confirm benchmark selection strategy for value, geolocation, and contract type.
- Define confidence statement logic for sparse or inconsistent historical data.
- Select a stable output contract for executive narrative sections.
- Define fallback behavior when SharePoint access is partial/unavailable.

## Phase 1: Design Scope

- Model input, comparison, and risk briefing entities with validation boundaries.
- Define contract for required output sections and risk item fields.
- Publish quickstart flow for pilot runs and acceptance checks.
- Capture agent-context update status for this repository setup.

## Agent Context Update

- Expected automation script (`scripts/bash/update-agent-context.sh`) is not present in this repository.
- Manual equivalent applied by maintaining explicit agent and prompt files under `.github/agents/` and `.github/prompts/`.
- No additional global agent context file exists to update.

## Post-Design Constitution Re-Check

- Result after design: **PASS WITH ASSUMPTION** (unchanged)
- No identified violations against explicit feature requirements.

## Complexity Tracking

> **Fill ONLY if Constitution Check has violations that must be justified**

| Violation | Why Needed | Simpler Alternative Rejected Because |
|-----------|------------|-------------------------------------|
| None | N/A | N/A |
