# IVG GitHub Issues Summary

## Research Strategy

**#11 - Define needed research information**

- Most important aspect: specify exact information requirements for each research agent
- Define input/output data structures, required fields, minimum viable information thresholds

**#12 - Research vs Generation (CRITICAL)**

- System generates variables FROM research, doesn't research them directly
- Need clear separation: questionnaire inputs → research data → synthesis → variable generation
- Prevent confusion between data collection and strategic generation

**#10 - Link company sources with research**

- Compare questionnaire data with independent research findings
- Flag congruency issues, contradictions, gaps requiring clarification
- Build cross-reference validation layer with congruency scoring

**#9 - Cross-agent congruency**

- Information from different research agents must be congruent
- Add validation to detect and flag contradictions between Company/Industry/Competitor/Audience agents

**#13 - Social media analysis scope too wide**

- Define specific data points to extract from social media
- Limit scope to actionable signals, specify API endpoints and filtering criteria

**#14 - Include KPIs in industry research**

- Define standard KPIs by industry vertical
- Specify data sources and integration into variable generation

**#15 - Industry research needs detail**

- Expand specification: data sources, extraction methods, output formats
- Document API integrations and output schema

**#16 - Competitor research relates to client objectives**

- Explore relationship between client goals and competitive intelligence
- Define objective-driven competitive analysis approach

**#21 - Successful creative families/variations**

- Define "creative family" taxonomy
- Capture patterns of successful creative variations in industry/vertical

**#17 - Creative engineering inputs**

- Define creative engineering input requirements
- Specify integration with variable generation process

**#20 - Context embedding information**

- Define context embedding strategy
- Specify embedding model, vector storage, integration with synthesis engine

---

## Variable Definitions

**#1 - Add examples to each variable**

- Provide concrete examples for all 9 variables showing proper structure
- Include correct/incorrect examples, real campaign references

**#2 - Clarify "psychological" vs observable**

- Emphasize PS must be OBSERVABLE BEHAVIOR, not internal states
- Update validation logic to check observability

**#3 - Link OF to S0/S1**

- Connect Outcome Function to User States framework (S0 → S1 transition)
- Map behavioral change to state transitions in OF Generator

**#18 - Define S0 and S1**

- Add S0 (starting state) and S1 (target state) definition step
- Include in Campaign Definition Sheet output

**#19 - Define progress signals**

- Create methodology for progress signals indicating S0 → S1 movement
- Link to observable behaviors and optimization events

**#4 - Cognitive Stage specifications**

- Document stage-specific constraints: objective, VE, optimization event, CTA range, targeting
- Create stage-specific constraint tables

**#5 - Define Emotional Axis**

- Add explicit definition: "defines emotional transition creative facilitates"
- Include example library (confusion→clarity, insecurity→confidence, overwhelm→control)

**#6 - Define Abstraction Level**

- Add explicit definition: "controls how conceptual vs. concrete creative is"
- Provide High/Medium/Low examples by stage

**#7 - Define CTA Intensity Range**

- Add definition: "defines how strong CTA can be without breaking coherence"
- Document coherence-breaking thresholds by stage

**#8 - SCR definition refinement**

- Add: "defines what cannot change without creating a new system"
- Emphasize system identity preservation

---

## Action Priority

**CRITICAL:**

- #12: Clarify research vs generation architecture

**HIGH:**

- #11: Define research requirements
- #10: Build source reconciliation
- #1: Add variable examples
- #3, #18, #19: S0/S1 framework integration

**MEDIUM:**

- #9, #13-15, #17, #20-21: Research enhancements
- #2, #4-7: Variable definition improvements

**LOW:**

- #8, #16: Minor refinements
