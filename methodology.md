# Ante Methodology

This document describes how the Ante team plans, tracks, and carries out its work. It covers the development process, how that process maps onto our GitHub Project, and the research practices that keep our results honest and reproducible.

- **Owner:** Daniils (Process Expert)
- **Last Updated:** 2026-10-19
- **Update Frequency:** When the process changes, usually after a retrospective

## Data Driven Scrum

The project follows **Data Driven Scrum (DDS)**, an agile framework designed for data science teams by Jeff Saltz and Alex Sutherland. Our reference for the framework is [Data Driven Scrum](https://www.datascience-pm.com/data-driven-scrum/) on the Data Science PM website. Where this document and the reference disagree, this document describes what the team actually does.

DDS was created because plain Scrum and Kanban fit data science poorly. In data science, it is hard to predict how long an experiment will take, and an experiment's results often change what should be done next. DDS keeps the parts of Scrum that help a team work together (roles, small iterations, reviews, retrospectives) and adds the visual flow and work-in-progress limits of Kanban. It drops fixed-length sprints and detailed time estimates.

### Principles

1. **Agility comes from iterative experimentation.** Progress is made by repeatedly trying something, looking at the result, and adapting.
2. **Every iteration is an experiment cycle.** An iteration starts with an idea, builds something to test it, observes the result, and analyzes what was observed. The analysis feeds the next idea.
3. **Iterations end when the cycle is complete, not when time runs out.** An iteration is capability-based: it is the smallest useful piece of work that tests an idea, however long that takes.

### Roles

| Role            | Who      | Responsibilities                                                                                                     |
| --------------- | -------- | -------------------------------------------------------------------------------------------------------------------  |
| Product Owner   | Jurijs   | Voice of the client. Owns and prioritizes the backlog, decides what to work on next, and confirms that work is done. |
| Process Expert  | Daniils  | Coaches the team in DDS, facilitates events, and removes impediments.                                                |
| Team Members    | Everyone | Self-organize to deliver the backlog items, contribute hands-on work, and take part in analysis.                     |

Each member also has a technical role and a lead work package, listed in the [project charter](project_charter.md).

### Artifacts

- **Item.** A unit of work on the backlog, such as a question to answer, a hypothesis to test, a user story, or other goals. See [Item Types](#item-types).
- **Task.** A concrete, assignable step of an item, created during refinement. Tasks belong to DDS phases (Create, Observe, Analyze) and specify definition of done.
- **Backlog.** The prioritized list of items, owned by the Product Owner and continuously refined by the team.
- **Item Breakdown Board.** Each item is broken down into tasks during refinement. Every item needs at least one **Create**, one **Observe**, and one **Analyze** task.
- **Task Board.** Shows the tasks currently being worked on, moving through Backlog, Refining, Ready, In Progress, and Done statuses.

### The Create - Observe - Analyze Cycle

Every item moves through three kinds of tasks:

1. **Create** - build or run the artifact: a dataset, a feature, a model, a report, an API endpoint.
2. **Observe** - measure the artifact: compute the metrics, run the tests, collect the outputs.
3. **Analyze** - interpret the observations as a team and decide what follows. For a hypothesis, this means comparing the observations against its decision rule and recording the outcome.

Analysis is shared by the whole team. It is not left only to the Product Owner.

### Activities and Events

- **Backlog refinement.** The team helps the Product Owner clarify, split, and estimate items. Each item gets a relative estimate of its **value**, **effort**, and **probability of success**. Estimates guide prioritization; they do not fix the scope or the length of an iteration. DDS suggests that team members spend roughly 5-10% of their capacity on refinement.
- **Backlog prioritization.** The Product Owner orders the backlog using these estimates and input from the team and the supervisor.
- **Backlog item selection.** When the team has capacity for a new iteration, it selects the next items from the top of the backlog. Finishing iterations already in progress takes priority over starting new ones.
- **Daily check-in.** A short sync on progress, plans, and blockers.
- **Iteration review.** Held weekly, scheduled by the Product Owner. The team presents results and analysis, the Product Owner and, when available, the supervisor give feedback, and backlog priorities are revisited.
- **Retrospective.** Held at the end of each Product Increment. The team reviews what is and is not working in the process and commits to a small number of improvements.

Unlike Scrum, reviews and retrospectives are **not tied to the end of an iteration**. Reviews run weekly and retrospectives at the end of each increment, and each one covers whichever iterations finished or progressed since the last. Iterations may also **overlap**: if an Observe step has to wait (for example, for a data export), the team can start another iteration in the meantime.

### Iterations and Product Increments

An **iteration** contains one or more items and runs through creation, observation, and analysis. It should be as small as possible while still producing a useful answer. It can be as short as a day, and generally should not exceed a month.

A **Product Increment** is a higher-level goal reached through several iterations over a fixed period. Our four increments, the milestones that close them, and the objectives each one delivers are defined in the [project plan](project_plan.md). Increments help us order iterations and set what each milestone should show; iterations within them remain capability-based.

### Work-In-Progress Limits

Following Kanban, the team limits how much work is in progress at once. Starting fewer things and finishing them keeps work flowing and makes blockers visible early. As a rule of thumb, a person should not hold more than one or two In Progress tasks at a time, and new items should not be pulled in while selected ones are stalled.

## Our GitHub Project

All work is tracked in the [Ante GitHub Project](https://github.com/orgs/ante-rg/projects/1). Issues may live in any of the organization's repositories (`ante-docs`, `ante-research`, `ante-app`) and are added to the project automatically by the issue templates.

### Items and Tasks

The project uses two GitHub issue types:

- **Item** - a backlog item in the DDS sense: a hypothesis, question, user story, or general goal.
- **Task** - a concrete unit of work. A task is normally a **sub-issue** of an item and has its **Phase** set to Create, Observe, or Analyze. A task can also be a standalone action without a parent.

### Fields

| Field                          | Applies to   | Meaning                                                                                                 |
| ------------------------------ | ------------ | ------------------------------------------------------------------------------------------------------- |
| Status                         | Items, Tasks | Where the work is in the flow: Backlog, Refining, Ready, In Progress, Done.                             |
| Value / Effort / Probability   | Items        | Relative refinement estimates on a five-point scale, from very low to very high.                        |
| Work Package                   | Items, Tasks | The work package (WP1-WP6) from the [project plan](project_plan.md) the work belongs to.                |
| Iteration                      | Items, Tasks | The DDS iteration the work was selected into.                                                           |
| Phase                          | Tasks        | Create, Observe, or Analyze.                                                                            |
| Outcome                        | Items        | For hypotheses: Supported, Rejected, or Inconclusive, as decided by the pre-registered decision rule.   |
| Start date / Target date       | Items, Tasks | Optional, used for work with external deadlines.                                                        |

### Views

| View                | Purpose                                                                                                                                         |
| ------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------- |
| **Backlog**         | All open items with their estimates and iteration. Used for refinement, prioritization, and item selection.                                     |
| **Item Breakdown**  | Tasks grouped by parent item and sorted by phase. Our Item Breakdown Board: shows whether each item has its Create, Observe, and Analyze tasks. |
| **Task Board**      | Board of tasks by status, grouped by parent item. Our Task Board, used day to day and in check-ins.                                             |
| **Work Packages**   | Items grouped by work package, with status, iteration, and outcome. Used to track progress against the plan.                                    |

### Flow

1. **Backlog.** Anyone can create an item using one of the templates. New items start in Backlog.
2. **Refining.** The team clarifies the item, fills in its estimates, and breaks it down into Create, Observe, and Analyze tasks as sub-issues. For a hypothesis, the decision rule is written in full here.
3. **Ready.** The item is clear enough to start (see [Definition of Ready](#definition-of-ready)). For a hypothesis, **the decision rule is locked from this point**.
4. **In Progress.** The item has been selected into an iteration (set the **Iteration** field) and its tasks are being worked on through the Task Board.
5. **Done.** All tasks are complete, the evidence is linked, and the Product Owner has confirmed the result (see [Definition of Done](#definition-of-done)).

When an iteration ends, its outcome, decisions, and follow-up items are recorded in the [iteration log](iteration_log.md). Reviews and retrospectives get their own notes in [meetings](meetings/README.md).

### Definition of Ready

An item can move to Ready when:

- Its goal, question, claim, or story is clear and agreed by the team.
- Value, effort, and probability (for exploratory or experimental work) are estimated.
- It has at least one Create, one Observe, and one Analyze task, each with a clear "done when".
- Blockers and dependencies are listed and linked as GitHub issue dependencies.
- For hypotheses: the decision rule states the metric, baseline, data and split, statistic, and the supported, rejected, and inconclusive conditions with the next step for each.
- For user stories: acceptance criteria are written.

### Definition of Done

An item can move to Done when:

- All its tasks are Done, each with linked evidence (a PR, notebook, report, or comment).
- Code went through a pull request reviewed by someone other than its author.
- For hypotheses: the **Outcome** field is set, and a comment on the issue explains how the observations meet the decision rule.
- For user stories: all acceptance criteria are checked.
- Results, limitations, and follow-up items are recorded in the [iteration log](iteration_log.md).
- The Product Owner has confirmed the result.

## Item Types

Each item type has a template in the organization's [`.github`](https://github.com/ante-rg/.github) repository.

| Type           | Title convention          | Use it for                                                                                   | Key fields                                         |
| -------------- | ------------------------- | -------------------------------------------------------------------------------------------- | -------------------------------------------------- |
| **Hypothesis** | `H<n>: <one-line claim>`  | A testable claim that we expect to accept or reject.                                         | Hypothesis, references, decision rule, blockers    |
| **Question**   | Plain question            | Open exploration without a claim to accept or reject.                                        | Question, done when, blockers                      |
| **User Story** | `US<n>: <short name>`     | A capability for a user of the application, such as an analyst using the dashboard.          | Story, acceptance criteria, blockers               |
| **General**    | Plain title               | Any other goal, such as an administrative or data engineering deliverable.                   | Goal, done when, blockers                          |
| **Task**       | Imperative phrase         | A concrete step of an item (a sub-issue with a Phase) or a standalone action.                | Goal, done when                                    |

**Hypotheses** follow the form "We believe that [claim], because [reasoning]", and are backed by references to literature or domain expertise. They are confirmatory: the decision rule says in advance what result would support or reject the claim.

**Questions** are exploratory. They are used when we do not yet know enough to state a claim, for example to check which data fields are usable. Findings from questions often lead to new hypotheses, but a question should never be turned into a confirmed claim after the fact.

**User stories** follow the form "As a [role], I want [capability], so that [benefit]". Their Create, Observe, and Analyze tasks are usually building the feature, testing or demonstrating it, and reviewing it against the acceptance criteria and review feedback.

## Research Practices

The following practices apply to all analytical and modeling work. They exist so that our results can be trusted, checked, and reproduced by someone outside the team.

### Pre-Registration and Avoiding P-Hacking

- **Decision rules are locked once a hypothesis is Ready.** The metric, baseline, data, split, statistic, and thresholds are fixed before any result is seen. This prevents us, consciously or not, from moving the goalposts until a result looks good.
- **Changes need a justification on record.** If a rule must change after it is locked (for example, a field turns out to be unusable), post a comment on the issue explaining what changed and why, before running the affected analysis.
- **Every outcome is reported.** Rejected and inconclusive results are recorded just like supported ones. We do not drop hypotheses that did not work out.
- **Exploratory and confirmatory work stay separate.** Patterns found while exploring (in questions, or by looking at data beyond a hypothesis's scope) are reported as exploratory and, if worth pursuing, become new hypotheses tested on data they were not found on.
- **Multiple testing is acknowledged.** We test many hypotheses on the same data. When reporting, state how many were tested, and apply a correction (such as Holm or Benjamini-Hochberg) or clearly mark results as exploratory.

### Leakage Prevention

- Features may only use information that was available at the moment the prediction would have been made.
- Preprocessing steps that learn from data (scaling, encoding, imputation, feature selection) are fit on the training split only.
- Hypothesis tests on individual markers describe the data; they do not choose model features or set rule thresholds. Any feature selection that looks at outcome labels uses the training folds only, so a test fold never influences which features a model uses.
- Labels and anything derived from them after the prediction time must never enter features.
- Leakage checks are part of the pull request review for any feature or pipeline change.

### Reproducibility

- **Seeds are fixed and recorded.** Every source of randomness (splits, sampling, model initialization, hyperparameter search) uses an explicit seed that is saved with the results. For stochastic models, report results over several seeds rather than the single best run.
- **Environments are pinned.** Dependencies are pinned with exact versions in a lock file committed to the repository.
- **Data is versioned.** Each dataset used in an analysis is identified by its source, version or export date, and checksum, as described in the [data management plan](data_management_plan.md). Raw data is never modified in place.
- **Results are traceable.** Every reported result can be traced back to the code commit, data version, configuration, and seed that produced it. Record these alongside the results.
- **Notebooks run top to bottom.** A notebook used as evidence must run cleanly from a fresh kernel. Code reused across notebooks is moved into a shared module and tested.

### Code and Review

- All code and public documentation changes go through pull requests, reviewed by someone other than the author.
- Pull requests link the task they complete, so the evidence trail from item to code is kept.
- Tests, privacy checks, and documentation readback happen before merge.

### Data Protection and Responsible Claims

- Raw data and player-level outputs never go into public repositories, issues, pull requests, or meeting notes. Only aggregated, public-safe results are shared.
- Every empirical claim states its dataset, population, outcome proxy, observation window, and limitations.
- Scores are presented as aids to human review, not as diagnoses or proof of reduced harm.
