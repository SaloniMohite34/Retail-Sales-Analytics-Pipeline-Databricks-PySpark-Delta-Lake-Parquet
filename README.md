# Retail Sales Analysis with Databricks & PySpark
"Medallion-architecture retail sales pipeline with Databricks, PySpark and Delta Lake"

## 📌 Project Overview

This project implements an end-to-end **retail sales data engineering pipeline using Databricks and PySpark**.

The objective is to ingest retail sales and store data, perform data cleaning and validation, transform and combine datasets, generate business-level analytics, and store the results using **Delta Lake and Parquet**.

The project follows the **Medallion Architecture**:

**Bronze → Silver → Gold**

It demonstrates practical data engineering concepts such as data ingestion, explicit schema definition, data-quality validation, deduplication, data transformation, joins, aggregations, window functions, and lakehouse data storage.

---

## 🎯 Business Objectives

The pipeline helps analyze retail sales and store performance to answer questions such as:

- Which stores generate the highest total sales?
- Which products have the highest quantity sold?
- How do stores perform across regions?
- What is the sales performance relative to store size?

---

## 📊 Dataset

The project uses two CSV datasets.

### 1. Sales Data

The sales dataset contains the following fields:

- `sale_id`
- `store_id`
- `product_id`
- `sale_date`
- `quantity`
- `total_amount`

### 2. Store Data

The store dataset contains the following fields:

- `store_id`
- `store_region`
- `store_size`
- `open_date`

The datasets are ingested using PySpark and stored in the Bronze layer as Delta data.

> **Note:** Update this section if your actual dataset uses different column names. The source datasets are not included if redistribution is not permitted.

---

## 🏗️ Project Architecture

The project uses the three layers of Medallion Architecture.

```text
          CSV Source Files
                 |
                 v
          BRONZE LAYER
       Raw Data Ingestion
       Explicit Schemas
           Delta Lake
                 |
                 v
          SILVER LAYER
        Data Cleaning
        Data Validation
        Deduplication
        Data Transformation
        Sales-Store Join
           Delta Lake
                 |
                 v
           GOLD LAYER
        Business Aggregations
        Store Performance
        Product Performance
        Ranking and Window Functions
           Delta Lake
                 |
                 v
         Delta / Parquet
```

### 🥉 Bronze Layer — Data Ingestion

The Bronze layer ingests the source CSV files and preserves the data in a persistent format.

**Key operations:**
- Load sales and store datasets using PySpark.
- Define explicit schemas for data types.
- Store the ingested datasets in Delta format.
- Create a reliable foundation for downstream processing.

**Output datasets:**

```text
/content/output/bronze/sales_data
/content/output/bronze/store_data
```

### 🥈 Silver Layer — Data Cleaning and Transformation

The Silver layer focuses on improving data quality and preparing the data for analysis.

**Key operations:**
- Identify missing values and calculate null counts.
- Remove duplicate records.
- Filter sales records with missing required fields.
- Remove invalid sales values, such as non-positive quantities and amounts.
- Validate store records.
- Handle missing store sizes using the average valid store size.
- Join sales and store datasets using `store_id`.
- Create derived columns for sales per square foot and sale year.

**Derived columns:**

- `sales_per_sqft` — sales amount divided by store size.
- `sale_year` — year extracted from the sale date.

**Output dataset:**

```text
/content/output/silver/combined_sales
```

### 🥇 Gold Layer — Business Analytics

The Gold layer generates aggregated datasets for business analysis.

**Key operations:**
- Aggregate total sales and quantity by store and region.
- Identify the top five stores by total sales.
- Aggregate product quantities sold.
- Identify the top five products by quantity sold.
- Use Spark window functions to rank stores and products.
- Persist analytical outputs in Delta format.
- Export final results as Parquet where required.

**Output datasets:**

```text
/content/output/gold/top5_products
/content/output/gold/top5_stores
```

---

## 🔄 Pipeline Workflow

1. **Ingestion:** Load CSV files into Spark DataFrames using explicit schemas.
2. **Bronze:** Store the ingested datasets in Delta format.
3. **Silver:** Clean, validate, deduplicate, transform, and join the datasets.
4. **Gold:** Generate store and product performance aggregations.
5. **Ranking:** Use window functions to identify the top-performing stores and products.
6. **Storage:** Persist the outputs using Delta Lake and Parquet.

---

## 🛠️ Technologies Used

- **Databricks** — data engineering environment
- **Apache Spark** — distributed data processing
- **PySpark** — Python API for Apache Spark
- **Delta Lake** — reliable storage for pipeline layers
- **Unity Catalog Volumes** — data storage and organization
- **Python** — data processing and transformation
- **Parquet** — columnar storage format
- **Spark DataFrame API** — data manipulation
- **Spark SQL Functions** — aggregations and transformations
- **Window Functions** — ranking and analytical operations

---

## 📁 Project Structure

```text
retail-sales-databricks/
│
├── README.md
├── notebooks/
│   ├── 01_Bronze_Layer
│   ├── 02_Silver_Layer
│   └── 03_Gold_Layer
├── data/
│   └── README.md
├── output/
│   ├── top5_stores/
│   └── top5_products/
└── docs/
    └── architecture.png
```

*Adjust the folder structure to match the files and folders actually present in your repository.*

---

## 📈 Key Data Engineering Concepts Demonstrated

### Data Ingestion
Loading structured CSV files into Spark using explicit schemas.

### Data Quality
Identifying and handling missing values, duplicates, and invalid records.

### Schema Management
Defining data types explicitly for more predictable processing.

### Data Transformation
Creating calculated columns and extracting date information.

### Data Integration
Combining sales and store datasets using a common business key.

### Distributed Processing
Using PySpark DataFrame operations for scalable data processing.

### Window Functions
Ranking stores and products according to business metrics.

### Medallion Architecture
Separating raw, cleaned, and business-ready datasets into Bronze, Silver, and Gold layers.

### Delta Lake and Parquet
Persisting intermediate datasets and exporting analytical results in efficient storage formats.

---

## 💡 Design Decisions

### Why use explicit schemas?

Explicit schemas provide control over data types and make data ingestion more predictable than relying entirely on schema inference.

### Why use Delta Lake between layers?

Persisting intermediate datasets in Delta allows each pipeline stage to read its inputs independently, without depending on DataFrame variables from another notebook.

### Why separate Silver and Gold?

The Silver layer focuses on data quality and reusable transformations, while the Gold layer focuses on business-oriented aggregations and analytical outputs.

---

## 🚀 Future Improvements

Potential enhancements include:

- Implement incremental data processing instead of full overwrites.
- Use Delta `MERGE` for insert and update operations.
- Add automated data-quality checks and expectations.
- Implement logging, monitoring, and error handling.
- Parameterize input and output paths using Databricks widgets.
- Orchestrate the pipeline using Databricks Workflows.
- Add automated tests for data transformations.
- Connect Gold-layer outputs to Power BI or Tableau.
- Store source data in Amazon S3 and integrate AWS services.

---

## 👩‍💻 Author

**Saloni Mohite**

- GitHub: [SaloniMohite34](https://github.com/SaloniMohite34)

---

## ⭐ Conclusion

This project demonstrates an end-to-end retail data engineering workflow using Databricks and PySpark. By implementing the Bronze, Silver, and Gold layers, it transforms raw sales and store data into structured, validated, and business-ready analytical datasets.

The project provides practical experience with distributed data processing, data quality, Delta Lake, Spark transformations, and business performance analysis.
