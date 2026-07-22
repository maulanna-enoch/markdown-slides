---

title: "Tentang Anak Homepage Revamp — Product Requirements Document"
subtitle: "Driving Engagement Without Sacrificing Simplicity"
summary: "PRD for the next iteration of the Tentang Anak Homepage"
authors: ["Maulanna Maryunani"]
tags: [case study]
categories: []
date: 2026-07-22
type: slides
slides:
  diagram: true
  theme: white
  highlight_style: github
  reveal_options:
    controls: true      # Show navigation arrows
    progress: true      # Show progress bar
    slideNumber: true   # Show slide numbers
    hash: true          # Update URL when navigating slides
  
---

<!-- ============================================================
SLIDE STRUCTURE — Tentang Anak Homepage Revamp PRD
"---" separates horizontal (top-level) slides.
"***" separates vertical (nested) sub-slides within a section.
Verify these separators match your HugoBlox/reveal.js config —
some versions default to different symbols.
============================================================= -->

# Tentang Anak Case Study
### Tentang Anak App Homepage Revamp

by Maulanna Maryunani

---

## Background & Context
 
- In **August 2025**, the Product team launched a major Homepage redesign
- In the redesign, the **Baby Tracker** (one of the most-used features) became the primary homepage focus, and most feature shortcuts were moved behind a dedicated **Menu page**.
 
_Immediately after launch, homepage drop-off improved and DAU/WAU stayed stable. Over the following months, however, **MAU declined** and **new installs continued to decrease**. Leadership expected engagement and growth to improve — those expectations were not met. Leadership now wants Product to determine **what should be improved next**._

---

## What the Data Shows

<div style="font-size: 0.6em;">
 
| Quantitative (last 6 months) | Qualitative research |
| :--- | :--- |
| • Homepage drop-off: **26% → 18%** after redesign | • Homepage feels "cleaner" but "less useful" |
| • DAU stable at **~15,000**/day; WAU stable at **~62,000**/week | • Some parents struggle to find important features |
| • MAU declined **145,000 → 123,000** | • Growth Tracking (Fitur Tumbuh), a core value proposition, is now harder to access |
| • Monthly installs declined **19,000 → 14,500** | • Many users are unaware of features hidden behind the Menu page |
 
*Note: the team has **not** concluded that homepage discoverability is the root cause of the declining metrics. Before/after homepage screenshots are provided separately.*

</div>

---

## Problem Statement

**Prioritizing Baby Tracker squeezes out non-daily/weekly features**
- **Baby Tracker** is a daily-cadence habitual activity (tracking naps, feeds, diapers)
- Prioritizing it leaves little homepage real estate for monthly-cadence features (Growth Tracking, vaccination reminders)
  -   This lines up with data: **DAU/WAU stable**, but **MAU declined**
  -   _Hypothesis_: MAU decrease --> less usage, less community referrals/word of mouth --> decrease in new installs
  -   This lines up with qualitative feedback: "app looks cleaner but feels less useful"

---

## Product Goal & Success Metrics
 
**Goal:** Recover MAU and install growth by restoring homepage visibility for non-daily-cadence features (Growth Tracking + Vaccination reminders)
 
- **Primary metrics**
  - MAU: trend back toward pre-redesign baseline (~145,000)
  - Monthly installs: trend back toward pre-redesign baseline (~19,000/month)
 
- **Guardrail metrics**
  - Homepage drop-off must not rise again to pre-redesign (**26%**), stretch goal: stays at **18%**
  - DAU (~15,000/day) and WAU (~62,000/week) must not rise again to pre-redesign, stretch goal: hold flat.

- **Supporting metrics**
  - % of MAU engaging with Growth Tracking or vaccination reminders at least once a month (feature breadth)
  - Tap-through concentration: share of homepage taps landing on the single primary CTA vs. spread across other elements

---
## Target User Personas
 
**Primary — "periodic check-in" parents:** parents w/ children due for a monthly-ish touchpoint (growth measurement, vaccination) 
 
**Secondary — existing "daily" Baby Trackers** — already well-served by the current homepage; need to try to not make their engagement worse
 
**Out of scope this iteration:** pregnant/Kehamilan-tab users — a distinct persona with different homepage needs. Candidate for a future iteration

---

## Opportunity Assessment
<div style="font-size: 0.8em;">
(Why Solve This First)

<!-- Why this bet, over other plausible bets, given the constraints -->

**Why this bet first:**
- Only hypothesis consistent with all four data points at once: DAU/WAU stable (daily habit intact) + MAU declining (monthly-cadence usage eroding) + installs declining (plausible referral/word-of-mouth spillover from that same eroding cohort)
- Direct evidence: quali research names Fitur Tumbuh (Growth Tracking) explicitly as a "core value proposition" that's now "harder to access"
- Protects what's already working — doesn't touch Baby Tracker, so the DAU/WAU and drop-off gains already banked aren't put at risk
- Fast to ship and validate — should fit resource constraints and have time to A/B test and get signals

**Why not other bets first:**
- Full Menu redesign — bigger effort accross domains
- Cleaning up homepage (get rid of some CTAs) — higher risk of alienating current baby tracking power users

</div>

---

## Scope & Proposed Solution

---

### In Scope

- **Promote Growth Tracker out of the "Gizi baik" pill** — give it its own properly-sized module (comparable visual weight to the Baby Tracker sub-cards)
- **Bring Vaccination reminder above the fold** — it already exists on Beranda but currently requires scrolling to reach; reposition so it's visible without scrolling
- **User-controlled module reordering** — let users reorder four homepage modules (Growth Tracker, Pencapaian, Baby Tracker, Vaccination reminder) via drag-and-drop or a simple reorder setting
  - Persist each user's chosen order (need BE but small effort)
  - Track reorder actions and engagement per module by position

