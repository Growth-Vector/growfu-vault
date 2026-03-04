# IVG Design Document Improvement Plan

## Context

The Intelligent Variable Generator (IVG) design document has **21 open GitHub issues** identifying areas that need clarification, expansion, or correction. These issues fall into four main categories:

1. **Research Phase Clarity** (9 issues) - What information to collect, how to validate it, and how to link company inputs with research findings
2. **Variable Definition Enhancement** (6 issues) - Adding examples and improving clarity of variable definitions
3. **S0/S1 Integration** (4 issues) - Properly integrating User States and Observable Signals throughout the workflow
4. **Cross-Validation** (2 issues) - Ensuring consistency and congruency across all components

The current IVG design is a 1,812-line specification that transforms minimal user inputs into complete GrowFu v3 campaign definitions. However, it has critical gaps in:
- Defining **what specific information** research agents should extract (vs. just listing data sources)
- Clarifying that variables are **generated from research**, not researched directly
- Properly integrating **S0/S1 user states** and **progress signals** into the variable generation process
- Providing **concrete examples** for each variable definition
- Ensuring **congruency validation** across research findings

This plan addresses all 21 issues systematically to create a complete, implementable IVG specification.

---

## Critical Files

- `/Users/danny/projects/growfu/growfu-vault/INTELLIGENT-VARIABLE-GENERATOR-DESIGN.md` - Main file to be improved
- `META-ADS-VAULT/02-STRUCTURAL-STRATEGY/07-Immutable-Global-Variables.md` - Variable definitions reference
- `META-ADS-VAULT/02-STRUCTURAL-STRATEGY/08-User-States-and-Observable-Signals.md` - S0/S1 templates
- `META-ADS-VAULT/02-STRUCTURAL-STRATEGY/09-Cognitive-Stages-and-Optimization-Contracts.md` - Stage specifications
- `META-ADS-VAULT/04-OPERATIONAL-CONTROL/22-Master-Checklists-and-Execution-Templates.md` - Output template
- `META-ADS-VAULT/04-OPERATIONAL-CONTROL/24-Marketing-Metrics-Analysis-Agent.md` - MMAA integration

---

## Phase 1: Research Phase Improvements (Issues #10, #11, #12, #13, #14, #15, #16, #17, #21)

### Problem

The current Research Phase (lines 114-290) lists **data sources** but doesn't specify **what strategic information** needs to be extracted. This is critical because:

- **Issue #12 (DANGEROUS)**: The document incorrectly implies we "research" variables like PS/OF/BR, when we actually **generate them from research findings**
- **Issue #11**: "The most important aspect" - we must define the needed information output from each research agent
- **Issue #10**: Research findings must be cross-validated with company-provided questionnaire data
- Issues #13-#17, #21: Specific research outputs are too vague or missing

### Solution

**1.1 Add "Research Intelligence Requirements" Section** (after line 125)

Insert a new subsection defining what each research agent must extract:

```markdown
### 1.1 Research Intelligence Requirements

**Critical Distinction**: The IVG does NOT research the 9 variables directly. It researches **strategic intelligence** that will be used to GENERATE variables.

**What We Research:**
- Observable user behaviors and pain points
- Behavioral patterns and cognitive errors in the problem space
- Competitive positioning and messaging patterns
- Brand voice and emotional positioning
- Product mechanics and behavioral outcomes
- Industry benchmarks and success patterns

**What We Generate (NOT Research):**
- PS, OF, BR, CS, VE, EA, AL, CTA-R, SCR definitions
- S0/S1 user state models
- Progress signals and false positive detection
- Campaign architecture recommendations

**Research Output Requirements** (per agent):

1. **Company Research Output Requirements:**
   - Observable behavioral outcomes (what users DO differently after using product)
   - Current brand voice patterns (tone, emotional positioning, semantic patterns)
   - Feature → Benefit → Behavioral Outcome mapping
   - Existing problem framing (if any)
   - Customer outcome language (from testimonials/case studies)
   - Brand positioning claims vs. actual product mechanics
   - **KPIs mentioned or implied** in existing materials
   - **Successful creative patterns** in current ads (if available)

2. **Industry Research Output Requirements:**
   - Common cognitive/behavioral errors in this problem space
   - Observable symptoms of the problem (what people DO wrong)
   - Typical customer journey stages and behavioral signals
   - Industry-standard success metrics and KPIs
   - Documented behavioral patterns in this vertical
   - Stage-specific CPA benchmarks for industry

3. **Competitor Research Output Requirements:**
   - Competitor problem framing approaches
   - Emotional axes used (inferred from messaging)
   - Brand role positioning (above/beside/behind)
   - CTA intensity patterns
   - Value expression types detected (INSIGHT/VALIDATION/FRAMEWORK/SYSTEM)
   - **Successful creative families** (dominant patterns, formats, hooks)
   - **Successful variations** within families (what changes, what stays constant)
   - Ad saturation analysis (which approaches are overused)
   - **Creative engineering insights**: format preferences, visual patterns, hook structures

4. **Audience Research Output Requirements:**
   - Observable S0 signals (what they consume, ignore, micro-actions, avoidance behaviors)
   - Problem language (how they describe issues in their own words)
   - Behavioral progression patterns (exploration → decision)
   - Rejection/avoidance behaviors
   - Trust-building signals they respond to
   - Typical progress signals per stage
```

