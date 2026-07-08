# dialogue-pronoun-claim-data

Annotated diagnostic data for pronoun-dependent claims in conversations.

This repository contains four post-adjudication CSV files derived from DialFact and FaithDial. Each example includes a dialogue context, a target text containing an annotated pronoun, inherited evidence/knowledge text and source label, and context-side referent annotations.

## Data files

The CSV files are in the `data/` folder.

| File | Source | Rows | Target column | Labels |
|---|---|---:|---|---|
| `df-valid-coref.csv` | DialFact validation-derived slice | 456 | `response` | `SUPPORTS`, `REFUTES`, `NOT ENOUGH INFO` |
| `df-test-coref.csv` | DialFact test-derived slice | 315 | `response` | `SUPPORTS`, `REFUTES`, `NOT ENOUGH INFO` |
| `fd-random.csv` | FaithDial random split-derived slice | 405 | `claim` | `HALLUCINATION`, `NON-HALLUCINATION` |
| `fd-topic.csv` | FaithDial topic split-derived slice | 445 | `claim` | `HALLUCINATION`, `NON-HALLUCINATION` |

Total: **1,621 examples**.

## Columns

Each file contains the following fields:

| Column | Description |
|---|---|
| `context_id` | Source-local context identifier |
| `id` | Row identifier |
| `context` | JSON-encoded list of dialogue turns |
| `response` / `claim` | Target text containing the annotated pronoun |
| `evidence_text` | Evidence or knowledge text inherited from the source dataset |
| `response_label` | Label inherited from the source dataset |
| `pronoun_info` | Annotated pronoun surface form and character span in the target text |
| `referent_info` | Context-side referent mention(s) and character span(s) |

Character offsets are zero-based and end-exclusive.

## Label distribution

| File | Rows | Label distribution |
|---|---:|---|
| `df-valid-coref.csv` | 456 | `SUPPORTS` 172 (37.7%), `REFUTES` 158 (34.6%), `NOT ENOUGH INFO` 126 (27.6%) |
| `df-test-coref.csv` | 315 | `SUPPORTS` 115 (36.5%), `REFUTES` 102 (32.4%), `NOT ENOUGH INFO` 98 (31.1%) |
| `fd-random.csv` | 405 | `HALLUCINATION` 294 (72.6%), `NON-HALLUCINATION` 111 (27.4%) |
| `fd-topic.csv` | 445 | `HALLUCINATION` 335 (75.3%), `NON-HALLUCINATION` 110 (24.7%) |

## Context and referent statistics

`Context turns` is the number of turns in the JSON-encoded `context` field. `Referent mentions` is the number of annotated context-side referent spans in `referent_info`.

Values are reported as **min / median / mean / max**.

| File | Context turns | Referent mentions | >1 referent mention |
|---|---:|---:|---:|
| `df-valid-coref.csv` | 1 / 4 / 4.41 / 9 | 1 / 2 / 2.09 / 7 | 257 (56.4%) |
| `df-test-coref.csv` | 1 / 3 / 3.56 / 9 | 1 / 1 / 1.70 / 8 | 118 (37.5%) |
| `fd-random.csv` | 1 / 5 / 4.47 / 9 | 1 / 1 / 1.75 / 8 | 148 (36.5%) |
| `fd-topic.csv` | 1 / 5 / 4.32 / 9 | 1 / 1 / 1.75 / 10 | 179 (40.2%) |

## Notes

- This is a diagnostic data release, not a new general-purpose coreference benchmark.
- DialFact and FaithDial labels come from different source datasets and should not be treated as a single unified label space.
- FaithDial labels are inherited hallucination labels, not DialFact-style verification labels.
- Some target texts may already contain an explicit mention of the annotated referent.
- The four files should not be treated as mutually exclusive benchmark splits without checking for overlaps.

## Citation

If you use this data, please cite the associated paper and the original DialFact and FaithDial papers.
