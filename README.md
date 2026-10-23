# Azure Data Factory Incremental Ingestion Pipeline

> **Learning project:** Hands-on Azure Data Factory practice project by [Prakash Kantumutchu (KP)](https://thisiskp.in) implementing watermark-based incremental extraction from Azure SQL Database into Azure Data Lake Storage Gen2.

---

## Overview

This repository stores the Git-integrated Azure Data Factory artifacts for a watermark-based incremental ingestion pipeline (`pipeline/incrementalingestion.json`):

1. **Lookup last watermark & current watermark:** Reads the prior high-water mark from ADLS Gen2 (`dataset/Jsoncdc.json`) and queries the current timestamp from Azure SQL Database (`dataset/AzureSqlTable.json`).
2. **Incremental copy:** Extracts rows added or modified since the last watermark and writes them as Parquet (`dataset/Parquet1.json`) to ADLS Gen2 (`linkedService/lsdatalakegen2.json`).
3. **Conditional watermark update:** If the copy activity transfers one or more rows, updates the stored watermark file (`dataset/Jsonupdatedcdc.json`) so subsequent runs only process new changes.

---

## Repository Structure

```text
├── dataset/
│   ├── AzureSqlTable.json       # Source Azure SQL table dataset
│   ├── Jsoncdc.json             # Stored watermark JSON dataset
│   ├── Jsonempty.json           # Empty JSON template dataset
│   ├── Jsonupdatedcdc.json      # Updated watermark JSON dataset
│   └── Parquet1.json            # Sink Parquet dataset on ADLS Gen2
├── factory/
│   └── azuredatafactorycsr212.json
├── linkedService/
│   ├── lsdatalakegen2.json      # Azure Data Lake Storage Gen2 linked service
│   └── lssqldb.json             # Azure SQL Database linked service
├── pipeline/
│   └── incrementalingestion.json # Watermark lookup + conditional copy pipeline
├── publish_config.json
└── LICENSE
```

---

## License

MIT — see [`LICENSE`](LICENSE).