**1.2 Enhance Section 1.2 "Company Research Agent"** (lines 128-171)

Add specific output requirements to the Company Intelligence Profile JSON schema:

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
    "behavioral_outcomes": ["what users DO differently"],
    "feature_to_outcome_map": {
      "feature_name": "observable behavioral change"
    }
  },
  "kpis_mentioned": {
    "explicit": ["KPIs mentioned in materials"],
    "implicit": ["KPIs implied by goals/positioning"]
  },
  "current_creative_patterns": {
    "formats": ["video", "carousel", "static"],
    "dominant_hooks": ["pattern types"],
    "cta_patterns": ["existing CTA approaches"],
    "visual_patterns": ["brand visual elements"]
  },
  "evidence": [{"claim": "...", "source": "url", "quote": "..."}]
}
```

**1.3 Enhance Section 1.4 "Competitor Research Agent"** (lines 197-233)

Expand the Competitive Intelligence Profile to include creative engineering insights:

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
      "value_expression_type": "INSIGHT|VALIDATION|FRAMEWORK|SYSTEM",
      "successful_creative_families": [
        {
          "family_name": "Problem-Agitation-Solution",
          "format": "video",
          "hook_pattern": "Question hook → pain amplification → solution reveal",
          "performance_indicators": "high engagement, strong CTR",
          "immutable_elements": ["problem statement", "solution mechanism"],
          "variable_elements": ["specific example", "visual style"]
        }
      ],
      "ad_examples": [{"text": "...", "image_url": "...", "analysis": "..."}]
    }
  ],
  "creative_engineering_insights": {
    "dominant_formats": ["which formats are most used"],
    "hook_patterns": ["question hooks", "stat hooks", "story hooks"],
    "visual_patterns": ["product demos", "testimonials", "diagrams"],
    "successful_variations": ["what changes while maintaining identity"]
  },
  "market_gaps": ["opportunities not addressed by competitors"],
  "saturation_analysis": "which approaches are overused"
}
```

**1.4 Add Cross-Validation Section** (after line 290)

Insert new section before Phase 2:

```markdown
### 1.6 Company Input vs. Research Cross-Validation

**Purpose**: Ensure congruency between what the company says about themselves and what research reveals.

**Process**:
1. Compare company-provided positioning with actual product mechanics
2. Validate claimed outcomes against customer testimonials
3. Identify discrepancies between brand voice claims and actual messaging
4. Flag misalignments for user clarification

**Validation Checks**:
```python
class CompanyResearchValidator:
    def validate_congruency(self, company_input, research_findings):
        """
        Cross-validate company questionnaire data with research findings
        """
        discrepancies = []

        # Check: Does claimed positioning match actual product mechanics?
        if company_input['positioning'] != research_findings['actual_positioning']:
            discrepancies.append({
                'type': 'positioning_mismatch',
                'company_claims': company_input['positioning'],
                'research_shows': research_findings['actual_positioning'],
                'severity': 'HIGH',
                'action': 'Clarify with user: which positioning should IVG use?'
            })

        # Check: Are claimed outcomes actually observable behaviors?
        for outcome in company_input['desired_outcomes']:
            if not is_observable_behavior(outcome):
                discrepancies.append({
                    'type': 'non_observable_outcome',
                    'claim': outcome,
                    'severity': 'MEDIUM',
                    'action': 'Convert to observable behavior during OF generation'
                })

        # Check: Does brand voice in materials match claimed voice?
        if brand_voice_mismatch(company_input['brand_voice'], research_findings['actual_voice']):
            discrepancies.append({
                'type': 'brand_voice_inconsistency',
                'severity': 'MEDIUM',
                'action': 'Present both options to user for selection'
            })

        # Check: Are objectives researchable or strategic decisions?
        for objective in company_input['objectives']:
            if is_strategic_decision(objective):  # e.g., "We want to target Decision stage"
                discrepancies.append({
                    'type': 'strategic_vs_research',
                    'objective': objective,
                    'severity': 'LOW',
                    'action': 'Note as user preference, validate economic viability'
                })

        return discrepancies
```

**When Discrepancies Found**:
- **HIGH severity**: Block and ask user to clarify before proceeding
- **MEDIUM severity**: Present both options with reasoning, let user choose
- **LOW severity**: Note in evidence pack, proceed with research-based recommendation
```

---

## Phase 2: Variable Definition Enhancements (Issues #1, #2, #5, #6, #7, #8)

### Problem

Variable definitions lack concrete examples and some have ambiguous language that could lead to incorrect generation.

### Solution

**2.1 PS Generator Section (lines 305-373)**

**Issue #1 & #2 Fixes:**

After line 311 (Framework Requirements), add:

