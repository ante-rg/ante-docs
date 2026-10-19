# Ante Meeting on 2026-09-29

- **Status:** Draft
- **Time:** 20:45-21:30 (EEST)
- **Facilitator:** Jurijs
- **Note taker:** Daniils
- **Reviewers:** None yet
- **Present:** Jurijs, Daniils, Andrejs, Arturs, Volodymyr; project supervisor (end of meeting)
- **Linked:** None

## Purpose

Choose a project topic that interests all five members, and check the idea with the supervisor before committing to it. There was no pre-read material.

## Observations

- Jurijs works in the online casino industry and has access to a large amount of operator data. Arturs works on a platform connected to Jurijs's casino, so two members already know the domain.
- Nobody proposed another topic.
- Jurijs's first idea was to predict which players move between different casinos, based on their KYC data. The team saw two problems: confirmed (true-positive) cases of such players would be hard to obtain, and it was unclear whether the KYC data held the features needed to predict them.
- Predicting self-exclusions from historical player data was suggested next. Daniils and Andrejs asked what self-exclusion means: a player's own request to be blocked from gambling with an operator, for a set period or permanently. The team then discussed how unreliable self-exclusion is as a label. Points raised included:
  - Players may self-exclude for reasons unrelated to harm, such as taking a break.
  - Many players experiencing harm never self-exclude, or do so with another operator.
  - The exclusion date shows when a player acted, not when the harm began.
- Discussion moved to what data would show problematic patterns of play. Nobody outside Jurijs and Arturs knew what fields the operator records, so the team could not judge feasibility without seeing a sample.

## Decisions

- The project will work in the online casino domain, using data from Jurijs's operator. Jurijs proposed it, Arturs supported it, and Daniils, Andrejs, and Volodymyr agreed.
  - **Why:** Two members have domain knowledge and access to real data. No other topic was put forward.
  - **Follow-up:** Data sample from Jurijs (see Actions).
- The cross-casino player movement idea was dropped.
  - **Why:** Labels and features for it would be hard or impossible to obtain from one operator's data.
  - **Follow-up:** None.
- Rather than predicting self-exclusion alone, the working topic is detecting patterns of player behavior that lead to gambling harm, as support for responsible gambling. Arturs and Jurijs proposed this generalization, and Daniils, Volodymyr, and Andrejs agreed.
  - **Why:** The system would have clear social value.
  - **Follow-up:** Which label to use remains open; see Risks and Feedback.

## Actions

- [x] Share a de-identified sample of transaction data with the team - Jurijs - reviewed at the [2026-10-06 meeting](2026-10-06-scope-and-roles.md)
- [x] Review the sample and assess what can be done with it - team - see the [2026-10-06 meeting](2026-10-06-scope-and-roles.md)

## Risks and Feedback

- **Label reliability.** Self-exclusion, and possibly other available signals, may not reliably indicate harm. Raised by the team during the discussion. Tracked as [R02 - No trustworthy harm proxy](../risk_register.md#r02---no-trustworthy-harm-proxy----16).
- **Single data source.** The topic depends on one operator's data, provided through one member. Tracked as [R01 - No permitted player data](../risk_register.md#r01---no-permitted-player-data----15).
- **Supervisor feedback.** Before the meeting ended, the team presented the idea to the supervisor, who asked about the general steps the team plans to take and the novelty it is aiming for. The team suggested that the novelty may lie in the decisions made when training such models (which features are needed, how the data should be cleaned and transformed, which kinds of model suit the problem, and which metrics to evaluate), packaged as a reusable "framework" that other operators could apply to their own data.
