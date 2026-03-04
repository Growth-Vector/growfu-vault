# GrowFu v3 Specification

Contains a knowledge-base of all GrowFu concepts and documentation. This is the main reference for all things GrowFu, including architecture, design principles, and implementation details. It serves as a comprehensive guide for developers, contributors, and users of the GrowFu framework.

It is an Obsidian vault, which means it is organized in a way that allows for easy navigation and linking between related concepts. Each concept is documented in its own markdown file, and these files are interconnected through links to create a cohesive knowledge base.

Location: ./META-ADS-VAULT
Index file: ./META-ADS-VAULT/00-INDEX/HOME.md

## 9 Immutable Global Variables

### Overview

GrowFu is a framework for building Meta Ads as a **learning and allocation system**. Meta doesn't "choose ads"—it allocates impressions by optimizing predicted outcomes under constraints. Your job is to create **learnable, stable, stage-appropriate creative systems** that the delivery system can confidently learn from and scale.

The most common failure mode in Meta Ads is **random variation that changes meaning, destroys learnability, and creates false learning**. When you change what your creative *means* (its problem space, promise, emotional axis, etc.), you reset the system's learning. The algorithm can't build on previous knowledge because you've fundamentally changed what it's trying to learn about.

These 9 Immutable Global Variables prevent this failure. They define the **structural identity** of your campaign system. Lock all 9 variables before creating any creative or campaign.

**Critical Rule:** If PS, OF, or BR change, it is not an iteration—it is another system. Start over.

---

### The 9 Variables

1. **Problem Space (PS)** — The recurring human error your campaign addresses

   **Purpose:** Defines what problem the campaign solves. This is the foundation of semantic identity—every creative must address the same core error pattern.

   **Why it matters:** If different ads address different problems, the system cannot learn "what works" because each ad means something different. The learning fragments instead of compounds.

   **Definition:** A recurring human error (cognitive, emotional, or behavioral) defined as a repeatable, observable pattern. Not a vague pain point—must be expressible as: 1 sentence definition + 3 observable symptoms.

   **Example:** "High-net-worth buyers engage with luxury property content but delay booking private showings, resulting in extended sales cycles, missed opportunities, and reliance on cold outreach"

2. **Outcome Function (OF)** — The observable behavioral change your campaign creates

   **Purpose:** Defines what success looks like as a measurable behavior change, not an aspiration or feeling.

   **Why it matters:** The delivery system learns to predict actions, not emotions. If your OF is vague or aspirational, the system has no clear signal to optimize toward.

   **Definition:** An observable state transition describing what the user *does* differently after intervention. Must be expressed as change in behavior, criteria, or action—not feelings or confidence.

   **Example:** "Prospects will request private viewings using property selection criteria (location, amenities, price range) rather than passively browsing listings" (not "Prospects will feel confident about their property search")

3. **Brand Role (BR)** — The functional relationship between brand and user

   **Purpose:** Defines the brand-user dynamic through three dimensions: Direction (Unidirectional/Bidirectional), Intensity (Low/Medium/High), Position (Above/Beside/Behind).

   **Why it matters:** BR governs what proof is required, how strong the CTA can be, and what tone is credible. A mismatch between BR and execution creates negative signals (hides, reports).

   **Definition:** The functional brand-user relationship that determines credible messaging boundaries. Position especially matters: a "beside" brand (peer/guide) cannot use authoritative top-down tone; an "above" brand cannot use casual peer tone.

   **Example:** "Bidirectional, High intensity, Beside position (trusted advisor)" → enables consultative tone, requires proof of market expertise, allows strong but personalized CTAs

