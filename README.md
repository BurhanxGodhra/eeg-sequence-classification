# CHB01 Seizure Sequence Classification

A notebook experiment that uses CHB01 CHB-MIT recordings, two-second epochs, CSP features, and ten-epoch windows to classify seizure versus non-seizure sequences with balanced logistic regression.

## Results

No saved accuracy, benchmark table, or evaluation output was present in the reviewed notebook. Therefore this draft makes **no performance claim**.

## Architecture

```mermaid
flowchart LR
  D[CHB01 EDF + summary] --> P[Two-second epochs]
  P --> C[CSP: 4 components]
  C --> W[10-epoch windows]
  W --> F[Flatten and scale]
  F --> M[Balanced logistic regression]
  M --> E[Classification report]
```

The notebook trains on CHB01 files 01–03 and 05–09 and tests on files 04 and 10–12. The ten-epoch windows are flattened before logistic regression; this is not a recurrent neural network.

## Quickstart and verification

The repository contains `sequence_model_pipeline.ipynb` and a minimal requirements file, but omits notebook dependencies including MNE, scikit-learn, and Matplotlib. CHB01 EDFs and `chb01-summary.txt` are external. No end-to-end run was verified.

```bash
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

Install the missing notebook dependencies, place the CHB01 EDFs and summary file where the notebook expects them, then open the notebook. Do not treat the commands above as a working experiment setup until those gaps are fixed.

## Limitations

- No recorded results despite an explicit CHB01 file split.
- Notebook-only implementation with incomplete dependency metadata.
- Train/test files all belong to CHB01, so this does not measure cross-patient generalization.

## Next steps

1. Pin all notebook dependencies and add a minimal setup script for CHB01.
2. Extract preprocessing and window construction into testable functions.
3. Save a deterministic report with class-level precision/recall and event-level metrics.
4. Add held-out-patient evaluation before making generalization claims.
