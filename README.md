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

# ocha-fts-appeal-funding-trajectory

Humanitarian-appeal funding-trajectory prediction task, built from OCHA's
Financial Tracking Service (FTS). Derived research dataset - **not** an OCHA or
FTS product.

## The prediction question

For a UN-coordinated humanitarian appeal or response plan (single-country HRP,
CAP, flash appeal and similar) at its **public launch instant** - requirements
first published, at or before the plan year starts - will the plan receive
funding equal to at least **50% of its ORIGINAL launch-vintage requirements** by
the close of its plan year?

A useful prediction identifies, months ahead, which appeals will end the year
underfunded - the quantity FTS/GHO gap analysis reports after the fact - which
is what donor advocacy and fundraising prioritization need.

- **Prediction instant:** the appeal's launch (event time; requirements
  announcement). Every feature is a launch-time attribute. Nothing that happens
  after launch ships.
- **Target:** `reached_half` = 1 when year-end funding >= 0.5 x original
  requirements (both US dollars from the same publisher; the threshold is a
  task-defined policy fraction fixed before construction, not data-derived).
- **Label source:** the FTS flow endpoint's per-plan-year `incoming.fundingTotal`
  - never shipped in any split. The HDX bulk CSV's funding column cross-checks
  it on every row at construction.
- **Splits (temporal on the plan year):** train 2000-2016 (437 rows, 279
  positive), eval 2017-2020 (139 rows, 81 positive), holdout 2021-2025 (182 rows,
  96 positive). The 2026+ live edge is excluded until those years close;
  exclusions are counted in their own buckets, never scored as negatives.
- **Id:** `plan_year_id` (one row per appeal-plan ID × plan year). (country, plan year) is **not** unique — 41 country-year groups carry more than one appeal (e.g. Tanzania 2001-43 and 2001-73).

## Files

| Path | What |
| --- | --- |
| `public/train.csv`, `public/eval.csv` | public splits (feature columns + target) |
| `private/holdout.csv` | final-scoring split; ships as an asset, never enters a runner workdir during development |
| `meta.json`, `quality.json` | runner task metadata and the full qualification declaration (timing, evaluation contract, split windows, exclusions) |
| `code/` | construction script (`build.py`), worker run order (`run.sh`), references implementation (`score.py`), workdir materializer (`materialize.py`), the qualification gate (`qualify_dataset.py`) |
| `baseline/` | the benchmark's own runner files, verbatim, plus the reproduce script |
| `get_dataset.py` | downloads the five release assets, verifies every size and sha256, restores the runner layout |
| `measurements.json` | the measured panel, references, baseline result and the finding beside it |
| `MANIFEST.json`, `SHA256SUMS` | every file's identity: sizes, digests, licences, qualification, baseline |

## Quick start

```bash
python3 get_dataset.py --dest ./task          # download + verify + lay out
python3 code/qualify_dataset.py ./task        # re-run the qualification gate
sh baseline/reproduce_baseline.sh ./task      # runner-contract baseline
```

See `REPRODUCE.md` for the full reproduction path, `DATA_DICTIONARY.md` for
every column's documented meaning, and `VERIFICATION.md` for what was verified
and what is not covered.

## The finding that qualifies every number

On the identical 139 eval rows: the stock runner's full model scores **0.6452**
AUC; the persistence reference (`persistence_last_coverage`, recomputed
scorer-side from prior-in-time labels) scores **0.7171**. The model trails
persistence by 0.0719 - recorded as **no demonstrated headroom under this
protocol for the stock runner**, with the information-asymmetry note (the model
is deliberately denied the last prior same-country outcome under the operator's
P0 leakage standard, while the persistence reference reads it scorer-side)
beside every quoted figure. A solver must beat `persistence_last_coverage` for
any headroom claim on this task. Full comparison in `measurements.json` and
`baseline/README.md`.

## Leakage posture

The 2026.10-era prior-outcome features (`country_prior_appeals`,
`country_prior_covered_rate`, `country_last_prior_covered`) allowed exact
cross-row label recovery and **do not ship** in this version: a 2026-11-01
independent audit recovered 120/139 eval and 128/182 holdout labels through
them, and the fts-appeal-003 rebuild removed the channel with rows unchanged.
The only history-derived column is `years_since_country_prior`, which reads the
YEARS of strictly-earlier same-country appeals - never any row's outcome - and
is asserted label-free by brute-force recompute at construction. The FTS API
exposes no historical vintages, so the panel is current-vintage retrospective:
`quality.json`'s `evaluation_contract` declares `isolated_rows` access and a
restricted retrospective-research scope, and no historical forecasting claim is
made. Eval is labeled development/validation; holdout is final scoring.

## Licence

Our code and documentation: MIT (`LICENSE-MIT.txt`). Our rights in the derived
compilation: CC0-1.0 (`LICENSE-CC0-1.0.txt`) - covering only our contribution.
The source's own terms are preserved: FTS use-and-republish terms plus CC BY-IGO
on the HDX bulk distribution, with attribution carried into every copy. See
`LICENSE.md` for the exact attribution statements and scope.

Derived dataset based on Financial Tracking Service (FTS) data,
https://fts.unocha.org . Not an OCHA or FTS product.
