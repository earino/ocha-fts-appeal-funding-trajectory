<!-- dataset-factory:links -->
**Dataset Factory · v2026.11**

[Dataset website](https://earino.github.io/ocha-fts-appeal-funding-trajectory/versions/v2026.11/) · [GitHub release](https://github.com/earino/ocha-fts-appeal-funding-trajectory/releases/tag/v2026.11) · [Hugging Face](https://huggingface.co/datasets/earino/ocha-fts-appeal-funding-trajectory/tree/v2026.11) · [Catalogue](https://earino.github.io/dataset-factory-site/)

Artifact: 7bbc851418920071eea5e3abc17fad9812e107295e0354afbeefa953077832e1

### Suitability and evaluation requirements

Retained for retrospective model-development research and agent evaluation with the labeled eval split as development/validation data. Each row is one single-country UN-coordinated appeal-year with a positive launch-vintage original requirements figure; every feature is the appeal's own launch-record attribute, except years_since_country_prior, which reads only WHICH strictly-earlier same-country appeals exist (their years, never any outcome), is derivable from the shipped row set itself, and is asserted label-free by brute-force recompute at construction. The prediction instant is the appeal's public launch (event_time, requirements announcement), months before the plan year closes; the label (year-end funding >= 50% of original requirements) is resolved from the FTS flow endpoint's per-plan-year fundingTotal, which never ships. The 2026.10-era prior-outcome features that allowed exact cross-row label recovery (the 2026-11-01 queue audit recovered 120/139 eval and 128/182 holdout labels through count x rounded-rate arithmetic plus the last-prior tie rule) no longer ship in this version; rows are unchanged vs the audited e7441e1f and every reference reproduced to the last digit after the rebuild. The FTS/HPC API exposes no historical vintages (checked), so training-label timing and full-row historical availability are unverified and none is claimed: this is current-vintage retrospective research under a restricted isolated-rows protocol, never a certified historical-forecasting setup. Measured finding carried beside every figure: on the identical 139 eval rows the stock runner scores 0.6452 while the persistence reference (persistence_last_coverage, recomputed scorer-side from prior-in-time labels because its feature form is exactly the removed P0 channel) scores 0.7171136653895275 - the model trails persistence by 0.0719 and every other measured simple reference except the majority-class rate: no demonstrated headroom under this protocol for the stock runner. The comparison carries an inherent information asymmetry that must travel with the number: the model is deliberately denied the last prior same-country outcome under the operator's P0 standard while the persistence reference reads it scorer-side (train+eval labels only; the holdout is never opened). Any headroom claim requires beating persistence_last_coverage on the same rows.

**Supported uses:** Retrospective research and method comparison on the pinned 2026-10-29/30 harvest, predicting row-wise from the shipped launch-instant columns under an isolated-rows protocol; Agent evaluation with the labeled eval split as development/validation data and the holdout kept outside agent development until a design is frozen; Study of appeal-level, plan-type and country-level prevalence and of which launch attributes carry outcome signal; Persistence-vs-model comparison research, quoting both figures on the identical rows with the information-asymmetry note

**Not supported:** Operational or live launch-instant funding screening: no historical operational-availability evidence exists and none is claimed; Point-in-time historical reconstruction: the FTS/HPC API serves a current vintage only; a later re-fetch is a different vintage, not what was knowable at an earlier instant; Quoting the model AUC (0.6452) without the reference comparison (persistence 0.71711) and the information-asymmetry note beside it; Reading the model-vs-persistence gap as model failure against an equal information set: the persistence reference reads a value the model is deliberately denied; Any historical-forecasting certification: a full-row availability ledger and reviewed as-of evidence do not exist for this source

**Evaluation access:** isolated rows. The labeled eval split is development/validation data. Keep the final holdout outside agent development; prevent later rows from influencing earlier predictions.

**Historical availability:** unverified. **Training-label timing:** unverified. **Vintage:** current snapshot. **Selection:** prediction time.

**Cross-row audit:** bounded no recovery. fts-appeal-003 construction asserts (in-build, exit 0 proves them) that no shipped column reads any row's outcome, with years_since_country_prior brute-force-recomputed label-free; the gate 1.5.0 cross-row audit block records the removed prior-outcome join with its rationale (probes empty). The P0 channel itself was demonstrated only on the PRE-rebuild artifact by the 2026-11-01 queue audit; the required fresh label-blind re-attack of these exact bytes is still pending (see required_actions)

Structural qualification and baseline scores do not certify operational forecasting validity.

- The FTS/HPC API retains no historical vintages (checked at construction), so a reverse-history probe is not performable: retrospective research over the pinned 2026-10-29/30 harvest, never a certified historical forecasting setup
- Training-label timing is unverified: labels resolve from current-vintage funding totals, not from evidence of what was published at each past instant
- Small panel: 139 eval rows (81 positives) across 51 countries and four appeal years; the recorded finding's scope is these rows under this runner configuration
- Flow totals differ from the HDX CSV funding column on 37/758 rows (the disclosed count); flow and CSV agreed to the dollar on the retained fixtures and the cross-check runs on every row at construction within a 10% guard
- The persistence and prior-mean references are recomputed scorer-side from prior-in-time labels because their feature form is exactly the prior-outcome channel removed under the operator's P0 standard; the information asymmetry against the model is inherent to the leakage standard, not a defect of either measurement
- A fresh independent adversarial audit of THESE rebuilt bytes has not yet run: the 2026-11-01 queue audit's frozen attack code recovered labels on the pre-rebuild artifact and must be re-run label-blind to complete the record before any flip

**Corrections to the historical documentation:**

- 2026-11-01 independent queue audit (Codex, read-only): DO NOT PUBLISH the 12-column artifact e7441e1f - prior-outcome features recovered 120/139 eval and 128/182 holdout labels exactly. Remediation performed as the one rebuild for this defect class: fts-appeal-003 removed country_prior_appeals, country_prior_covered_rate and country_last_prior_covered, rows unchanged, every reference reproduced to the last digit, gate 1.5.0 clean, exact-byte accept on the worker. The superseded v2026.10-era staged artifacts (staging releases 430422823, 430443206) remain preserved as historical evidence and were never public
- 2026-11-03 re-audit condition 1 applied (PUBLISH WITH CONDITIONS): the grain is described as one FTS appeal-plan ID x plan year everywhere (quality.json id_columns_note, README, card, builder copy), with the measured country-year non-uniqueness recorded (41 repeated groups; e.g. Tanzania 2001-43 and 2001-73). Descriptor-only change: the three CSVs and meta.json are byte-identical to the audited v2026.11 bytes; re-qualified as 7bbc8514.

Review: 2026-11-03; applies to v2026.11 / `7bbc851418920071eea5e3abc17fad9812e107295e0354afbeefa953077832e1`. Frozen data and tags are unchanged.
<!-- /dataset-factory:links -->

# Data dictionary - ocha-fts-appeal-funding-trajectory

One row per plan-year appeal: a UN-coordinated single-country humanitarian plan
(HRP, CAP, flash appeal and similar) with a positive launch-vintage original
requirements figure, plan year 2000-2025. Population selection reads only the
appeal's own launch record; excluded groups (multi-country regional groups,
no-orig groups, the pre-2000 window and the 2026+ live edge) are counted in
`quality.json`'s exclusion buckets and never scored.