```markdown
**Clarification on "Not Psychological"**:
- PS can involve emotional or cognitive errors
- The key is that symptoms must be **observable behaviors**, not internal states
- ✅ CORRECT: "Users feel overwhelmed" → Observable symptom: "Users abandon task after 3+ tool switches"
- ❌ INCORRECT: Symptom is "Users feel confused" (internal state, not observable)

**Complete PS Examples**:

**Example 1: B2B SaaS Marketing Analytics**
- **PS Definition**: Marketing teams make strategic decisions using incomplete data because their metrics are fragmented across disconnected tools
- **Symptom 1**: Spending 15+ hours weekly manually compiling reports from 5+ sources
- **Symptom 2**: Making channel allocation decisions based on most accessible data rather than most relevant
- **Symptom 3**: Presenting inconsistent numbers across meetings due to different data pulls
- **Structural Cause**: Tool fragmentation creates information access inequality
- **Evidence**: 73% of marketing teams lack unified dashboards (industry report), testimonials mention "spreadsheet hell"

**Example 2: E-commerce Conversion Optimization**
- **PS Definition**: Online store owners optimize for conversion without understanding behavioral segmentation, treating all traffic identically
- **Symptom 1**: Running same landing page for cold and warm traffic
- **Symptom 2**: Measuring only aggregate conversion rate, missing segment-specific patterns
- **Symptom 3**: Making optimization decisions based on overall CTR rather than segment performance
- **Structural Cause**: Analytics tools show aggregates by default, segmentation requires manual setup
- **Evidence**: Default GA4 dashboards show totals, customer interviews reveal "we just look at the main number"

**Example 3: B2C Fitness Coaching**
- **PS Definition**: People abandon fitness programs because they lack observable progress milestones between "start" and "goal weight"
- **Symptom 1**: Checking scale daily, feeling discouraged when no change
- **Symptom 2**: Quitting programs in weeks 2-4 (before visible results)
- **Symptom 3**: Restarting programs repeatedly rather than progressing through one
- **Structural Cause**: Long feedback loops (4-6 weeks for visible results) create motivation gaps
- **Evidence**: Retention data shows 67% drop-off in weeks 2-4, forum posts mention "not seeing results"
```

**2.2 OF Generator Section (lines 375-439)**

**Issue #3, #18, #19, #20 Fixes:**

After line 417, add:

```markdown
**OF Must Link to S0/S1 User States**

Every OF must decompose into:
1. **S0 (Observable Initial State)** - Behavioral signals BEFORE intervention
2. **S1 (Target State)** - Observable progression AFTER engagement
3. **Progress Signals** - Confirm S0→S1 transition

**OF Examples with S0/S1 Mapping**:

**Example 1: Marketing Analytics SaaS (Identification Stage)**
- **OF**: Marketing leaders evaluate channel performance using unified attribution methodology across all channels instead of fragmented data sources
- **S0 Observable Signals**:
  - What they consume: "marketing analytics" content, comparison articles, >6s video views
  - What they ignore: Purchase CTAs, high-commitment forms
  - Micro-actions: LPV on "how it works" pages, engagement with framework content
  - Avoidance: Avoid trial signups, skip pricing pages
- **S1 Target State**: User views framework presentation (LPV on framework page, >30s engagement)
- **Progress Signals**:
  - PRIMARY: LPV with >30s engagement on framework page
  - SECONDARY: Return visits, save post, profile click
  - CONFIRMATION: Engagement with specific framework elements (clicks on diagram sections)
- **False Positives**: LPV <5s (bounce), fast scroll-through without stops

**Example 2: E-commerce Optimization Tool (Validation Stage)**
- **OF**: Store owners implement segment-specific landing pages for traffic sources instead of one-size-fits-all approach
- **S0 Observable Signals**:
  - What they consume: Case studies, implementation guides, demo videos
  - Micro-actions: Lead form views (not submissions), demo request page visits
  - What they engage: "How to implement" content, setup documentation
  - Avoidance: Skip generic "sign up" CTAs
- **S1 Target State**: User requests demo or implementation guide (Lead event)
- **Progress Signals**:
  - PRIMARY: Lead form submission
  - SECONDARY: Demo video watch time >80%, documentation downloads
  - CONFIRMATION: Return visits within 48 hours
- **False Positives**: Low-quality leads (fake emails, bounces), form abandonment >50%

**Context Embedding for OF** (Issue #20):

When generating OF, embed full context:
- PS definition (the error being addressed)
- Research findings on current user behaviors
- Product mechanics (how intervention creates change)
- Competitive landscape (what others promise)
- Stage requirements (what's achievable at this stage)
```

**2.3 EA Generator Section (lines 559-573)**

**Issue #5 Fix:**

Replace lines 559-573 with:

