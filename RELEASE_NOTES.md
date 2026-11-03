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

# Release notes - v2026.11

## ocha-fts-appeal-funding-trajectory (first versioned package)

Humanitarian-appeal funding-trajectory prediction: for a single-country
UN-coordinated appeal at its public launch instant, will it receive at least 50%
of its ORIGINAL launch-vintage requirements by the close of its plan year?
Built from OCHA's Financial Tracking Service (HPC API + HDX bulk CSV).
758 rows: train 2000-2016 (437/279), eval 2017-2020 (139/81), holdout 2021-2025
(182/96).

## What is in this version

- The rebuilt 9-column artifact `ac529cd4e9d4da90...` (gate 1.5.0, failed
  checks empty, exact-byte `--accept` on the worker, re-accepted after download
  in the baseline job).
- The P0 remediation: the 2026-11-01 independent queue audit recovered 120/139
  eval and 128/182 holdout labels exactly through the shipped prior-outcome
  features (`country_prior_appeals`, `country_prior_covered_rate`,
  `country_last_prior_covered`). Those columns no longer ship. Rows are
  unchanged vs the audited artifact; every remaining feature is a function of
  the row's own launch record, except `years_since_country_prior`, which reads
  only prior appeal YEARS and is asserted label-free at construction.
- The measured comparison on the identical 139 eval rows: stock runner
  **0.6452** vs persistence **0.7171** (and prior-mean 0.7143, ask-size 0.7126,
  country-history 0.6729, plan-type 0.6692, majority accuracy 0.5827). The
  model trails persistence by 0.0719 AUC: **no demonstrated headroom under this
  protocol for the stock runner**, recorded as a defect beside the number, with
  the information-asymmetry note (the model is deliberately denied the last
  prior same-country outcome under the P0 standard; the persistence reference
  reads it scorer-side from prior-in-time labels). A solver must beat
  `persistence_last_coverage` for any headroom claim.
- Licence: MIT (our code/docs), CC0-1.0 (our compilation contribution), source
  terms preserved (FTS use-and-republish + CC BY-IGO on the HDX bulk input) with
  attribution carried; see `LICENSE.md`.

## Known limitations (disclosed, not hidden)

- **Current-vintage retrospective.** The FTS API exposes no historical vintages,
  so no as-of reconstruction is claimed; `quality.json`'s `evaluation_contract`
  declares `isolated_rows` access and a restricted retrospective-research scope.
  Labeled eval is development/validation; the holdout is final scoring and was
  never evaluated in this package's preparation.
- **Flow totals vs the CSV.** 37/758 rows differ between the flow endpoint's
  year total and the HDX CSV's funding column (the disclosed count); flow and
  CSV agreed to the dollar on the retained fixtures, and the cross-check runs
  on every row at construction with a 10% guard.
- **Small panel.** 139 eval rows (81 positives) across 51 countries; four eval
  years. Intervals are not the point of the headline number - the comparison
  and its scope are recorded beside it.
- **Predecessor note.** The same runner measured 0.6298 on the pre-rebuild
  12-column artifact; removing the leaky features slightly improved the model
  while closing the recovery channel.

## Provenance

Construction commit, input digests, worker job IDs, the gate report and the
baseline evidence are recorded in `MANIFEST.json` and `VERIFICATION.md`. The
holdout ships as a release asset like the other splits; during evaluation runs
it stays outside the evaluated agent's workspace.
