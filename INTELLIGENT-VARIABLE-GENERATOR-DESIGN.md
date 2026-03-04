# Intelligent Variable Generator (IVG) System Design

## Executive Summary

The **Intelligent Variable Generator (IVG)** is a sophisticated AI-powered system that transforms minimal user inputs (company description, brand info, product details) into complete, framework-compliant definitions of the 9 Immutable Global Variables required for GrowFu v3 campaigns.

The system combines deep automated research, multi-LLM analysis, strict validation logic, and interactive refinement to produce expert-quality variable definitions that would normally require deep expertise and hours of strategic work.

---

## System Architecture Overview

### Core Principles

1. **Depth over speed**: Prioritize quality of reasoning over quick generation
2. **Evidence-based**: Every variable backed by research, not assumptions
3. **Framework compliance**: Hard constraints on variable structure and requirements
4. **Iterative refinement**: Generate, validate, refine cycle before user sees outputs
5. **Explainable**: Every decision comes with reasoning and evidence trail

### System Components

```
┌─────────────────────────────────────────────────────────────┐
│                    USER INPUT INTERFACE                      │
│  (Minimal: company, brand, product, audience, materials)     │
└───────────────────┬─────────────────────────────────────────┘
                    │
                    ▼
┌─────────────────────────────────────────────────────────────┐
│              RESEARCH ORCHESTRATOR                           │
│  Coordinates parallel research across multiple sources       │
└───────┬─────────────┬──────────────┬───────────────┬────────┘
        │             │              │               │
        ▼             ▼              ▼               ▼
┌─────────────┐ ┌──────────┐ ┌───────────┐ ┌────────────────┐
│  Company    │ │ Industry │ │Competitor │ │   Audience     │
│  Research   │ │ Research │ │ Research  │ │   Research     │
│   Agent     │ │  Agent   │ │   Agent   │ │     Agent      │
└─────┬───────┘ └────┬─────┘ └─────┬─────┘ └────────┬───────┘
      │              │              │                 │
      └──────────────┴──────────────┴─────────────────┘
                            │
                            ▼
┌─────────────────────────────────────────────────────────────┐
│              KNOWLEDGE SYNTHESIS ENGINE                      │
│  Consolidates research into structured intelligence base     │
└───────────────────┬─────────────────────────────────────────┘
                    │
                    ▼
┌─────────────────────────────────────────────────────────────┐
│              VARIABLE GENERATION ENGINE                      │
│     9 Specialized Analyzers (one per variable)              │
│  Each uses LLM + framework rules + research context         │
└───────┬─────────────┬──────────────┬───────────────┬────────┘
        │             │              │               │
        ▼             ▼              ▼               ▼
   ┌────────┐   ┌────────┐   ┌────────┐   ┌────────────┐
   │PS Gen  │   │OF Gen  │   │BR Gen  │   │ CS/VE/EA   │
   │        │   │        │   │        │   │  Gen       │
   └────┬───┘   └───┬────┘   └───┬────┘   └──────┬─────┘
        │           │            │                │
        └───────────┴────────────┴────────────────┘
                            │
                            ▼
┌─────────────────────────────────────────────────────────────┐
│              VALIDATION & CONSISTENCY ENGINE                 │
│  Hard constraints + cross-variable coherence checks          │
└───────────────────┬─────────────────────────────────────────┘
                    │
                    ▼
┌─────────────────────────────────────────────────────────────┐
│              ITERATIVE REFINEMENT LOOP                       │
│  Auto-fix violations, regenerate with constraints            │
└───────────────────┬─────────────────────────────────────────┘
                    │
                    ▼
┌─────────────────────────────────────────────────────────────┐
│              USER INTERACTION INTERFACE                      │
│  Present options, explain reasoning, gather feedback         │
└───────────────────┬─────────────────────────────────────────┘
                    │
                    ▼
┌─────────────────────────────────────────────────────────────┐
│              FINAL OUTPUT GENERATOR                          │
│  Campaign Definition Sheet + Evidence Pack                   │
└───────────────────┬─────────────────────────────────────────┘
                    │
                    ▼
┌─────────────────────────────────────────────────────────────┐
│         ECONOMIC VIABILITY ANALYZER (MMAA)                  │
│  Pre-launch gate validating unit economics feasibility      │
└───────┬─────────────┬──────────────┬───────────────┬────────┘
        │             │              │               │
        ▼             ▼              ▼               ▼
┌──────────────┐ ┌────────────┐ ┌────────────┐ ┌──────────────┐
│ LTV Engine   │ │ Viable CAC │ │Expected CPA│ │  Viability   │
│              │ │ Calculator │ │ Estimator  │ │Decision Logic│
└──────────────┘ └────────────┘ └────────────┘ └──────────────┘
        │             │              │               │
        └─────────────┴──────────────┴───────────────┘
                            │
                            ▼
                   GO / CAUTION / NO-GO
                            │
                            ▼
                    Campaign Launch Gate
```

---

## Phase 1: Deep Research Strategy

### 1.1 Research Orchestrator

**Responsibilities**:

- Coordinate parallel research agents
- Manage research depth/breadth tradeoffs
- Consolidate findings into structured knowledge graph
- Track evidence provenance for all claims

---

### 1.2 Company Research Agent

**Data Sources**:

1. **Website Deep Crawl**
   - Technology: Firecrawl, Apify, or custom Playwright crawler
   - Extract: Homepage, About, Product pages, Blog, Case studies, Testimonials
   - Parse: Value propositions, problem statements, solution mechanisms, customer stories

2. **Social Media Analysis**
   - Technology: Official APIs (Twitter/X, LinkedIn, Facebook Graph API)
   - Extract: Recent posts, engagement patterns, messaging themes, visual identity
   - Analyze: Tone, emotional positioning, brand personality

3. **Existing Marketing Materials**
   - Technology: Multi-modal LLM (GPT-4o, Claude 3.5 Sonnet)
   - Analyze: Current ads if provided, brand guidelines, positioning docs
   - Extract: Current PS/OF if implicit, emotional axes, semantic patterns

4. **Product/Service Analysis**
   - Technology: Claude Opus 4.6 for deep reasoning
   - Map: Features → Benefits → Behavioral outcomes
   - Identify: What user behavior actually changes (critical for OF)

**Output**: Company Intelligence Profile

```json
{
  "value_propositions": ["..."],
  "problem_statements_found": ["..."],
  "solution_mechanisms": ["..."],
  "customer_outcomes": ["observable behavior changes"],
  "brand_voice": {
    "tone": "authoritative|conversational|empowering",
    "emotional_positioning": "from X to Y",
    "semantic_patterns": ["repeated phrases", "core language"]
  },
  "product_mechanics": {
    "features": ["..."],
    "behavioral_outcomes": ["what users DO differently"]
  },
  "evidence": [{ "claim": "...", "source": "url", "quote": "..." }]
}
```

---

### 1.3 Industry Research Agent

**Data Sources**:

1. **Industry Intelligence**
   - Technology: Perplexity AI, Exa.ai, or custom web research
   - Extract: Market size, growth trends, competitive dynamics
   - Identify: Common pain points, typical customer journeys

2. **Problem Space Research**
   - Technology: Semantic Scholar API for academic papers, industry reports
   - Research: Documented behavioral/cognitive errors in this domain
   - Extract: Observable symptoms, state transitions

3. **Best Practices & Case Studies**
   - Successful campaigns in this vertical
   - Common messaging patterns that work
   - Typical cognitive stages and conversion paths

**Output**: Industry Intelligence Profile

---

### 1.4 Competitor Research Agent

**Data Sources**:

1. **Meta Ad Library API** (official Meta Ad Library)
   - Current active ads from competitors
   - Historical ad patterns
   - Creative approaches, messaging, hooks, CTAs

2. **Competitor Website Analysis**
   - Positioning strategies
   - Problem framing approaches
   - Outcome promises