```markdown
### 2.6 EA (Emotional Axis) Generator

**Framework Requirements**:
- **Definition**: EA defines the emotional transition the creative facilitates (not the behavioral change - that's OF)
- **Format**: [From State] → [To State]
- **One per campaign** (never mixed)
- **Common axes**:
  - confusion → clarity
  - insecurity → confidence
  - overwhelm → control
  - frustration → relief
  - anxiety → calm
  - doubt → certainty

**Key Distinction**:
- **EA** = EMOTIONAL journey (internal state transition)
- **OF** = BEHAVIORAL change (observable action)
- They must be complementary

**EA Examples with OF Pairing**:

| EA (Emotional) | OF (Behavioral) | Why They Align |
|---|---|---|
| confusion → clarity | Users evaluate options using a framework rather than guessing | Framework provides structure that creates clarity |
| overwhelm → control | Users segment traffic sources instead of treating all traffic identically | Segmentation gives sense of control over chaos |
| anxiety → calm | Users track progress with daily milestones instead of only checking final weight | Frequent milestones reduce anxiety of long feedback loops |
| frustration → relief | Users consolidate data into one dashboard instead of switching between 5+ tools | Relief from manual compilation frustration |

**Validation Logic**:
```python
def validate_ea(ea_definition, of_definition):
    errors = []

    if not follows_format(ea_definition, "X → Y"):
        errors.append("EA must be in format 'from_state → to_state'")

    if contains_behavioral_language(ea_definition):
        errors.append("EA describes actions/behaviors - should be emotions only")

    if not complements_of(ea_definition, of_definition):
        errors.append("EA emotional transition doesn't complement OF behavioral change")

    return errors
```
```

**2.4 AL Generator Section (lines 575-583)**

**Issue #6 Fix:**

Replace lines 575-583 with:

```markdown
### 2.7 AL (Abstraction Level) Generator

**Framework Requirements**:
- **Definition**: AL controls how conceptual vs. concrete the creative is
- **Levels**: High / Medium / Low
- **Content**: Can be High or Medium (thought leadership, frameworks)
- **Ads**: Must be Medium or Low (never High)
- **Stage Constraint**:
  - Early stage (Exploration) → can be more abstract (Medium)
  - Decision stage → must be concrete (Low)

**Abstraction Level Examples**:

| Level | Description | Example Content | When to Use |
|---|---|---|---|
| **High** | Abstract concepts, philosophical | "Rethinking attribution in the age of privacy" | Thought leadership blog posts, NOT ads |
| **Medium** | Concept + concrete example | "The 3-Layer Attribution Framework: Source → Channel → Touchpoint" | Exploration/Identification ads, frameworks |
| **Low** | Specific, actionable, tangible | "See your Instagram ad ROI in 4 clicks: Dashboard → Instagram → Performance → ROI" | Validation/Decision ads, demos |

**Stage-AL Mapping**:
- Exploration: Medium (can introduce framework/concept with example)
- Identification: Medium (show framework application)
- Validation: Low (concrete implementation steps)
- Decision: Low (specific action, tangible outcome)

**Validation Logic**:
```python
def validate_al(al_level, cs_stage):
    errors = []

    if al_level == 'High':
        errors.append("Ads must not use High abstraction (content only)")

    if cs_stage == 'Decision' and al_level != 'Low':
        errors.append("Decision stage requires Low abstraction (concrete)")

    return errors
```
```

**2.5 CTA-R Generator Section (lines 587-607)**

**Issue #7 Fix:**

After line 607, add:

```markdown
**Complete CTA-R Definition**:

CTA-R defines how strong you can push the call-to-action without breaking coherence. It is constrained by:
1. **Cognitive Stage** (dominant constraint)
2. **Brand Role** (secondary constraint)
3. **Trust Level** (from research findings)

**Stage-Specific Ranges** (Hard Constraints):

| Stage | Min Intensity | Max Intensity | Example CTAs | Why Constrained |
|---|---|---|---|---|
| **Exploration** | Passive curiosity | Light information | "See how it works", "Watch the breakdown" | User just learning problem exists |
| **Identification** | Informational | Educational | "Learn the framework", "Discover the approach" | User seeing if they match |
| **Validation** | Educational | Commitment signal | "Get the guide", "Register for demo" | User validating trust |
| **Decision** | Commitment | Direct action | "Start your trial", "Buy now", "Join today" | User ready to execute |

**Brand Role Modulation**:
- **Position = Above** (Authority): Can use stronger CTAs at each stage
- **Position = Beside** (Peer): Must use collaborative CTAs ("Let's explore")
- **Position = Behind** (Enabler): Must use empowering CTAs ("Start building")

**Examples**:

**Exploration Stage + Above Brand Role**:
- Minimum: "See how it works"
- Maximum: "Learn from experts"
- Too weak: "Maybe check this out"
- Too strong: "Get started today"

**Validation Stage + Beside Brand Role**:
- Minimum: "Explore the implementation guide"
- Maximum: "Join the workshop"
- Too weak: "Learn more"
- Too strong: "Buy now"
```

**2.6 SCR Generator Section (lines 609-625)**

**Issue #8 Fix:**

After line 625, replace with:

