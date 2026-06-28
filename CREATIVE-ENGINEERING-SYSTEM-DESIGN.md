# Creative Engineering System (CES) — Detailed Design Document

> **Source:** Extracted and formalized from `META-ADS-VAULT/03-CREATIVE-ENGINEERING`
> (Notes 11–15) of the GrowFu v3 specification.
> **Related system docs:** [GROWFU-V3-SYSTEM-DESIGN.md](./GROWFU-V3-SYSTEM-DESIGN.md) (§2.2 Semantic Consistency Engine, §2.3 Creative Intelligence System), [INTELLIGENT-VARIABLE-GENERATOR-DESIGN.md](./INTELLIGENT-VARIABLE-GENERATOR-DESIGN.md) (upstream producer of inputs).

---

## Executive Summary

The **Creative Engineering System (CES)** is the GrowFu sub-system that treats ad
creative as an **engineering discipline rather than a subjective one**. Its
governing question is not *"is this a good ad?"* but *"does this creative produce
the signals Meta's delivery system needs to learn, allocate, and scale — while
remaining within the locked semantic identity of the campaign?"*

CES takes a **locked campaign definition** (the 9 Immutable Global Variables) plus
optional creative assets, account history, and live performance telemetry, and
operates across the full creative lifecycle: it **designs** multimodal creative as
a deliberate signal object, **engineers** the first 2–3 seconds for micro-signal
generation, **enforces** semantic identity across a portfolio, **structures**
variation testing on a single-axis discipline, and **adapts** creative
generalization as spend scales. It emits machine-readable artifacts (creative
briefs, signal specs, portfolio plans, test plans, validation verdicts, scaling
guidance) that can be consumed by the wider GrowFu platform **or** run as a
standalone creative-governance module wrapped around any Meta Ads account.

The core design premise (the "Creative Engineering Framing"):

> Every creative decision is a **signal decision**. CES designs for the machine's
> embedding (`A`) and prediction systems, while remaining compelling enough to
> generate the human behaviors those systems measure.

---

## System Architecture Overview

### Core Principles

1. **Creative is representation, not message.** An ad is a multimodal object the
   system encodes into a latent Ad embedding (`A` in the U–A–C triad). Every
   element contributes to `A` whether intended or not.
2. **Identity is locked; framing is free (within bounds).** PS, OF, BR, VE, EA and
   the core promise are immutable across the whole portfolio. Changing them is not
   an iteration — it is a *different campaign system*.
3. **Signals before macro-conversions.** Micro-signals (hold rate, completion) are
   the highest-volume early data; the first 2–3 seconds determine embedding
   positioning and initial budget allocation.
4. **Never vary randomly.** Variation is permitted only through a controlled
   single-axis matrix so that performance deltas are attributable.
5. **You scale portfolios, not ads.** A single creative inevitably fatigues; CES
   manages a structured, diversified portfolio with a defined lifecycle.
6. **Generalize, don't dilute.** At scale, framing broadens incrementally while the
   thesis stays fixed.
7. **Explainable & evidence-bound.** Every verdict cites the rule and (where
   relevant) the stage/immutable it derives from.

### Component Diagram

