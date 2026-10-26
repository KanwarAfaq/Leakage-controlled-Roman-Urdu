# Leakage-controlled Roman Urdu--English code-mixed sentiment classification

Reproducibility material for *Leakage-Controlled Roman Urdu--English Code-Mixed Sentiment Classification: A Comparison of TF-IDF and Instruction-Tuned Language Models*.

**Study repository:** https://github.com/KanwarAfaq/Leakage-controlled-Roman-Urdu

## Study populations and published contents

- `data/development/train.csv`: **8,108 review/comment texts and source-derived or weak sentiment labels** (not independently human-gold).
- `data/development/validation.csv`: **2,027 texts and source-derived or weak labels**.
- `data/human_gold/Phase10P_Human_Gold_315_Public.csv`: **315 text records and adjudicated final labels** (146 Negative, 41 Neutral, 128 Positive).
- `predictions/Phase10P_Sealed_Predictions_Sanitized.csv`: **1,575 selected outcomes**, including 42 invalid outcomes, across five conditions.
- `results/`: published metrics, confusion matrices, class scores, model usage and integrity manifests.
- `figures/`: five manuscript illustrations in PNG/SVG.

**Release rights:** The maintainer expressly states he possesses the necessary licenses and permissions to publish these datasets. This release relies on that representation; it does not independently certify third-party permissions. Original source copyright and license terms still apply. MIT licenses the authors’ original code and CC BY 4.0 is offered for original author-controlled annotations/curation/documentation, *not third-party review text*. One direct email in validation data has been masked for public distribution. See `LICENSE`, `LICENSE_NOTICE.md`, and `docs/AUTHOR_PUBLICATION_ATTESTATION.md`. Private reviewer records, credentials and raw model reasoning are excluded.

## Direct offline reproduction — no model/API access required

Python **3.10+**, from the extracted repository root:

```powershell
python code/offline_verify_results.py --repo . --output-dir offline_reproduction
```

The command validates the released prediction/gold ID join, calculates accuracy, macro-F1, class-level metrics, coverage, invalid counts, and confusion matrices, checks against the saved published metrics, and writes machine-readable outputs. The original public-export mismatch has been corrected using the frozen label-free source manifest: all **315/315** released texts now verify against their stored SHA-256 hashes. Frozen IDs, hashes, labels, predictions, and metrics are unchanged. See `docs/TEXT_HASH_AUDIT.md`.

If needed, install environment dependencies with `python -m pip install -r requirements.txt`. The offline checker itself uses Python standard library only. The original development utilities are under `code/01_audit_sources.py` through `code/10_generate_tables_figures.py`; check `--help` on the individual scripts before running them with permitted inputs.

## Experimental protocol

The original two-window CGU local-model run wrote 2,069 attempt records for 1,260 unique LLM record-condition keys (809 additional attempts). Before gold-label scoring, the deterministic **first recorded response** per key was selected label-blind; it is not necessarily the first request sent. Invalid selected outcomes count as incorrect. The published selected predictions are derived from that sealed set; no duplicate responses were selected according to gold correctness.

Hosted model inference requires separate authorized CGU endpoint access. This repository is sufficient to verify the **published reported evaluation statistics offline** but does not establish independent re-execution of the model calls. Archival scripts `code/phase10p_recover_and_seal.py` and `code/phase10p_score.py` rely on additional private experiment inputs and the historic folder layout; they are provided for provenance, **not** as standalone clean-release executables.

## License, attribution, and access

- **Software:** MIT License (root `LICENSE`) for authors' original rights-controlled code.
- **Original human annotations, dataset curation, and documentation:** CC BY 4.0 where the project authors have the necessary rights; original third-party review/comment texts remain subject to their original license and permission conditions.
- **Data publication authorization:** The maintainer has expressly confirmed that he has the necessary source permissions and licenses to publish these data. This release relies on his statement rather than asserting independent third-party legal verification. See `docs/AUTHOR_PUBLICATION_ATTESTATION.md`.
- **Privacy protection:** One development validation text containing a contact email was masked before public release. The 315 frozen gold test texts, their hashes, gold labels, selected predictions, and official model scores are untouched.

For repository upload steps, see `docs/GITHUB_UPLOAD_INSTRUCTIONS.md`.
