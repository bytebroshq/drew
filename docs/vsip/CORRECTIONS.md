# VSIP 4 Deck — Prompt Corrections Reference

## What this is

The `final prompt.txt` was written after Rudy's first round of questions to MP but **before** MP came back with VSIP's actual answers via Mr. Hai. This document flags every assumption in the prompt that now needs correction so the deck reflects what we actually know.

The corrections are organized by slide, then theme, then severity.

---

## Critical Corrections (changes the technical design)

### 1. RTS Ownership

| Prompt assumed | Actual (from MP via Mr. Hai) |
|---|---|
| Tenant-owned rooftop solar; VSIP wants grid-level control but may face access barriers | **VSIP is the direct investor, owner, and operator** of all 187 MW RTS. They have full visibility and control authority — generation management, dispatch optimization, curtailment. |

**Impact on deck:**
- **Slide 5 (Assumptions):** Changes the "Assumptions" column entirely. No longer a "tenant-owned" problem to solve.
- **Slide 9 (Architecture):** Control arrows between SurvalentONE and RTS can be direct — no tenant-negotiation layer needed.
- **Slide 10 (Zero-Export):** Curtailment strategy is simpler — VSIP can directly dispatch RTS without tenant permission.
- **Slide 16 (Key Decision #3):** "Clarify RTS ownership before tender" is no longer a decision — it's already confirmed.

### 2. BESS Placement

| Prompt assumed | Actual |
|---|---|
| Centralized utility-scale BESS at main 22kV substation | **BESS is distributed across individual factories**, paired with local RTS + local Microgrid Controllers. Central DERMS coordinates at higher level. |

**Impact on deck:**
- **Slide 5 (Assumptions):** BESS assumption was wrong. Must correct.
- **Slide 9 (Architecture diagram):** Currently shows "3× 110/22kV Substations with BESS at each" — must move BESS boxes down to factory level with local Microgrid Controller.
- **Slide 11 (Islanding & Black Start):** Black start sequence changes — BESS is distributed, so island formation uses multiple BESS units, not one centralized unit.
- **Slide 16 (Key Decision #4):** "BESS at substation level — not tenant factories" is the **opposite** of the correct recommendation. Must flip.

### 3. Timeline & Phasing

| Prompt assumed | Actual |
|---|---|
| 5–7 year phased build-out across 5 phases | **Full implementation in 2–3 years** as an integrated program. No desire for long-drawn phases. Plus: **50-year architectural vision** for scalability. |

**Impact on deck:**
- **Slide 5 (Assumptions):** Timeline assumption was wrong.
- **Slide 12 (5-Phase Roadmap):** Five phases over 5–7 years doesn't match reality. Need to rethink: either compress phases into a 2–3 year delivery plan with capability layers, or reframe as implementation stages within a 2–3 year window (not years-long phases).
- **Slide 13–15 (Phase deep dives):** The notion of spread-out phases is incorrect. VSIP wants it all designed up front as a unified platform.
- **Slide 16 (Key Decision #5):** "Define who operates" still valid, but timeline assumptions need rework.

### 4. VPP Role

| Prompt assumed | Actual |
|---|---|
| "API-ready for VPP integration" — passive posture, connect to external VPP | **Survalent platform should inherently function as the VPP** (Scenario A) — aggregate, optimize, and dispatch RTS+BESS assets directly for market participation or grid services. |

**Impact on deck:**
- **Slide 7 (Platform Overview):** Top layer "VPP / Smart energy ecosystem" should emphasize SurvalentONE _is_ the VPP, not just VPP-ready.
- **Slide 8 (Key Capabilities):** VPP card should say "SurvalentONE as VPP" not "VPP Readiness."
- **Slide 15 (Phase 5):** VPP is not a future phase feature — it's a core capability from the start.

---

## Moderate Corrections (changes the narrative or positioning)

### 5. Status of Project Parameters

| Prompt framing | Actual |
|---|---|
| Parameters are "working assumptions — we will refine these together" | Parameters are **confirmed through MP** but VSIP acknowledged they were "hypothetical/indicative" at first. However, VSIP is not expecting Survalent to question them — they want Survalent to **design around and guide from** these parameters. |

**Impact on deck:**
- **Slide 3 (Project at a Glance):** The label "Working parameters — we will refine these together" feels weak if VSIP already committed these numbers. Better: "Design parameters — validated through our consultation process."
- **Slide 5 (Assumptions):** The split "confirmed facts" vs "our assumptions" is now more nuanced. Some of the "assumptions" column items are actually confirmed (greenfield, protocols).

### 6. System Scope (Greenfield)

| Prompt assumed | Actual |
|---|---|
| "Assumed: greenfield, no legacy ADMS" | **Confirmed**: 100% greenfield, no dependence on VSIP 1's existing ADMS. No migration or integration required. |

**Impact:**
- **Slide 5:** Move this from "assumptions" to "confirmed facts."
- Simplifies the narrative — no "but what about..." baggage.

### 7. AMI/VPP Vendor Openness

| Prompt assumed | Actual |
|---|---|
| Not addressed in assumptions | VSIP has **no preferred AMI or VPP vendors** — they're open. This is an opportunity for Survalent to recommend partners. |

**Impact:**
- **Slide 16:** Could add as a recommendation: "Leverage this window to recommend AMI/VPP partners aligned with SurvalentONE."

---

## Minor Corrections (language/tone tuning)

### 8. "5-Phase Investment Roadmap" Naming

| Prompt | Issue |
|---|---|
| Uses term "5-phase" throughout | VSIP explicitly said they don't want long-term multi-phase implementation. "Phases" may imply years of waiting. Consider "Capability Layers" or "Implementation Stages" within a 2–3 year delivery plan. |

### 9. Slide 4 — "Your Vision" Horizon

| Prompt | Issue |
|---|---|
| "What VSIP wants to achieve in 5 years" | VSIP said 2–3 year implementation with 50-year vision. The 5-year reference doesn't align with either. Use "2–3 year horizon with 50-year architecture."

### 10. Slide 16 — Decision Cards That No Longer Apply

| Prompt item | Status |
|---|---|
| (03) "Clarify RTS ownership before tender" | ✅ Resolved — VSIP owns RTS |
| (04) "BESS at substation level — not tenant factories" | ❌ Wrong — BESS is at factories |
| (06) "Influence the tender spec — now" | ✅ Still relevant, but the tender is in Q4 2026 — this meeting _is_ the influence opportunity |

---

## Open Question (Unanswered by MP)

Rudy's final clarification on **VPP strategy (Scenario A vs B)** has **no recorded response from MP or VSIP**. This matters because:

- The prompt assumes "API-ready for VPP" (Scenario B posture)
- The deck narrative should hedge unless we know VSIP's answer
- **Recommendation**: Default to Scenario A (SurvalentONE as VPP) since it's the stronger position and aligns with Survalent's capabilities. But Andrew should use the meeting to validate this in conversation.

---

## Summary: What Changes Are Needed

| Slide | Change |
|---|---|
| 3 | Label: "Working parameters" → "Design parameters (validated)" |
| 4 | Horizon: "5 years" → "2–3 year delivery, 50-year vision" |
| 5 | Major rework: RTS ownership (confirmed VSIP), BESS (distributed, not centralized), timeline (2–3 years), greenfield (confirmed) |
| 7 | Top layer: "VPP/API-ready" → "SurvalentONE as VPP" emphasis |
| 8 | VPP card: "VPP Readiness" → "Built-in VPP Capability" |
| 9 | Architecture diagram: Move BESS from substation to factory level, add local Microgrid Controller between RTS+BESS and DERMS |
| 10 | Zero-export: Simplify — VSIP owns RTS so curtailment is direct, no tenant negotiation |
| 11 | Black start: Distributed BESS changes the restoration sequence |
| 12 | 5-phase → compress or reframe for 2–3 year delivery; add 50-year architecture anchor |
| 13–15 | Phase deep dives: Shorten timeline references; emphasize unified platform design from day one |
| 16 | Remove decision #3 (RTS ownership resolved); flip #4 (BESS _is_ at factories); adjust #6 framing |
| 17 | Keep as-is — still valid |