4. **Cognitive Stage (CS)** — Where the user is in their learning journey

   **Purpose:** Defines the user's current stage (Exploration → Identification → Validation → Decision), which locks in the campaign's objective, message type, CTA, and optimization event.

   **Why it matters:** Stage-inappropriate optimization events cause learning failure. Optimizing for purchases when users are in Exploration stage generates wrong signals and destroys the learning system.

   **Definition:** The stage in the user's journey that determines acceptable message types, CTAs, and optimization events. Each stage has specific requirements that cannot be violated without breaking coherence.

   **Example:** "Identification stage" → objective is consideration, message type is FRAMEWORK, CTA is "Schedule a private showing", optimization event is Lead/Landing Page View

5. **Value Expression Type (VE)** — The message category for the campaign

   **Purpose:** Defines which of 4 closed message types the campaign uses: INSIGHT (reframes problem), VALIDATION (normalizes error), FRAMEWORK (organizes problem), or SYSTEM (step-by-step execution).

   **Why it matters:** Mixing VE types creates semantic ambiguity. The system cannot learn "what kind of creative this is" when each ad has a different semantic identity. One campaign = one VE.

   **Definition:** The type of message that determines how value is expressed. Must align with Cognitive Stage. Only one VE per campaign—never mixed.

   **Example:** "INSIGHT campaign" → all creatives reframe luxury property investment through market timing, exclusivity, or lifestyle elevation, suited for Exploration stage

6. **Emotional Axis (EA)** — The emotional transition your creative facilitates

   **Purpose:** Defines the single emotional journey the campaign takes users on (e.g., confusion → clarity, overwhelm → control).

   **Why it matters:** Different emotional axes create different semantic identities. The system cannot learn what emotional transition "works" if each creative moves users along different axes.

   **Definition:** The emotional state transition the creative facilitates. Must be one axis per campaign, never mixed. Cannot combine multiple emotional journeys in the same campaign.

   **Example:** "uncertainty → confidence" (in making a multi-million dollar property decision; cannot mix with "aspiration → attainment" in same campaign)

7. **Abstraction Level (AL)** — How conceptual vs. concrete the creative is

   **Purpose:** Controls whether creative is highly conceptual, balanced, or very concrete/specific. Ensures messaging stays learnable and stage-appropriate.

   **Why it matters:** Wrong abstraction level reduces clarity and learning efficiency. Early-stage (Exploration) can be more abstract; Decision-stage must be concrete and action-oriented.

   **Definition:** The degree of abstraction in creative execution. Content (organic) typically uses High/Medium AL. Ads use Medium/Low AL to maintain clarity and actionability.

   **Example:** "Medium-Low AL for ads" → shows specific properties with contextual lifestyle benefits, not purely aspirational imagery nor just property specs

8. **CTA Intensity Range (CTA-R)** — How strong your call-to-action can be

   **Purpose:** Defines the acceptable range of CTA strength based on Stage (dominant constraint), Brand Role, and established trust level.

   **Why it matters:** Aggressive CTAs in early stages or with low-trust BR create negative signals (hides, reports). Stage-inappropriate CTAs break coherence and damage learning.

   **Definition:** The range of acceptable CTA strength constrained primarily by Cognitive Stage, then by Brand Role and trust. Must match stage requirements to maintain quality signals.

   **Example:** "Identification stage, Beside role" → "View exclusive portfolio" or "Schedule private tour" (not "Browse listings" or "Buy now")

9. **Semantic Consistency Rules (SCR)** — What cannot change without creating a new system

   **Purpose:** Explicitly defines the language, promises, themes, and claim limits that must remain constant across all creatives.

   **Why it matters:** Changing core language or promises changes semantic identity, resetting learning. SCR prevents drift that would fragment the system's accumulated knowledge.

   **Definition:** The immutable constraints on language, claims, and themes. Includes: core promise, specific required/forbidden words, thematic boundaries, and claim limits.

   **Example:** "Never claim 'guaranteed appreciation.' Always use 'curated' not 'selected.' Never show property interiors in initial creative. All messaging emphasizes 'exclusive access'"

---

**Detailed documentation:** ./META-ADS-VAULT/02-STRUCTURAL-STRATEGY/07-Immutable-Global-Variables.md
