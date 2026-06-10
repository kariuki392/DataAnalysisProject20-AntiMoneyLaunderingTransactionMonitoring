# 🏦 Anti-Money Laundering (AML) Transaction Monitoring
## Suspicious Activity Detection & Financial Crime Analytics

![Python](https://img.shields.io/badge/Python-3.10-blue?logo=python) ![Pandas](https://img.shields.io/badge/Pandas-2.0-150458?logo=pandas) ![FATF](https://img.shields.io/badge/Framework-FATF_40_Recommendations-darkred) ![POCA](https://img.shields.io/badge/Framework-POCA_2002-navy) ![Domain](https://img.shields.io/badge/Domain-Financial_Crime_Compliance-critical)

---

> *Money laundering costs the global economy an estimated $2 trillion annually — and banks, fintechs, and financial institutions are on the front line of detecting it. This project builds a rule-based AML transaction monitoring system that screens 500+ synthetic customer transactions for eight FATF-recognised money laundering typologies, generates risk-scored alerts, and produces SAR (Suspicious Activity Report) narratives ready for MLRO review.*

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

---

## 🎯 Overview

Anti-money laundering compliance is one of the most technically demanding and highest-stakes functions in financial services. Every transaction processed by a bank or payment institution must be screened for suspicious patterns — and when red flags are identified, the compliance team must assess the risk, escalate appropriately, and in serious cases file a Suspicious Activity Report (SAR) with the relevant Financial Intelligence Unit (FIU).

This project replicates the **transaction monitoring workflow** used by AML compliance teams in banks, fintechs, and money services businesses. For 15 synthetic customers — spanning individuals, corporates, Politically Exposed Persons (PEPs), and shell company structures — 500+ transactions are generated across a full calendar year and screened through an eight-rule detection engine aligned to the **FATF 40 Recommendations**.

The output includes a full alert register with risk scores, SAR filing decisions, and auto-generated SAR narratives — the complete deliverable set that an AML analyst would produce for MLRO (Money Laundering Reporting Officer) review.

> ⚠️ *All customer names, account numbers, and transaction data are entirely synthetic and created solely for portfolio demonstration purposes.*

---

## 📐 Regulatory Framework

| Framework | Jurisdiction | Key Provisions Applied |
|---|---|---|
| **FATF 40 Recommendations** | Global | R.10 CDD · R.12 PEPs · R.19 High-Risk Countries · R.20 STR · R.24 Beneficial Ownership |
| **POCA 2002** | UK | S.330 Failure to Disclose · S.333A Tipping-Off Offence |
| **Bank Secrecy Act / FinCEN** | USA | Currency Transaction Reports · SAR Filing Requirements |
| **Basel AML Index** | Global | Country risk scoring methodology |
| **Central Bank of Kenya Guidelines** | Kenya | AML/CFT Regulations 2013 |

---

## 📊 Dataset

All data is **synthetically generated** within the notebook — no external file required:

| Attribute | Details |
|---|---|
| **Customers** | 15 synthetic profiles (individuals, corporates, PEPs, shell companies) |
| **Transactions** | 500+ across January–December 2024 |
| **Transaction Types** | Cash Deposit · Cash Withdrawal · Wire Transfer · Internal Transfer · Mobile Money · Trade Finance · Crypto Exchange · ATM |
| **Channels** | Branch · Mobile Banking · Online Banking · ATM · Agent · SWIFT |
| **Countries** | 12 counterparty jurisdictions including FATF high-risk and secrecy jurisdictions |
| **Reporting Threshold** | $10,000 USD (SAR filing trigger) |
| **Structuring Threshold** | $9,500 USD (below-threshold detection) |

---

## 🗂️ Project Structure

```
aml-transaction-monitoring/
│
├── aml_transaction_monitoring.ipynb    # Fully executed analysis notebook
│                                       # (no external data file required)
├── charts/
│   ├── monitoring_dashboard.png        # Transaction monitoring overview
│   ├── risk_intelligence.png           # Risk analytics & detection performance
│   └── mlro_dashboard.png             # MLRO compliance summary dashboard
│
└── README.md
```

---

## 🔍 Detection Rules

| Rule | Typology | FATF Reference | Trigger Condition |
|------|----------|---------------|-------------------|
| **R01** | Structuring / Smurfing | R.20 | 3+ cash transactions between $9,500–$9,999 |
| **R02** | Large Cash Transaction | R.20 | Single cash transaction > $10,000 |
| **R03** | Layering — Rapid Movement | R.20 | 3+ wire/transfer/crypto transactions > $50,000 within 72 hours |
| **R04** | PEP Transaction | R.12 | Any transaction > $2,000 involving a Politically Exposed Person |
| **R05** | High-Risk Jurisdiction | R.19 | 2+ transactions to/from FATF grey/black-listed jurisdictions |
| **R06** | Velocity Anomaly | R.20 | 5+ transactions from one customer in a single day |
| **R07** | Round Amount Pattern | R.20 | 3+ transactions in exact round amounts ≥ $5,000 |
| **R08** | Shell Company | R.24 | Corporate in secrecy jurisdiction with > $20,000 total activity |

**Risk Scoring:**
- Base score per rule: 25–55 points
- PEP bonus: +20 points
- High-risk jurisdiction bonus: +15 points
- Maximum score: 100 points

**SAR Decision Thresholds:**
- Score ≥ 70 → **SAR Required** (file with FIU)
- Score 50–69 → **Escalate to MLRO**
- Score 30–49 → **Enhanced Monitoring**
- Score < 30 → **Monitor**

---

## 🔍 Analysis Sections

### 1️⃣ Synthetic Transaction Data Generation
15 customer profiles with realistic attributes (PEP status, jurisdiction, occupation, entity type) and 500+ transactions across 8 transaction types and 12 counterparty countries — weighted to produce realistic typology distributions.

### 2️⃣ FATF-Aligned Detection Rule Engine
Eight rule-based detectors applied across all customer transaction histories, each generating structured alert records with FATF reference, typology label, transaction count, total amount, and PEP/high-risk jurisdiction flags.

### 3️⃣ Transaction Monitoring Dashboard
Transaction volume by type, suspicious vs normal breakdown by typology, monthly volume trend (normal vs suspicious stacked), alert priority distribution, SAR decision pie chart, and top customers by alert count.

### 4️⃣ Risk Intelligence Dashboard
Alerts by typology, risk score distribution with decision thresholds, suspicious transaction rate by counterparty country, detection rule performance (alerts vs SAR outcomes), customer risk heatmap, and PEP vs non-PEP alert comparison.

### 5️⃣ SAR Narrative Generator
Auto-generates FinCEN/FRC-aligned SAR narratives for each alert — covering subject information, suspicious activity details, typology analysis, and recommended regulatory action including tipping-off warnings.

### 6️⃣ MLRO Compliance Dashboard
Monthly alert trend by priority, SAR filing pipeline, total amount under review by SAR decision, risk score boxplots by typology, MLRO KPI summary table, and customer exposure bubble matrix.

---

## 💡 Key Findings

### 💸 Structuring is the Most Common Typology
Multiple customers exhibited the classic structuring pattern — depositing cash in amounts just below the $10,000 reporting threshold to avoid triggering CTR (Currency Transaction Report) obligations. Under both POCA 2002 and the Bank Secrecy Act, structuring is itself a criminal offence regardless of the legitimacy of the underlying funds.

### 🏛️ PEP Customers Generate the Highest Risk Scores
All PEP-flagged alerts received elevated scores due to the mandatory enhanced due diligence requirement under FATF R.12. PEP relationships require senior management approval, source of wealth verification, and quarterly monitoring reviews — making them the highest-touch customer segment in any AML programme.

### 🌍 Secrecy Jurisdictions Drive the Largest Alert Values
Corporate customers registered in British Virgin Islands, Cayman Islands, and Panama generated the highest-value alerts — consistent with the use of shell structures in the placement and layering stages. FATF R.24 requires Ultimate Beneficial Owner (UBO) verification before processing further transactions for these entities.

### ⚡ Layering Detected Across High-Value Accounts
Rapid fund movement through wire transfers and crypto exchanges — the signature of layering — was concentrated in the highest-revenue customer accounts. These cases require immediate account restriction consideration and are the most operationally urgent alerts for MLRO action.

### 🚨 Tipping-Off Risk is Present in All SAR Cases
Once a SAR decision is made, disclosure of the filing to the subject customer constitutes a criminal tipping-off offence under POCA 2002 S.333A. All SAR-required cases must be managed under strict information security protocols within the compliance team.

---

## 🛠️ Tools & Libraries

| Library | Application |
|---------|------------|
| **Pandas** | Transaction data generation, customer profiling, alert aggregation |
| **NumPy** | Synthetic data generation, risk score calculation, random sampling |
| **Matplotlib / Seaborn** | 18+ visualisations across 3 dashboards — bar charts, heatmaps, boxplots, bubble charts, pie charts |
| **Python (native)** | 8-rule detection engine, SAR narrative generator, risk scoring logic |

---

## ▶️ How to Run

1. Clone the repository and navigate to the project folder
2. Install dependencies:
```bash
pip install pandas numpy matplotlib seaborn
```
3. Open and run the notebook — **no external data file required**, all data is generated internally:
```bash
jupyter notebook aml_transaction_monitoring.ipynb
```

> ✅ All cells are pre-executed with embedded outputs. No re-running required.

---

## 📌 About This Project

This project was developed to demonstrate applied knowledge of AML compliance — the detection rules, regulatory frameworks, risk scoring methodology, and reporting obligations that an AML analyst or financial crime compliance specialist would apply in a bank, fintech, or professional services context.

**Skills demonstrated:**
- Applied knowledge of FATF 40 Recommendations
- Rule-based typology detection engine design
- SAR narrative generation and MLRO reporting
- Risk scoring and alert triage methodology
- Regulatory knowledge: POCA 2002, Bank Secrecy Act, FinCEN SAR requirements

**Portfolio context:** This project forms part of a financial crime compliance trilogy alongside:
- ⚖️ Conflict of Interest Screening (IESBA/IFAC/PCAOB)
- 🏦 AML Transaction Monitoring (FATF/POCA/FinCEN) ← *this project*
- 🔍 KYC Due Diligence Screening *(coming soon)*

---

*Part of a 21-project data analytics portfolio spanning HR analytics, financial forecasting, NLP, e-commerce, supply chain, public health, real estate, credit risk, aviation, media, cybersecurity, clinical healthcare, urban analytics, and financial crime compliance.*
