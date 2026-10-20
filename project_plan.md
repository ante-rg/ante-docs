# Ante Project Plan

This plan supports the course portfolio. It sets out the project objectives, the six thematic work packages (WPs) that deliver them, the four Product Increments, and six milestones that pace the work.

## Objectives

Each objective is due at a milestone, and each milestone checks the objectives due at that point.

| ID | Objective                                                                                                                                                                                                              | Due         | Milestone | Main WPs      |
| -- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------- | --------- | ------------- |
| O1 | Build a one-command pipeline turning at least 100 accounts' raw events into sessions and behavioral markers, freeze the outcome label and evaluation protocol, and score the rule baseline against the label.          | 08 Nov 2026 | MS2       | WP2, WP3, WP4 |
| O2 | Compare at least two machine-learning models with the rule baseline at the same review capacity on the share of harm-related events flagged 7 to 30 days ahead and on median lead time, evaluated on held-out players. | 22 Nov 2026 | MS3       | WP4           |
| O3 | Deploy an API and a dashboard that score a replayed event stream, return each score with its top three reasons, and pass tests confirming that API scores match the offline model.                                     | 06 Dec 2026 | MS4       | WP5           |
| O4 | Publish the documented pipeline with a model card covering data protection, ethical risks, and limitations, verified by an independent rerun.                                                                          | 15 Dec 2026 | MS6       | WP6           |

## Product Increments

Each increment closes on a milestone and adds something the team can show.

| Increment                      | Planned dates             | What it adds                                                                                                                                           | Closing milestone | Objectives |
| ------------------------------ | ------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------ | ----------------- | ---------- |
| 1 - Baseline benchmark         | 20 Oct 2026 - 08 Nov 2026 | We know how well transparent rules flag at-risk players on our data, and have the pipeline, label, and frozen protocol to test any model against them. | MS2               | O1         |
| 2 - Models vs rule baseline    | 09 Nov 2026 - 22 Nov 2026 | The first answer to the research question, and a walking-skeleton MVP serving baseline scores end to end.                                              | MS3               | O2         |
| 3 - Explained review queue     | 23 Nov 2026 - 06 Dec 2026 | An analyst can open the MVP and see players ranked by the selected model, each with its top three reasons, over a replayed event stream.               | MS4               | O3         |
| 4 - Reproducible and presented | 07 Dec 2026 - 15 Dec 2026 | The documented pipeline is published with its model card and verified by an independent rerun, and the results are presented with a live demo.         | MS6               | O4         |

## Milestones

MS2, MS3, MS4, and MS6 close an increment. MS1 is a data gate before modeling work can start, and MS5 freezes the results before the final synthesis.

| Milestone | Description                     | Planned date | Closes      | Evidence                                                                                                                   |
| --------- | ------------------------------- | ------------ | ----------- | -------------------------------------------------------------------------------------------------------------------------- |
| MS1       | Data and label source confirmed | 30 Oct 2026  | -           | Data management plan reviewed, dataset for Increment 1 decided, and source of harm-event labels decided                    |
| MS2       | Baseline ready                  | 08 Nov 2026  | Increment 1 | O1: pipeline runs with one command, label and evaluation protocol frozen before any model is trained, rule baseline scored |
| MS3       | Models compared                 | 22 Nov 2026  | Increment 2 | O2: models compared with the baseline; walking-skeleton MVP serves baseline scores end to end                              |
| MS4       | MVP complete                    | 06 Dec 2026  | Increment 3 | O3: MVP serves the selected model's scores with top three reasons, parity tests pass, demonstrated at the iteration review |
| MS5       | Results frozen                  | 10 Dec 2026  | -           | All reported results final and traceable, with no new experiments after this point                                         |
| MS6       | Final delivery                  | 15 Dec 2026  | Increment 4 | O4: documented pipeline and model card published; portfolio and presentation materials complete                            |

## Work Packages

