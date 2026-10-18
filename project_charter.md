# Ante Project Charter

**Status:** Draft (15 October 2026).

## Purpose and Research Question

Ante will research whether changes in permitted player event data can help a responsible-gambling analyst prioritize cases for human review. The research question is: **Can transparent, time-aware features prioritize cases more usefully than a simple rules baseline at the same review capacity?** A score is an aid to review, not a diagnosis, account decision, or proof that an intervention reduces harm. The project does not claim that any regulator requires this particular system for licensing.

## Scope and Outputs

### In Scope

The work is organized into six work packages. The [project plan](project_plan.md) details each package's tasks and deliverables.

- **WP1 - Project management and documentation.** Proposal and charter, risk register, meeting and iteration logs, and contribution record.
- **WP2 - Data governance and domain knowledge.** Data management plan; problem specification with target label, prediction horizon, and observation window; indicator catalog; and a transparent rule-based baseline computed only from information available at prediction time.
- **WP3 - Data engineering.** Data quality and exploration report, versioned canonical schema, ingestion and quality checks, leakage-safe temporal splits, and tests.
- **WP4 - Predictive modeling and evaluation.** Evaluation protocol fixed before modeling; baseline vs. model comparison; and explainability and fairness analysis, if labels permit it.
- **WP5 - Demonstration (MVP).** API and dashboard serving the baseline first, then the model with explanations, using synthetic or approved de-identified records.
- **WP6 - Framework and dissemination.** Method description and code templates, final presentation, and live demo.

### Out of Scope

- **Clinical diagnosis.** Scores support human review; they do not diagnose problem gambling.
- **Automatic player sanctions.** A score never triggers an account action on its own.
- **Live production use.** Nothing is deployed against live players or connected to operator systems.
- **Claims of harm reduction.** The project does not measure whether any intervention reduces harm.
- **Publishing sensitive data.** Public artifacts contain no identifiable player records, private event rows, individual scores, or credentials.

## Success and Acceptance

1. **Reproducible software.** The pipeline reruns and demonstrates input validation, feature boundaries, the baseline, and API behavior on synthetic examples, with linked tests and reviews.
2. **Qualified claims.** Every empirical claim states its dataset, population, outcome proxy, observation window, and limitations. With suitable labels, model and rules share one player-disjoint, chronological holdout and review capacity; without them, the result is a feasibility study.
3. **Traceable portfolio.** The public portfolio links problem, sources, decisions, meetings, contributions, iterations, code, tests, analyses, limitations, and final recommendation.
4. **Shared ownership.** All five members can explain the work in the viva. Each reflection is individually authored.

No accuracy target is set until the proxy, denominator, and review capacity are defined; threshold hypotheses on the board are questions to test, not acceptance criteria. Passing tests show software behavior, not clinical or operational validity.

## Team and Decision Rights

| Member                 | Roles                                | Leads    | Primary responsibilities                                                                                                     |
| ---------------------- | ------------------------------------ | -------- | ---------------------------------------------------------------------------------------------------------------------------- |
| Jurijs Kaminskis       | Product Owner, Business Intelligence | WP1, WP2 | Scope, priorities, stakeholder and course decisions, data access and domain knowledge, acceptance of outputs                 |
| Daniils Buts           | Process Expert, Data Scientist       | WP6      | Data Driven Scrum process, proxy and label critique, evaluation protocol, fairness analysis, framework and its dissemination |
| Andrejs Fjodorovs      | Lead Data Scientist                  | WP4      | Modeling, baseline comparison, error analysis, and explainability                                                            |
| Arturs Greķe           | Data Engineer                        | WP3      | Source inventory, event contract, ingestion, data quality, feature pipeline, and controlled data flow                        |
| Volodymyr Stishkovskyi | Software Developer, ML Engineer      | WP5      | MVP API and dashboard, model serving, reproducibility, software tests, and deployment boundary                               |

A work package lead is accountable for its deliverables, but not the only contributor.

## Milestones and Gates

Work is delivered in four Product Increments (20 Oct - 15 Dec 2026), each closing on a milestone. The [project plan](project_plan.md) lists the deliverables due at each point.

| Planned date | Milestone or deliverable                                    |
| ------------ | ----------------------------------------------------------- |
| 20 Oct 2026  | D1.1 Proposal and Charter                                   |
| 23 Oct 2026  | MS1 Data access confirmed; D2.1 Data Management Plan        |
| 08 Nov 2026  | MS2 Problem defined and baseline ready                      |
| 22 Nov 2026  | MS3 End-to-end prototype                                    |
| 04 Dec 2026  | MS4 Stakeholder MVP demo                                    |
| 15 Dec 2026  | MS5 Final delivery                                          |
| 15 Dec 2026  | Presentation                                                |
| 27 Dec 2026  | Individual reflections                                      |

## Data and Ethics Gate

Jurijs reports that, as the casino owner, he permits educational use of a dataset that he will anonymize, and that clauses 3.2, 3.7, and 11.1 of the casino's customer agreement allow use and transfer of gameplay information for Data Science purposes, including model training, at his discretion. He identifies Curaçao as the operator's jurisdiction; player, processing, and recipient locations have not been established. The clause text has not been supplied or independently reviewed. Before loading the full operator dataset, obtain and review the current agreement wording and document its applicability to the specific dataset, purpose, team, and transfer, plus any applicable course or ethics approval. Record the actual fields, de-identification method, permitted purpose, access list, storage location, retention, and deletion rule in the [data management plan](data_management_plan.md). Keep raw data and player-level outputs outside the public repositories. Record whether any label is independently assessed (for example, staff reviews of players), what it means, who assigned it, when it became available, and which players were eligible for review. Unreviewed players are not assumed negative. If representative labels are absent, use only descriptive indicators and software scenarios.

The team will document false-positive and false-negative costs, selection bias, temporal leakage, subgroup limitations, re-identification risk, and automation bias. A human specialist must interpret any review score. Nothing in this charter authorizes deployment against live players.

## Ways of Working and Change Control

- Work follows Data Driven Scrum. Each board item records its work package, owner, status, and Create, Observe, and Analyze evidence, and is Done only when its question, creation, observation, analysis, and conclusion have evidence links; the [iteration log](iteration_log.md) records iterations, reviews, retrospectives, and feedback.
- Keep meeting notes and decisions in [versioned repository files](meetings/README.md), with date, participants, evidence, decision, action owner, and follow-up item. Do not invent attendance or outcomes for meetings that have not happened.
- Track risks, owners, and triggers in the [risk register](risk_register.md) and review it weekly.
- Use pull requests for code and public documentation. A contributor and an independent reviewer should be different people. Tests, privacy review, and documentation readback precede merge.
- The Product Owner may reprioritize scope; any change to data use, target label, prediction time, or public claims requires a recorded team decision and an updated problem specification or evaluation protocol before analysis continues.
- If the data gate fails, the team will deliver the reproducible pipeline, rule-based scenario demo, and explicit feasibility report described in the proposal.

## Open Decisions

1. Confirm the course team number, five-member approval record, and Moodle deadlines.
2. Review the current wording and applicability of clauses 3.2, 3.7, and 11.1 to the specific data, purpose, and team before the full export; record the de-identified event schema and handling and deletion decisions (MS1, [R01](risk_register.md)).
3. Decide whether independently assessed labels exist and freeze the outcome definition and holdout plan (MS2, [R02](risk_register.md)).
4. Have each member confirm their role, WP lead assignment, and contribution entries in the [contributions record](contributions.md).