```
┌──────────────────────────────────────────────────────────────────────────┐
│                              INPUTS (see §1)                               │
│  Mandatory: Locked 9 Immutable Variables (Campaign Definition Sheet)       │
│             Cognitive Stage + Optimization-Event Contract                  │
│  Optional:  Creative assets · Account/performance priors · Existing        │
│             portfolio · Live Meta telemetry · Landing-page metadata        │
└───────────────────────────────────┬────────────────────────────────────────┘
                                     │
                                     ▼
┌──────────────────────────────────────────────────────────────────────────┐
│                     CREATIVE ENGINEERING ORCHESTRATOR                      │
│      Routes work by lifecycle phase; holds the locked-identity context     │
└──┬──────────────┬──────────────┬──────────────┬──────────────┬────────────┘
   │              │              │              │              │
   ▼              ▼              ▼              ▼              ▼
┌────────┐  ┌──────────┐  ┌────────────┐  ┌────────────┐  ┌──────────────┐
│  M1    │  │   M2     │  │    M3      │  │    M4      │  │     M5       │
│Multi-  │  │ Micro-   │  │ Semantic   │  │ Portfolio  │  │  Structured  │
│modal   │  │ Signal / │  │ Consistency│  │ Architect  │  │  Testing     │
│Designer│  │ Hook Eng.│  │ & Identity │  │ & Lifecycle│  │  Engine      │
│(File11)│  │ (File12) │  │  (File13)  │  │  (File13)  │  │   (File14)   │
└───┬────┘  └────┬─────┘  └─────┬──────┘  └─────┬──────┘  └──────┬───────┘
    │            │              │               │                │
    └────────────┴──────────────┴───────┬───────┴────────────────┘
                                         │
                                         ▼
                              ┌────────────────────┐
                              │       M6           │
                              │ Scaling Adaptation │
                              │ / Generalization   │
                              │     (File 15)      │
                              └─────────┬──────────┘
                                        │
                                        ▼
┌──────────────────────────────────────────────────────────────────────────┐
│                              OUTPUTS (see §3)                              │
│  Creative brief · Signal/Hook spec · Consistency verdict + scores ·        │
│  Portfolio plan + lifecycle state · Test plan + verdicts ·                 │
│  Scaling-readiness + generalization variants                              │
└──────────────────────────────────────────────────────────────────────────┘
```

CES corresponds to (and unifies) two sub-systems named in the GrowFu master design
— the **Semantic Consistency Engine** (§2.2) and the **Creative Intelligence
System** (§2.3) — and extends them with explicit design, hook-engineering, testing,
and scaling-adaptation modules drawn directly from Notes 11–15.

---

## 1. Inputs

Inputs are split into **mandatory** (CES cannot operate coherently without them)
and **optional** (each unlocks additional capability/precision). Inputs map
directly onto the U–A–C triad: most CES inputs shape the **Ad embedding (`A`)**;
structural inputs describe the **Context embedding (`C`)**; CES does not own the
**User embedding (`U`)**.

### 1.1 Mandatory Inputs

| Input | Source | Why it is mandatory |
|---|---|---|
| **Locked 9 Immutable Global Variables** (PS, OF, BR, CS, VE, EA, AL, CTA-R, SCR) | IVG / Campaign Definition Sheet | These are the *constraints* every creative decision is validated against. Without them CES cannot judge whether a creative preserves or breaks identity. |
| **Cognitive Stage (CS)** | Campaign Definition Sheet | Determines acceptable hook type, message type, optimization event, and which micro/macro signal is the primary test metric. Drives M2, M5, M4 portfolio sizing. |
| **Optimization-event contract** (the declared event + attribution window intent) | Campaign Definition Sheet / Stage contract | The hook and payoff must be consistent with the declared optimization event; test metrics derive from it. |
| **Core promise + SCR** (required/forbidden words, claim limits, thematic boundaries) | Campaign Definition Sheet | The hard rule-set for M3 consistency enforcement and the M1 claim-strength checks. |

> **Hard gate:** PS, OF, BR, VE, EA and the core promise are *immutable across the
> entire portfolio*. CES treats any proposed creative that alters them not as a
> failed variant but as belonging to a **different campaign system**, and rejects
> it from the portfolio.

### 1.2 Optional Inputs (each enables more capability)