3. **SimilarWeb / Semrush APIs** (if available)
   - Traffic patterns, audience overlap
   - Top performing content

**Output**: Competitive Intelligence Profile

```json
{
  "competitors": [
    {
      "name": "...",
      "positioning": "...",
      "problem_framing": "...",
      "emotional_axis_detected": "from X to Y",
      "cta_intensity_range": "passive|moderate|aggressive",
      "brand_role_inference": "above|beside|behind",
      "ad_examples": [{ "text": "...", "image_url": "...", "analysis": "..." }]
    }
  ],
  "market_gaps": ["opportunities not addressed by competitors"],
  "saturation_analysis": "which approaches are overused"
}
```

---

### 1.5 Audience Research Agent

**Data Sources**:

1. **Behavioral Signal Research**
   - Reddit API: Search for discussions of the problem space
   - Quora: Common questions and frustrations
   - Review sites: Behavioral patterns in reviews

2. **Meta Audience Insights** (if API access available)
   - Demographics interested in this category
   - Interest overlaps
   - Typical engagement patterns

3. **User Journey Mapping**
   - Typical paths from problem awareness → purchase
   - Observable signals at each stage
   - Common rejection/avoidance behaviors

**Output**: Audience Intelligence Profile

```json
{
  "observable_s0_signals": {
    "what_they_consume": ["content types", "formats"],
    "what_they_ignore": ["scroll patterns", "cta_avoidance"],
    "micro_actions": ["typical early signals"],
    "avoidance_behaviors": ["what they don't do"]
  },
  "cognitive_journey": {
    "exploration_signals": ["..."],
    "identification_signals": ["..."],
    "validation_signals": ["..."],
    "decision_signals": ["..."]
  },
  "problem_language": ["how they describe the problem in their own words"],
  "outcome_desires": ["what they say they want to do differently"]
}
```

---

### 1.6 Knowledge Synthesis Engine

**Technology**: Claude Opus 4.6 (best reasoning model)

**Process**:

1. Ingest all 4 research agent outputs
2. Cross-reference and validate findings
3. Identify contradictions and resolve with evidence weight
4. Build unified knowledge graph
5. Tag all claims with evidence provenance

**Output**: Synthesized Intelligence Base with full evidence trails, conflict resolution notes, confidence scores, and gaps identified

---

## Phase 2: Variable Generation Engine

### Architecture: 9 Specialized Generator Modules

Each variable has a dedicated generator following this pattern:

```
Input: Synthesized Intelligence Base + Framework Rules + Variable-Specific Constraints
Process: Multi-step reasoning with explicit constraint checking
Output: Variable definition + reasoning + evidence + alternatives
```

---

### 2.1 PS (Problem Space) Generator

**Framework Requirements** (from [File 7](./META-ADS-VAULT/02-STRUCTURAL-STRATEGY/07-Immutable-Global-Variables.md)):

- Must be a recurring human error (cognitive, emotional, or behavioral)
- Must be OBSERVABLE, not psychological
- Must identify structural cause (not blame user)
- Must be expressible as: 1 sentence + 3 observable symptoms (behaviors)

**LLM Strategy**:

- **Model**: Claude Opus 4.6 (best reasoning)
- **Approach**: Multi-shot prompting with framework requirements embedded

**Prompt Template**:

```xml
<context>
You are a GrowFu strategist expert defining Problem Space (PS) for a campaign.

FRAMEWORK REQUIREMENTS:
- PS is a RECURRING HUMAN ERROR (cognitive, emotional, or behavioral)
- It must be OBSERVABLE behavior, not internal psychology
- Identify the STRUCTURAL CAUSE (do not blame the user)
- Express as: 1 sentence definition + 3 observable symptoms

HARD CONSTRAINTS:
- Symptoms must be BEHAVIORS (things people DO), not feelings
- Must be RECURRING pattern, not one-time mistake
- Must be addressable by the product/service offered

RESEARCH INTELLIGENCE:
{synthesized_intelligence_base}

TASK:
Generate 3 alternative PS definitions for {company_name} offering {product}.
For each:
1. One-sentence PS definition identifying the structural cause
2. Three observable behavioral symptoms
3. Evidence from research supporting each symptom
4. Explanation of why this is a structural cause, not user blame
5. Confidence score (1-10) based on evidence quality
</context>
```

**Validation Logic** (hard-coded Python):

```python
def validate_ps(ps_definition):
    errors = []

    # Check: Is it behavioral/observable?
    if contains_psychological_terms(ps_definition['sentence']):
        errors.append("PS uses psychological terms instead of observable behavior")

    # Check: Are symptoms behavioral?
    for symptom in ps_definition['symptoms']:
        if not is_observable_behavior(symptom):
            errors.append(f"Symptom not observable: {symptom}")

    # Check: Does it have structural cause framing?
    if blames_user(ps_definition['sentence']):
        errors.append("PS blames user instead of identifying structural cause")

    # Check: Is it addressable by the product?
    if not product_can_address(ps_definition, product_info):
        errors.append("PS not addressable by offered product/service")

    return errors
```

**Output**: 3 ranked PS options with evidence and reasoning

---

### 2.2 OF (Outcome Function) Generator

**Framework Requirements**:

- NOT aspiration - observable state transition
- Describe what user DOES differently after intervention
- Express as change in behavior, criteria, or action
- Must be measurable/observable

**Critical Example**:

- NOT: "users will feel confident"
- YES: "users will evaluate options using a defined framework rather than guessing"

**LLM Prompt Template**:

```xml
<context>
You are defining Outcome Function (OF) - the observable behavior change.

FRAMEWORK REQUIREMENTS:
- Observable state transition (S0 → S1)
- What the user DOES differently (not feels differently)
- Behavioral change, not aspiration
- Must be measurable in principle

HARD CONSTRAINTS:
- No feelings/emotions as the OF (those are on the EA axis)
- Must be an ACTION or BEHAVIOR CHANGE
- Must be attributable to the intervention
- Must decompose across stages

RESEARCH INTELLIGENCE:
{synthesized_intelligence_base}

PS DEFINITION (already decided):
{ps_definition}

TASK:
Generate 3 alternative OF definitions that:
1. Describe the behavioral state transition (what they DO differently)
2. Are observable/measurable
3. Directly address the PS structural cause
4. Decompose across cognitive stages appropriately
</context>
```

**Validation Logic**:

```python
def validate_of(of_definition):
    errors = []

    if contains_emotional_language(of_definition):
        errors.append("OF describes feelings, not behaviors")

    if not is_measurable(of_definition):
        errors.append("OF not observable/measurable")

    if not addresses_problem(of_definition, ps_definition):
        errors.append("OF doesn't address the PS structural cause")

    if not can_decompose_to_stages(of_definition):
        errors.append("OF can't decompose across cognitive stages")

    return errors
```

---

### 2.3 BR (Brand Role) Generator

**Framework Requirements**:

- **Direction**: Unidirectional / Bidirectional
- **Intensity**: Low / Medium / High
- **Position**: Above (authority) / Beside (peer/guide) / Behind (enabler)

**Implications**:

- Position "Above" (authority) → cannot use peer tone
- Position "Beside" (peer) → cannot use authoritative tone
- Position "Behind" (enabler) → user is hero, brand is platform

**LLM Prompt Template**:

```xml
<context>
You are defining Brand Role (BR) - the functional brand-user relationship.

FRAMEWORK:
BR has 3 dimensions:
1. DIRECTION: Unidirectional (brand tells user) vs Bidirectional (conversation/co-creation)
2. INTENSITY: Low (light touch) / Medium (engaged) / High (deep relationship)
3. POSITION:
   - Above: Authority, expert, teacher (cannot use peer tone)
   - Beside: Peer, guide, partner (cannot use authoritative tone)
   - Behind: Enabler, platform, tool (user is hero)

BR governs:
- What proof is required
- How strong CTA can be
- What tone is credible

RESEARCH INTELLIGENCE:
{synthesized_intelligence_base}

Analyze:
- Current brand voice and positioning
- Competitor positioning
- Product type (SaaS platform = behind, Consulting = above, Course = beside)

TASK:
Determine the appropriate BR with:
1. Classification on each dimension with reasoning
2. Implications for proof requirements
3. Implications for CTA intensity
4. Implications for tone/voice
5. Evidence from research
</context>
```

