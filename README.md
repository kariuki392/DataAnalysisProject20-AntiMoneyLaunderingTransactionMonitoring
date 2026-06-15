# 🏦 Anti-Money Laundering (AML) Transaction Monitoring
## Suspicious Activity Detection & Financial Crime Analytics

![Python](https://img.shields.io/badge/Python-3.13-blue?logo=python) ![Pandas](https://img.shields.io/badge/Pandas-2.3-blue?logo=pandas) ![FATF](https://img.shields.io/badge/Framework-FATF_40_Recommendations-darkred) ![POCA](https://img.shields.io/badge/Framework-POCA_2002-navy) ![Domain](https://img.shields.io/badge/Domain-Financial_Crime_Compliance-critical)

---

> *A synthetic AML transaction monitoring demonstration built to showcase rule-based suspicious activity detection, risk scoring, SAR narrative generation, and compliance dashboard analytics.*

---

## 📋 Table of Contents

- [Overview](#-overview)
- [Regulatory Framework](#-regulatory-framework)
- [Dataset](#-dataset)
- [Project Structure](#-project-structure)
- [Detection Rules](#-detection-rules)
- [Analysis Sections](#-analysis-sections)
- [Key Findings](#-key-findings)
- [Tools & Libraries](#-tools--libraries)
- [How to Run](#-how-to-run)
- [Recent Updates](#-recent-updates)

---

## 🎯 Overview

This repository contains a Jupyter notebook that generates synthetic AML transaction data and applies a rule-based detection engine for suspicious activity monitoring.

It simulates a full AML monitoring workflow for 15 synthetic customer profiles and 500+ transactions across a 12-month timeline, producing:
- structured alerts with typology and risk score
- SAR narrative output for MLRO review
- AML dashboards for monitoring, risk intelligence, and compliance reporting

> ⚠️ All customer names, account numbers, transaction data, and alerts are synthetic and created solely for portfolio demonstration.

---

## 📐 Regulatory Framework

| Framework | Jurisdiction | Coverage |
|---|---|---|
| **FATF 40 Recommendations** | Global | R.10 CDD · R.12 PEPs · R.19 High-Risk Countries · R.20 STR · R.24 Beneficial Ownership |
| **POCA 2002** | UK | S.330 Failure to Disclose · S.333A Tipping-Off |
| **FinCEN / Bank Secrecy Act** | USA | SAR filing and suspicious transaction reporting |
| **Basel AML Index** | Global | Jurisdiction risk scoring |
| **Central Bank of Kenya Guidelines** | Kenya | AML/CFT regulatory expectations |

---

## 📊 Dataset

The notebook generates the dataset internally; no external data files are required.

| Attribute | Details |
|---|---|
| **Customers** | 15 synthetic profiles including individuals, corporates, PEPs, and shell companies |
| **Transactions** | 500+ records covering January–December 2024 |
| **Transaction Types** | Cash Deposit · Cash Withdrawal · Wire Transfer · Internal Transfer · Mobile Money · Trade Finance · Crypto Exchange · ATM |
| **Channels** | Branch · Mobile Banking · Online Banking · ATM · Agent · SWIFT |
| **Counterparty Jurisdictions** | Includes FATF high-risk and secrecy jurisdictions |
| **SAR Threshold** | $10,000 USD |
| **Structuring Threshold** | $9,500 USD |

---

## 🗂️ Project Structure

```
aml_transaction_monitoring/
├── README.md
├── notebooks/
│   └── aml_transaction_monitoring.ipynb
├── reports/
└── src/
```

- `notebooks/aml_transaction_monitoring.ipynb` is the main analysis notebook.
- `reports/` is available for exportable summaries or report outputs.
- `src/` is available for reusable helper code or future modularization.

---

## 🔍 Detection Rules

| Rule | Typology | FATF Reference | Trigger Condition |
|---|---|---|---|
| **R01** | Structuring / Smurfing | R.20 | 3+ cash transactions between $9,500 and $9,999 within 7 days |
| **R02** | Large Cash Transaction | R.20 | Single cash transaction > $10,000 |
| **R03** | Layering | R.20 | 3+ wire/transfer/crypto transactions totaling > $50,000 within 72 hours |
| **R04** | PEP Transaction | R.12 | Transactions involving flagged PEP customers |
| **R05** | High-Risk Jurisdiction | R.19 | Transactions to/from FATF grey/black-listed jurisdictions |
| **R06** | Velocity Anomaly | R.20 | Unusually high transaction frequency in a short window |
| **R07** | Round Amount Pattern | R.20 | Repeated round-dollar transaction amounts |
| **R08** | Shell Company | R.24 | Corporate entity in a secrecy jurisdiction with elevated activity |

**Risk Scoring**
- Base score is assigned by rule logic
- PEP indicator adds additional risk
- High-risk jurisdiction indicator adds additional risk
- Final score is capped at 100

**SAR Decision Logic**
- Score ≥ 70 → SAR Required
- Score 50–69 → Escalate to MLRO
- Score 30–49 → Enhanced Monitoring
- Score < 30 → Monitor

---

## 🔍 Analysis Sections

### 1. Synthetic Transaction Data Generation
Produces 500+ synthetic transactions for 15 customers with realistic AML attributes.

### 2. Detection Engine
Applies eight rule-based AML detectors and creates `df_alerts` for downstream dashboards.

### 3. Transaction Monitoring Dashboard
Visualizes transaction volume, suspicious vs normal activity, alert priorities, SAR decisions, and top customers.

### 4. Risk Intelligence Dashboard
Shows typology counts, risk score distribution, jurisdiction risk, detection rule performance, and PEP comparison.

### 5. SAR Narrative Generator
Auto-generates SAR narratives aligned to AML reporting expectations.

### 6. MLRO Summary Dashboard
Summarizes monthly alert volume, SAR pipeline, amount under review, and key compliance KPIs.

---

## 💡 Key Findings

- **Structuring is the most common typology** among synthetic alerts.
- **PEP alerts carry elevated risk** and require enhanced due diligence.
- **Secrecy jurisdictions drive higher-value alerts** in the dataset.
- **Layering is detected in rapid fund movement via wire and crypto channels**.
- **Tipping-off risk is explicitly noted for SAR-required cases**.

---

## 🛠️ Tools & Libraries

- **Python 3.13**
- **Pandas 2.3**
- **NumPy 2.3**
- **Matplotlib 3.10**
- **Seaborn 0.13**

---

## ▶️ How to Run

1. Install dependencies:
```bash
pip install pandas numpy matplotlib seaborn
```
2. Launch the notebook:
```bash
jupyter notebook notebooks/aml_transaction_monitoring.ipynb
```

> The notebook generates its own synthetic dataset and produces alerts, dashboards, and SAR narratives.

---

## 🔧 Recent Updates

- Fixed rolling-window extraction in the detection engine to avoid pandas scalar/Series formatting errors.
- Added `df_alerts` creation after rule execution so dashboard and SAR cells run consistently.
- Corrected alert priority dashboard indexing errors.

---

*This repository is a synthetic AML portfolio demonstration. No real customer data is used.*