| Input | Enables | Notes |
|---|---|---|
| **Creative assets** (text, image, video, audio, overlays) | M1 signal decomposition, M2 hook scoring, M3 consistency scoring | Without assets, CES operates in *brief/spec* mode (prescriptive); with assets it operates in *evaluation* mode (diagnostic). |
| **Account & performance priors** (CTR/CVR history, negative-feedback history, fatigue history) | Prior-aware initialization; clickbait-risk flagging | Priors are not destiny but raise/lower initial resistance; poor history → build quality from the start. |
| **Existing portfolio** (current creatives + roles) | M3 similarity/identity grouping, M4 lifecycle placement, Creative-Similarity-Score prediction | Lets CES diff a new creative against the established latent identity. |
| **Live Meta telemetry** (hold rate, watch time, completion, CTR, CVR, CPA, frequency, hide/report, CPM) | M4 fatigue/lifecycle transitions, M5 test verdicts, M6 scaling readiness | Required for the monitoring/lifecycle/testing/scaling loops; not needed for pure pre-launch design. |
| **Structural / context metadata** (placement, format, device, landing type, category, country) | Context-aware (`C`) format guidance | CES treats these as *context variation, not message variation* — it changes **format**, never the message, to match placement. |
| **Landing-page metadata** (what the landing fulfills) | Hook-payoff alignment checks (M2/M5 clickbait detection) | Used to detect the "payoff problem" (high micro-signal + low macro-signal). |

---

## 2. Modules — What the System Does and How

### M1 — Multimodal Creative Designer / Signal Encoder *(Note 11)*

**Purpose:** Decompose (or prescribe) every creative element by its contribution to
the Ad embedding `A`, so creative is engineered as a deliberate signal object.

**How it works:**

- **Content signals** (meaning-bearing, shape `A` directly):
  - *Text* — semantic clarity (decodes < 3s), claim strength, urgency, landing alignment.
  - *Image/Video* — faces (attention + trust), overlay text (meaning when muted), production style (UGC vs polished → identity), visual rhythm, first-frame anchor.
  - *Audio* — tone, authority, emotional cadence.
- **Structural signals** (metadata → context embedding `C`): placement, format,
  device, optimization objective, landing type, category, country/regulation.
  Rule: treat placement as **context variation**, change *format* not *message*.
- **Performance priors:** ingest CTR/CVR/negative-feedback/fatigue history to set
  the initialization prior and flag `CTR↑ + CVR↓` clickbait risk.
- **Creative identity:** recognizes identity is **latent** (Educational / Clickbait
  / Luxury / Aggressive / Low-trust) and emerges from *structure + signals +
  reactions* — enforces single identity per campaign.

**Operational artifact:** the **Creative Signal Checklist** (semantic clarity <3s;
claim within CTA-R + SCR; first-frame anchor; production-style consistency; audio
tone matches EA; format matches placements; landing alignment).

### M2 — Micro-Signal / Hook Engineering *(Note 12)*

**Purpose:** Engineer the first 2–3 seconds (video) or first line (static) as a
*signal-generation* problem, because micro-signals position the embedding and
allocate initial budget before any macro-signal exists.

**How it works:**

- **Micro-signal inventory it designs for / reads:** hold rate, scroll stop, early
  drop-off, partial completion, view>3s (low intent), view>6s (meaningful;
  Exploration-stage event), completion rate (strongest video signal).
- **Four first-moment requirements:** immediate clarity, immediate relevance,
  pattern interrupt, cognitive anchor — framed as signal-generation requirements,
  not aesthetics.
- **Dual-master hook architecture:** each hook must satisfy the human (recognition/
  curiosity/relevance/payoff promise) *and* the system (hold rate, reduced early
  drop-off, partial completion, optimization-event consistency).
- **Stage-matching:** Exploration hooks (curiosity/problem recognition) vs Decision
  hooks (urgency/social proof) generate different micro-signals; mismatched hook =
  confusing signal data.
- **Payoff-problem detection:** high micro-signal + low macro-signal ⇒ `pCTR↑ +
  pCVR↓` dissonance ⇒ variance up, delivery confidence down. Every signal the hook
  generates must have a path to the macro-signal.
- **Efficiency rationale:** strong micro-signals accumulate volume faster → reach
  the ~50-event learning threshold sooner → earlier CPA stability. Creative quality
  is a **budget-efficiency mechanism**.

