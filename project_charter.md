# Ante Project Charter

**Status:** Draft (20 October 2026).

## Purpose

The project aim is to test whether gambling-related harm can be predicted early from player account data, starting with transparent rules built from published harm markers and comparing them to machine learning approaches, demonstrating in an MVP how the resulting risk scores may help analysts prioritize players for review. The project does not claim that any regulator requires or explicitly requested this particular system for licensing.

## Objectives

Each objective is due at a milestone. The [project plan](project_plan.md) maps them to work packages and increments.

- **O1 (8 Nov 2026, MS2).** Build a one-command pipeline turning at least 100 accounts' raw events into sessions and behavioral markers, freeze the outcome label and evaluation protocol, and score the rule baseline against the label.
- **O2 (22 Nov 2026, MS3).** Compare at least two machine-learning models with the rule baseline at the same review capacity on the share of harm-related events flagged 7 to 30 days ahead and on median lead time, evaluated on held-out players.
- **O3 (6 Dec 2026, MS4).** Deploy an API and a dashboard that score a replayed event stream, return each score with its top three reasons, and pass tests confirming that API scores match the offline model.
- **O4 (15 Dec 2026, MS6).** Publish the documented pipeline with a model card covering data protection, ethical risks, and limitations, verified by an independent rerun.

## Scope and Outputs

### In Scope

The project uses one operator's pseudonymized data, and the work is organized into six work packages. The [project plan](project_plan.md) details each package's tasks and deliverables.

- **WP1 - Project management and documentation.** Proposal and charter, risk register, meeting and iteration logs, and contribution record.
- **WP2 - Data governance and domain knowledge.** Data management plan, indicator catalog, and a transparent rule-based baseline computed only from information available at prediction time and frozen at MS2.
- **WP3 - Data engineering.** Data contract, data quality report, and a reproducible data and feature pipeline with ingestion and quality checks, leakage-safe validation folds, and tests.
- **WP4 - Predictive modeling and evaluation.** Evaluation protocol, including the outcome label, prediction times, look-back window, and horizon, fixed before modeling; comparison of models with the baseline, including early recall and lead time; and per-player explanations for the MVP.
- **WP5 - Demonstration (MVP).** Scoring API and analyst dashboard serving the baseline first, then the selected model with explanations, replaying held-out pseudonymized records, so each player is scored by a model trained without them; and a CI/CD pipeline that tests and deploys both.
- **WP6 - Synthesis and dissemination.** Documented pipeline and model card, final presentation and live demonstration, and public project profile.

### Out of Scope

- **Live-platform integration.** Nothing is deployed against live players or connected to operator systems.
- **Automated interventions.** A score never triggers an intervention or account action on its own.
- **Measuring intervention effects.** The project does not measure whether any intervention reduces harm.
- **Clinical diagnosis.** Scores support human review; they do not diagnose problem gambling.
- **Compliance certification.** The project does not certify the baseline or the models against any regulation.
- **External validation.** Results are not validated on other operators' data; transferability is a limitation and future work.
- **Publishing sensitive data.** Public artifacts contain no identifiable player records, private event rows, individual scores, or credentials.

## Success and Acceptance

1. **Reproducible software.** The pipeline reruns and demonstrates input validation, feature boundaries, the baseline, and API behavior, with linked tests and reviews. A member who did not write it can rerun it from its README (O4).
2. **Qualified claims.** Every empirical claim states its dataset, population, outcome proxy, observation window, and limitations. With suitable labels, model and rules share the same data splits and the same review capacity (the same number of top-ranked players each week, fixed in the evaluation protocol); without them, the result is a feasibility study.
3. **Traceable portfolio.** The public portfolio links problem, sources, decisions, meetings, contributions, iterations, code, tests, analyses, limitations, and final recommendation.
4. **Shared ownership.** All five members can explain the work in the viva. Each reflection is individually authored.

No accuracy target is set: the objectives fix what is measured, not how good the result must be. Threshold hypotheses on the board are questions to test, not acceptance criteria. Passing tests show software behavior, not clinical or operational validity.

## Team and Decision Rights

| Member                 | Roles                                | Leads    | Primary responsibilities                                                                                 |
| ---------------------- | ------------------------------------ | -------- | -------------------------------------------------------------------------------------------------------- |
| Jurijs Kaminskis       | Product Owner, Business Intelligence | WP1, WP2 | Prioritizes the backlog, supplies domain knowledge, owns data and casino                                 |
| Daniils Buts           | Process Expert, Data Scientist       | WP6      | Facilitates events and safeguards the process, supports in data exploration and experiments              |
| Andrejs Fjodorovs      | Lead Data Scientist                  | WP4      | Drives exploration, research, and modeling activities, designs experiments and evaluation                |
| Arturs Greķe           | Data Engineer                        | WP3      | Extracts and prepares player data, maintains data contract and quality checks, provides domain expertise |
| Volodymyr Stishkovskyi | Software Developer, ML Engineer      | WP5      | Builds the scoring API and dashboard, handles deployment and DevOps                                      |

