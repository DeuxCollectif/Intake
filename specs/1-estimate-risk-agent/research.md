# Research: Chief Estimator Risk Agent

## Decision 1: Comparator Selection Strategy
- Decision: Use a weighted matching order of contract type, value band proximity, and geolocation/market similarity, then recency.
- Rationale: This reflects estimator decision logic and preserves relevance before expanding sample size.
- Alternatives considered:
  - Equal-weight scoring across all dimensions: rejected due to weaker contract relevance.
  - Recency-first filtering: rejected because recent but structurally dissimilar projects can bias risk posture.

## Decision 2: Sparse Data Confidence Handling
- Decision: Require an explicit confidence level based on sample size and data completeness, and always disclose gaps.
- Rationale: Executive trust depends on transparent uncertainty, especially in conceptual estimating.
- Alternatives considered:
  - Suppress confidence labels for low sample sizes: rejected because it hides decision risk.
  - Binary confidence (high/low only): rejected as insufficiently informative for steering discussions.

## Decision 3: Output Contract Shape
- Decision: Standardize a five-section narrative output with numbered top risks containing evidence, likelihood/impact, exposure direction, mitigation, and owner suggestion.
- Rationale: This directly matches sponsor-ready communication needs and the accepted feature spec.
- Alternatives considered:
  - Free-form narrative: rejected due to inconsistent completeness.
  - Table-first output: rejected because default style requires non-tabular narrative unless requested.

## Decision 4: Missing Data and Access Fallback
- Decision: If SharePoint data is partial or unavailable, continue with a best-effort assessment using provided project inputs and clearly list assumptions/data gaps.
- Rationale: Estimating workflows require continuity while preserving data integrity.
- Alternatives considered:
  - Hard-fail on missing data: rejected because it blocks time-sensitive estimate reviews.
  - Fill unknowns with synthetic values: rejected due to non-fabrication requirement.

## Decision 5: Delivery Artifact Strategy in This Repository
- Decision: Implement as workspace Copilot customization files plus planning/spec documentation, without adding application runtime code.
- Rationale: Repository purpose and requested deliverable focus on agent behavior rather than deployable service code.
- Alternatives considered:
  - Build standalone web service in this phase: rejected as out of scope for the requested feature package.