```markdown
### 2.9 SCR (Semantic Consistency Rules) Generator

**Framework Requirements**:
- **Definition**: SCR defines what cannot change without creating a new system, and what must remain consistent across all creatives to enable learning
- **Core promise**: Must appear in all creatives (exact phrase or semantic equivalent)
- **Required language**: Specific words/phrases to always use
- **Forbidden claims**: What cannot be promised (regulatory, competitive, brand)
- **Immutable theme**: The unchanging semantic identity

**Purpose**:
- Prevent semantic variation that destroys learning
- Ensure platform can identify this as ONE system
- Maintain brand and regulatory compliance

**SCR Components**:

1. **Core Promise** (must appear in every creative):
   - The fundamental value proposition
   - Can be reworded but semantic meaning must be identical
   - Example: "Unified marketing dashboard" vs "All your marketing data in one place" (same meaning)

2. **Required Language** (words that must appear):
   - Brand-specific terms
   - Category-defining language
   - Differentiators
   - Example: "unified", "attribution", "single source of truth"

3. **Forbidden Claims** (never promise):
   - Regulatory violations
   - Unsubstantiated superlatives
   - Competitor mentions (if prohibited)
   - Example: "Never use 'guaranteed results', '100% ROI', specific competitor names"

4. **Immutable Theme**:
   - The semantic identity that cannot change
   - Links to PS, OF, EA
   - Example: "Overwhelm → Control through consolidation" (theme: consolidation solves overwhelm)

**Complete SCR Example**:

```json
{
  "core_promise": {
    "canonical_form": "See all your marketing performance in one unified dashboard with consistent attribution",
    "semantic_equivalents": [
      "All marketing data consolidated with unified attribution",
      "One dashboard, consistent attribution across all channels"
    ],
    "forbidden_variations": [
      "Multiple dashboards" (contradicts "one"),
      "Estimated attribution" (contradicts "consistent")
    ]
  },
  "required_language": {
    "must_include": ["unified", "attribution", "dashboard"],
    "frequency": "At least 2 of 3 in every creative",
    "reasoning": "Category definition + differentiation"
  },
  "forbidden_claims": [
    "guaranteed ROI",
    "100% accurate attribution",
    "mention competitor names",
    "promise specific percentage improvements"
  ],
  "immutable_theme": "Consolidation solves fragmentation overwhelm",
  "semantic_boundaries": {
    "can_vary": ["specific examples", "use cases", "customer stories"],
    "cannot_vary": ["core consolidation promise", "attribution accuracy claim", "emotional outcome (control)"]
  }
}
```

**Why This Matters**:
- Changing core promise = different system (resets learning)
- Varying required language = semantic drift (confuses platform)
- Breaking forbidden claims = regulatory risk
- Losing immutable theme = identity confusion
```

---

## Phase 3: S0/S1 Integration Throughout (Issues #3, #18, #19, #20)

### Problem

S0/S1 user states are mentioned but not properly integrated into the variable generation workflow. Progress signals are missing from outputs.

### Solution

**3.1 Add S0/S1 Generator to Phase 2** (after line 625)

Insert new section:

```markdown
### 2.10 S0/S1 User State Generator

**Framework Requirements** (from File 8):
- **S0 (Observable Initial State)**: Behavioral signal profile BEFORE intervention
- **S1 (Target State)**: Measurable progression AFTER engagement
- **Progress Signals**: Confirm S0→S1 transition
- **False Positive Signals**: Noise to ignore

**Dependencies**:
- Requires PS, OF, and CS to be locked first
- S0/S1 must match the cognitive stage
- Must use platform-observable signals only

**LLM Prompt Template**:
```xml
<context>
You are defining S0/S1 User States for GrowFu campaign.

FRAMEWORK REQUIREMENTS:
- S0 = Observable behavioral signals BEFORE intervention
- S1 = Measurable progression AFTER engagement
- All signals must be platform-observable (no internal psychology)
- Must align with Cognitive Stage optimization event

LOCKED VARIABLES:
PS: {ps_definition}
OF: {of_definition}
CS: {cs_stage} (optimizes for {optimization_event})

S0 TEMPLATE:
- What they consume (content types, formats, engagement depth)
- What they ignore (scroll patterns, skips, avoidance)
- Micro-actions they perform (clicks, views, engagement signals)
- What they avoid (high-commitment CTAs, forms)

S1 TEMPLATE:
- Primary signal (matches optimization event)
- Secondary signals (supporting indicators)
- Confirmation signals (validate genuine progress)