### M3 — Semantic Consistency & Creative Identity Engine *(Note 13)*

**Purpose:** Guarantee every creative variation stays inside the same latent
identity cluster (the campaign's "Entity-ID neighborhood").

**How it works:**

- Validates assets against **SCR** (forbidden claims, required language, thematic
  boundaries, claim limits) and the immutables (PS/OF/BR/VE/EA + core promise).
- Detects when a variant crosses a semantic boundary → reclassifies it as a
  *different campaign system* rather than a portfolio member.
- Maintains identity consistency: production-style consistency, tone matched to EA,
  language within SCR, claims within approved limits.
- Predicts Meta's **Creative Similarity Score** (penalize near-duplicate content →
  higher CPMs) and rewards genuine semantic diversity over cosmetic variation.

**Outputs a semantic-consistency score (0–100) + violation report.**

### M4 — Portfolio Architecture & Lifecycle Manager *(Note 13)*

**Purpose:** Manage a stable, diversified portfolio — because you scale portfolios,
not ads.

**Portfolio structure (four functional clusters):**

| Cluster | Purpose | Varies |
|---|---|---|
| Core Control | Best proven creative; comparison anchor; never modified, only retired | nothing |
| Variation A | Hook variations of control (same thesis) | Hook only |
| Variation B | Emotional/visual framing variations (same thesis) | Emotion / example / narrative order / visual framing |
| Exploratory | New creative families being tested (may fail) | free (within immutables) |

**Immutable across all clusters:** core promise, PS, OF, BR, VE, EA.

**Lifecycle:** `Exploratory → Control Candidate → Control → Fatiguing → Retired`
(retired creatives are never resurrected). Transitions are driven by live telemetry
(micro-signal monitoring, watch-time decline, CVR softening, rising CPM/negative
signals).

**Portfolio sizing by stage:** Exploration 3–5 · Identification 3–5 · Validation
2–4 · Decision 2–3 (highest specificity). Refresh cadence ~2–4 weeks scaled by
spend velocity. Fewer high-quality creatives beat large inconsistent portfolios.

### M5 — Structured Testing Engine *(Note 14)*

**Purpose:** Produce attributable learning by enforcing single-axis variation.

**The 5-axis variation matrix:** (1) Hook type, (2) Proof mechanism, (3) Emotional
framing, (4) Visual pacing, (5) CTA framing. **One axis per test.**

**Test protocol:**
1. Lock all non-test axes (identical across variants).
2. Pre-define evaluation criteria *before launch* (primary KPI, secondary KPIs,
   min impressions, min events, evaluation window).
3. Do not evaluate during the learning phase (~50 events / 7 days).
4. Apply consistent attribution windows across all variants.

**Stage-aware test metrics:** Exploration → hold rate, completion% (sec: profile
clicks); Identification → LPV rate, scroll depth (sec: engagement); Validation →
lead rate, lead-quality proxy (sec: LPV); Decision → purchase rate / CPA (sec:
checkout initiation).

**Result interpretation:** higher hold **and** CVR → promote to control candidate;
higher CTR + lower CVR → clickbait, do not promote, investigate hook-landing
mismatch; no significant difference → extend window or redesign; both underperform
control → keep control.

### M6 — Scaling Adaptation / Generalization Engine *(Note 15)*

**Purpose:** Adapt creative as spend grows, because scaling expands delivery into
progressively less-aligned user embeddings.

**How it works:**

- Frames rising CPA at scale as **expansion physics, not failure** (the system
  serves lower-conversion-probability users at the margin).
- Enforces **generalization, not dilution**:
  - *Acceptable:* broaden example pool, widen problem description, soften language
    specificity slightly, add broader-segment social proof.
  - *Unacceptable:* change core promise, PS, OF, EA, or VE.
