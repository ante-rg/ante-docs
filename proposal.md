# Project proposal

Submitted 16 October 2026. Kept here for background; the specs in this folder take precedence for implementation details.

## Introduction & Main Problem

Licensed online casinos are expected to notice when a player's gambling is turning harmful and to step in early. Most operators still do this with a handful of fixed rules, such as a deposit total above a threshold. These rules fire late, usually after the losses, and flag many players who are not at risk. A regulator also has no simple way to check whether an operator's detection works. We will build a monitoring system for a national gambling regulator: licensed casinos send player game events to one API, and the system returns a risk score with reasons that a human reviewer can check.

## Background & Initial Research

Studies of real account data point to a fairly stable set of warning signs. LaBrie et al. (2008) and Braverman and Shaffer (2012) showed that high-risk online gamblers can be told apart early by how often they bet, how much their stakes vary and how fast their activity grows. Percy et al. (2016) trained supervised models to predict self-exclusion, and Auer and Griffiths (2023) predicted self-reported problem gambling from account data with machine learning. Commercial tools such as Playtech's BetBuddy and Mindway AI's GameScanner exist, but they are sold to operators and their models are closed.

Regulators now expect this kind of monitoring. The UK Gambling Commission (2022) requires remote operators to watch for indicators of harm and act on them, and in Latvia the IAUI keeps a national register of self-excluded persons (IAUI, n.d.).

What is missing is the regulator's view. Published models are usually trained on one operator's data and labelled with self-exclusion, which many harmed players never use, so it is unclear how they behave across operators. Our anonymised dataset covers 100 accounts from five operators, about 7.6 million events, which lets us test a model on an operator it has never seen.

## Objectives & Scope

**Objectives**

1. By 6 November 2026, build a reproducible pipeline that turns the raw events of all 100 accounts into session records and behavioural markers, define a proxy label for loss-chasing behaviour, and score a fixed-rule baseline against it.
2. By 27 November 2026, train a risk model and report precision and recall among the 20% highest-scored players for 7-, 14- and 30-day observation windows, using leave-one-operator-out cross-validation, against the fixed-rule baseline.
3. By 4 December 2026, deploy an API and a dashboard that score a replayed event stream, return each score with its top three reasons, and pass contract tests showing that API scores match the offline model.
4. By 10 December 2026, run a blind team review of 40 player cases drawn from the model's list and the rules' list, and present the result at the final review.

**In scope:** proxy labelling, behavioural markers, a gradient-boosted model with SHAP explanations, a REST API, a regulator dashboard, deployment with CI/CD, and an ethics and GDPR analysis.

**Out of scope:** real-time streaming, connection to real operators, clinical diagnosis, measuring the effect of interventions, support-chat text, and publishing raw data. The public repository holds code, aggregates and a synthetic sample only.

## Team Collaboration & Roles

- Daniils Buts, Product Owner: owns and orders the backlog, researches regulation and ethics, defines the label and builds the fixed-rule baseline.
- Andrejs Fjodorovs, Process Expert and lead data scientist: runs the Data Driven Scrum events, builds the model and the early-detection experiments.
- Arturs Greķe, data engineer: data pipeline, quality audit, feature tables and the synthetic dataset.
- Jurijs Kaminskis, data scientist: behavioural markers, explanations and evaluation.
- Volodymyr Stishkovskyi, developer and DevOps: Go API, React dashboard, deployment and CI/CD.

Day-to-day communication runs through a WhatsApp group. We hold short in-person syncs after lectures and a review every Thursday. Decisions and meeting notes are kept in the repository.

## Proposed Work Packages & Methodology

