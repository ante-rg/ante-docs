# Ante Risk Register

This register supports the [project plan](project_plan.md). Update it whenever a risk, trigger, score, or response changes.

- **Register Owner:** Jurijs
- **Last Updated:** 2026-10-20
- **Review Frequency:** Weekly; at each iteration review

## Scoring Key

| Score | Rating    | Action                            |
| ----- | --------- | --------------------------------- |
| 1-6   | 🟢 Low    | Monitor                           |
| 8-12  | 🟡 Medium | Actively manage                   |
| 15-25 | 🔴 High   | Escalate at the next team meeting |

Score = Likelihood (1-5) × Impact (1-5)

## Summary

| ID  | Risk                              |  L  |  I  | Score | Status | Owner     |
| --- | --------------------------------- | :-: | :-: | :---: | ------ | --------- |
| R01 | No permitted player data          |  3  |  5  | 🔴 15 | Open   | Jurijs    |
| R02 | No trustworthy harm proxy         |  4  |  4  | 🔴 16 | Open   | Daniils   |
| R03 | Future leakage                    |  3  |  4  | 🟡 12 | Open   | Andrejs   |
| R04 | Privacy exposure                  |  2  |  5  | 🟡 10 | Open   | Arturs    |
| R05 | Misleading interpretation         |  3  |  3  | 🟡 9  | Open   | Andrejs   |
| R06 | Schedule or contribution gaps     |  3  |  3  | 🟡 9  | Open   | Jurijs    |
| R07 | Data owner's conflict of interest |  2  |  4  | 🟡 8  | Open   | Daniils   |
| R08 | Automated decisions about players |  1  |  4  | 🟢 4  | Open   | Volodymyr |
| R09 | Scores used for other purposes    |  2  |  4  | 🟡 8  | Open   | Daniils   |

## Risks

### R01 - No permitted player data - 🔴 15

**Category:** Data access · **Owner:** Jurijs · **Status:** Open · **Likelihood:** 3 · **Impact:** 5

The team may not obtain written, applicable permission to use operator player data, leaving no real dataset for analysis.

**Mitigation:**

- [ ] Obtain current wording of customer agreement clauses 3.2, 3.7, and 11.1 (due 2026-10-30)
- [ ] Document applicability to the specific dataset, purpose, team, and transfer (due 2026-10-30)
- [ ] Record fields, pseudonymization method, access list, storage, retention, and deletion rule
- [ ] Keep the synthetic-data route ready as the fallback deliverable; do not claim external validation

**Trigger:** No written permission or usable public dictionary by the 30 Oct data and label decision.
**Residual score (after mitigation):** L1 × I5 = 5 🟢

### R02 - No trustworthy harm proxy - 🔴 16

**Category:** Evaluation · **Owner:** Daniils · **Status:** Open · **Likelihood:** 4 · **Impact:** 4

Available labels may not reliably indicate gambling harm, so predictive performance cannot be measured meaningfully.

**Mitigation:**

- [ ] Record whether any label is independently assessed, what it means, who assigned it, and when (due 2026-10-30)
- [ ] Decide the source of harm-event labels (due 2026-10-30, MS1)
- [ ] Draft the outcome definition right after MS1 and freeze it with the evaluation protocol (due 2026-11-06, D4.1)
- [ ] Document selection and uncertainty
- [ ] If representative labels are absent, limit results to rules/feature feasibility and software scenarios

**Trigger:** Labels absent, self-selected, or inconsistently assessed.
**Residual score (after mitigation):** L4 × I2 = 8 🟡

### R03 - Future leakage - 🟡 12

**Category:** Technical · **Owner:** Andrejs · **Status:** Open · **Likelihood:** 3 · **Impact:** 4

Information unavailable at prediction time may leak into features or evaluation, inflating reported performance.

**Mitigation:**

- [ ] Enforce as-of cutoffs in the pipeline and evaluate only on held-out players
- [ ] Review source lineage and the holdout protocol

**Trigger:** Feature after cutoff, label unavailable at evaluation time, or shared train/test players.

### R04 - Privacy exposure - 🟡 10

**Category:** Privacy · **Owner:** Arturs · **Status:** Open · **Likelihood:** 2 · **Impact:** 5

Player-level information could become identifiable through public artifacts, outputs, or repositories.

**Mitigation:**

- [ ] Keep player-level rows, scores, and models in ignored, access-controlled storage
- [ ] Aggregate and disclosure-check all outputs before publishing

**Trigger:** Public record, ID, rare trajectory, or individual score.

### R05 - Misleading interpretation - 🟡 9

**Category:** Communication · **Owner:** Andrejs · **Status:** Open · **Likelihood:** 3 · **Impact:** 3

Review scores may be presented or read as clinical diagnosis or proven harm reduction.

**Mitigation:**

- [ ] Use human-review framing and measured proxy language
- [ ] Hold a critical review of claims before presentation

**Trigger:** Score described as diagnosis, loss, or measured harm reduction.

### R06 - Schedule or contribution gaps - 🟡 9

**Category:** Process · **Owner:** Jurijs · **Status:** Open · **Likelihood:** 3 · **Impact:** 3

Work may slip or individual contributions may go unrecorded, weakening milestones and assessment evidence.

**Mitigation:**

- [ ] Record weekly decisions and link contributions to board cards
- [ ] Revise scope early when milestones are at risk

**Trigger:** Cards without owners, evidence, or review.

### R07 - Data owner's conflict of interest - 🟡 8

**Category:** Ethics · **Owner:** Daniils · **Status:** Open · **Likelihood:** 2 · **Impact:** 4

Jurijs owns the operator that supplies the data and also leads data governance and the rule baseline, so the extract, the label, or the reporting of results could be shaped by the operator's interests, even unintentionally.

**Mitigation:**

- [ ] Approve the outcome label and evaluation protocol as a team, not by the data owner alone
- [ ] Freeze the evaluation protocol before any model is trained (MS2)
- [ ] Record how each extract was selected and who chose it
- [ ] Report every pre-registered result, whatever it shows

**Trigger:** Extract, label, or reported results changed at the data owner's request without a recorded team decision.

### R08 - Automated decisions about players - 🟢 4

**Category:** Ethics · **Owner:** Volodymyr · **Status:** Open · **Likelihood:** 1 · **Impact:** 4

A score could be used to act on a player without a staff decision, such as an automatic limit or account action, which the GDPR restricts (Art. 22).

**Mitigation:**

- [ ] Use scores only to rank players for staff review, each with its top three reasons
- [ ] Keep interventions and account actions out of the API and dashboard

**Trigger:** A feature, endpoint, or claim that acts on a player without a staff decision.

### R09 - Scores used for other purposes - 🟡 8

**Category:** Ethics · **Owner:** Daniils · **Status:** Open · **Likelihood:** 2 · **Impact:** 4

Scores, features, or the pipeline could be reused for purposes other than harm prevention, such as marketing.

**Mitigation:**

- [ ] Record harm prevention as the only permitted purpose in the data management plan
- [ ] Warn against other uses in the model card (D6.1)

**Trigger:** A request or proposal to use scores, features, or outputs outside harm prevention.

## Closed Risks

| ID  | Risk     | Closed | Outcome |
| --- | -------- | ------ | ------- |
| -   | None yet | -      | -       |