---

### 2.4 CS (Cognitive Stage) Generator

**Framework Requirements**:

- Choose ONE stage: Exploration → Identification → Validation → Decision
- Stage determines: objective, optimization event, CTA range, targeting
- Must match where users actually are (not aspiration)
- Must ensure sufficient signal volume (~50 events/week)

**Stage Mapping**:

- **Exploration**: Awareness | Event: ThruPlay/VV | CTA: Passive
- **Identification**: Recognition | Event: LPV | CTA: Informational
- **Validation**: Trust | Event: Lead | CTA: Commitment signal
- **Decision**: Action | Event: Purchase/Value | CTA: Buy/Join

**Critical Rule**: Never skip stages. If users can't consistently perform an action, don't optimize for it.

**Validation Logic**:

```python
def validate_cs(cs_definition, budget_estimate):
    errors = []
    warnings = []

    # Can achieve ~50 events/week with budget?
    estimated_events = estimate_weekly_events(
        cs_definition['stage'],
        budget_estimate,
        industry
    )
    if estimated_events < 50:
        warnings.append(
            f"May struggle to achieve 50 events/week. "
            f"Estimated: {estimated_events}. "
            f"Consider moving to earlier stage."
        )

    # Logical progression check
    if cs_definition['stage'] == 'Decision' and not warm_audience_exists:
        warnings.append(
            "Decision stage requires retargeting audience. "
            "May want to start with earlier stage."
        )

    return errors, warnings
```

---

### 2.5 VE (Value Expression Type) Generator

**Framework Requirements**:

- **Closed set**: INSIGHT / VALIDATION / FRAMEWORK / SYSTEM
- **One per campaign** (NEVER mix)
- Must align with stage

**Mapping**:

- **INSIGHT**: Reframes the problem (Exploration)
- **VALIDATION**: Normalizes the error (Exploration/Identification)
- **FRAMEWORK**: Organizes the problem (Identification)
- **SYSTEM**: Step-by-step execution (Validation/Decision)

**Critical Rule**: Mixing VE types creates semantic ambiguity that destroys learning.

---

### 2.6 EA (Emotional Axis) Generator

**Framework Requirements**:

- Format: [From State] → [To State]
- One per campaign (never mixed)
- Common axes: confusion→clarity, insecurity→confidence, overwhelm→control

**Key Distinction**:

- **EA** is the EMOTIONAL journey
- **OF** is the BEHAVIORAL change
- They should be complementary

**Example**:

- EA: confusion → clarity (emotional)
- OF: Users evaluate options using a framework rather than guessing (behavioral)

---

### 2.7 AL (Abstraction Level) Generator

**Framework Requirements**:

- High / Medium / Low
- Ads should be Medium or Low (not High)
- Early stage (Exploration) can be more abstract
- Decision stage must be concrete

---

### 2.8 CTA-R (CTA Intensity Range) Generator

**Framework Requirements**:

- Constrained by: **Stage (dominant)**, Brand Role, Trust level

**Per-Stage Ranges**:

- **Exploration**: Passive/curiosity ("See how it works")
- **Identification**: Informational ("Learn more", "Discover")
- **Validation**: Commitment ("Register", "Get access")
- **Decision**: Action ("Buy", "Join", "Start")

**Output Format**:

```json
{
  "minimum_intensity": "softest acceptable CTA",
  "maximum_intensity": "strongest acceptable CTA",
  "reasoning": "why this range",
  "acceptable_ctas": ["See how it works", "Learn more", "Discover"],
  "too_weak": ["Maybe look"],
  "too_strong": ["Buy now", "Start trial"]
}
```

---

### 2.9 SCR (Semantic Consistency Rules) Generator

**Framework Requirements**:

- **Core promise**: Must appear in all creatives
- **Required language**: Specific words/phrases to always use
- **Forbidden claims**: What cannot be promised
- **Immutable theme**: The unchanging semantic identity

**Purpose**: Prevent semantic variation that destroys learning

**LLM Prompt includes**:

- Brand language patterns from research
- Competitor claims to differentiate from
- Regulatory constraints for industry
- All other locked variables (PS, OF, VE, EA)

---

## Phase 3: Validation & Consistency Engine

### 3.1 Hard Constraint Validation

Each variable's output is validated against:

1. **Structural requirements** (format, required fields)
2. **Framework compliance** (behavioral vs psychological, observable vs aspirational)
3. **Cross-variable consistency** (do variables work together?)

### 3.2 Cross-Variable Consistency Checks

```python
class ConsistencyValidator:
    def check_all_consistency(self, variables):
        errors = []
        warnings = []

        # PS-OF coherence
        if not of_addresses_ps(variables['OF'], variables['PS']):
            errors.append("OF doesn't address PS structural cause")

        # CS-VE alignment
        stage_ve_map = {
            'Exploration': ['INSIGHT', 'VALIDATION'],
            'Identification': ['VALIDATION', 'FRAMEWORK'],
            'Validation': ['FRAMEWORK', 'SYSTEM'],
            'Decision': ['SYSTEM']
        }
        if variables['VE'] not in stage_ve_map[variables['CS']]:
            errors.append(f"VE {variables['VE']} not aligned with stage {variables['CS']}")

        # CS-CTA-R alignment
        if not cta_range_matches_stage(variables['CTA-R'], variables['CS']):
            errors.append("CTA intensity doesn't match cognitive stage")

        # BR-CTA-R consistency
        if variables['BR']['position'] == 'Beside' and cta_too_authoritative(variables['CTA-R']):
            errors.append("Peer brand role with authoritative CTA breaks credibility")

        # CS-AL consistency
        if variables['CS'] == 'Decision' and variables['AL'] == 'High':
            errors.append("Decision stage requires Low abstraction, not High")

        # EA-OF complementarity
        if not ea_complements_of(variables['EA'], variables['OF']):
            warnings.append("Emotional axis doesn't complement behavioral outcome")

        return errors, warnings
```

### 3.3 System Identity Rule Check

**Critical Validation** (from [File 7](./META-ADS-VAULT/02-STRUCTURAL-STRATEGY/07-Immutable-Global-Variables.md)):

> If PS, OF, or BR change, it is not an iteration. It is another system.

Validates that PS, OF, BR form ONE coherent system identity.

---

## Phase 4: Iterative Refinement Loop

### 4.1 Auto-Fix Mechanism

When validation errors are detected, the system attempts automatic fixes:

```python
class RefinementEngine:
    def auto_fix_violations(self, variable, errors, all_variables):
        """
        Attempts to fix validation errors automatically
        """
        for error in errors:
            if error.type == 'psychological_language_in_ps':
                # Regenerate PS with stronger behavioral constraint
                prompt = self.build_refinement_prompt(
                    variable='PS',
                    error=error,
                    constraint="Must use ONLY observable behaviors, NO psychological terms",
                    previous_attempt=variable
                )
                refined = self.llm_call(prompt)
                return refined

            elif error.type == 'cta_stage_mismatch':
                # Regenerate CTA-R with explicit stage constraint
                prompt = self.build_refinement_prompt(
                    variable='CTA-R',
                    error=error,
                    constraint=f"Stage is {all_variables['CS']}. CTA must be {STAGE_CTA_MAP[all_variables['CS']]}",
                    previous_attempt=variable
                )
                refined = self.llm_call(prompt)
                return refined
```

### 4.2 Refinement Loop Flow