TASK:
Generate S0/S1 definitions that:
1. Describe observable behaviors aligned with PS
2. Define S1 progression that moves toward OF
3. Match CS stage optimization event
4. Provide progress signals and false positive detection
</context>
```

**Complete S0/S1 Example** (Identification Stage, Marketing Analytics SaaS):

```json
{
  "s0_observable_initial_state": {
    "what_they_consume": {
      "content_categories": ["marketing analytics", "attribution guides", "tool comparisons"],
      "formats": ["video >6s", "framework diagrams", "case studies"],
      "engagement_depth": "Moderate - watch 40-60% of videos, skim articles",
      "platform_signals": ["Video View >6s", "ThruPlay on shorter content", "2+ post engagement"]
    },
    "what_they_ignore": {
      "scroll_patterns": "Fast scroll past generic CTAs",
      "skips": "Skip purchase-focused content immediately",
      "avoidance_signals": ["Hide ads with 'Buy now'", "Bounce from pricing pages <5s"],
      "platform_signals": ["Skip <1s", "Hide ad", "Negative feedback"]
    },
    "micro_actions": {
      "light_intent": ["Profile click", "Save post", "LPV on 'how it works' page"],
      "exploration": ["Watch framework explanation video >50%", "Engage with diagram"],
      "platform_signals": ["LPV", "Save", "Engagement >15s"]
    },
    "what_they_avoid": {
      "high_commitment": ["Trial signup", "Demo request", "Purchase"],
      "forms": "Avoid lead forms at this stage",
      "platform_signals": ["Lead form view but no submit", "Bounce from trial page"]
    }
  },
  "s1_target_state": {
    "primary_signal": {
      "event": "LPV (Landing Page View)",
      "requirement": "View framework presentation page",
      "duration": ">30s engagement",
      "platform_optimization": "Optimize for LPV event"
    },
    "description": "User views framework presentation, indicating they see themselves in the positioning and want to understand the approach",
    "behavioral_shift": "From passive content consumption to active framework exploration"
  },
  "progress_signals": {
    "primary": {
      "signal": "LPV on framework page",
      "threshold": ">30s engagement",
      "confidence": "HIGH - matches optimization event"
    },
    "secondary": [
      {
        "signal": "Return visit within 48 hours",
        "threshold": "2+ visits",
        "confidence": "MEDIUM - indicates consideration"
      },
      {
        "signal": "Engagement with specific framework elements",
        "threshold": "Click on diagram sections, scroll to examples",
        "confidence": "MEDIUM - indicates genuine interest"
      }
    ],
    "confirmation": {
      "signal": "Time on framework page",
      "threshold": ">1 minute",
      "confidence": "HIGH - reading, not bouncing"
    }
  },
  "false_positive_detection": {
    "signals": [
      {
        "signal": "LPV <5s (bounce)",
        "reason": "Accidental click, not genuine interest",
        "action": "Exclude from positive learning"
      },
      {
        "signal": "Fast scroll-through without stops",
        "reason": "Scanning, not reading",
        "action": "Low-quality signal, weight down"
      },
      {
        "signal": "High CTR + low LPV rate",
        "reason": "Clickbait creative, misleading hook",
        "action": "Negative feedback - creative attracts wrong users"
      }
    ]
  },
  "stage_transition_readiness": {
    "ready_for_validation": [
      "Multiple LPVs on framework page",
      "Return visits",
      "Engagement >2 minutes total"
    ],
    "signals_user_not_ready": [
      "Only Video Views, no LPVs",
      "Bounce from framework page",
      "No return visits"
    ]
  }
}
```

**Validation Logic**:
```python
def validate_s0_s1(s0_s1_definition, cs_stage, of_definition):
    errors = []

    # S1 primary signal must match CS optimization event
    stage_event_map = {
        'Exploration': 'ThruPlay',
        'Identification': 'LPV',
        'Validation': 'Lead',
        'Decision': 'Purchase'
    }

    if s0_s1_definition['s1_target_state']['primary_signal']['event'] != stage_event_map[cs_stage]:
        errors.append(f"S1 primary signal must be {stage_event_map[cs_stage]} for {cs_stage} stage")

    # S1 must move toward OF
    if not s1_progresses_toward_of(s0_s1_definition['s1_target_state'], of_definition):
        errors.append("S1 target state doesn't progress toward OF behavioral change")

    # All signals must be platform-observable
    for signal_category in s0_s1_definition['s0_observable_initial_state'].values():
        if not all_signals_observable(signal_category):
            errors.append("S0 contains non-observable signals (internal psychology)")

    return errors
```
```

**3.2 Update Phase 6 "Final Output Generation"** (lines 799-830)

Add S0/S1 and Progress Signals to Campaign Definition Sheet output:

```markdown
### 6.1 Campaign Definition Sheet

Complete 22-field Campaign Definition Sheet in File 22 format:

**Sections**:
1. System Identity (PS, OF, BR)
2. Campaign Configuration (CS, VE, EA, AL, CTA-R)
3. Semantic Rules (SCR)
4. **User State Model** (S0, S1, Progress Signals, False Positives) ← ENHANCED
5. Campaign Architecture
6. Governance

**User State Model Section** (added to output):
```json
{
  "user_state_model": {
    "s0_observable_initial_state": {
      "what_they_consume": "...",
      "what_they_ignore": "...",
      "micro_actions": "...",
      "what_they_avoid": "..."
    },
    "s1_target_state": {
      "primary_signal": "LPV",
      "behavioral_shift": "...",
      "description": "..."
    },
    "progress_signals": {
      "primary": "LPV >30s",
      "secondary": ["Return visit", "Engagement depth"],
      "confirmation": "Time on page >1min"
    },
    "false_positive_detection": [
      "LPV <5s (bounce)",
      "High CTR + low LPV"
    ]
  }
}
```
```