Each WP has a lead (accountable person), objectives, deliverables, and planned timing. Deliverables are tagged by type: R for report, S for software.

### WP1: Project management and documentation

**Lead:** Jurijs. **Active:** all increments. **Objectives:** all (supporting).

This WP keeps the project coordinated, documented, and on track, covering Data Driven Scrum events, the backlog, risk management, and the project's administrative record.

- D1.1 Proposal and charter (R, due 20 Oct)
- D1.2 Risk register (R, initial version due 20 Oct, continuously updated)
- D1.3 Meeting and iteration logs (R, continuous until 15 Dec)

### WP2: Data governance and domain knowledge

**Lead:** Jurijs. **Active:** mainly Increments 1-2. **Objectives:** O1.

This WP secures lawful, ethical access to player data and turns domain expertise into the indicator catalog and the rule-based baseline that every model is compared against.

- D2.1 Data management plan, including GDPR and ethics considerations (R, due 30 Oct)
- D2.2 Indicator catalog (R, due 1 Nov)
- D2.3 Rule baseline (S, due 8 Nov)

### WP3: Data engineering

**Lead:** Arturs. **Active:** mainly Increments 1-2, with support later. **Objectives:** O1.

This WP produces clean, reproducible, leakage-safe data for all downstream work, from ingestion and quality checks to features and validation folds.

- D3.1 Data contract: versioned event schema that every extract is validated against (R, due 1 Nov)
- D3.2 Data quality report, including data exploration (R, due 6 Nov)
- D3.3 Data and feature pipeline: reproducible ingestion, quality checks, and feature building, producing a versioned modeling dataset with validation folds (S, first version by 8 Nov, extended until 22 Nov)

### WP4: Predictive modeling and evaluation

**Lead:** Andrejs. **Active:** all increments, mainly 2-3. **Objectives:** O1, O2.

This WP develops and evaluates the machine-learning models, always against the rule-based baseline and under an evaluation protocol fixed before any modeling.

- D4.1 Evaluation protocol: outcome label, prediction times, look-back window, horizon, metrics, review capacity, validation scheme (R, due 6 Nov)
- D4.2 Models vs baseline report: comparison of the models with the rule baseline, including early recall and lead time (R, due 22 Nov)
- D4.3 Selected model with explanations: the reasons behind each player's score (R+S, due 29 Nov)

### WP5: Demonstration (MVP)

**Lead:** Volodymyr. **Active:** Increments 2-4. **Objectives:** O3.

This WP builds the MVP: an API and an analyst dashboard that serve the risk scores as a ranked review queue, first for the baseline and then for the selected model.

- D5.1 Scoring API: REST service with a documented contract, serving baseline scores first and then the selected model's scores with top three reasons, with parity tests against the offline model (S, first version by 22 Nov, extended until 6 Dec)
- D5.2 Analyst dashboard: ranked review queue over a replayed event stream, showing each player's score and top three reasons (S, first version by 22 Nov, extended until 6 Dec)
- D5.3 CI/CD pipeline: tests, including parity tests, on every pull request, and one-command deployment of the API and dashboard (S, due 22 Nov)

### WP6: Synthesis and dissemination

**Lead:** Daniils. **Active:** mainly Increments 3-4. **Objectives:** O4.

This WP brings the results together: it documents the pipeline so others can rerun and adapt it, presents the findings, and maintains the public project profile that indexes all outputs.

- D6.1 Documented pipeline and model card (R+S, due 15 Dec)
- D6.2 Presentation and live demonstration (R, materials due 15 Dec; presentation date per course schedule)
- D6.3 Public project profile: organization README with project summary, team, annotated index of all outputs, and contribution attribution (R, due 15 Dec)

## Responsibilities

The RACI matrix shows each member's planned part in every deliverable (R: responsible, A: accountable, C: consulted, I: informed). Work package leads are accountable, but not necessarily solely responsible.