```
Generate All Variables
     ↓
Validate Each Variable
     ↓
Validate Cross-Variable Consistency
     ↓
Errors Found? ──Yes──> Auto-Fix Attempt ──> Validate Again
     │                                            │
     No                                     Still Errors?
     ↓                                            ↓
Calculate Confidence Scores              Manual Refinement Needed
     ↓                                            ↓
Confidence > 80%? ──No──> Flag for User Review
     │
    Yes
     ↓
Proceed to User Interaction
```

---

## Phase 5: User Interaction Interface

### 5.1 Presentation Strategy

**Technology**: Web interface (React/Next.js) or CLI with rich formatting

**Approach**: Present one variable at a time, grouped logically

**Groups**:

1. **System Identity** (PS, OF, BR) - most critical, lock these first
2. **Campaign Configuration** (CS, VE, EA, AL, CTA-R) - dependent on system identity
3. **Semantic Rules** (SCR) - derived from all above

### 5.2 Variable Presentation Format

```
┌─────────────────────────────────────────────────────┐
│ PS: PROBLEM SPACE                                    │
├─────────────────────────────────────────────────────┤
│                                                      │
│ RECOMMENDED:                                         │
│ Operators launch ads without defined structural     │
│ variables first, resulting in:                      │
│   1. Inconsistent creative briefing                 │
│   2. Poor learning accumulation                     │
│   3. Wasted budget on semantic variation            │
│                                                      │
│ WHY THIS PS:                                         │
│ - Research shows 73% lack campaign templates        │
│ - Your ads show variation in emotional axis         │
│ - Structural cause addressable by your product      │
│                                                      │
│ CONFIDENCE: 8.5/10                                   │
│                                                      │
│ ALTERNATIVES:                                        │
│ Option B: [Different PS with reasoning]             │
│ Option C: [Different PS with reasoning]             │
│                                                      │
│ [✓ Accept] [→ Alternatives] [✏️ Refine] [❌ Reject] │
└─────────────────────────────────────────────────────┘
```

### 5.3 Interactive Refinement Options

**User Actions**:

1. **Accept**: Lock variable and proceed
2. **See Alternatives**: View 2-3 alternative definitions
3. **Refine**: Provide feedback, system regenerates
4. **Reject**: Manually input definition (system validates)

---

## Phase 6: Final Output Generation

### 6.1 Campaign Definition Sheet

Complete 22-field Campaign Definition Sheet in [File 22](./META-ADS-VAULT/04-OPERATIONAL-CONTROL/22-Master-Checklists-and-Execution-Templates.md) format:

**Sections**:

1. System Identity (PS, OF, BR)
2. Campaign Configuration (CS, VE, EA, AL, CTA-R)
3. Semantic Rules (SCR)
4. User State Model (S0, S1, Progress Signals)
5. Campaign Architecture
6. Governance

### 6.2 Evidence Pack

Separate document with:

- Research summary from all 4 agents
- Evidence trail (every claim → source)
- Confidence scores
- Alternative definitions considered
- Risks and limitations

### 6.3 Next Steps Guide

Automatic generation of action plan:

1. Review and approve Campaign Definition Sheet
2. User State Definition (S0/S1)
3. Campaign Architecture Planning
4. Creative Brief Development
5. Launch Checklist

---

## Phase 6.5: Economic Viability Analysis (MMAA Pre-Launch Gate)

### Purpose

Validate that the campaign defined by IVG variables is economically viable before spending any budget. This prevents unprofitable campaigns from launching by comparing estimated CPA against viable CAC ceiling based on LTV economics.

**Key Question Answered**: _"Is this campaign profitable?"_ (not just "Is this campaign performing well?")

### Integration Point

**Data Flow**:

```
Campaign Definition Sheet (IVG Output)
    ↓
MMAA receives:
├─ CS (Cognitive Stage) → determines expected CPA range
├─ PS, OF, BR → context for viability assessment
├─ Budget estimate → validates signal volume
└─ Industry/audience data → calibrates benchmarks
    ↓
User provides to MMAA:
├─ LTV estimate ($)
├─ LTV confidence score (1-10)
├─ Safety margin preference (30-50%)
└─ LTV calculation method
    ↓
MMAA Pre-Launch Viability Analyzer
├─ Step 1: Calculate viable CAC ceiling
│   Formula: Base = LTV × Safety Margin
│            Adjusted = Base × Confidence Adjustment
│
├─ Step 2: Estimate expected CPA for CS
│   Uses stage-specific benchmarks:
│   - Exploration: $15-40
│   - Identification: $60-120
│   - Validation: $80-180
│   - Decision: $150-400+
│
├─ Step 3: Calculate CPA utilization
│   Utilization = Estimated CPA / Viable CAC Ceiling
│
├─ Step 4: Determine viability status
│   <50% utilization → GO ✓
│   50-80% utilization → CAUTION ⚠️
│   >80% utilization → NO-GO ✗
│
└─ Step 5: Generate reasoning + recommendations
    Uses Claude Opus 4.6 for nuanced synthesis
```

### MMAA Pre-Launch Analyzer Components

#### 1. LTV Estimation Engine

Supports three calculation methods:

**Method A: Cohort Projection** (best for subscription/SaaS)

- Input: ARPU, Gross Margin %, Churn Rate, Time Horizon
- Formula: `LTV = ARPU × Margin × (1 / Churn)`
- Example: $50/mo × 75% margin × (1 / 0.05 monthly churn) = $750 LTV

**Method B: First-Year Proxy** (for e-commerce)

- Input: AOV (Average Order Value), Purchase Frequency, Margin %
- Formula: `LTV = AOV × Frequency × Margin`
- Example: $150 AOV × 4 purchases/year × 75% margin = $450 LTV

**Method C: Industry Benchmark** (fallback)

- Input: Vertical, Price Point
- Uses industry standards database
- Example: B2B SaaS at $50/month → estimated $600-900 LTV

**Output**: LTV estimate with confidence score (1-10)

---

#### 2. Viable CAC Ceiling Calculator

**Formula**:

```python
base_ceiling = ltv_estimate * safety_margin  # safety_margin = 0.30 to 0.50

confidence_adjustment = {
    10: 1.0,    # Historical data (no adjustment)
    7-9: 0.95,  # Well-researched estimate
    4-6: 0.90,  # Moderate confidence estimate
    1-3: 0.80   # Speculative
}

viable_cac_ceiling = base_ceiling * confidence_adjustment[ltv_confidence]
```

**Example Calculation**:

- LTV: $450
- Safety Margin: 40% (moderate conservatism)
- Confidence: 6/10 (estimated, not historical)
- Base Ceiling: $450 × 0.40 = $180
- Confidence Adjustment: 0.90 (for 6/10 confidence)
- Adjusted Ceiling: $180 × 0.90 = $162
- **Result: Viable CAC Ceiling = $162**

**Why Safety Margin?**

- Accounts for unknowns in LTV calculation
- Provides buffer for learning phase variance
- Ensures sustainable unit economics (prevents break-even campaigns)

**Why Confidence Adjustment?**

- Reduces ceiling if LTV is speculative
- Historical data gets no penalty (1.0 multiplier)
- Protects against overconfident estimates

---

#### 3. Expected CPA Estimator

Uses **CS (Cognitive Stage)** from IVG variables to estimate expected CPA based on industry benchmarks and competitive density.

**Stage-Specific Benchmarks** (B2B SaaS example):

| CS Stage       | Optimization Event       | Typical CPA Range | Stage Multiplier |
| -------------- | ------------------------ | ----------------- | ---------------- |
| Exploration    | ThruPlay / Video Views   | $15-$40           | 1.0 (baseline)   |
| Identification | LPV (Landing Page Views) | $60-$120          | 1.5-2.0          |
| Validation     | Lead                     | $80-$180          | 2.0-3.0          |
| Decision       | Purchase / Value         | $150-$400+        | 4.0-8.0          |