- **Pre-scale checklist (gate):** stage stabilized (plateaued, not declining);
  event density sufficient (learning complete); CPA stable 7+ consecutive days; no
  rising negative feedback; budget increment < 30%; portfolio diverse enough to
  survive audience expansion; generalization variants pre-built.
- **Portfolio diversity at scale:** different sub-segments respond to different
  hooks; frequency pressure accelerates fatigue; build generalization variants
  *before* CPA spikes.

---

## 3. Outputs

All outputs are emitted as structured, machine-readable artifacts (JSON) plus a
human-readable rendering. They are designed to be consumed either by downstream
GrowFu sub-systems or by an external caller in standalone mode.

| Output | Produced by | Consumed by (GrowFu) | Standalone use |
|---|---|---|---|
| **Creative Brief / Signal Spec** (per-element design directives + Creative Signal Checklist) | M1 | Creative production workflow | A prescriptive brief for any designer/agency |
| **Hook & Micro-Signal Spec** (first-moment requirements, stage-matched hook, payoff path) | M2 | Reporting & Insights | Hook QA before upload |
| **Semantic Consistency Verdict** (score 0–100, violation report, predicted Creative Similarity Score, in-tolerance variations) | M3 | Governance & Change Mgmt (blocks identity-breaking changes) | Pre-upload creative compliance gate |
| **Portfolio Plan & Lifecycle State** (cluster assignment, lifecycle phase, portfolio-health score, refresh schedule) | M4 | Fatigue & Rotation, Budget & Scaling | Portfolio dashboard |
| **Test Plan & Verdicts** (axis under test, locked axes, criteria, winner/interpretation/action) | M5 | Learning Phase Manager, Reporting | Standalone A/B governance |
| **Scaling-Readiness Report + Generalization Variants** (gate verdict, increment guidance, prepared broader-framing variants) | M6 | Budget & Scaling Optimizer | Scale-decision checklist |

### 3.1 Integration outputs (wider GrowFu)

- **→ Governance & Change-Management Engine:** the consistency verdict acts as a
  hard gate — identity-breaking variants are rejected; "one-axis" test plans satisfy
  the "one variable per iteration" rule.
- **→ Learning Phase Manager:** test windows respect the ~50-event / 7-day
  threshold; CES never evaluates mid-learning.
- **→ Fatigue, Saturation & Rotation (Note 20):** lifecycle states and fatigue
  signals (rising CPM, CVR softening) trigger rotation.
- **→ Budget & Scaling Optimizer (Notes 17/19):** scaling-readiness gate +
  pre-built generalization variants inform increment timing/size.
- **→ Reporting & Insights:** signal specs and verdicts become narrative insights.

### 3.2 Standalone module outputs

In standalone mode CES is a **creative-governance microservice**: given a campaign
identity definition + creative assets (+ optional telemetry), it returns the
consistency verdict, hook/signal spec, portfolio/lifecycle guidance, test plans,
and scaling verdicts — usable around any Meta Ads account without the rest of
GrowFu.

---

## 4. Standalone Module — Data Exchange Specification

### 4.1 Inbound contract (caller → CES)

```jsonc
{
  "campaign_identity": {                 // MANDATORY — locked immutables
    "ps": "string (1 sentence + 3 observable symptoms)",
    "of": "string (observable state transition)",
    "br": { "direction": "uni|bi", "intensity": "low|med|high",
            "position": "above|beside|behind" },
    "cs": "exploration|identification|validation|decision",
    "ve": "INSIGHT|VALIDATION|FRAMEWORK|SYSTEM",
    "ea": "string (single emotional axis, e.g. 'uncertainty->confidence')",
    "al": "high|medium|low",
    "cta_r": "string (allowed CTA strength range)",
    "scr": { "core_promise": "string", "required_words": [], "forbidden_words": [],
             "thematic_boundaries": [], "claim_limits": [] },
    "optimization_event": "string"
  },
  "creative_assets": [                   // OPTIONAL — enables evaluation mode
    { "id": "string", "type": "text|image|video|carousel",
      "text": "string", "media_uri": "string", "overlays": [], "audio": {} }
  ],
  "existing_portfolio": [                 // OPTIONAL
    { "id": "string", "cluster": "control|var_a|var_b|exploratory",
      "lifecycle": "exploratory|candidate|control|fatiguing|retired" }
  ],
  "performance_priors": {},               // OPTIONAL — CTR/CVR/neg-feedback/fatigue history
  "live_telemetry": {},                   // OPTIONAL — hold/completion/CTR/CVR/CPA/freq/CPM/hide-report
  "context_metadata": {},                 // OPTIONAL — placement/format/device/landing/country
  "request": "design|evaluate|consistency|portfolio|test_plan|scale_check"
}
```