---

### Out of Scope

- Menu redesign
- Nav bar changes
- Any other major BE architecture
- Algorithmic/ML-based auto-reordering
- Changes to the Baby Tracker widget's own internal functionality

---

### Proposed Solution

- **Growth Tracker module:** replace the small green "Gizi baik" pill with a full module card
  — latest weight/height/nutrition status plus a clear CTA into the full Growth Tracker, sized on par with the daily tracker cards
- **Vaccination module:** keep existing content, move it up so it renders above the scroll fold
- **Reorder capability:** long-press or a lightweight "customize homepage" entry point lets a user drag Growth Tracker, Pencapaian, Baby Tracker, and Vaccination reminder into their preferred order;
  - saved per user, order retained on following visits

---

## High-Level User Flow

<div style="font-size: 0.8em;">
 
```mermaid
flowchart TD
    Start([User opens Homepage]) --> Modules[Homepage displays modules in equal hierarchy]
    Modules --> GT[Growth Tracker]
    Modules --> AT[Activity Tracker]
    Modules --> VR[Vaccination Reminder]
 
    GT --> Reorder{Reorder modules?}
    AT --> Reorder
    VR --> Reorder
 
    Reorder -- Yes --> Customize[Long-press / Customize Homepage]
    Customize --> DragDrop[Drag & drop modules into preferred order]
    DragDrop --> Save[Order saved per user]
    Save --> Modules
 
    Reorder -- No --> Detail[Tap a module for full detail / action]
```

</div>

---

## Functional Requirements & Edge Cases

***

### Functional Requirements
- **Homepage** renders Growth Tracker, Activity Tracker, Vaccination Reminder, and Pencapaian as _distinct modules with similar visual weight_
- **Growth Tracker** module
  - shows latest weight/height/nutrition status
  - CTA into the full Growth Tracker detail view
- Users can **reorder** the four modules via drag-and-drop or an equivalent "customize homepage" button
- **Chosen order is persisted** per user
- Users who never customize see the current default order
- A **reset to default order** option is available
- Every module impression, tap-through, and reorder action (module, from-position, to-position) is logged for the success metrics

***

### Edge Cases
- **No Growth Tracker data yet** — show an empty/prompt state ("log your child's first measurement")
- **No upcoming/overdue vaccination** — show a neutral state ("up to date," next due date)
- **Multiple children on one account** — one account use the same order accross multiple children is OK
- **Reorder save fails** — fall back to last known good order
- **Reorder on one device, opened on another** — order must sync via the account, cache is permissible
- **Accessibility** — drag-and-drop needs a non-drag alternative (e.g., up/down buttons) for motor-impaired users
- **Child aged out of standard vaccination schedule** — show general vaccination history/info

---

## Rollout Strategy, Risks & Trade-offs

***

### Dev Timelines and Rollout
 
<div style="font-size: 0.3em;">

| Week | PM | PD | BE | FE | QA |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | PRD, kickoff | design Growth Tracker module | design docs for Reorder | design docs for Reorder | review PRD, draft test plan |
| 2 | review GT design | finalize + UT Growth Tracker designs; start reorder design | finalize Reorder design docs | Build GT module | test cases |
| 3 | draft dogfood plan | finalize + UT drag-and-drop reorder design | Build reorder persistence API (save/read per-user order) | Build reorder drag-and-drop UI | Test: GT module |
| 4 | draft rollout plan | Polish reorder UI, non-drag accessibility alt | Finish reorder API, add analytics events | Build + wire reorder end-to-end + analytics | Test: GT module + reorder, dogfooding release |
| 5 | finalize rollout plan| Monitor UI issues from dogfooding | Bug fixes, performance checks | Bug fixes from QA/dogfooding | Full regression pass, sign-off |
| 6 | Run staged rollout, monitor guardrails | Monitor UI feedback | Monitor backend health | Monitor client errors/crashes | Monitor rollout |
 
</div>
<div style="font-size: 0.8em;">

- **Initial rollout**: A/B test, add 10%/20%/50%/100% weekly
- **Success gate before full rollout:** no regression on guardrail metrics (drop-off, DAU, WAU) + directionally positive signal on module engagement/reorder adoption
- **Expectation-setting:** MAU is a 30-day metric — the 6-week window delivers the shipped MVP and early leading indicators, not final proof; full MAU validation needs more time post-launch

</div>

***

### Risks and Trade-offs
- **Clutter creep:** a bigger Growth Tracker module could lengthen the homepage (the default state carries most of the risk)
- **Reorder discoverability:** if users don't find the "customize homepage" entry point, this fix inherits the same discoverability problem the PRD is trying to solve
- **Daily-cadence ease-of-use vs. monthly-cadence visibility:** giving Growth Tracker and Vaccination equal hierarchy means Baby Tracker is no longer the _most prioritised feature_ on homepage
  — logging flow becomes marginally less immediate than it is today
  - this is a **conscious trade-off** of a small amount of daily-user convenience for a shot at reversing the MAU/install decline
  - it risks the one thing that's currently working (DAU/WAU)

---

<!-- Add this at the bottom of index.md -->
<style>
  .reveal .slides section p, 
  .reveal .slides section li {
    font-size: 0.7em;  /* Adjust this number (0.6 - 0.9) to find your perfect size */
    line-height: 1.2;  /* Optional: tightens the space between lines */
  }
</style>
