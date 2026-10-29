# ILSF: Institutional LLM Security Framework (experiment notebook)

Companion code for *Design and Preliminary Experimental Evaluation of an Access-Control and Data Governance Framework for Secure Institutional LLM Systems* (Matima, Mhlari, Chisom, Kgatla; Tshwane University of Technology).

ILSF is a deny-by-default attribute-based access-control layer placed before retrieval and before the LLM call in an institutional RAG system. This repository holds a single notebook that regenerates a fully fictional benchmark and runs experiments E1-E5.

## Run

```bash
pip install -r requirements.txt
jupyter notebook ILSF_Experiments.ipynb
```

Or open the notebook in Google Colab and run all cells. Sections 1-6 and 10 need no model and run in seconds. Sections 7-9 (E4, E5) download `google/flan-t5-small` and are skipped automatically if it cannot be loaded. Outputs are written to `ILSF/data`, `ILSF/results` and `ILSF/figures`.

## Expected results (sections 1-6, 10)

| Check | Value |
|---|---|
| Requests authorised / unauthorised | 120 / 240 |
| Unauthorised permits: B0 / B1 / ILSF | 240 / 120 / 0 |
| E3 correct of 24: B0 / B1 / ILSF | 12 / 12 / 24 |
| E3 exact McNemar (vs ILSF), Holm-adjusted | p = 0.000488, 0.001465 |
| Second policy reading disagrees with implemented policy | 52 of 360 |
| Student records with a valid owner (original / corrected) | 4 / 30 |

Latencies vary by machine.

## Limitations

- The reference policy in E1, E2 and E4 is ILSF's own policy, so zero ILSF permits there are expected by construction.
- E3 expected outcomes were written by the authors, not independently.
- E5 is an eight-trial pilot on a very small model and is not evidence of injection resistance.
- The response validator and audit logger described in the paper are not implemented.
- The benchmark generator in this notebook was reconstructed to reproduce the original data's counts; minor fields (such as document text) may differ from the original run. The corrected dataset (section 10) is an extension not reported in the paper.
- All data are fictional.
