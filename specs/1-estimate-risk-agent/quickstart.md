# Quickstart: Chief Estimator Risk Agent

## Purpose
Run a conceptual estimate risk analysis using project inputs and SharePoint historical estimate comparables, then produce an executive-ready textual briefing.

## Prerequisites
- Workspace contains:
  - `.github/agents/chief-estimator-risk.agent.md`
  - `.github/prompts/estimate-risk-from-sharepoint.prompt.md`
- User has access to enterprise SharePoint estimate repository.
- Historical estimate files include comparable metadata (value, location/geomarket, contract type).

## Run Flow
1. Open Copilot Chat in VS Code in this workspace.
2. Invoke the prompt from `.github/prompts/estimate-risk-from-sharepoint.prompt.md`.
3. Provide required project inputs:
   - Project name
   - Target estimate value (and optional range)
   - Location/geolocation
   - Contract type
   - Delivery timeline
   - Scope summary
4. Review generated response for required five sections:
   - Executive Summary
   - Project-to-History Fit
   - Top Estimate Risks
   - Recommended Contingency Position
   - Assumptions and Data Gaps

## Acceptance Checks
- Output includes evidence-backed risk statements with likelihood and impact.
- Output includes mitigation action and suggested owner per risk.
- Output states sample size and confidence level.
- If data access is partial, output explicitly lists missing fields/data sources.
- Output remains narrative and presentation-ready without default tables.

## Troubleshooting
- No comparables found:
  - Expand value band and geolocation tolerance.
  - Keep contract type strict first, then document relaxation assumptions.
- Low confidence:
  - Pull additional recent records.
  - Normalize currency year and estimate basis metadata.
- Missing SharePoint access:
  - Run best-effort mode with explicit assumptions/data gaps.
  - Coordinate connector/permissions before executive decisions.