**Formula**:

```python
expected_cpa = median_cpa_for_industry_and_stage * competitive_density_factor

# competitive_density_factor ranges 1.0-1.5 depending on market saturation
# 1.0 = low competition
# 1.3 = moderate competition
# 1.5 = high competition (e.g., Q4 spike)
```

**Integration with File 19** (Competitive Density & Marginal CPA):

- MMAA queries competitive density data for the industry vertical
- Adjusts expected CPA upward if market is saturated
- Typical adjustment: 1.0 (low competition) to 1.5 (Q4 spike, high saturation)

**Example**:

- Industry: B2B SaaS
- CS: Identification (LPV)
- Median CPA: $80
- Stage Multiplier: 1.2
- Competitive Density: 1.3 (Q4)
- **Expected CPA: $80 × 1.2 × 1.3 = $124.80**

---

#### 4. Viability Decision Engine

**Decision Matrix**:

| Estimated CPA vs. Viable Ceiling | Utilization | Status         | Action                                                             |
| -------------------------------- | ----------- | -------------- | ------------------------------------------------------------------ |
| < 50% of ceiling                 | < 50%       | **GO** ✓       | Green light - proceed with confidence                              |
| 50-80% of ceiling                | 50-80%      | **CAUTION** ⚠️ | Yellow light - proceed with conservative budget + close monitoring |
| > 80% of ceiling                 | > 80%       | **NO-GO** ✗    | Red light - recommend pivot or variable adjustment                 |

**Example Viability Assessment**:

```json
{
  "viability_status": "CAUTION",
  "viable_cac_ceiling": 162,
  "estimated_cpa": 120,
  "cpa_utilization": 0.74,
  "ltv_cac_ratio_expected": 3.75,
  "confidence": 75,
  "reasoning": "LTV of $450 supports viable CAC ceiling of $162 (36% after confidence adjustment). Estimated CPA of $120 is 74% of ceiling, leaving moderate margin. However, LTV confidence is only 6/10 (estimated, not historical data), which increases risk. Learning phase variance (File 17) could push CAC to 80-85% of ceiling. Identification stage CPA of $120 is within healthy range ($60-$120 for B2B SaaS).",
  "risk_factors": [
    {
      "risk": "LTV is estimated without historical data",
      "severity": "MEDIUM",
      "mitigation": "Implement LTV realization tracking after launch"
    },
    {
      "risk": "Thin margin to viable CAC ceiling (74% utilization)",
      "severity": "MEDIUM",
      "mitigation": "Start with conservative budget; monitor actual CAC closely"
    },
    {
      "risk": "Learning phase variance could push CAC above 85% threshold",
      "severity": "LOW",
      "mitigation": "Maintain budget discipline (≤20-30% increases per File 17)"
    }
  ],
  "recommendations": [
    "PROCEED with CAUTION - approve Identification stage campaign",
    "Target minimum 50 LPV conversions at $120 CPA = $6,000 budget",
    "Monitor actual CAC daily; if exceeds $145 (90% ceiling) for 3+ days post-learning, pause and optimize CVR",
    "Implement LTV realization tracking immediately to validate $450 estimate within 3 months"
  ]
}
```

---

#### 5. Strategic Recommendation Generator (LLM-Powered)

**Model**: Claude Opus 4.6 (best reasoning model)

**Why LLM vs. Rule Engine?**

Viability assessment requires **context-dependent judgment** beyond simple thresholds:

- Same 75% utilization could be **GO** (high LTV confidence, early-stage campaign) or **CAUTION** (low confidence, competitive industry)
- LLMs synthesize multiple factors: LTV confidence, cognitive stage, industry dynamics, competitive density, learning phase status
- Natural language reasoning is more actionable than simple "Status: CAUTION (75% utilization)"

**Prompt Template**:

```xml
You are a GrowFu viability analyst. Synthesize the following unit economics data
into a clear viability assessment with reasoning.

DATA:
- LTV: ${ltv_estimate} (confidence: {ltv_confidence}/10 - {calculation_method})
- Viable CAC Ceiling: ${viable_cac_ceiling} ({ceiling_ratio}% of LTV with confidence adjustment)
- Estimated CPA: ${estimated_cpa}
- CPA Utilization: {utilization}%
- Cognitive Stage: {cs_stage} ({optimization_event} optimization)
- Industry: {industry_vertical}

FRAMEWORK CONTEXT:
- File 17: Learning phase requires ~50 optimization events over 7 days
- File 17: Daily CPA variance <15% is healthy, >30% is problem
- File 19: Marginal CPA rises with scaling (expansion physics, not failure)
- File 9: {cs_stage} stage optimizes for {optimization_event}; typical CPA range {cpa_range}

TASK:
1. Determine viability status (GO, CAUTION, NO-GO)
2. Provide clear reasoning (3-5 sentences)
3. Identify 2-3 key risk factors with severity and mitigation
4. Recommend 2-3 actionable next steps
5. Assign confidence score (1-100)

Output as JSON.
```

**Output Structure**: Nuanced assessment with framework-grounded reasoning, not just threshold comparison.

---

### Feedback Loop to IVG

If MMAA returns **NO-GO**, it suggests variable adjustments to improve economic viability:

**Common Recommendations**:

1. **Move to earlier cognitive stage** (Decision → Validation → Identification)
   - Reduces expected CPA significantly
   - Allows viability validation before full-funnel commitment
   - Example: If Decision stage CPA $400 exceeds $350 ceiling, suggest Validation stage CPA $180 instead

2. **Adjust OF to match viable stage**
   - If Decision-stage OF is not economically viable, reframe as Validation-stage OF
   - Example: "Users purchase product" (Decision) → "Users register for product demo" (Validation)

3. **Increase LTV through business model changes**
   - Suggest pricing increase (e.g., 10% price increase improves viable ceiling by 10%)
   - Suggest upsell/cross-sell mechanisms
   - Suggest retention improvements to extend customer lifetime

4. **Optimize targeting to reduce expected CPA**
   - Use more qualified audiences (reduces waste, improves CPA)
   - Adjust EA (Emotional Axis) or VE (Value Expression) to improve creative relevance
   - Tighten audience definition

**Example NO-GO Scenario**:

```
Decision stage CPA: $400 (expected)
Viable CAC Ceiling: $350 (LTV $1,000 × 35%)
Utilization: 114% → NO-GO ✗

Recommendations:
1. Move to Validation stage: Expected CPA $180 → 51% utilization → CAUTION ✓
2. Alternative: Increase pricing 15% → LTV $1,150 → Ceiling $402 → GO ✓
3. Alternative: Optimize targeting to reduce expected CPA to <$350
```

---

### User Experience Flow

**Step 1: IVG Completion**

```
User completes IVG variable generation
    ↓
System presents Campaign Definition Sheet
    ↓
User approves all 9 variables (PS, OF, BR, CS, VE, EA, AL, CTA-R, SCR)
```

**Step 2: MMAA Handoff**

```
System displays transition message:

"Your campaign variables are locked. Before launching, let's validate economic viability."

Expected CPA for Identification stage: $80-$120 (industry benchmark)

To proceed, please provide:
1. Your estimated LTV per customer
2. How confident are you in this LTV? (1-10 scale)
3. What calculation method did you use? (Cohort / First-Year / Benchmark)
```

**Step 3: MMAA Analysis** (<10 seconds)

```
System calculates and displays:

Viable CAC ceiling: $162
Estimated CPA: $100
Utilization: 62%
Status: CAUTION ⚠️

[Viability Card displays]
├─ Color-coded status indicator
├─ Clear reasoning (3-5 sentences)
├─ Risk factors with severity
├─ Actionable recommendations
└─ Confidence score
```

**Step 4: User Decision**