## Columns (9, shipped order)

| Column | Role | Meaning |
| --- | --- | --- |
| `plan_year_id` | id | Stable identifier for the plan-year appeal (`<planId>-<year>`); unique across the artifact; the runner's `id_columns`. |
| `plan_year_anchor` | feature | The anchor date the panel's temporal reasoning hangs off: the appeal's launch-instant anchor within its plan year (launch evidence: GHO launches early December for the following year; HRP launches end-December to early January; flash appeals launch at event onset). |
| `country_iso3` | feature | ISO3 code of the single country the appeal covers (primary population; multi-country regional groups are excluded and counted). High-cardinality by nature; declared in `quality.json`, not a leak - it reaches perfect AUC only by memorising one row per level. |
| `plan_year` | feature | The plan year the appeal covers. Also the artifact's `time_column`; the temporal split is keyed on it. |
| `plan_type` | feature | The plan's type as FTS records it (Humanitarian Response Plan, flash appeal, etc.). |
| `is_part_of_gho` | feature | Whether the plan-year is part of the Global Humanitarian Overview family, as the plan record states at harvest. |
| `orig_requirements_usd` | feature | ORIGINAL launch-vintage requirements in US dollars (`origRequirements` from the HPC plan endpoint). This is the denominator of the target's 0.5 fraction. Not the revised/current requirements: those are re-publications, unusable as launch features. |
| `years_since_country_prior` | feature | Appeal-recency: plan year minus the plan year of the country's most recent STRICTLY-EARLIER appeal; -1 when the country has no prior appeal. Reads only WHICH strictly-earlier same-country appeals exist (their years) - never any row's outcome - and is derivable by any reader from the shipped row set itself. Asserted label-free by brute-force recompute at construction. |
| `reached_half` | target | 1 when year-end funding >= 50% of original launch-vintage requirements ("covered"), else 0. `positive_label` is 1. Label source: the FTS flow endpoint's per-plan-year `incoming.fundingTotal`, cross-checked against the HDX bulk CSV's funding column on every row at construction; the funding value never ships in any split. |

## What is deliberately absent

- **No prior-outcome history.** The 2026.10-era `country_prior_appeals`,
  `country_prior_covered_rate` and `country_last_prior_covered` columns allowed
  exact cross-row label recovery (a later appeal's features contained a prior
  appeal's outcome) and were removed in the fts-appeal-003 rebuild. No shipped
  column reads any row's outcome.
- **No funding value ships.** The label numerator exists only in the label
  source, outside the CSVs.
- **No revised requirements.** Only launch-vintage `origRequirements` ships.

## Splits

| Split | Plan years | Rows | Positives | Positive rate | Distinct countries |
| --- | --- | ---: | ---: | ---: | ---: |
| train | 2000-2016 | 437 | 279 | 0.638444 | 78 |
| eval | 2017-2020 | 139 | 81 | 0.582734 | 51 |
| holdout | 2021-2025 | 182 | 96 | 0.527473 | 43 |

Temporal on `plan_year`; windows are disjoint. `plan_year_id` does not repeat
across splits (cross-split identifier check is part of the gate). Eval is
labeled development/validation; holdout is final scoring and stays outside
evaluated agents' workspaces until the design is frozen.

## Units and reference frame

Both operands of the target are US dollars from the same publisher in the same
vintage frame: year-end funding (flow `incoming.fundingTotal`) against 0.5 x
launch-vintage `origRequirements`. The 0.5 fraction is a task-defined policy
threshold fixed before construction, not data-derived. In-build fixtures pin the
unit and frame to exact dollar values (AFG 2023 orig 4,627,363,573 / funding
1,678,347,238 / label 0 with the CSV's revised 3,227,372,908 NOT the
denominator; YEM 2023 funding 1,774,327,599; Burundi RRP 2021 slice 14,978,233
of plan total 19,282,778), asserted on every build.
