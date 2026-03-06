# Feature Specification: Chief Estimator Risk Agent

**Feature Branch**: `[1-estimate-risk-agent]`  
**Created**: 2026-03-06  
**Status**: Draft  
**Input**: User description: "Chief Estimator Risk Agent that compares conceptual project estimates against historical SharePoint estimate files and returns executive-ready estimate risk narrative"

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Generate Risk Briefing (Priority: P1)

A Chief Estimator submits project context (value, location, contract type, timeline, scope) and receives an executive-ready narrative identifying the top estimate risks based on historical estimate comparables.

**Why this priority**: This is the core business outcome and primary reason the feature exists.

**Independent Test**: Can be fully tested by submitting a complete input set and confirming the response includes all required briefing sections and risk details.

**Acceptance Scenarios**:

1. **Given** historical estimate records are available and project inputs are complete, **When** the estimator requests risk analysis, **Then** the system returns a textual briefing with executive summary, project-to-history fit, top risks, contingency position, and assumptions/data gaps.
2. **Given** comparables exist across multiple regions and contract types, **When** the estimator requests risk analysis for a specific project profile, **Then** the system prioritizes relevant comparables and cites evidence in each risk statement.

---

### User Story 2 - Handle Incomplete Data Gracefully (Priority: P2)

A Chief Estimator still receives a useful structured risk narrative even when parts of the historical dataset are missing or inaccessible.

**Why this priority**: Estimating workflows must continue despite imperfect data quality or temporary connectivity gaps.

**Independent Test**: Can be tested by running analysis with one or more unavailable data inputs and verifying the response lists missing data and assumptions while still providing a best-effort risk narrative.

**Acceptance Scenarios**:

1. **Given** partial historical data is available, **When** the estimator runs analysis, **Then** the output explicitly states data gaps and assumptions and still returns ranked risk statements with mitigations.

---

### User Story 3 - Executive Presentation Readiness (Priority: P3)

A project sponsor or steering committee member can directly use the response in leadership discussions without technical translation.

**Why this priority**: Decision speed improves when outputs are concise, business-focused, and presentation-ready.

**Independent Test**: Can be tested by reviewing output format and tone for business clarity, scanability, and absence of technical jargon.

**Acceptance Scenarios**:

1. **Given** a completed risk analysis, **When** executive stakeholders review the response, **Then** they can identify top risks, risk direction, and recommended contingency posture in under 5 minutes.

### Edge Cases

- What happens when no historical estimate records meet all three filters (value, geolocation, contract type)?
- How does the system handle conflicting signals across comparables (for example, low market risk but high productivity risk)?
- What happens when project value is outside historical ranges (extremely small or extremely large)?
- How does the system handle missing mandatory user input fields?
- What happens when historical files use inconsistent naming or missing metadata?

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: System MUST accept project input parameters including target value, location, contract type, timeline, and scope summary.
- **FR-002**: System MUST retrieve historical estimate records from the configured SharePoint repository when access is available.
- **FR-003**: System MUST prioritize comparison records by matching contract type, comparable value band, and similar geolocation/market conditions.
- **FR-004**: System MUST prefer recent historical records and include older records only when sample size is insufficient.
- **FR-005**: System MUST assess data quality of selected comparison records and reflect confidence level in the response.
- **FR-006**: System MUST identify variance drivers across cost, schedule, and commercial assumptions.
- **FR-007**: System MUST produce explicit risk statements for the defined risk categories: scope, quantity/takeoff, market/escalation, labor/productivity, geolocation/logistics, contract/commercial, schedule compression, stakeholder decision latency, and benchmark relevance.
- **FR-008**: System MUST assign likelihood and impact ratings (Low/Medium/High) with rationale for each listed risk.
- **FR-009**: System MUST include mitigation actions and a suggested owner for each listed risk.
- **FR-010**: System MUST generate output using the required textual structure: Executive Summary, Project-to-History Fit, Top Estimate Risks, Recommended Contingency Position, and Assumptions and Data Gaps.
- **FR-011**: System MUST explicitly state missing data or unavailable access conditions and continue with a best-effort risk framework.
- **FR-012**: System MUST maintain executive-facing tone that is concise, business-focused, non-technical, and scannable.
- **FR-013**: System MUST avoid tabular output unless explicitly requested by the user.

### Key Entities *(include if feature involves data)*

- **Project Input Profile**: Submitted project context including value/range, location, contract type, timeline, and scope summary used to define comparison criteria.
- **Historical Estimate Record**: A past estimate entry with normalized attributes such as value band, location, contract model, date recency, and estimate assumptions.
- **Comparison Set**: Curated subset of historical records selected as the benchmark basis for risk analysis.
- **Risk Statement**: A structured narrative item containing risk description, supporting evidence, likelihood/impact rating, exposure direction, mitigation action, and suggested owner.
- **Executive Risk Briefing**: Final textual deliverable containing required sections, confidence statement, contingency posture, and assumptions/data gaps.

### Assumptions

- Users have permission to query the designated SharePoint estimate repository.
- Historical estimate records contain enough metadata to filter by value, geolocation, and contract type.
- Currency and estimate baselines are normalized or interpretable for comparison.
- Stakeholders prefer narrative output that can be presented without additional formatting.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: 95% of analysis requests with complete inputs produce a full five-section briefing in a single response.
- **SC-002**: 90% of pilot users report the response is clear enough for executive discussion without rewriting.
- **SC-003**: For requests with accessible historical data, at least 85% of generated risk statements include explicit comparator-based evidence.
- **SC-004**: 100% of responses generated with incomplete data include a clearly labeled assumptions and data gaps section.
- **SC-005**: During pilot usage, Chief Estimators can complete input submission and receive a briefing within 10 minutes in at least 90% of sessions.
