---
mode: agent
description: "Generate an executive-ready conceptual estimate risk briefing from SharePoint historical estimates by value, geolocation, and contract type."
---

Use the `chief-estimator-risk` agent behavior to evaluate conceptual estimate risk for this project context.

## Project Context
- Project name: ${input:projectName}
- Target estimate value: ${input:targetValue}
- Location/geolocation: ${input:location}
- Contract type: ${input:contractType}
- Delivery timeline: ${input:timeline}
- Scope summary: ${input:scopeSummary}

## Output Requirements
Produce a textual executive briefing with:
1. Executive summary of risk posture.
2. Project-to-history fit (value, geolocation, contract type).
3. Top estimate risks with evidence, likelihood/impact, and mitigations.
4. Recommended contingency posture.
5. Assumptions and data gaps.

If SharePoint data cannot be queried directly, state what is missing and continue with a structured risk assessment based on available inputs.