---

## Phase 4: Cross-Validation Enhancements (Issues #4, #9)

### Problem

No explicit congruency validation across research agents, and CS stage specifications need better definition.

### Solution

**4.1 Enhance Section 1.6 "Knowledge Synthesis Engine"** (lines 277-290)

Add congruency validation:

```markdown
### 1.6 Knowledge Synthesis Engine

**Technology**: Claude Opus 4.6 (best reasoning model)

**Process**:
1. Ingest all 4 research agent outputs
2. **Cross-reference and validate congruency** ← ENHANCED
3. Identify contradictions and resolve with evidence weight
4. Build unified knowledge graph
5. Tag all claims with evidence provenance

**Congruency Validation** (Issue #9):

**Purpose**: Ensure research findings from different agents are consistent and complementary. If not, flag discrepancies for user clarification.

**Validation Checks**:
```python
class ResearchCongruencyValidator:
    def validate_cross_agent_congruency(self, company_research, industry_research,
                                        competitor_research, audience_research):
        """
        Check if research from 4 agents tells a consistent story
        """
        discrepancies = []

        # Check 1: Company brand voice vs. competitor analysis
        company_voice = company_research['brand_voice']['tone']
        inferred_positioning = competitor_research['gap_positioning']

        if voice_contradicts_positioning(company_voice, inferred_positioning):
            discrepancies.append({
                'type': 'voice_positioning_mismatch',
                'company_claims': company_voice,
                'market_analysis_suggests': inferred_positioning,
                'severity': 'MEDIUM',
                'action': 'Present both to user: maintain claimed voice or adapt to market gap?'
            })

        # Check 2: Company outcome claims vs. audience research
        company_outcomes = company_research['customer_outcomes']
        audience_desires = audience_research['outcome_desires']

        if not outcomes_match_audience_language(company_outcomes, audience_desires):
            discrepancies.append({
                'type': 'outcome_language_mismatch',
                'company_describes': company_outcomes,
                'audience_describes': audience_desires,
                'severity': 'HIGH',
                'action': 'Use audience language for OF, note company language in SCR'
            })

        # Check 3: Industry benchmarks vs. competitive reality
        industry_cpa = industry_research['stage_cpa_benchmarks']
        competitive_density = competitor_research['saturation_analysis']

        if high_competition_contradicts_benchmarks(competitive_density, industry_cpa):
            discrepancies.append({
                'type': 'cpa_competition_mismatch',
                'industry_benchmark': industry_cpa,
                'competitive_reality': 'High saturation suggests 20-30% higher CPA',
                'severity': 'MEDIUM',
                'action': 'Adjust expected CPA in MMAA viability analysis'
            })

        # Check 4: Product mechanics vs. problem space
        product_mechanics = company_research['product_mechanics']
        industry_problems = industry_research['common_errors']

        if not product_addresses_problem(product_mechanics, industry_problems):
            discrepancies.append({
                'type': 'product_problem_mismatch',
                'product_solves': product_mechanics['behavioral_outcomes'],
                'industry_problems': industry_problems,
                'severity': 'HIGH',
                'action': 'BLOCK: Product may not address researchable problem space'
            })

        # Check 5: Audience S0 signals vs. competitor targeting
        audience_s0 = audience_research['observable_s0_signals']
        competitor_targeting = competitor_research['targeting_patterns']

        if audience_already_saturated(audience_s0, competitor_targeting):
            discrepancies.append({
                'type': 'audience_saturation',
                'finding': 'Audience S0 signals heavily targeted by competitors',
                'severity': 'LOW',
                'action': 'Note in risk factors, may require different S0 identification'
            })

        return discrepancies
```

**Resolution Process**:
- **HIGH severity**: Block generation, require user input to resolve
- **MEDIUM severity**: Present both options with reasoning
- **LOW severity**: Note in evidence pack, proceed with best judgment

**Output**: Synthesized Intelligence Base with:
- Full evidence trails
- Conflict resolution notes
- **Congruency validation report** ← NEW
- Confidence scores
- Gaps identified
```

**4.2 Enhance Section 2.4 "CS (Cognitive Stage) Generator"** (lines 493-535)