```
Options presented:
[✓ Proceed with campaign] - If GO or user accepts CAUTION
[← Adjust variables] - Returns to IVG Phase 5 to modify CS/OF
[💰 Adjust LTV/pricing] - User provides different economics inputs
[❌ Cancel campaign] - If NO-GO and not economically viable
```

---

### Data Exchange Specification

#### IVG → MMAA Inputs

**From Campaign Definition Sheet**:

```json
{
  "campaign_definition_id": 12345,
  "ps": "Marketing teams make strategic decisions using incomplete data...",
  "of": "Marketing leaders evaluate channel performance using unified attribution...",
  "br": {
    "direction": "Bidirectional",
    "intensity": "Medium",
    "position": "Beside"
  },
  "cs": {
    "stage": "Identification",
    "optimization_event": "LPV",
    "objective": "Recognition"
  },
  "ve": "FRAMEWORK",
  "ea": "Overwhelm → Control",
  "al": "Medium",
  "cta_r": {
    "minimum_intensity": "See how it works",
    "maximum_intensity": "Learn more"
  },
  "scr": "Core promise: unified attribution dashboard...",
  "budget_estimate": 6000,
  "industry_vertical": "B2B SaaS",
  "target_audience": "Marketing directors at mid-market B2B (50-500 employees)"
}
```

#### User → MMAA Inputs

```json
{
  "ltv_estimate": 450,
  "ltv_confidence_score": 6,
  "ltv_calculation_method": "First-Year Proxy",
  "ltv_calculation_details": {
    "aov": 150,
    "purchase_frequency": 4,
    "margin": 0.75
  },
  "safety_margin": 0.4
}
```

#### MMAA → User Outputs

```json
{
  "viability_status": "CAUTION",
  "viable_cac_ceiling": 162,
  "estimated_cpa": 100,
  "cpa_utilization": 0.62,
  "ltv_cac_ratio_expected": 4.5,
  "confidence": 75,
  "reasoning": "LTV of $450 supports viable CAC ceiling...",
  "risk_factors": [
    {
      "risk": "LTV is estimated without historical data",
      "severity": "MEDIUM",
      "mitigation": "Implement LTV realization tracking after launch"
    }
  ],
  "recommendations": [
    "PROCEED with CAUTION - approve Identification stage campaign",
    "Target minimum 50 LPV conversions at $100 CPA = $5,000 budget",
    "Monitor actual CAC daily post-learning phase"
  ],
  "approval_action": "PROCEED_WITH_MONITORING",
  "next_steps": [
    "Start with conservative budget $6,000",
    "Monitor actual CAC daily post-learning",
    "Implement LTV realization tracking"
  ]
}
```

---

### Integration with Existing IVG Phases

#### Optional Enhancement to Phase 5 (User Interaction)

While MMAA is a separate post-generation step, **Phase 5 could be enhanced** to prepare users for economic validation:

**Add "Economic Feasibility Indicator" to CS Variable Presentation**:

```
┌─────────────────────────────────────────────────────┐
│ CS: COGNITIVE STAGE                                  │
├─────────────────────────────────────────────────────┤
│                                                      │
│ RECOMMENDED: Identification (LPV optimization)       │
│                                                      │
│ 💡 ECONOMIC INSIGHT:                                │
│ Expected CPA range: $60-$120 (B2B SaaS benchmark)  │
│ To validate viability, your LTV should be >$180    │
│ (assuming 3:1 healthy LTV:CAC ratio)                │
│                                                      │
│ This will be validated in Economic Viability step.  │
│                                                      │
│ [✓ Accept] [→ Alternatives] [✏️ Refine]            │
└─────────────────────────────────────────────────────┘
```

**Benefits**:

- Users think about economics during variable selection (not after)
- Reduces surprise rejections at MMAA gate
- Educates users on stage-CPA relationships
- No blocking behavior - just informational

**Implementation**: Add lightweight CPA range display; does NOT block variable selection or require LTV input yet.

---

### Why MMAA is Separate from IVG

**Architectural Decision**: MMAA is a **post-generation analyzer**, not embedded within IVG's core workflow.

**Reasons for Separation**:

1. **Separation of Concerns**
   - IVG's job: Define WHAT the campaign is (strategic variables: PS, OF, BR, etc.)
   - MMAA's job: Verify IF the campaign is economically viable (unit economics)
   - Mixing them creates scope creep and confuses responsibilities

2. **Different Expertise Required**
   - IVG: GrowFu framework expertise, strategic thinking, creative positioning
   - MMAA: Financial modeling, LTV calculation, business unit economics

3. **Different User Inputs**
   - IVG: Company info, product details, audience, brand materials
   - MMAA: LTV data, financial assumptions, safety margin preferences

4. **Sequential Dependency**
   - MMAA **requires** CS (Cognitive Stage) from IVG to estimate expected CPA
   - Cannot run MMAA without completed variable definitions
   - Clean handoff: Variables locked → Economics validated → Launch approved

5. **Modularity**
   - IVG can be used independently (define variables without launching)
   - MMAA can be bypassed for campaigns without economic constraints (awareness campaigns)
   - Future: MMAA could validate campaigns defined outside IVG

---

## Technology Stack

### Economic Analysis Layer (MMAA)

**LTV Calculation Engine**:

- **Language**: Python 3.11+
- **Libraries**: NumPy for financial calculations, Pandas for cohort analysis
- **Methods**: Cohort Projection, First-Year Proxy, Industry Benchmark lookup

**Viability Decision Engine**:

- **Rule Engine**: Python with hard-coded decision matrix (GO/CAUTION/NO-GO thresholds)
- **LLM Reasoning**: Claude Opus 4.6 (Anthropic) for nuanced viability synthesis
- **Response Time**: <3 seconds for calculation + <10 seconds for LLM reasoning

**Industry Benchmark Database**:

- **Storage**: PostgreSQL table `industry_benchmarks`
- **Schema**:
  ```sql
  CREATE TABLE industry_benchmarks (
    id SERIAL PRIMARY KEY,
    industry_vertical VARCHAR(100),
    cognitive_stage VARCHAR(50),
    median_cpa DECIMAL(10,2),
    p25_cpa DECIMAL(10,2),
    p75_cpa DECIMAL(10,2),
    competitive_density_factor DECIMAL(3,2),
    last_updated TIMESTAMP
  );
  ```
- **Data Source**: Aggregated from File 19 (Competitive Density) + industry reports + historical campaign data

**Integration API**:

- **Framework**: FastAPI endpoint `/api/v1/mmaa/pre-launch-viability`
- **Authentication**: Shared JWT with IVG system
- **Method**: POST with Campaign Definition Sheet + LTV inputs
- **Response Time**: <5 seconds total (calculation + LLM reasoning + database lookups)
- **Error Handling**: Fallback to conservative estimates if industry data missing

---

### Core Infrastructure

- **Language**: Python 3.11+
- **Orchestration**: Apache Airflow or Prefect
- **Database**: PostgreSQL for research, variables, evidence
- **Vector DB**: Pinecone or Weaviate for semantic search
- **Caching**: Redis for API call caching

### LLM Layer

- **Primary Reasoning**: Claude Opus 4.6 (Anthropic) - best reasoning for complex variables
- **Fast Analysis**: Claude Sonnet 4.5 (Anthropic) - research synthesis
- **Multimodal**: GPT-4o (OpenAI) - analyze existing ads/images
- **Embedding**: text-embedding-3-large (OpenAI) or Voyage AI

### Research Tools

- **Web Scraping**: Firecrawl API, Apify, or custom Playwright
- **Meta Ad Library**: Official Meta Ad Library API
- **Web Research**: Perplexity API, Exa.ai, or Tavily AI
- **Social Media**: Twitter API, LinkedIn API, Reddit API
- **Academic**: Semantic Scholar API
- **Website Analysis**: Custom crawler + Beautiful Soup

### Validation Layer

