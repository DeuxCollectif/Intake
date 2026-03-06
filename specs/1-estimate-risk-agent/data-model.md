# Data Model: Chief Estimator Risk Agent

## 1. ProjectInputProfile

Represents the user-submitted conceptual project context for analysis.

### Fields
- `projectName` (string, required)
- `targetEstimateValue` (number, required, > 0)
- `targetEstimateRangeLow` (number, optional, >= 0)
- `targetEstimateRangeHigh` (number, optional, >= targetEstimateRangeLow)
- `currencyCode` (string, required, ISO-like code)
- `locationCountry` (string, required)
- `locationRegion` (string, optional)
- `locationCity` (string, optional)
- `contractType` (enum, required: `lump-sum|gmp|unit-price|design-build|other`)
- `deliveryTimeline` (string, required)
- `scopeSummary` (string, required, min length 20)
- `submittedAt` (datetime, system-generated)

### Validation Rules
- Required fields must be non-empty.
- Value range fields must be numeric and coherent if both provided.
- Contract type must map to an allowed value set.

## 2. HistoricalEstimateRecord

Represents one historical estimate source item retrieved from SharePoint files.

### Fields
- `recordId` (string, required)
- `projectLabel` (string, required)
- `estimateValue` (number, required)
- `currencyCode` (string, required)
- `contractType` (string, required)
- `geoMarket` (string, required)
- `country` (string, optional)
- `region` (string, optional)
- `city` (string, optional)
- `estimateDate` (date, required)
- `unitRateBasis` (string, optional)
- `productivityAssumptions` (string, optional)
- `escalationAssumptions` (string, optional)
- `contingencyAssumption` (string, optional)
- `dataCompletenessScore` (number, 0-100)

### Validation Rules
- Must include minimum filter fields: value, contract type, and geolocation marker.
- Records missing required filter fields are excluded from comparator selection.

## 3. ComparisonSet

Represents the selected historical benchmark records and fit metadata.

### Fields
- `comparisonSetId` (string, required)
- `inputProfileId` (string, required)
- `selectedRecordIds` (array[string], required)
- `selectionCriteria` (object, required)
- `sampleSize` (integer, required, >= 0)
- `fitSummary` (string, required)
- `confidenceLevel` (enum, required: `low|medium|high`)
- `dataQualityIssues` (array[string], optional)

### Validation Rules
- `confidenceLevel` must account for sample size and data completeness.
- `sampleSize=0` requires explicit no-match condition handling.

## 4. RiskStatement

Represents one explicit estimate risk output item.

### Fields
- `riskId` (string, required)
- `category` (enum, required)
- `riskStatement` (string, required)
- `historicalEvidence` (string, required unless no data available)
- `likelihood` (enum, required: `low|medium|high`)
- `impact` (enum, required: `low|medium|high`)
- `exposureDirection` (enum, required: `cost-up|cost-down|schedule-right|schedule-left|mixed`)
- `mitigationAction` (string, required)
- `suggestedOwner` (string, required)

### Validation Rules
- Must include both likelihood and impact ratings.
- Must include mitigation and owner suggestion.
- If no historical evidence exists, assumptions/data gaps must reference reason.

## 5. ExecutiveRiskBriefing

Represents the final narrative response for leadership consumption.

### Fields
- `executiveSummary` (string, required)
- `projectToHistoryFit` (string, required)
- `topEstimateRisks` (array[RiskStatement], required, min 1)
- `recommendedContingencyPosition` (string, required)
- `assumptionsAndDataGaps` (array[string], required)

### Validation Rules
- Must contain all five required sections.
- Must remain text-first and presentation-ready.
- Must not default to table formatting unless user requested.

## Relationships
- `ProjectInputProfile` 1..1 -> 1..n `HistoricalEstimateRecord` (filtered candidates)
- `ProjectInputProfile` 1..1 -> 1..1 `ComparisonSet`
- `ComparisonSet` 1..1 -> 1..n `RiskStatement`
- `ExecutiveRiskBriefing` 1..1 aggregates 1..n `RiskStatement`

## State Transitions
1. `InputCaptured` -> 2. `DataQueried` -> 3. `ComparisonBuilt` -> 4. `RisksSynthesized` -> 5. `BriefingGenerated`

Fallback path:
- If transition 2 has partial/no access: continue to transition 3 using available records and mark low confidence with explicit data gaps.