Add complete stage specifications (Issue #4):

```markdown
### 2.4 CS (Cognitive Stage) Generator

**Framework Requirements**:
- Choose ONE stage: Exploration → Identification → Validation → Decision
- **Each stage has one of each** (Issue #4): ← ENHANCED
  - **One objective** (what user is trying to do)
  - **One Value Expression Type** (how you present value)
  - **One dominant optimization event** (what platform optimizes for)
  - **One CTA intensity range** (how strong you can push)
  - **Specific targeting logic** (who to target)

**Complete Stage Specifications**:

| Stage | Objective | VE Type | Opt. Event | CTA Range | Targeting | Min Events/Week |
|---|---|---|---|---|---|---|
| **Exploration** | Awareness | INSIGHT or VALIDATION | ThruPlay, VV | Passive curiosity | Broad, Advantage+ | 50+ |
| **Identification** | Recognition | VALIDATION or FRAMEWORK | LPV | Informational | Soft retargeting, Lookalike | 50+ |
| **Validation** | Trust | FRAMEWORK or SYSTEM | Lead | Commitment signal | Strong retargeting | 50+ |
| **Decision** | Action | SYSTEM | Purchase, Value | Direct action | Pure retargeting | 50+ |

**Detailed Stage Specifications**:

**Exploration Stage**:
- **Objective**: Create awareness that problem exists and is addressable
- **VE Type**: INSIGHT (reframe problem) or VALIDATION (normalize error)
- **Optimization Event**: ThruPlay (15s+ video view) or Video View (3s+)
- **CTA Range**:
  - Minimum: "See what we mean"
  - Maximum: "Learn how this works"
  - Never: "Buy", "Sign up", "Get started"
- **Targeting Logic**:
  - Broad interest targeting (500K+ audience)
  - Advantage+ for discovery
  - Lookalike 1-5% of all engaged users
- **Minimum Signal Volume**: 50+ ThruPlays per week
- **Typical CPA Range**: $15-40 (B2B SaaS), $5-20 (E-commerce)

[Continue for Identification, Validation, Decision with same detail level]

**Stage Selection Logic**:
```python
def select_cognitive_stage(product_type, audience_maturity, budget, ltv):
    """
    Recommend appropriate starting stage based on context
    """
    recommendations = []

    # Budget constraint check
    if budget < 5000:
        recommendations.append({
            'stage': 'Exploration',
            'reasoning': 'Budget <$5K best served by cheaper Exploration events',
            'expected_events': estimate_events('Exploration', budget)
        })

    # Product complexity check
    if product_complexity == 'high' and audience_maturity == 'cold':
        recommendations.append({
            'stage': 'Exploration',
            'reasoning': 'Complex product + cold audience requires problem framing first'
        })

    # LTV check
    if ltv < 300:
        recommendations.append({
            'stage': 'Exploration or Identification',
            'reasoning': 'Low LTV requires cheap events; Decision stage CPA likely exceeds viable CAC'
        })

    # Warm audience check
    if warm_audience_size > 1000:
        recommendations.append({
            'stage': 'Validation or Decision',
            'reasoning': 'Existing warm audience enables later-stage targeting',
            'prerequisite': 'Ensure warm audience is qualified (not just website visitors)'
        })

    return recommendations
```
```

---

## Phase 5: Final Verification & Plan File Completion

### Implementation Approach

All changes will be implemented as **additions and clarifications** to the existing INTELLIGENT-VARIABLE-GENERATOR-DESIGN.md file:

1. **Research Phase** (lines 114-290):
   - Add Section 1.1 "Research Intelligence Requirements" after line 125
   - Enhance Sections 1.2-1.5 with detailed output JSON schemas
   - Add Section 1.6 cross-validation before Phase 2

2. **Variable Generation** (lines 292-625):
   - Add concrete examples to PS, OF, EA, AL, CTA-R, SCR sections
   - Clarify ambiguous language (PS "not psychological" but observable)
   - Add Section 2.10 S0/S1 Generator after line 625

3. **Validation** (lines 627-685):
   - Enhance congruency validation in Section 3.2
   - Add complete CS stage specifications

4. **Output Generation** (lines 799-830):
   - Add S0/S1 and Progress Signals to Campaign Definition Sheet

5. **All Issues Cross-Reference**:
   - Each change will include comment noting which GitHub issue(s) it addresses

### Verification Plan

After implementation:
1. ✅ All 21 GitHub issues have corresponding improvements in the document
2. ✅ All examples are concrete and framework-compliant
3. ✅ All JSON schemas are complete and implementable
4. ✅ All validation logic is in working Python pseudo-code
5. ✅ S0/S1 integration is complete throughout the workflow
6. ✅ Cross-validation logic prevents incongruent research findings
7. ✅ Document maintains existing structure while adding clarity

### Success Criteria

- **Completeness**: Every research agent output is explicitly defined
- **Clarity**: All ambiguous language is clarified with examples
- **Integration**: S0/S1 user states properly integrated into variable generation
- **Validation**: Congruency checks prevent inconsistent research findings
- **Implementability**: All JSON schemas and code are ready for development
- **Framework Compliance**: All additions strictly follow File 7, 8, 9, 22 requirements

### Estimated Impact

- **Lines added**: ~800-1000 lines (examples, schemas, validation logic)
- **Sections added**: 3 new sections (1.1, 1.6 enhanced, 2.10)
- **Examples added**: 15-20 complete examples across all 9 variables
- **Validation logic added**: 5 new validation functions
- **GitHub issues resolved**: All 21 issues addressed

---

## Next Steps After Approval

1. Create detailed examples for all 9 variables
2. Write complete JSON schemas for all research outputs
3. Implement validation logic for congruency checks
4. Add S0/S1 generator with stage-specific templates
5. Update final output section with progress signals
6. Add inline comments referencing GitHub issues
7. Update verification standards to match new requirements
