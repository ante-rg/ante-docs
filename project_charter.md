# Ante Project Charter

**Status:** Draft (20 October 2026).

## Purpose and Research Question

Ante will research whether changes in permitted player event data can help a responsible-gambling analyst prioritize cases for human review. The research question is: **Does machine learning flag players at risk of gambling-related harm earlier than a transparent rule-based baseline at the same review capacity?** The project answers it on one operator's data and delivers the resulting risk scores through an MVP. A score is an aid to review, not a diagnosis, account decision, or proof that an intervention reduces harm. The project does not claim that any regulator requires this particular system for licensing.

## Objectives

Each objective is due at a milestone. The [project plan](project_plan.md) maps them to work packages and increments.

- **O1 (8 Nov 2026, MS2).** Build a one-command pipeline turning at least 100 accounts' raw events into sessions and behavioral markers, freeze the outcome label and evaluation protocol, and score the rule baseline against the label.
- **O2 (22 Nov 2026, MS3).** Compare two machine-learning models with the rule baseline on the share of harm-related events flagged 7 to 30 days ahead at a 5% review capacity, using player-grouped cross-validation and bootstrap confidence intervals.
- **O3 (6 Dec 2026, MS4).** Deploy an API and a dashboard that score a replayed event stream, return each score with its top three reasons, and pass tests confirming that API scores match the offline model.
- **O4 (10 Dec 2026, MS5).** Conduct a blind review of 40 player cases, 20 flagged only by the model and 20 only by the rules, each rated by two members against a fixed rubric, and report the share judged concerning per group with inter-rater agreement.
- **O5 (15 Dec 2026, MS6).** Publish the documented pipeline with a model card covering data protection, ethical risks and limitations, verified by an independent rerun.

## Scope and Outputs

### In Scope

The work is organized into six work packages. The [project plan](project_plan.md) details each package's tasks and deliverables.

- **WP1 - Project management and documentation.** Proposal and charter, risk register, meeting and iteration logs, contribution record, and project portfolio.
- **WP2 - Data governance and domain knowledge.** Data management plan; problem specification with target label, prediction horizons, and look-back window; indicator catalog; and a transparent rule-based baseline computed only from information available at prediction time and frozen at MS2.
- **WP3 - Data engineering.** Data quality and exploration report, versioned canonical schema, ingestion and quality checks, leakage-safe player-grouped folds, and tests.
- **WP4 - Predictive modeling and evaluation.** Evaluation protocol fixed before modeling; comparison of models with the baseline, including early recall, lead time, and per-brand results; and per-player explanations for the MVP.
- **WP5 - Demonstration (MVP).** API and dashboard serving the baseline first, then the selected model with explanations, replaying held-out de-identified records, so each player is scored by a model trained without them. The team also uses the dashboard for the blind case review.
- **WP6 - Synthesis and dissemination.** Blind case review, documented pipeline and model card, final presentation, and live demo.

### Out of Scope

- **Clinical diagnosis.** Scores support human review; they do not diagnose problem gambling.
- **Automatic player sanctions.** A score never triggers an account action on its own.
- **Live production use.** Nothing is deployed against live players or connected to operator systems.
- **Claims of harm reduction.** The project does not measure whether any intervention reduces harm.
- **Compliance certification.** The project does not certify the baseline or the models against any regulation.
- **External validation.** Results are not validated on other operators' data; transferability is a limitation and future work.
- **Publishing sensitive data.** Public artifacts contain no identifiable player records, private event rows, individual scores, or credentials.

## Success and Acceptance

1. **Reproducible software.** The pipeline reruns and demonstrates input validation, feature boundaries, the baseline, and API behavior on synthetic examples, with linked tests and reviews. A member who did not write it can rerun it from its README (O5).
2. **Qualified claims.** Every empirical claim states its dataset, population, outcome proxy, observation window, and limitations. With suitable labels, model and rules share the same cross-validation folds and the same review capacity (the top 5% of players active each week); without them, the result is a feasibility study, and the blind case review (O4) is the main check of what the scores flag.
3. **Traceable portfolio.** The public portfolio links problem, sources, decisions, meetings, contributions, iterations, code, tests, analyses, limitations, and final recommendation.
4. **Shared ownership.** All five members can explain the work in the viva. Each reflection is individually authored.

No accuracy target is set: the objectives fix what is measured and at which review capacity, not how good the result must be. Threshold hypotheses on the board are questions to test, not acceptance criteria. Passing tests show software behavior, not clinical or operational validity.

## Team and Decision Rights

