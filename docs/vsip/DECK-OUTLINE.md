# VSIP 4 — Deck Outline

**Deck**: `vsip4-strategy.html`
**Presenter**: Andrew Cruz (Senior Consultant, Survalent APAC)
**Meeting**: June 26, 2026 · 9:00 AM · VSIP I Office
**Team**: Max Woo (Senior Regional Director, APAC) · Andrew Cruz (Solutions Consultant, presenting) · Rudy Thiara (Solutions Specialist) · Local partner: MP

---

## Design decisions (before we begin)

- **Timeline**: 2–3 year delivery, anchored to a 50-year architectural vision
- **BESS**: Distributed at factory level, paired with local RTS + Microgrid Controllers
- **RTS**: Fully VISP-owned — no tenant-negotiation layer in control strategy
- **VPP**: SurvalentONE inherently functions as the VPP (Scenario A; validate in meeting)
- **Tone**: Consultative — we are the system architect, not a vendor
- **Density**: Mix — self-contained stat cards and one-idea-per-slide for technical, contentful grids for roadmap/capabilities
- **Case study**: Ho Chi Minh City FLISR (95% SAIDI / 93% SAIFI reduction) — credibility anchor

---

## Section 1 — Opening

### Slide 1 · Title
- *Smart Grid & Energy Management Strategy*
- *A Consultative Roadmap for VSIP 4 Industrial Park*
- Date, venue, "Confidential" badge, team names
- Dark background, Survalent brand feel

### Slide 2 · Today's Agenda
- 6 items in a 2×3 card grid with numbered badges:
  1. Understanding VSIP 4's vision and parameters
  2. What we know & what we're designing around
  3. The SurvalentONE platform
  4. Recommended system architecture
  5. Your implementation roadmap
  6. Decisions & next steps

---

## Section 2 — Understanding Your Vision

### Slide 3 · VSIP 4 at a Glance
- 5 stat cards: 750 ha / 3× 110/22kV substations / ~200 MW peak / 187 MW RTS / 50–100 MWh BESS
- Core requirements as a clean icon+label list below
- Label: "Design parameters — validated through our consultation with MP/VSIP"

### Slide 4 · Your Vision: Green, Smart, Zero-Carbon
- One bold statement: *"VSIP 4 is not just an industrial park. It's a platform for the energy future of Vietnamese industry."*
- Three pillars in large cards:
  1. **Reliability** — tenants never lose power
  2. **Sustainability** — zero carbon, ESG-ready
  3. **Intelligence** — data-driven, automated, built for 50 years of growth

---

## Section 3 — What We Know

> Replaces the original "Assumptions & Design Basis" slide. Most of the prompt's "assumptions" are now confirmed through MP. Position this as thoroughness — we did the homework.

### Slide 5 · What We've Confirmed
- Two-column layout: **Confirmed** (left) → **What This Means for Design** (right)
- Confirmed items: Greenfield / VSIP owns all RTS / BESS distributed at factories with local Microgrid Controllers / 2–3 year delivery target / 50-year vision / IEC-104 & Modbus protocols / No legacy ADMS dependency
- Footer: "These confirmed facts shape the architecture we're recommending today."

---

## Section 4 — The Survalent Platform

### Slide 6 · Why a Grid-First Platform Matters
- 187 MW of distributed solar + BESS + 200 MW load → must be built for grid operations, not market aggregation
- 3 pain points without grid-first:
  1. No real-time visibility of DER impacts on the 22kV network
  2. Zero-export can't be enforced reliably without topology awareness
  3. Islanding and black start require tight SCADA+DERMS integration
- Survalent answer: *"Built for utility operations. Proven in 24/7 control room environments."*

### Slide 7 · SurvalentONE ADMS + DERMS: Platform Overview
- Layered diagram (built with CSS/SVG shapes):
  - Layer 1: SCADA — Real-time data acquisition
  - Layer 2: ADMS — Topology, OMS, FLISR, Volt/VAR
  - Layer 3: DERMS — RTS monitoring, curtailment, zero-export, forecasting
  - Layer 4: Microgrid — BESS dispatch, islanding, black start (local controllers at factory level)
  - Layer 5: VPP — SurvalentONE *is* the VPP (aggregation, optimization, dispatch)
- Right side: protocol icons — IEC-104, Modbus, IEC 61850, DNP3, IEEE 2030.5, REST API
- Survalent teal + orange brand colors

### Slide 8 · Key Capabilities for VSIP 4
- 2×3 card grid:
  1. **ADMS** — Grid topology, FLISR, real-time operations
  2. **DERMS** — RTS generation management, curtailment, zero-export enforcement
  3. **Microgrid + BESS Control** — Distributed BESS dispatch, local island formation
  4. **Multi-vendor Integration** — IEC-104, Modbus, DNP3, IEC 61850 across all assets
  5. **Industrial Cybersecurity** — OT-grade security from day one
  6. **Built-in VPP** — SurvalentONE aggregates and dispatches RTS+BESS as a virtual power plant