- **Framework Rules**: Custom Python validation library
- **Linguistic Analysis**: Spacy/NLTK (check psychological vs behavioral language)
- **ML Classifier**: Fine-tuned model for PS/OF compliance detection

### User Interface

- **Web UI**: Next.js + React + Tailwind CSS
- **Backend API**: FastAPI (Python)
- **Real-time**: WebSocket for progress tracking
- **CLI Alternative**: Rich library for terminal interface

---

## Data Flow

```
USER INPUT (minimal)
    ↓
INPUT VALIDATION & ENRICHMENT
    ↓
RESEARCH ORCHESTRATION (parallel)
    ├─ Company Research Agent
    ├─ Industry Research Agent
    ├─ Competitor Research Agent
    └─ Audience Research Agent
    ↓
KNOWLEDGE SYNTHESIS
    ↓
VARIABLE GENERATION (sequential)
    ├─ PS Generator → Validate
    ├─ OF Generator → Validate
    ├─ BR Generator → Validate
    ├─ CS Generator → Validate
    ├─ VE Generator → Validate
    ├─ EA Generator → Validate
    ├─ AL Generator → Validate
    ├─ CTA-R Generator → Validate
    └─ SCR Generator → Validate
    ↓
CROSS-VARIABLE VALIDATION
    ↓
ERRORS? ──Yes──> REFINEMENT LOOP ──> Re-validate
    │
    No
    ↓
CONFIDENCE SCORING
    ↓
USER INTERACTION INTERFACE
    ↓
All Variables Locked?
    ↓
   Yes
    ↓
FINAL OUTPUT GENERATION
    ├─ Campaign Definition Sheet
    ├─ Evidence Pack
    └─ Next Steps Guide
    ↓
MMAA ECONOMIC VIABILITY ANALYZER
    ├─ User provides LTV estimate + confidence
    ├─ Calculate viable CAC ceiling
    ├─ Estimate expected CPA for CS
    ├─ Determine GO/CAUTION/NO-GO status
    └─ Generate recommendations
    ↓
Viability Status?
    ├─ GO → Proceed to Campaign Launch
    ├─ CAUTION → User decides (proceed or adjust)
    └─ NO-GO → Suggest variable adjustments or cancel
    ↓
Campaign Launch (if approved)
```

---

## Implementation Phases

### Phase 1: MVP (8-10 weeks)

**Core system with manual research assistance**

**Components**:

1. Input interface (simple web form)
2. Company Research Agent (web scraping + LLM)
3. Variable Generation Engine (all 9 generators)
4. Hard validation layer
5. Simple user review interface
6. Campaign Definition Sheet output

**Research**: Semi-automated (tool suggests, user provides inputs)

### Phase 2: Enhanced Research (4-6 weeks)

**Fully automated research**

**Add**:

1. Industry Research Agent
2. Competitor Research Agent (Meta Ad Library)
3. Audience Research Agent (Reddit/Quora)
4. Knowledge Synthesis Engine
5. Evidence tracking

### Phase 3: Advanced Interaction (4-6 weeks)

**Sophisticated user interaction**

**Add**:

1. Alternative generation (2-3 options per variable)
2. Interactive refinement with feedback loop
3. Progress tracking UI
4. Evidence Pack generation
5. Confidence scoring

### Phase 4: Intelligence Layer (6-8 weeks)

**Learning and improvement**

**Add**:

1. Historical campaign performance integration
2. A/B testing of variable definitions
3. Success pattern recognition
4. Industry-specific tuning
5. Custom ML classifier
6. Active learning from user feedback

### Phase 5: Integration & Scale (4-6 weeks)

**Production-ready**

**Add**:

1. Meta Ads Manager integration
2. JSON export
3. API for programmatic access
4. Multi-user/agency support
5. Template library (per industry)
6. Batch processing

---

## Success Metrics

### System Quality Metrics

- **Framework Compliance Rate**: >95% (variables passing all validation)
- **Cross-Variable Coherence**: >85/100
- **Research Quality**: >80/100 average confidence

### User Experience Metrics

- **Time to Complete**: <60 minutes (vs 6-8 hours manual)
- **User Acceptance Rate**: >70% (variables accepted without modification)
- **Refinement Iterations**: <2 iterations per variable

### Business Outcome Metrics

- **Campaign Success Rate**: >80% (meet learning phase goals)
- **Expert Review Pass Rate**: >90% (validated by GrowFu experts)
- **Cost Savings**: 85%+ time reduction

### MMAA Economic Viability Metrics

**Viability Prediction Accuracy**:

- **Target**: >80% accuracy
- **Measurement**: % of GO/NO-GO assessments matching actual 30-day profitability
- **Calculation**: Compare MMAA prediction vs. actual CAC < Viable Ceiling at Day 30

**Unprofitable Campaign Prevention Rate**:

- **Target**: >90% prevention
- **Measurement**: % of campaigns with predicted negative ROI caught pre-launch
- **Impact**: Estimated budget saved per prevented campaign

**False Positive Rate** (NO-GO on viable campaigns):

- **Target**: <15%
- **Measurement**: % of NO-GO assessments that were incorrect (campaign would have been profitable)
- **Impact**: Opportunity cost of rejected campaigns

**User Acceptance of CAUTION Campaigns**:

- **Target**: >70% proceed despite warning
- **Measurement**: % of CAUTION campaigns user chooses to launch vs. adjust/cancel
- **Insight**: Indicates whether CAUTION threshold is appropriately calibrated

**Time to Viability Decision**:

- **Target**: <5 minutes
- **Measurement**: Time from LTV submission to GO/CAUTION/NO-GO result display
- **Breakdown**: Calculation (<3s) + LLM reasoning (<10s) + UI rendering (<2s)

### Combined IVG + MMAA End-to-End Metrics

**End-to-End Campaign Profitability**:

- **Target**: >85% of IVG-defined + MMAA-approved campaigns achieve profitability within 90 days
- **Measurement**: Actual CAC < Viable CAC Ceiling at Day 90
- **Impact**: Validates entire system (variable generation + economic gating)

**System Efficiency (Total Time)**:

- **Target**: <70 minutes total (IVG 45-60 min + MMAA 5-10 min)
- **Measurement**: Time from initial user input to campaign launch approval
- **Comparison**: vs. 6-8 hours manual strategic work

**Economic Value Added**:

- **Target**: Measurable ROI improvement from MMAA-approved campaigns
- **Measurement**: Average LTV:CAC ratio of MMAA-approved campaigns vs. industry benchmark
- **Expected**: >3:1 LTV:CAC ratio (vs. 2:1 industry average)

---

## Example Walkthrough

### Input

```json
{
  "company_name": "DataFlow Analytics",
  "company_description": "B2B SaaS platform helping marketing teams consolidate data from multiple sources into actionable dashboards",
  "brand_info": "Positioned as the 'single source of truth' for marketing performance",
  "product": "Dashboard software with automated reporting, multi-channel integration, AI-powered insights",
  "target_audience": "Marketing directors and CMOs at mid-market B2B companies (50-500 employees)",
  "existing_materials": "https://dataflowanalytics.com"
}
```

### Generated Variables (Summary)

**PS**: Marketing teams make strategic decisions using incomplete data because their metrics are fragmented across disconnected tools, resulting in: (1) 15+ hours weekly compiling reports, (2) making decisions based on most accessible data not most relevant, (3) presenting inconsistent numbers in meetings

**OF**: Marketing leaders evaluate channel performance using unified attribution methodology across all channels instead of making decisions based on fragmented, inconsistent data sources

**BR**: Direction: Bidirectional | Intensity: Medium | Position: Beside (guide/enabler)

**CS**: Identification (LPV optimization event)

**VE**: FRAMEWORK (presenting "3-Layer Attribution Framework")

**EA**: Overwhelm → Control

**AL**: Medium (concept with concrete examples)

