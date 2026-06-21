# Risk-Based Anti-Money Laundering Analytics for High-Volume Digital Transactions

A deployment-oriented machine learning project for **Anti-Money Laundering (AML) alert prioritization** in high-volume digital transaction environments. The project evaluates baseline and advanced models, translates model outputs into financial impact, and applies model-risk governance to determine whether the solution is suitable for operational deployment.

> **Project position:** This repository supports a technical white paper, not an academic paper. The focus is executive decision-making, defensible model validation, economic value, and transparent model-risk control.

---

## Project Overview

Financial institutions process millions of transactions, but only a very small proportion are suspicious or related to money laundering. Reviewing every transaction manually is operationally impossible, while missing true AML cases can lead to regulatory, financial, and reputational damage.

This project builds a machine learning framework to prioritize transactions for AML review. The goal is not to replace compliance officers, but to support risk-based triage by identifying transactions that deserve investigation attention first.

---

## Key Result

The original Extra Trees model achieved perfect performance only when `Laundering_type` was included. After removing this feature, performance dropped sharply, proving that the original perfect score is not production-safe unless `Laundering_type` is confirmed as a real-time pre-investigation field.

| Model Version                         | Precision | Recall | PR-AUC | False Positives | False Negatives | Net Expected Cost |
| ------------------------------------- | --------: | -----: | -----: | --------------: | --------------: | ----------------: |
| Extra Trees with `Laundering_type`    |    1.0000 | 1.0000 | 1.0000 |               0 |               0 |       -$1,443,975 |
| Extra Trees without `Laundering_type` |    0.0380 | 0.5219 | 0.3559 |          19,566 |             708 |        $3,275,475 |

**Final recommendation:** do not approve direct production deployment. Proceed with feature-lineage validation and shadow testing first.

---

## Repository Structure

```text
.
├── README.md
├── notebooks/
│   └── Fintech_solved_deployment_ready.ipynb
├── reports/
│   └── AML_Technical_White_Paper_READY_Ablation_Updated.docx
├── outputs/
│   ├── aml_laundering_type_ablation_comparison.csv
│   ├── aml_threshold_table_with_laundering_type.csv
│   ├── aml_threshold_table_without_laundering_type.csv
│   ├── extra_trees_with_laundering_type.joblib
│   └── extra_trees_without_laundering_type.joblib
├── figures/
│   └── business_impact_removing_laundering_type.png
└── requirements.txt
```

---

## Disclaimer

This project is for educational and research purposes. It is not a production AML system, legal compliance tool, or regulatory reporting solution. Any real-world deployment would require independent validation, legal review, model-risk approval, data-lineage confirmation, and ongoing monitoring.