### 4.2 Outbound contract (CES → caller)

```jsonc
{
  "request": "consistency",
  "verdict": "pass|warn|reject",
  "scores": { "semantic_consistency": 0,        // 0-100
              "predicted_creative_similarity": 0 },
  "violations": [ { "rule": "SCR.forbidden_words", "detail": "...",
                    "immutable": "VE", "severity": "hard|soft" } ],
  "creative_signal_checklist": { "...": "pass|fail" },
  "hook_spec": { "...": "..." },
  "portfolio": { "cluster": "var_a", "lifecycle": "candidate",
                 "health_score": 0, "refresh_due": "ISO-date" },
  "test_plan": { "axis": "hook", "locked_axes": [],
                 "primary_kpi": "...", "min_events": 50, "window_days": 7 },
  "scaling": { "ready": true, "blocking_reasons": [],
               "max_increment_pct": 30, "generalization_variants": [] },
  "explanation": "rule-cited natural-language rationale"
}
```

---

## 5. Technology Stack

| Layer | Technology | Role in CES |
|---|---|---|
| **Multimodal LLM** | Claude (Sonnet/Opus), GPT-4V | Decompose text+image+video+audio; consistency reasoning; brief generation |
| **Embedding models** | OpenAI `text-embedding-3`, CLIP | Semantic-distance / identity-cluster measurement; Creative Similarity prediction |
| **Rule engine** | Custom / Drools-style | SCR enforcement, immutable-variable gates, one-axis test rules, scaling gate |
| **Computer vision** | CLIP / Meta-Andromeda-style simulation | First-frame analysis, production-style classification, similarity clustering |
| **Time-series store** | TimescaleDB / InfluxDB | Micro/macro-signal history, lifecycle transitions, fatigue detection |
| **ML (fatigue/forecast)** | XGBoost, Prophet/ARIMA | 5–7-day-early fatigue prediction, CPA-at-scale projection |
| **Event ingestion** | Kafka / Meta Conversions API | Live telemetry into M4/M5/M6 |
| **API surface** | REST/gRPC microservice | Standalone data-exchange contract (§4) |

> Per the GrowFu master design, the LLM/embedding layers map to the **Semantic
> Consistency Engine** (§2.2) and the ML/time-series layers map to the **Creative
> Intelligence System** (§2.3).

---

## 6. Success Metrics

**System quality**
- Consistency-verdict precision/recall vs. expert human review of identity breaks.
- Predicted Creative Similarity Score vs. Meta's reported metric (error band).
- Fatigue prediction lead time (target: 5–7 days before performance collapse).

**Signal/efficiency**
- Hook rate / hold rate vs. benchmarks (≈25–35% hook, ≈40–50% hold).
- Time-to-learning-exit (events to ~50) for CES-engineered vs. baseline creative.
- Clickbait-flag rate (`CTR↑ + CVR↓`) caught pre-promotion vs. escaped to spend.

**Portfolio/scaling**
- Portfolio health score; share of spend on in-identity creative.
- CPA stability days before scale; CPA delta vs. predicted at +30% increments.

---

## 7. Example Walkthrough (condensed)

