# Data engineering portfolio

Three independent, open-source projects covering the data engineering stack:
streaming ingestion, batch warehouse modeling, and a managed lakehouse with
data-quality monitoring. All of them run free - locally or on free tiers - and
all of them are CI-tested.

## [de-energy-streaming](https://github.com/kaeldrin-gh/de-energy-streaming)

Streaming lakehouse for German day-ahead power prices.

`Python · PySpark · Spark Structured Streaming · Kafka · Apache Iceberg · Airflow · PostgreSQL · Grafana · Terraform · Docker`

- Kafka → Spark → Iceberg with revision-aware MERGE ingestion and a dead-letter queue
- Airflow orchestration, freshness SLA checks, operations runbook
- 2,328 hours of real market data analyzed (duck curve, negative-price patterns)
- Live showcase: [de-energy-streaming](https://kaeldrin-gh.github.io/de-energy-streaming/)

## [nl-energy-warehouse](https://github.com/kaeldrin-gh/nl-energy-warehouse)

Dutch power-price and weather warehouse.

`Python · SQL · dbt · DuckDB · PostgreSQL · Power BI · GitHub Actions · FastAPI`

- 58,500+ delivery hours with incremental dbt models and revision-aware reprocessing
- Model contracts, SCD2 revision snapshots and quality tests (uniqueness, exchange limits, cross-source alignment), built on PostgreSQL 17 in CI
- Live report: [nl-energy-warehouse](https://kaeldrin-gh.github.io/nl-energy-warehouse/report.html)

## [databricks-energy-quality](https://github.com/kaeldrin-gh/databricks-energy-quality)

Data-quality monitoring lakehouse on Databricks.

`Python · SQL · Unity Catalog · Delta Lake · Lakeflow pipelines · Workflows · Declarative Automation Bundles`

- Medallion lakehouse with pipeline expectations and revision-aware dedupe
- Three-task workflow whose quality checks fail the job when data is unhealthy
- Everything deployed as code, dashboard included
- Screenshots and architecture: [databricks-energy-quality README](https://github.com/kaeldrin-gh/databricks-energy-quality#what-it-looks-like)

## How they fit together

- One domain (European power markets) on three platforms: self-hosted streaming,
  local batch analytics engineering, managed lakehouse
- The same correctness idea everywhere: idempotent ingestion, one row per
  `(region, delivery time)`, newest revision wins
- MIT-licensed, no paid services, CI on every push