A work package lead is accountable for its deliverables, but not the only contributor.

## Milestones and Gates

Work is delivered in four Product Increments (20 Oct - 15 Dec 2026). Each increment closes on a milestone; MS1 is the data gate and MS5 freezes the results before the final synthesis. The [project plan](project_plan.md) lists what each increment adds and the deliverables due at each point.

| Planned date | Milestone or deliverable                                                 |
| ------------ | ------------------------------------------------------------------------ |
| 20 Oct 2026  | D1.1 Proposal and charter                                                |
| 30 Oct 2026  | MS1 Data and label source confirmed; D2.1 Data management plan           |
| 08 Nov 2026  | MS2 Baseline ready, closing Increment 1 (Baseline benchmark); O1         |
| 22 Nov 2026  | MS3 Models compared, closing Increment 2 (Models vs rule baseline); O2   |
| 06 Dec 2026  | MS4 MVP complete, closing Increment 3 (Explained review queue); O3       |
| 10 Dec 2026  | MS5 Results frozen                                                       |
| 15 Dec 2026  | MS6 Final delivery, closing Increment 4 (Reproducible and presented); O4 |
| 15 Dec 2026  | Presentation materials (D6.2); presentation date per course schedule     |
| 27 Dec 2026  | Individual reflections                                                   |

## Data and Ethics Gate

Jurijs reports that, as the casino owner, he permits educational use of a dataset that he will anonymize, and that clauses 3.2, 3.7, and 11.1 of the casino's customer agreement allow use and transfer of gameplay information for Data Science purposes, including model training, at his discretion. He identifies Curaçao as the operator's jurisdiction; player, processing, and recipient locations have not been established. The clause text has not been supplied or independently reviewed. Before loading the full operator dataset, obtain and review the current agreement wording and document its applicability to the specific dataset, purpose, team, and transfer, plus any applicable course or ethics approval. Record the actual fields, de-identification method, permitted purpose, access list, storage location, retention, and deletion rule in the [data management plan](data_management_plan.md). Keep raw data and player-level outputs outside the public repositories. The team approves the label definition, consulting Jurijs as data owner and domain expert. Record whether any label is independently assessed (for example, staff reviews of players), what it means, who assigned it, when it became available, and which players were eligible for review. Unreviewed players are not assumed negative. If representative labels are absent, use only descriptive indicators, software scenarios, and the blind case review.

The team will document false-positive and false-negative costs, selection bias, temporal leakage, subgroup limitations, re-identification risk, and automation bias. A human specialist must interpret any review score. Harm prevention is the only permitted purpose, and the model card warns against other uses, such as marketing. The EU AI Act does not apply to research before a system is placed on the market or put into service (Art. 2(8)); an operator deploying such a system would need its own assessment. Nothing in this charter authorizes deployment against live players.

## Ways of Working and Change Control

- Work follows Data Driven Scrum. Each board item records its work package, owner, status, and Create, Observe, and Analyze evidence, and is Done only when its question, creation, observation, analysis, and conclusion have evidence links; the [iteration log](iteration_log.md) records iterations, reviews, retrospectives, and feedback.
- Keep meeting notes and decisions in [versioned repository files](meetings/README.md), with date, participants, evidence, decision, action owner, and follow-up item. Do not invent attendance or outcomes for meetings that have not happened.
- Track risks, owners, and triggers in the [risk register](risk_register.md) and review it weekly.
- Use pull requests for code and public documentation. A contributor and an independent reviewer should be different people. Tests, privacy review, and documentation readback precede merge.
- The Product Owner may reprioritize scope; any change to data use, target label, prediction time, or public claims requires a recorded team decision and an updated evaluation protocol before analysis continues.
- If the data gate fails, the team will deliver the reproducible pipeline, rule-based scenario demo, and explicit feasibility report ([R01](risk_register.md)).

## Open Decisions

1. Review the current wording and applicability of clauses 3.2, 3.7, and 11.1 to the specific data, purpose, and team before the full export; record the pseudonymized event schema and handling and deletion decisions (MS1, [R01](risk_register.md)).
2. Decide whether independently assessed labels exist (MS1) and freeze the outcome label and evaluation protocol (MS2, [R02](risk_register.md)).