| Member                 | Roles                                | Leads    | Primary responsibilities                                                                                       |
| ---------------------- | ------------------------------------ | -------- | -------------------------------------------------------------------------------------------------------------- |
| Jurijs Kaminskis       | Product Owner, Business Intelligence | WP1, WP2 | Scope, priorities, course decisions, data access and domain knowledge, acceptance of outputs                   |
| Daniils Buts           | Process Expert, Data Scientist       | WP6      | Data Driven Scrum process, proxy and label critique, blind case review, documented pipeline, and dissemination |
| Andrejs Fjodorovs      | Lead Data Scientist                  | WP4      | Evaluation protocol, modeling, baseline comparison, error analysis, and explainability                         |
| Arturs Greķe           | Data Engineer                        | WP3      | Source inventory, event contract, ingestion, data quality, feature pipeline, and controlled data flow          |
| Volodymyr Stishkovskyi | Software Developer, ML Engineer      | WP5      | MVP API and dashboard, model serving, reproducibility, software tests, and deployment boundary                 |

A work package lead is accountable for its deliverables, but not the only contributor.

## Milestones and Gates

Work is delivered in four Product Increments (20 Oct - 15 Dec 2026). Each increment closes on a milestone; MS1 is the data gate and MS5 freezes the results before the final write-up. The [project plan](project_plan.md) lists what each increment adds and the deliverables due at each point.

| Planned date | Milestone or deliverable                                                |
| ------------ | ----------------------------------------------------------------------- |
| 20 Oct 2026  | D1.1 Proposal and Charter                                               |
| 30 Oct 2026  | MS1 Data and label source confirmed; D2.1 Data Management Plan          |
| 08 Nov 2026  | MS2 Baseline ready, closing Increment 1 (Baseline benchmark); O1        |
| 22 Nov 2026  | MS3 Models compared, closing Increment 2 (Models vs rules); O2          |
| 06 Dec 2026  | MS4 MVP complete, closing Increment 3 (Explained review queue); O3      |
| 10 Dec 2026  | MS5 Results frozen; O4                                                  |
| 15 Dec 2026  | MS6 Final delivery, closing Increment 4 (Reviewed and reproducible); O5 |
| 15 Dec 2026  | Presentation materials (D6.3); presentation date per course schedule    |
| 27 Dec 2026  | Individual reflections                                                  |

## Data and Ethics Gate

Jurijs reports that, as the casino owner, he permits educational use of a dataset that he will anonymize, and that clauses 3.2, 3.7, and 11.1 of the casino's customer agreement allow use and transfer of gameplay information for Data Science purposes, including model training, at his discretion. He identifies Curaçao as the operator's jurisdiction; player, processing, and recipient locations have not been established. The clause text has not been supplied or independently reviewed. Before loading the full operator dataset, obtain and review the current agreement wording and document its applicability to the specific dataset, purpose, team, and transfer, plus any applicable course or ethics approval. Record the actual fields, de-identification method, permitted purpose, access list, storage location, retention, and deletion rule in the [data management plan](data_management_plan.md). Keep raw data and player-level outputs outside the public repositories. The team approves the label definition, consulting Jurijs as data owner and domain expert. Record whether any label is independently assessed (for example, staff reviews of players), what it means, who assigned it, when it became available, and which players were eligible for review. Unreviewed players are not assumed negative. If representative labels are absent, use only descriptive indicators, software scenarios, and the blind case review.

The team will document false-positive and false-negative costs, selection bias, temporal leakage, subgroup limitations, re-identification risk, and automation bias. A human specialist must interpret any review score. Nothing in this charter authorizes deployment against live players.

## Ways of Working and Change Control

- Work follows Data Driven Scrum. Each board item records its work package, owner, status, and Create, Observe, and Analyze evidence, and is Done only when its question, creation, observation, analysis, and conclusion have evidence links; the [iteration log](iteration_log.md) records iterations, reviews, retrospectives, and feedback.
- Keep meeting notes and decisions in [versioned repository files](meetings/README.md), with date, participants, evidence, decision, action owner, and follow-up item. Do not invent attendance or outcomes for meetings that have not happened.
- Track risks, owners, and triggers in the [risk register](risk_register.md) and review it weekly.
- Use pull requests for code and public documentation. A contributor and an independent reviewer should be different people. Tests, privacy review, and documentation readback precede merge.
- The Product Owner may reprioritize scope; any change to data use, target label, prediction time, or public claims requires a recorded team decision and an updated problem specification or evaluation protocol before analysis continues.
- If the data gate fails, the team will deliver the reproducible pipeline, rule-based scenario demo, and explicit feasibility report described in the proposal.

## Open Decisions

1. Review the current wording and applicability of clauses 3.2, 3.7, and 11.1 to the specific data, purpose, and team before the full export; record the de-identified event schema and handling and deletion decisions (MS1, [R01](risk_register.md)).
2. Decide whether independently assessed labels exist and freeze the outcome definition and holdout plan (MS2, [R02](risk_register.md)).
