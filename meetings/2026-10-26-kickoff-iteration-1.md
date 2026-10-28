# Ante Meeting on 2026-10-26

- **Status:** Draft
- **Time:** 20:00-21:00 (EET)
- **Facilitator:** Daniils
- **Note taker:** Daniils
- **Reviewers:** None yet
- **Present:** Jurijs, Daniils, Andrejs, Arturs, Volodymyr
- **Linked:** None

## Purpose

Kick off the project after the proposal was submitted. With roles already assigned in the [project charter](../project_charter.md#team-and-decision-rights), the meeting had two goals: brief the team on the [methodology](../methodology.md) (the GitHub Project board, the repository structure, and the intended DDS process), and plan the work for the first iteration.

## Observations

- Daniils shared his screen and walked the team through each view of the GitHub Project board: Backlog, Item Breakdown, Task Board, and Work Packages. He explained that:
  - Backlog items hold hypotheses, questions, and user stories, which are refined into tasks following the Create - Observe - Analyze cycle.
  - All tasks planned for the current iteration can be viewed together.
  - The Work Packages view shows which items each work package contains. Each work package has an accountable lead, who is responsible for its results by the end of the project.
- Discussion of the initial hypotheses taken from prior studies:
  - Jurijs was concerned that these hypotheses may not fit the modeling approach, because it would be hard to show that a black-box model (such as a neural network) has learned a specific behavioral marker such as loss chasing.
  - Andrejs disagreed: the hypotheses are a useful starting point because they point to patterns that substantial literature says should already exist in the data, and they are the main source of features for training. Explainability is a separate question that depends heavily on the choice of model.
  - Arturs noted that these patterns do not need any modeling to be applied, and could be applied directly with basic heuristics and statistical analysis.
  - Daniils noted that the project must include a non-AI baseline in any case, and that a rule-based approach built on simple logic or statistics is exactly that baseline. Andrejs agreed that such a baseline is useful both for comparison and as a way to validate the hypotheses.
  - Arturs stressed that, methodologically, the team must find a way to validate whether either the rule-based or the AI-based solution is actually correct, and how the two can be compared at all.
- Discussion of the target feature:
  - Daniils pointed out that the current sample has no target feature, such as self-exclusion labels.
  - Jurijs said he had verified that self-exclusion data is available and can be extracted without issues.
  - Arturs reminded the team that self-exclusion is an unreliable proxy, and suggested a more unsupervised approach that identifies player behavior deviating substantially from normal (healthy) behavior.
  - Daniils asked whether other target features are available. Jurijs and Arturs both said that finding an objective label for harmful behavior is generally problematic.
  - Arturs noted that detecting that a player is experiencing problematic behavior now is a different problem from predicting it ahead of time. The hypotheses from existing papers may well be true, but whether they can be used for early prediction, which is what the project is interested in, is a separate question.
  - Daniils noted that the state of the art appears to focus mostly on assessing whether a player is currently experiencing problems, and that how early such predictions can be made remains an unaddressed research gap.
  - Arturs suggested framing the problem as a player having a window of normal behavior followed by a window leading to problematic behavior, where the task is to identify the transition between them as early as possible.
- Volodymyr shared wireframes for the MVP dashboard (an interactive prototype): a review queue, individual player cases (with an activity timeline and an explanation of why the player was flagged), and an operator breakdown showing player statistics across multiple operators.
- Discussion of the MVP's users and architecture:
  - Volodymyr asked who the end users would be, suggesting an analyst or inspector working for a regulator.
  - Arturs described the split: the backend (API) would be owned and provided by the regulator, while the frontend would be used by the casino. The backend should expose everything a casino needs to, in principle, build its own dashboard, so the team's dashboard is only a demonstration.
  - Volodymyr noted that this could be designed as an event-driven architecture, where the system consumes each event published by the casino to maintain its own database.
  - Andrejs agreed that the architecture should clearly separate backend and frontend responsibilities because their stakeholders differ, and that event sourcing could provide the necessary decoupling.
- Daniils noted that the [data management plan](../data_management_plan.md) is still a draft.

## Decisions

- The hypotheses from prior literature remain the basis for exploration and will be studied in more detail. Agreed by the team.
  - **Why:** They describe patterns that should already exist in the data, they are the main source of candidate features, and they also define the rule-based baseline. The concern that a black-box model cannot be shown to learn these specific markers was treated as a separate explainability question that depends on the model chosen.
  - **Follow-up:** Andrejs (H1-H3) and Daniils (H4-H5) will check whether the hypothesized relationships hold in the data (see Actions).
- The project needs a rule-based baseline. The specific rules will be derived only after initial exploration of the data and once the team has assessed which other fields can or should be added. Agreed by the team.
  - **Why:** A non-AI baseline is needed for comparison with machine-learning models and to validate the hypotheses. Fixing the rules before the data and fields are known would be premature.
  - **Follow-up:** Hypothesis exploration (Andrejs, Daniils) and dataset field assessment (Arturs), see Actions.
- No target feature was chosen. The team agreed that the label may be later derived based on behavioral markers described in the hypotheses, combined with self-exclusion.
  - **Why:** Self-exclusion can be extracted but is an unreliable proxy, and no objective label for harmful behavior has been identified.
  - **Follow-up:** Self-exclusion export (Jurijs) and dataset field assessment (Arturs), see Actions.
- The dashboard's end users are the casino's own staff, not regulators. Jurijs stated this as Product Owner, and Arturs supported it.
  - **Why:** In the intended setup, the regulator owns and provides the backend API, while each casino uses a frontend on top of it. The team's dashboard demonstrates what a casino could build. The alternative considered was an analyst or inspector working for a regulator.
  - **Follow-up:** Volodymyr will reflect this split in the system design and requirements (see Actions). An event-driven architecture and event sourcing were discussed but not decided.
- The next short meeting will be held on Thursday (2026-10-29), during or after classes.
  - **Why:** To check on progress early in the first iteration. Minor tasks, such as finishing the data management plan and cleaning up the backlog, should be done by then. No other due dates were set.

## Actions

- [ ] Review the linked research papers and hypotheses H1-H3, and report whether the relationships hold in our data and can be exploited - Andrejs
- [ ] Review the linked research papers and hypotheses H4-H5 and report whether the relationships hold in our data and can be exploited - Daniils
- [ ] Export the self-exclusion data and propose the initial data format for exploration - Jurijs - [ante-research#17](https://github.com/ante-rg/ante-research/issues/17)
- [ ] Assess the dataset's fields (whether they can be aggregated and whether other useful fields should be exported from the platform's database) and audit the data's overall quality - Arturs - [ante-research#16](https://github.com/ante-rg/ante-research/issues/16)
- [ ] Choose the technology stack for the application and create a preliminary design of its backend and frontend architecture - Volodymyr - [ante-app#8](https://github.com/ante-rg/ante-app/issues/8)
- [ ] Finish the [data management plan](../data_management_plan.md) - Jurijs (due 2026-10-29) - [ante-docs#5](https://github.com/ante-rg/ante-docs/issues/5)
- [x] Clean stale backlog items and prepare the tasks for the first iteration - Daniils (due 2026-10-29)
- [ ] Make it possible to see who is currently responsible for each task (for example, the reviewer) on the GitHub Project board - Daniils
- [x] Link each task to its corresponding documents in the repository - Daniils

## Risks and Feedback

- **No objective harm label.** Self-exclusion is available but unreliable, and no other objective label has been identified. Tracked as [R02 - No trustworthy harm proxy](../risk_register.md#r02---no-trustworthy-harm-proxy----16).
- **Validating and comparing approaches.** Without a trustworthy label, it is unclear how to show that either the rule baseline or a machine-learning model is correct, or how to compare them. Raised by Arturs. This affects freezing the evaluation protocol for MS2 and is tracked under [R02](../risk_register.md#r02---no-trustworthy-harm-proxy----16).
- **Current-state markers versus early signals.** The literature hypotheses may describe players who are already experiencing harm, rather than early signs that come before it, so they may not support predicting harm ahead of time. Raised by Arturs. Not yet in the [risk register](../risk_register.md).
- **Explainability of black-box models.** It may be hard to show that a model has learned specific behavioral markers, which affects the dashboard's "why flagged" explanations. Raised by Jurijs. Related to [R05 - Misleading interpretation](../risk_register.md#r05---misleading-interpretation----9).
- **Changed assumption about the system's owner.** The backend is now framed as a regulator-owned API consumed by casinos, rather than a tool owned by a single operator. This may need to be reflected in the [project charter](../project_charter.md) and [project plan](../project_plan.md).
- **Board organization feedback.** Members asked that the GitHub Project board show who is currently responsible for each task and that each task link to its documents. Daniils took this on (see Actions).
