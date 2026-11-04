# NYC Taxi Data Engineering Pipeline

An end-to-end data engineering project built using **Python, PySpark, Databricks, SQL, Apache Airflow and AWS S3** to process and analyze NYC Yellow Taxi trip data.

## Project Overview

This project builds a data pipeline to ingest, clean, transform, validate and analyze NYC Yellow Taxi trip records.

The pipeline processes millions of records using PySpark on Databricks, generates daily business metrics and uses Apache Airflow to orchestrate the Databricks ETL job.

## Architecture

```text
NYC Yellow Taxi Parquet Data
             |
             v
       Databricks
             |
             v
    PySpark ETL Pipeline
             |
      +------+------+
      |             |
      v             v
 Data Cleaning   Data Validation
      |             |
      +------+------+
             |
             v
     Processed Data
             |
       +-----+-----+
       |           |
       v           v
   SQL Analytics  Daily Metrics
       |           |
       +-----+-----+
             |
             v
          AWS S3
       (Manual Upload)

Apache Airflow
       |
       v
Triggers Databricks ETL Job
```

## Technologies Used

- **Python:** Pipeline development and transformations.
- **PySpark:** Distributed data processing.
- **Databricks:** Cloud-based data engineering and execution.
- **SQL:** Analytical queries and business insights.
- **Apache Airflow:** Workflow orchestration and job triggering.
- **AWS S3:** Cloud storage for raw, processed and analytics exports.
- **Parquet and CSV:** Data storage formats.

## Data Processing

The project processes approximately 3.33 million taxi trip records.

Key transformation steps:

1. Read raw Parquet data.
2. Remove records with negative fares.
3. Remove invalid pickup and drop-off timestamps.
4. Remove duplicate records.
5. Calculate trip duration.
6. Extract pickup date and pickup hour.
7. Remove invalid trip durations.
8. Generate daily aggregated metrics.
9. Save processed data in Parquet format.

### Data Quality

- Original records: 3,336,716
- Final processed records: 3,279,482
- Records removed: 57,234

Validation checks ensure that the processed dataset is not empty and contains no negative fares or invalid trip durations.

## SQL Analytics

SQL analysis was performed to understand taxi trip patterns and revenue distribution.

Key analysis includes:

- Revenue by pickup hour.
- Payment type distribution.
- Top pickup and drop-off locations.
- Average trip duration by hour.
- Daily revenue trends.
- Borough-level revenue analysis.
- Trip distribution across boroughs.

### Key Findings

- 6 PM recorded the highest hourly revenue.
- Manhattan accounted for approximately 86.78% of trips.
- Manhattan and Queens together accounted for approximately 96.25% of trips.
- JFK Airport was the leading pickup zone by trip count.

## Workflow Orchestration

Apache Airflow orchestrates the ETL workflow by triggering a Databricks Job.

The Airflow DAG includes:
- Databricks job execution.
- Two retries in case of failure.
- A two-minute retry delay.

The Databricks job executes the PySpark ETL notebook.

## AWS Integration

AWS S3 is used to store project data exports:

- `raw/` – Raw taxi dataset.
- `processed/` – Processed Parquet data.
- `analytics/` – Daily taxi metrics CSV.

**Note:** Files were uploaded manually to S3. Automated Databricks-to-S3 integration is not currently implemented.

## Future Improvements

- Automate cloud data ingestion.
- Implement automated S3 data loading.
- Add more advanced data quality checks.
- Integrate a cloud data warehouse such as Snowflake.

## Project Status

Core ETL processing, data validation, SQL analytics and Airflow-to-Databricks orchestration have been implemented successfully.

