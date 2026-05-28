# PyPeselReader-ETL 🚀

## Overview
A professional, production-ready Python-based ETL (Extract, Transform, Load) pipeline designed for batch processing, rigorous validation, and analytical enrichment of Polish PESEL numbers. 

This repository showcases commercial-grade Data Engineering design patterns, strict Object-Oriented Programming (OOP), and production-level system observability.

## 🛠 Tech Stack
* **Language:** Python 3.x
* **Database:** SQLite3 (Relational batch storage)
* **Core Modules:** `zipfile` & `io` (In-memory archive streaming), `csv.DictReader` (Header-mapped extraction)
* **Monitoring:** `logging` (Industrial event tracking)
* **Temporal Data:** `datetime` (Century-aware date parsing)

---

## ⚙️ ETL Pipeline Architecture

### 1. Extract 📂
* **In-Memory Buffer Processing:** Automatically scans and unpacks `.zip` archives. 
* **Batch Ingestion:** Streamlines multiple `.csv` targets simultaneously using memory-efficient generators to eliminate high-volume RAM bottlenecks.

### 2. Transform 🧠
* **Algorithmic Validation:** Implements the official government-weighted checksum algorithm to flag corrupted or fake identification numbers.
* **Century-Aware Decoding:** Highly robust date extraction engine capable of handling century offsets across multiple generations (covering years 1800 to 2299).
* **Data Enrichment:** Derives and segments raw inputs into clean database attributes: Birth Day, Month Name, Year, and Gender.
* **Encoding Awareness:** Native integration with `windows-1250` character mapping to guarantee data integrity for Polish linguistic structures and names.

### 3. Load 💾
The pipeline enforces a strict **Dual-Storage Strategy** to separate production-ready metrics from corrupted logs:
* **Success Table:** Stores successfully validated and enriched employee/user records.
* **Rejection Table:** Acts as an audit dead-letter queue. Captures "dirty" data and automatically appends a precise error reason for data quality review.

---

## 📊 System Observability & Monitoring
The application implements an enterprise logging architecture (`pesel.log`). Every pipeline state, structural anomaly, warning, and fatal error is tracked with an active timestamp, allowing administrators to monitor full data lineage and pipeline health in real time.

---

## 🚀 Usage

### Prerequisites
Prepare a `.zip` archive containing one or more `.csv` files. Ensure every CSV document contains a header column explicitly named `pesel`.

### Execution
Run the orchestrator script directly from your terminal:
```bash
python PeselReader.py