- Highlight ADMS and DERMS (most relevant to VSIP's immediate needs)

### Slide 9 · Proven at Scale: Ho Chi Minh City
> Credibility anchor — real results in Vietnam. Makes the engagement tangible.
- Big stat: **SAIDI reduced 95% · SAIFI reduced 93%**
- 2.72 million meters, SurvalentONE FLISR deployment
- Short quote-style text: *"The same platform running Vietnam's largest utility can be architected for VSIP 4's specific requirements."*
- Teal/orange accent, big numbers

---

## Section 5 — Recommended Architecture

### Slide 10 · VSIP 4 System Architecture (Conceptual)
- Structural diagram (CSS/SVG):
  - Top: National Grid (110kV connection)
  - Below: 3× 110/22kV Substations
  - 22kV feeder network (reclosers, LBS, RMUs) radiating down
  - Factory nodes: each with local RTS + BESS + Microgrid Controller
  - Overlay: SurvalentONE ADMS+DERMS as the central intelligence layer, connecting to each node
- Key callout: BESS is distributed — each factory is a self-sustaining microgrid node
- Color code: teal (grid), orange (DER assets), dark gray (Survalent platform)

### Slide 11 · Zero-Export Control Strategy
- Critical requirement — dedicated slide
- Control flow: RTS generation → POI measurement → DERMS compares vs grid limit → if excess: curtail RTS / charge local BESS / alert operator → hard limit enforced
- VSIP owns RTS → curtailment is direct, no tenant permission needed
- Key message: *"Zero export is not a feature. It's a regulatory obligation. The enforcement path must be designed from day one."*

### Slide 12 · Islanding & Black Start Strategy
- Scenario: National grid trips → VSIP must sustain power to tenants
- Distributed BESS changes the play:
  - Each factory's local Microgrid Controller + BESS forms an island
  - Black start: BESS energizes local bus → RTS reconnects → loads restored in priority order
  - Central DERMS coordinates across islands for park-wide stability
- Requirements: Grid-forming inverters, protection coordination, defined island boundaries
- Key message: *"Islanding is what lets VSIP tell premium tenants: you will never lose power."*

---

## Section 6 — Your Implementation Roadmap

> VSIP wants 2–3 years, not 5–7. Reframe phases as **capability layers** that accumulate, not standalone projects. All designed up front as a unified platform. Anchored to a 50-year architecture.

### Slide 13 · Capability Roadmap: 2–3 Year Delivery
- Horizontal timeline with 5 capability layers, each building on the last:
  1. **Foundation** (Month 0–6): SCADA, substations, reclosers/LBS/RMU, comms backbone, OT security
  2. **Grid Intelligence** (Month 4–12): ADMS, FLISR, Volt/VAR, zero-export monitoring
  3. **Renewable Integration** (Month 10–20): DERMS, RTS monitoring + curtailment, BESS optimization, closed-loop zero-export
  4. **Microgrid & Resilience** (Month 16–28): Distributed Microgrid Controllers, islanding, black start
  5. **Smart Energy Ecosystem** (Month 24–36): VPP operations, demand response, ESG dashboard, market readiness
- Layers overlap — designed together, deployed incrementally
- Below the timeline: 50-year architecture callout — "This platform is built to accommodate load growth, DER expansion, and market evolution for decades."

### Slide 14 · Foundation + Grid Intelligence (Deep Dive)
- Why the first 12 months determine the next 50 years
- Foundation: Comms backbone, OT security, data model → these are architectural decisions, not just procurement
- Grid Intelligence: ADMS goes live — zero-export monitoring starts here, before full DERMS
- Design principle: *"The data model, communication backbone, and OT security you choose in months 0–6 either unlock or constrain everything that follows. Get this right first."*
- HCMC FLISR result as a proof point for Phase 1→2 value

### Slide 15 · Layers 3–5: From DERMS to Smart Energy
- Three-column summary:
  - **Renewable Integration**: DERMS goes live, RTS connected, zero-export automated, BESS dispatch
  - **Microgrid & Resilience**: Islanding proven, black start tested, tenants experience uninterrupted power
  - **Smart Energy Ecosystem**: VPP live, market participation, ESG reporting, demand response
- Closing line: *"Each layer adds intelligence. Each layer adds value. No layer requires a rip-and-replace. Everything was architected from day one."*
- Note: Full VPP/market readiness is the long play — part of the 50-year vision, not day-one requirement

---

## Section 7 — Closing

### Slide 16 · Decisions We Recommend Today
- 6-card grid (2×3), numbered:
  1. **Design the data model once** — it's the foundation for all future capability
  2. **Zero-export enforcement starts at Layer 2** — don't wait for full DERMS
  3. **Build for SurvalentONE as the VPP** — the platform that operates the grid should aggregate the DERs
  4. **Procure Microgrid Controllers with BESS** — distributed architecture from the start
  5. **Define the operations team early** — who runs the control room post-commissioning
  6. **Shape the Q4 tender** — this meeting is the window to influence the spec
- White cards, teal number badges, subtle shadow

### Slide 17 · How We Move Forward
- 4 next steps as horizontal cards:
  1. **Validate parameters** — confirm and refine together today
  2. **Reference architecture document** — Survalent APAC delivers within 2 weeks
  3. **Technical workshop** — deep-dive with VSIP engineering team
  4. **Reference site visit** — see SurvalentONE at scale
- Dark background — signals conclusion
- Closing line: *"We come as your system architects. Our goal is to help you make decisions today that you will not regret in 50 years."*

---

## Slide count

| Section | Content slides | Section dividers |
|---|---|---|
| Opening | 2 | — |
| Understanding Your Vision | 2 | 1 |
| What We Know | 1 | 1 |
| The Survalent Platform | 4 | 1 |
| Recommended Architecture | 3 | 1 |
| Your Implementation Roadmap | 3 | 1 |
| Closing | 2 | 1 |
| **Total** | **17 content + 6 dividers = 23** | |

---

## Open items for discussion

1. **VPP Scenario A vs B** — MP never answered Rudy's final question. Default to Scenario A (SurvalentONE is the VPP) and validate in the meeting.
2. **Slide 9 (HCMC case study)** — worth its own slide, or embed as a callout in the platform section?
3. **Depth of the architecture diagram** — CSS/SVG shapes vs a simplified approach?
4. **Speaker notes** — Andrew wants them. Embedded as collapsed callouts on each slide, or as a separate sheet?