**WP1 Discovery and set-up (O1). Lead: Daniils.**
- Arturs checks the sample data, decides whether its fields are sufficient and defines the format of the full export ([issue](https://github.com/orgs/ante-rg/projects/1/views/1?pane=issue&itemId=271802481)).
- Daniils and Andrejs formulate the first testable hypothesis ([issue](https://github.com/orgs/ante-rg/projects/1/views/1?pane=issue&itemId=272041682)) and propose the model and a baseline method to compare it against ([issue](https://github.com/orgs/ante-rg/projects/1/views/1?pane=issue&itemId=271803513)).
- Daniils organises a meeting to fix the stages, deadlines and roles ([issue](https://github.com/orgs/ante-rg/projects/1/views/1?pane=issue&itemId=271803190)).
- Volodymyr compares hardware and infrastructure options for training and hosting ([issue](https://github.com/orgs/ante-rg/projects/1/views/1)).

**WP2 Markers and model (O2). Lead: Andrejs, Jurijs.** Build markers from the literature, such as repeated deposits within a session, deposit escalation, session length and night play. Train logistic regression and LightGBM, compare 7-, 14- and 30-day windows, and validate across operators.

**WP3 Explanations (O2, O3). Lead: Jurijs, Daniils.** Convert SHAP values into plain-language reasons and check that a reader without a data science background understands them.

**WP4 API and dashboard (O3). Lead: Volodymyr, with Arturs.** A REST API in Go (chi) receives event batches and returns a score, a risk band and reasons. The model runs as a Python scoring service that uses the same feature code as training. A React (Vite) dashboard shows the review queue, the player view and a per-operator summary. Docker, GitHub Actions and a team server provide deployment.

**WP5 Evaluation and demonstration (O4). Whole team, led by Daniils.** Run the blind review, write the model card and ethics section, and prepare the demonstration.

## Implementation Plan & Timeline

We use Data Driven Scrum (Saltz, Sutherland and Hotz, 2022) instead of fixed sprints, because data work is hard to time-box: a label question may take three days, a model experiment two weeks. Each DDS iteration answers one question and ends when the result is analysed, so iterations vary in length and can overlap. Every card states its question, what we build, what we measure and who interprets the result. The board has the columns Backlog, Create, Observe, Analyze and Done.

Iterations run from 19 October to 11 December 2026, with milestones on 6 November, 27 November, 4 December and 10 December (demonstration).

Project board and Gantt chart: [GitHub Projects](https://github.com/orgs/ante-rg/projects/1)
Risk register: [RISKS.md](https://github.com/ante-rg/ante-research/blob/main/RISKS.md)

The main risks are a weak proxy label, a small sample, a server outage before the viva (we keep a local Docker fallback) and differences between Python and Go scoring, which contract tests catch.

## References

Auer, M. and Griffiths, M.D. (2023) 'Using artificial intelligence algorithms to predict self-reported problem gambling with account-based player data in an online casino setting', *Journal of Gambling Studies*, 39, pp. 1273–1294.

Braverman, J. and Shaffer, H.J. (2012) 'How do gamblers start gambling: identifying behavioural markers for high-risk internet gambling', *European Journal of Public Health*, 22(2), pp. 273–278.

Gambling Commission (2022) *Customer interaction: formal guidance for remote gambling operators*. Birmingham: Gambling Commission.

IAUI (n.d.) *Register of self-excluded persons*. Riga: Lotteries and Gambling Supervisory Inspection of Latvia. Available at: https://www.iaui.gov.lv/en/register-self-excluded-persons (Accessed: 15 October 2026).

LaBrie, R.A., Kaplan, S.A., LaPlante, D.A., Nelson, S.E. and Shaffer, H.J. (2008) 'Inside the virtual casino: a prospective longitudinal study of actual Internet casino gambling', *European Journal of Public Health*, 18(4), pp. 410–416.

Percy, C., França, M., Dragičević, S. and d'Avila Garcez, A. (2016) 'Predicting online gambling self-exclusion: an analysis of the performance of supervised machine learning models', *International Gambling Studies*, 16(2), pp. 193–210.

Saltz, J., Sutherland, A. and Hotz, N. (2022) 'Achieving lean data science agility via Data Driven Scrum', *Proceedings of the 55th Hawaii International Conference on System Sciences (HICSS-55)*.
