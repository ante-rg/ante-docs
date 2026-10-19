# Ante Meeting on 2026-10-06

- **Status:** Draft
- **Time:** 20:45-21:30 (EEST)
- **Facilitator:** Jurijs
- **Note taker:** Daniils
- **Reviewers:** None yet
- **Present:** Jurijs, Daniils, Andrejs, Arturs, Volodymyr
- **Linked:** None

## Purpose

Review the de-identified transaction sample that Jurijs agreed to share at the [2026-09-29 meeting](2026-09-29-project-topic.md), then agree on the project's scope and the roles it needs.

## Observations

- The sample held transactions only. It had no indicators that could be used to label problematic behavior, such as self-exclusions, limit changes, or actions by responsible-gambling staff.
- Jurijs said such indicators can be retrieved and the sample extended, but the team must first agree on exactly what should be collected.
- While scope was being discussed, Andrejs suggested several modeling approaches based on neural networks that could suit the problem, and Volodymyr emphasized the product side: who would use the results and how they would reach them.
- Arturs noted that such a system could, in principle, help regulators: a standardized API that casino operators call to score their players for risk. This was raised as a possible wider use, not as a commitment.
- Daniils had prepared a shared template for the project proposal in Google Drive, and the team discussed what information would need to be filled into it.

## Decisions

- The aim is not to deliver a pre-trained open model for general-purpose use, but a documented process (framework) with an MVP demonstration.
  - **Why:** A model trained on one operator's data would not necessarily transfer to other operators, and publishing a model trained on player data raises privacy concerns. The alternative considered was the pre-trained general-purpose model.
  - **Follow-up:** Jurijs offered to prepare a project charter to formalize the scope and objectives (see Actions).
- For the MVP demonstration, a simple dashboard for responsible-gambling analysts will suffice.
  - **Why:** Analysts are the intended users of the scores, and a simple dashboard is enough to show the process working end to end.
- The project will follow Data Driven Scrum (DDS), as the supervisor recommended. Following DDS, the team identified the roles it needs: Product Owner, Process Expert, data scientists, a data engineer, a software developer, and an ML engineer.
  - **Why:** DDS is designed for data science work, where the next step depends on experiment results.
- The final split of roles between members was not agreed at this meeting.
  - **Follow-up:** Each member will say which roles they would like to take, and the team will agree the split afterward (see Actions).

## Actions

- [x] Prepare a project charter formalizing the project's scope and objectives - Jurijs - [project charter](../project_charter.md)
- [ ] Agree on the exact indicators and fields to request for the extended sample - team
- [ ] Extend the sample with the agreed indicators - Jurijs
- [x] Agree on the final role split - team - recorded in the [project charter](../project_charter.md#team-and-decision-rights)

## Risks and Feedback

- **No labels in the sample.** Without harm-related indicators, no outcome can be labeled or evaluated. This depends on the extended sample. Tracked as [R02 - No trustworthy harm proxy](../risk_register.md#r02---no-trustworthy-harm-proxy----16).
- **Data scope not yet fixed.** What the extended sample will contain depends on the team agreeing on what to request. Tracked as [R01 - No permitted player data](../risk_register.md#r01---no-permitted-player-data----15).
- **Supervisor feedback.** The supervisor recommended DDS as the project methodology, and the team adopted it.
