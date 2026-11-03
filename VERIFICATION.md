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

# Verification record - ocha-fts-appeal-funding-trajectory v2026.11

Artifact `ac529cd4e9d4da90f804ecef425e74c94a946b857fe39095fd73a0407506b8c0`,
gate 1.5.0. What was verified, how, and what is **not** covered.

## Verified

| Check | Evidence |
| --- | --- |
| Qualification on the full artifact, on the worker | Job fts-appeal-003 (2026-11-02, cx23/hel1, 1396.6 s, exit 0): gate 1.5.0 `ok: true`, `failed_checks: []` over all 758 rows; contract checks 6/6. Report shipped as `qualification.json`. |
| Exact-byte acceptance on the worker | `--accept` ACCEPTED for `ac529cd4...` against the gate's own report (run.sh stage 3; nothing scored before it). |
| References reproduced after the rebuild | Job fts-appeal-003 stage 4, post-acceptance: every reference matches the pre-rebuild figures to the last digit - persistence 0.7171136653895275, prior-mean 0.7143465304384845, ask-size 0.7126436781609196, country-history 0.6729459344401874, plan-type 0.669220945083014, majority accuracy 0.5827338129496403, per-year persistence 0.73611 / 0.66579 / 0.74716 / 0.72727. Equality proves both the unchanged panel and the scorer-side recompute. |
| Rows unchanged by the remediation | train 437/279, eval 139/81, holdout 182/96 - identical to the audited e7441e1f artifact; the rebuild removed columns, not rows. |
| Download + checksums + re-accept | Job fts-baseline-002 (2026-11-02, 52.8 s, exit 0): the five accepted assets fetched from private staging release 431492902 with every sha256 verified on arrival, then gate `--accept` re-run on the fetched bytes BEFORE any score (accept.log: ACCEPTED, matches `ac529cd4e9d4da90`). |
| Runner-contract baseline on the released bytes | Same job: benchmark's own `train.py` + `validate.sh` unmodified (bundled sha256 equal the read-only clone's, recorded `unmodified: true`), `[validate] CONTRACT OK`, eval AUC **0.6452** from both the runner's own log and `validate.py`'s independent predict_proba recompute. Workdir materialized from public splits only; the holdout was never copied. Result: `measurements.json` and the candidate record. |
| In-build fixtures (units and frame) | Asserted on every build (exit 0 proves them): AFG 2023 orig 4,627,363,573 / funding 1,678,347,238 / label 0 (revised 3,227,372,908 NOT the denominator); YEM 2023 funding 1,774,327,599; Burundi RRP 2021 slice 14,978,233 of 19,282,778; flow-vs-CSV within the 10% guard, 37/758 disclosed differences. |
| Label provenance | Every label recomputed independently in the 2026-11-01 audit from the staged compact source caches: 0/758 label discrepancies, 0 original-requirement discrepancies, 0 country discrepancies. |
| Licence instruments | FTS use-and-republish terms and the HDX record's CC BY-IGO, both read 2026-10-29 and quoted in the candidate record's license_evidence; attribution carried in `LICENSE.md`. Class A (explicit permission for redistribution and derivatives with attribution). |
| Worker cleanup | Both workers collected then destroyed with provider 404 read-backs (fts-appeal-003: server 174163321; fts-baseline-002: server 174177604; project server list empty). |

## The finding, stated with its qualifier

The stock runner's full model scores **0.6452** eval AUC; the persistence
reference (`persistence_last_coverage`, scorer-side recompute from prior-in-time
labels, train+eval only) scores **0.7171136653895275** on the identical 139 eval
rows. The model trails persistence by 0.0719 and every other measured reference
except the majority-class rate: **no demonstrated headroom under this protocol
for the stock runner**. The information-asymmetry note travels with the number:
the model is deliberately denied the last prior same-country outcome (the P0
recovery channel), while the persistence reference reads it scorer-side. An
observed result on these rows with this configuration - not a bound on other
models, not an operational-validity claim.

## NOT covered

- **No historical-vintage reconstruction.** The FTS API exposes no historical
  vintages (checked); which values were visible at each past instant cannot be
  re-established, and no as-of claim is made. The panel is current-vintage
  retrospective research data under a restricted-protocol declaration
  (`quality.json` `evaluation_contract`, access `isolated_rows`).
- **No full independent API re-harvest.** The audit's label recompute used the
  staged compact source caches, not fresh API responses; the original raw API
  response bodies were not retained by the builder. Rebuilding today fetches
  the current vintage and may differ from the shipped bytes if the publisher's
  data has moved.
- **No holdout evaluation.** The holdout was fetched for exact-byte acceptance
  but never scored, never copied into a workdir, and stays sealed until the
  design is frozen.
- **No agent/harness comparison.** The baseline is the runner contract only; no
  claim is made about coding-agent performance.
- **A fresh independent pre-flip audit of these rebuilt bytes** is required
  before any public flip: the 2026-11-01 audit's frozen attack code recovered
  labels on the PREVIOUS artifact; it must be re-run label-blind against these
  bytes and find no operand columns. That audit has not yet been executed for
  this version.