**CTA-R**: Informational ("See How It Works", "Learn the Framework")

**SCR**: Core promise: "See all your marketing performance in one unified dashboard with consistent attribution" | Required language: "unified", "attribution", "single source of truth"

**Total Time (IVG)**: 45 minutes | **Confidence**: 8.5/10

---

### MMAA Economic Viability Assessment

**After User Approves All Variables in IVG:**

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
MMAA PRE-LAUNCH VIABILITY GATE
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Your campaign variables are locked. Before launching, let's validate
economic viability.

Expected CPA for Identification stage: $60-$120 (B2B SaaS benchmark)

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
PROVIDE UNIT ECONOMICS
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

1. Estimated LTV per customer: $600

   Calculation method: First-Year Proxy
   - Monthly subscription: $50/month
   - Average retention: 12 months
   - Gross margin: 80%
   - LTV = $50 × 12 × 0.80 = $480 (conservative)
   - With upsells/expansion: $600 estimated

2. Confidence in LTV (1-10): 7/10

   Reasoning: Based on industry benchmarks for similar B2B SaaS pricing
   ($40-60/month MRR). No historical data yet, but well-researched
   competitive analysis.

3. Safety margin preference: 40%

   (Moderate conservatism - want healthy buffer below break-even)

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
CALCULATING VIABILITY...
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

✓ Viable CAC Ceiling calculated: $228
  (LTV $600 × 40% safety margin × 0.95 confidence adjustment)

✓ Expected CPA estimated: $90
  (B2B SaaS, Identification stage, moderate competition)

✓ CPA Utilization: 39% ✓

✓ LTV:CAC Ratio: 6.7:1 (well above 3:1 healthy benchmark)

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
STATUS: GO ✓
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

REASONING (Confidence: 85/100):

Your campaign shows strong economic viability. With LTV of $600 and
estimated CPA of $90, you have a healthy 6.7:1 LTV:CAC ratio (well above
the 3:1 benchmark for sustainable growth). The Identification stage is
appropriate for your market position, and expected CPA is in the healthy
range for B2B SaaS ($60-$120).

Your 39% CAC utilization provides substantial buffer for learning phase
variance and potential scaling. The FRAMEWORK value expression type aligns
well with your "3-Layer Attribution Framework" positioning, which should
drive strong engagement in the Identification stage.

LTV confidence of 7/10 is reasonable for a well-researched estimate. The
5% confidence adjustment reduces your viable ceiling modestly to $228,
maintaining a conservative approach.

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
RISK FACTORS
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

1. LTV based on industry benchmarks, not historical data [LOW severity]

   Mitigation: Track actual LTV realization at 30/60/90 days post-launch.
   Monitor churn rate closely in first 3 months to validate $600 assumption.

2. Competitive density moderate in B2B marketing analytics [LOW severity]

   Mitigation: Monitor CPC trends weekly. If CPC spikes >20%, prepare
   creative refresh using File 20 guidance (Creative Intelligence System).

3. Expansion revenue assumption in LTV ($120 beyond base $480) [MEDIUM severity]

   Mitigation: Track expansion revenue separately. If expansion <$100
   per customer, viable ceiling drops to $182 (still healthy at 49% utilization).

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
RECOMMENDATIONS
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

1. ✓ PROCEED with launch - economics are sound

2. Target 50 LPV conversions minimum to exit learning phase
   Budget: 50 LPV × $90 CPA = $4,500 minimum
   Recommend: $6,000 to allow for learning phase variance

3. Monitor actual CAC post-learning phase:
   - Alert if actual CAC exceeds $180 (80% of ceiling) for 3+ days
   - Auto-pause if actual CAC exceeds $205 (90% of ceiling) for 2+ days

4. Implement LTV tracking infrastructure immediately:
   - Tag customers by acquisition source (LPV campaign)
   - Track actual retention, expansion, churn at 30/60/90 days
   - Validate $600 LTV assumption within 3 months
   - Adjust viable ceiling if actual LTV differs >15%

5. If scaling campaign later (File 17 Budget & Scaling Optimizer):
   - Watch for expansion physics (gradual CAC rise is expected)
   - Maintain budget increases ≤20-30% per adjustment
   - Wait 48-72 hours between scaling actions

6. Competitive monitoring (File 19 Competitive Density):
   - Track competitor ad activity in Meta Ad Library
   - If new competitor enters with similar positioning, expect CPA +10-15%
   - Prepare differentiation messaging in creative rotation

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
NEXT STEPS
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

[✓ Proceed to Campaign Launch] [← Adjust Variables] [💰 Revise LTV]
```

**User selects**: ✓ Proceed to Campaign Launch

**MMAA Processing Time**: 8 minutes (LTV input 5 min + calculation 3 min)

**Total Time**: IVG 45 min + MMAA 8 min = **53 minutes total**

**Comparison**: vs. 6-8 hours manual strategic work + viability analysis

---

### Alternative Scenario: NO-GO Example

**If Economics Were Different:**

```
LTV: $300 (lower pricing tier)
Viable CAC Ceiling: $114 (after adjustments)
Expected CPA: $120 (Identification stage)
Utilization: 105% → NO-GO ✗

REASONING:
Estimated CPA of $120 exceeds viable CAC ceiling of $114 by 5%. This
indicates the campaign would likely operate at break-even or slight loss.
LTV:CAC ratio would be 2.5:1, below the 3:1 healthy benchmark.

RECOMMENDATIONS:
1. ✗ DO NOT proceed with Identification stage at current pricing
2. Option A: Move to Exploration stage (expected CPA $30) → 26% utilization → GO ✓
3. Option B: Increase pricing 20% → LTV $360 → Ceiling $137 → 88% utilization → CAUTION ⚠️
4. Option C: Optimize targeting to reduce expected CPA to <$100 → 88% utilization → CAUTION ⚠️

[← Adjust Variables] [💰 Revise Pricing] [❌ Cancel Campaign]
```

---

## Risk Mitigation

### Research Quality Risks

- Multi-source validation (2+ sources for key claims)
- Confidence scoring for all findings
- Human review checkpoints for low-confidence areas
- Source quality filtering

### LLM Hallucination Risks

- Hard validation rules prevent structural violations
- Evidence requirement: every claim cites research
- Multi-LLM validation (cross-check with different models)
- User review mandatory for all variables

### Framework Misinterpretation Risks

- Extensive prompt engineering with framework quotes
- Examples library of correct definitions
- Fine-tuning on validated variable sets
- Framework creator review (initially)

---

## Critical Reference Files

1. **[07-Immutable-Global-Variables.md](./META-ADS-VAULT/02-STRUCTURAL-STRATEGY/07-Immutable-Global-Variables.md)** - Complete variable definitions, requirements, validation rules
2. **[22-Master-Checklists-and-Execution-Templates.md](./META-ADS-VAULT/04-OPERATIONAL-CONTROL/22-Master-Checklists-and-Execution-Templates.md)** - Campaign Definition Sheet template structure
3. **[09-Cognitive-Stages-and-Optimization-Contracts.md](./META-ADS-VAULT/02-STRUCTURAL-STRATEGY/09-Cognitive-Stages-and-Optimization-Contracts.md)** - Stage definitions, optimization events, CTA ranges
4. **[08-User-States-and-Observable-Signals.md](./META-ADS-VAULT/02-STRUCTURAL-STRATEGY/08-User-States-and-Observable-Signals.md)** - S0/S1 definitions, observable signals
5. **[Glossary-and-Acronyms.md](./META-ADS-VAULT/05-REFERENCE/Glossary-and-Acronyms.md)** - Authoritative definitions for all 9 variables

---

_This Intelligent Variable Generator system represents a sophisticated application of AI research agents, multi-LLM reasoning, and strict validation logic to automate the complex strategic process of defining campaign variables, reducing expert-level work from 6-8 hours to 45-60 minutes while maintaining framework compliance and quality._
