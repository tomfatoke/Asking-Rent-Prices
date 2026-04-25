# Asking Rent Price Prediction

## Project Overview
This project analyzes and predicts Canadian asking rent prices using
experimental estimates published by Statistics Canada. The data covers
average asking rent by rental unit type, number of bedrooms, and
geography across major Canadian cities from 2019 onwards.

The pipeline is built entirely on Databricks using the Medallion
Architecture pattern, with analysis and natural language querying
powered by Databricks Genie.

---

## Data Source
- **Publisher:** Statistics Canada
- **Dataset:** Asking rent prices, by rental unit type and number
  of bedrooms, experimental estimates
- **Format:** CSV
- **Last Updated:** March 11, 2026
- **URL:** https://www150.statcan.gc.ca/n1/tbl/csv/46100092-eng.zip

---

## Tech Stack
| Tool | Purpose |
|---|---|
| **Databricks** | Primary data platform |
| **Apache Spark** | Distributed data processing |
| **Delta Lake** | Storage layer for all tables |
| **Unity Catalog** | Data governance and table management |
| **Databricks Genie** | Natural language querying and analysis |
| **GitHub** | Version control |

---

## Architecture — Medallion Pattern  

---

## Bronze Layer — Complete ✅
The bronze layer is responsible for ingesting the raw Statistics Canada
CSV file exactly as received, with no transformations or cleaning applied.

### What was done:
- Connected Databricks to a Unity Catalog Volume containing the raw CSV
- Read the CSV into a Spark DataFrame using spark.read with header
  and inferSchema options
- Inspected the raw schema to identify all 16 original StatCan columns
  and their data types
- Added ingestion metadata columns:
  - ingestion_timestamp: records when the data was loaded
  - source_file: records the file path the data came from
- Wrote all 8,188 rows as-is to a Delta table with no columns dropped
  or modified

### Bronze Delta Table
`rent_project.rent_raw_data.bronze_rent_raw`

### Raw Schema
| Column | Data Type | Description |
|---|---|---|
| REF_DATE | date | Reference period |
| GEO | string | City and province |
| DGUID | string | StatCan geographic ID |
| Rental unit type | string | Unit type and bedroom count |
| Estimates | string | Estimate type |
| UOM | string | Unit of measure |
| UOM_ID | integer | Unit of measure ID |
| SCALAR_FACTOR | string | Scaling metadata |
| SCALAR_ID | integer | Scalar ID |
| VECTOR | string | StatCan series ID |
| COORDINATE | string | StatCan coordinate |
| VALUE | integer | Average asking rent |
| STATUS | string | Data quality flag |
| SYMBOL | string | Symbol field |
| TERMINATED | string | Series termination flag |
| DECIMALS | integer | Decimal places metadata |

---

## Current Status
- [x] GitHub repository created
- [x] Databricks Git folder connected
- [x] Raw CSV uploaded to Databricks Volume
- [x] Bronze layer complete — 8,188 rows ingested
- [ ] Silver layer in progress
- [ ] Gold layer pending
- [ ] ML prediction model pending
- [ ] Genie setup pending

---

## Author
GitHub: your-github-tomfatoke