| Deliverable                              | Jurijs | Daniils | Andrejs | Arturs | Volodymyr |
| ---------------------------------------- | :----: | :-----: | :-----: | :----: | :-------: |
| D1.1 Proposal and charter                |  A/R   |    R    |    C    |   C    |     C     |
| D1.2 Risk register                       |  A/R   |    C    |    C    |   C    |     C     |
| D1.3 Meeting and iteration logs          |   A    |    R    |    C    |   C    |     C     |
| D2.1 Data management plan                |  A/R   |    C    |    I    |   C    |     C     |
| D2.2 Indicator catalog                   |  A/R   |    C    |    C    |   C    |     I     |
| D2.3 Rule baseline                       |  A/R   |    C    |    C    |   R    |     I     |
| D3.1 Data contract                       |   C    |    I    |    C    |  A/R   |     C     |
| D3.2 Data quality report                 |   C    |    R    |    R    |  A/R   |     I     |
| D3.3 Data and feature pipeline           |   C    |    I    |    C    |  A/R   |     C     |
| D4.1 Evaluation protocol                 |   R    |    R    |   A/R   |   C    |     I     |
| D4.2 Models vs baseline report           |   C    |    R    |   A/R   |   C    |     I     |
| D4.3 Selected model with explanations    |   C    |    C    |   A/R   |   I    |     C     |
| D5.1 Scoring API                         |   C    |    I    |    C    |   C    |    A/R    |
| D5.2 Analyst dashboard                   |   C    |    I    |    C    |   I    |    A/R    |
| D5.3 CI/CD pipeline                      |   I    |    C    |    C    |   C    |    A/R    |
| D6.1 Documented pipeline and model card  |   C    |   A/R   |    R    |   R    |     R     |
| D6.2 Presentation and live demonstration |   R    |   A/R   |    R    |   R    |     R     |
| D6.3 Public project profile              |   C    |   A/R   |    C    |   C    |     C     |

## WP vs Increments

|     | Increment 1 | Increment 2 | Increment 3 | Increment 4 |
| --- | :---------: | :---------: | :---------: | :---------: |
| WP1 |      ●      |      ●      |      ●      |      ●      |
| WP2 |      ●      |      ●      |      ○      |             |
| WP3 |      ●      |      ●      |      ○      |      ○      |
| WP4 |      ○      |      ●      |      ●      |      ○      |
| WP5 |             |      ●      |      ●      |      ○      |
| WP6 |             |             |      ○      |      ●      |

● marks main focus, ○ marks lighter or supporting activity.

```mermaid
---
displayMode: compact
---
gantt
    title Ante Work Packages
    dateFormat YYYY-MM-DD
    axisFormat %d %b
    tickInterval 1week
    weekday monday
    todayMarker off
    %% End and milestone dates are exclusive (the day after the planned date) so bars cover the full last day
    section Increments
    1 - Baseline benchmark :2026-10-20, 2026-11-09
    2 - Models vs rule baseline :2026-11-09, 2026-11-23
    3 - Explained review queue :2026-11-23, 2026-12-07
    4 - Reproducible and presented :2026-12-07, 2026-12-16
    section WP1
    Management :2026-10-20, 2026-12-16
    section WP2
    Governance and domain :2026-10-20, 2026-12-07
    section WP3
    Data engineering :2026-10-20, 2026-12-16
    section WP4
    Modeling and evaluation :2026-10-26, 2026-12-16
    section WP5
    Demonstration (MVP) :2026-11-09, 2026-12-12
    section WP6
    Synthesis and dissemination :2026-11-23, 2026-12-16
    section Milestones
    MS1 :milestone, 2026-10-31, 0d
    MS2 :milestone, 2026-11-09, 0d
    MS3 :milestone, 2026-11-23, 0d
    MS4 :milestone, 2026-12-07, 0d
    MS5 :milestone, 2026-12-11, 0d
    MS6 :milestone, 2026-12-16, 0d
```
