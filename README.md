# Patient Treatment in Emergency Departments
### Process Mining & Business Information Systems Analysis

> **Course project** — Business Information Systems, Prof. Paolo Ceravolo  
> Università degli Studi di Milano · A.A. 2025–2026  
> **Author:** Iliano Fasolino

---

## Overview

This project applies **process mining** to a real-world Emergency Department (ED) event log to uncover structural inefficiencies invisible to traditional reporting. Starting from raw, noisy event data, it constructs a rigorous analytical pipeline — from preprocessing through conformance checking — and closes with data-driven improvement proposals grounded in quantitative evidence.

The work is organized around four pillars:

1. **Preprocessing pipeline** — transforming a dirty, high-dimensionality event log into a reliable dataset for process analysis
2. **Performance analysis** — measuring throughput, bottlenecks, and patient flow with multiple KPIs
3. **Process discovery & conformance checking** — building and evaluating a formal process model from the data
4. **Improvement scenarios** — two concrete, implementation-ready proposals with measurable targets and phased timelines

---

## The Dataset

The analysis operates on an ED event log with over 25,000 events across nearly 2,000 patient cases, each representing a full stay from arrival to discharge. The log captures a rich set of attributes — acuity level, patient demographics, clinical activities, timestamps, and disposition outcomes — recorded across heterogeneous activity types with distinct logging patterns.

Understanding *why* the data looks the way it does proved as important as cleaning it.

---

## Methodology

### Phase 1 — Filtering & Cleaning

The preprocessing phase is not a mechanical step but a series of deliberate modeling decisions. The event log presents three non-trivial challenges:

- **Simultaneous events with identical timestamps** — a phenomenon that could be misread as a data quality error, but carries a specific semantic meaning in the clinical context
- **Structured missing values at ~70–90%** — not data corruption, but an expected pattern arising from the difference between case-level and event-level attributes
- **Noise and outliers** — incomplete cases, traces too short to represent a real ED pathway, and duration extremes that would distort any time-based analysis

Each challenge is addressed with an explicit, justified decision rather than a default fix. The result is a clean log that preserves the integrity of the process structure while eliminating statistical artifacts.

### Phase 2 — Performance Analysis

Six metrics are computed and analyzed:

| KPI | What it reveals |
|-----|----------------|
| Throughput Time | End-to-end duration distribution and variability |
| Time-to-Triage | A metric that surfaces a significant data artifact — and why it must be excluded |
| Time-to-Discharge | Post-clinical administrative delay |
| Process Variants | Fragmentation and adherence to the Pareto principle |
| Acuity Segmentation | Per-priority-level performance — where the most counterintuitive finding emerges |
| Bottleneck Identification | The transition pair responsible for the greatest accumulated delay |

Several findings in this phase run against intuition. The relationship between patient urgency and actual wait time reveals a structural paradox that sits at the core of the department's inefficiency. Variant analysis tells a story about standardization — or the absence of it.

### Phase 3 — Process Discovery & Conformance Checking

The process model is discovered using **Inductive Miner**, chosen for its robustness to noise and its suitability for fragmented event logs. The resulting **Petri Net** is then evaluated on four standard conformance dimensions: fitness, precision, generalization, and simplicity.

The conformance results are paradoxical: two metrics pull in opposite directions in a way that reframes the entire problem. Rather than indicating non-compliance, the numbers point to something more fundamental about how the ED operates. This finding directly shapes the improvement proposals.

Visualizations are produced using both **PM4PY** (integrated pipeline) and **Disco** (alternative DFGs and case variant trees), offering complementary perspectives on the same process.

### Phase 4 — Improvement Proposals

Two scenarios are proposed, each with specific targets, implementation timelines, cost considerations, and expected impact:

**Scenario 1 — Care Pathway Standardization by Acuity Level**  
A redesign of the end-to-end patient flow, addressing the root cause of the Pareto violation and the acuity paradox. The proposal defines four distinct pathways, each with target durations, dedicated resource logic, and a phased rollout plan — pilot, full implementation, and continuous monitoring.

**Scenario 2 — Discharge Process Optimization**  
A targeted intervention on the post-clinical administrative window, combining process redesign (anticipatory planning), digital tooling (EHR integration, e-prescriptions), and role extension (nurse-led discharge for appropriate cases). Quantified targets and real-world benchmarks from the literature are included.

---

## Tools & Stack

| Tool | Role |
|------|------|
| Python 3.x | Core language |
| Pandas & NumPy | Data manipulation and numerical analysis |
| Matplotlib & Seaborn | Statistical visualization |
| PM4PY | Process discovery, Petri Net modeling, conformance checking |
| Disco | Additional DFG and variant visualizations |
| Jupyter Notebook | End-to-end reproducible analysis |

---

## Repository Contents

```
Business-Information-Systems/
├── BIS Project Fasolino.ipynb          # Full analysis notebook (code + commentary)
├── Fasolino_Iliano_181225_ED_report.pdf  # Written report with findings and proposals
├── case_study.pdf                      # Original case study assignment
└── README.md
```

The notebook contains the complete implementation of all four phases, with inline commentary explaining each decision. The report provides the written narrative, quantitative findings, and the full improvement proposals — including the numbers, the paradoxes, and the reasoning behind every recommendation.

---

## Key Themes

- The difference between a data quality problem and a domain-specific data pattern
- When a "perfect" conformance metric is actually a red flag
- How process fragmentation makes protocol-based improvement impossible before it makes it necessary
- Why the most urgent non-critical patients may systematically wait longer than the critical ones — and what the data says about why

---

*Full analysis, findings, and improvement scenarios are documented in `Fasolino_Iliano_181225_ED_report.pdf`.*
