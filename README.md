# 📊 Performance Scoring & Top Talent Identification Engine

This project implements an **end-to-end performance scoring system** designed to evaluate employees across different roles (EVs, ECs, SDRs) using business KPIs, benchmarking, and eligibility rules.

It combines **data processing, scoring models, business logic, and reporting** into a fully automated and auditable pipeline.

---

## 🚀 Overview

The system:

- Cleans and standardizes raw data from multiple sources
- Calculates **cluster benchmarks**
- Applies **multi-model scoring (R1–R5)**
- Evaluates **eligibility based on business rules**
- Identifies **Top Talents**
- Generates **monthly and quarterly insights**
- Produces a **fully structured Excel report**
- Provides a **detailed audit layer for transparency**

---

## 🧠 Scoring Models

The engine uses five scoring approaches:

- **R1 – Weighted Percentile**  
  Performance ranking within cluster using weighted KPIs

- **R2 – Simple Percentile**  
  Average percentile across KPIs

- **R3 – Weighted Normalized Score**  
  Distance from top performer (scaled 0–100)

- **R4 – Simple Normalized Score**  
  Average normalized performance

- **R5 – Cluster Benchmark Comparison (Main Model)**  
  Compares individual performance vs cluster average  
  → **Primary model for Top Talent identification**

---

## 📐 Business Rules

### ✅ Unit Eligibility
A unit (franchise) must meet its commercial target in at least:

- **60% of months in the period**

---

### 📊 Share Thresholds

Two types of thresholds are applied:

#### 1. Fixed Threshold (Business Rule)
- EV/EC: 40% (or 60% if solo)
- SDR: 50% (or 70% if solo)

#### 2. Dynamic Threshold (HC-based)
- Calculated as:  
  **1 / Headcount (HC)**  
- Capped by a maximum threshold

---

### 🏆 Top Talent Criteria (R5)

An employee is classified as **Top Talent** if:

- Unit achieved target ✅  
- Individual share ≥ threshold ✅  
- Performance ≥ cluster average (≥ 100) ✅  

---

## 🏗️ Architecture

### 🔹 Data Processing
- Column standardization
- Franchise name cleaning
- Date filtering (including inactive employees)

### 🔹 Benchmarking
- Cluster-level averages per KPI
- Historical tracking of benchmarks

### 🔹 Scoring Engine
- Percentile ranking
- Normalization (0–100 scale)
- Cluster comparison metrics

### 🔹 Eligibility Layer
- R1–R4: Fixed threshold logic
- R5: Dynamic + benchmark-based logic

### 🔹 Output Layer
- Monthly and quarterly aggregations
- Role-based segmentation (EV, EC, SDR)
- Excel report generation

---

## 📁 Outputs

The pipeline generates an Excel file with multiple sheets:

- **Monthly_TopTalent_Summary**
- **Monthly_TopTalent_Detail**
- **General_Summary**
- **R5_General_View (Fixed Rule)**
- **R5_HC_View (Dynamic Rule)**
- **Eligibility_R1_R4 (per role)**
- **Cluster_Benchmarks**
- **Audit_Detailed_Calculation**
- **Top_Performer_Retention**
- **Methodology**

---

## 🔍 Auditability

The project includes a dedicated **audit dataset** with:

- Raw KPI values
- Percentiles
- Normalized scores
- Cluster comparisons
- Share and thresholds applied
- Eligibility reasons

This ensures **full transparency and traceability** of all calculations.

---

## 📅 Monthly vs Quarterly Logic

### Monthly
- Performance calculated independently per month
- Used for trend analysis

### Quarterly
- Aggregated view
- Includes **continuity rule (3 months participation)**

---

## 🔁 Continuity Rule

Only employees who participated in **all months of the period** are considered in the final quarterly results.

---

## 📈 Retention Analysis

The system tracks:

- Total Top Talents
- Active vs inactive employees
- Retention rate (%)

---

## 🛠️ Tech Stack

- **Python**
- **Pandas**
- **NumPy**
- **Excel (XlsxWriter)**

---

## 💡 Key Design Decisions

- Removed **Early Churn** and redistributed weights
- Separated **fixed vs dynamic threshold logic**
- Built **multiple scoring perspectives (R1–R5)**
- Ensured **auditability by design**
- Supported **multi-role logic with different KPIs**

---

## 📌 How to Run

1. Update input file paths:
   ```python
   ARQUIVO_EXCEL = "your_file.xlsx"