**Input:** Locked identity for a luxury-property campaign — `VE=INSIGHT`,
`EA=uncertainty→confidence`, `CS=Identification`, SCR forbids "guaranteed
appreciation", requires "curated", forbids interior shots in initial creative.
Caller submits 4 candidate video assets + 30 days of account priors.

1. **M3** rejects asset #3 (uses "selected" not "curated" and shows an interior) →
   verdict `reject`, violation `SCR`, reclassified as different system.
2. **M1** decomposes the remaining 3: flags #2's polished style as inconsistent
   with the portfolio's UGC identity → consistency score 62/100.
3. **M2** scores hooks: #1 opens on problem recognition with overlay text (works
   muted) → strong predicted hold rate; #4 opens on brand logo → flagged.
4. **M4** assigns #1 as Control Candidate, #2 to Variation B (after restyle), #4 to
   Exploratory; sets Identification portfolio size 3–5, refresh ~3 weeks.
5. **M5** emits a single-axis **hook test** (#1 vs a curiosity-opening variant), all
   other axes locked, primary KPI = LPV rate, min 50 events, 7-day window.
6. **M6** marks campaign *not yet scale-ready* (CPA not yet stable 7 days) and
   pre-builds two broader-framing generalization variants for later.

---

## 8. Risks & Limitations

- **Similarity-score prediction is a simulation** of Meta's proprietary Andromeda
  metric — treat as directional, calibrate against reported values.
- **LLM identity judgments can hallucinate boundaries**; the rule engine (SCR /
  immutables) must be the hard gate, with the LLM as advisory.
- **Latent identity is observed, not controlled** — CES *influences* identity via
  consistent signals but cannot directly set the system's category for a creative.
- **Telemetry-dependent modules (M4–M6) degrade gracefully** to prescriptive mode
  when live data is absent (pre-launch).
- **Stage mismatch upstream propagates** — if CS in the Campaign Definition Sheet is
  wrong, every stage-derived hook/test/metric decision inherits the error.

---

## 9. Reference Files

- [`03-CREATIVE-ENGINEERING/_MOC-Creative-Engineering.md`](./META-ADS-VAULT/03-CREATIVE-ENGINEERING/_MOC-Creative-Engineering.md)
- [`11-Multimodal-Creative-Design.md`](./META-ADS-VAULT/03-CREATIVE-ENGINEERING/11-Multimodal-Creative-Design.md)
- [`12-Micro-Signal-Optimization.md`](./META-ADS-VAULT/03-CREATIVE-ENGINEERING/12-Micro-Signal-Optimization.md)
- [`13-Creative-Identity-and-Portfolio-Architecture.md`](./META-ADS-VAULT/03-CREATIVE-ENGINEERING/13-Creative-Identity-and-Portfolio-Architecture.md)
- [`14-Structured-Testing-Framework.md`](./META-ADS-VAULT/03-CREATIVE-ENGINEERING/14-Structured-Testing-Framework.md)
- [`15-Scaling-Adaptation.md`](./META-ADS-VAULT/03-CREATIVE-ENGINEERING/15-Scaling-Adaptation.md)
- [`07-Immutable-Global-Variables.md`](./META-ADS-VAULT/02-STRUCTURAL-STRATEGY/07-Immutable-Global-Variables.md) — upstream identity inputs
- [`U-A-C-Triad-Reference.md`](./META-ADS-VAULT/05-REFERENCE/U-A-C-Triad-Reference.md) — `A = f(Text + Image/Video + Audio + Temporal + Metadata + History)`
- [GROWFU-V3-SYSTEM-DESIGN.md](./GROWFU-V3-SYSTEM-DESIGN.md) §2.2, §2.3
- [INTELLIGENT-VARIABLE-GENERATOR-DESIGN.md](./INTELLIGENT-VARIABLE-GENERATOR-DESIGN.md) — produces the Campaign Definition Sheet consumed as CES input
