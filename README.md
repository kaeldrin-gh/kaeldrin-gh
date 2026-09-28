# Data engineering portfolio

Four independent, open-source projects covering the data engineering stack:
change data capture into a cloud warehouse, streaming ingestion, batch
warehouse modeling, and a managed lakehouse with data-quality monitoring. All
of them run free - locally or on free tiers - and all of them are CI-tested.

## [nl-parliament-warehouse](https://github.com/kaeldrin-gh/nl-parliament-warehouse)

Dutch House of Representatives votes, from the parliament's own change feed.

`Python · SQL · BigQuery · dbt · DuckDB · Terraform · GitHub Actions`

- Change data capture from a public change feed: checkpoints, tombstones, and a snapshot bootstrap that loses nothing between snapshot and feed
- Append-only raw layer on the BigQuery sandbox (no DML, 60-day table expiry, lifetime storage quota) with renewal and a storage ledger
- dbt dimensional model (votes, decisions, cases, party membership over time) with enforced contracts, 108 data tests and a unit test, on DuckDB in CI and BigQuery daily
- Terraform and keyless GitHub Actions access through Workload Identity Federation
- Live report: [nl-parliament-warehouse](https://kaeldrin-gh.github.io/nl-parliament-warehouse/)

## [de-energy-streaming](https://github.com/kaeldrin-gh/de-energy-streaming)

Streaming lakehouse for German day-ahead power prices.

`Python · PySpark · Spark Structured Streaming · Kafka · Apache Iceberg · Airflow · PostgreSQL · Grafana · Terraform · Docker · GitHub Actions`

- Kafka → Spark → Iceberg with revision-aware MERGE ingestion and a dead-letter queue
- Airflow orchestration, freshness SLA checks, daily Iceberg compaction and snapshot expiry, operations runbook
- 2,712 hours of real market data analyzed (duck curve, negative-price patterns)
- Live showcase: [de-energy-streaming](https://kaeldrin-gh.github.io/de-energy-streaming/)

## [nl-energy-warehouse](https://github.com/kaeldrin-gh/nl-energy-warehouse)

Dutch power-price and weather warehouse.

`Python · SQL · dbt · DuckDB · PostgreSQL · Power BI · GitHub Actions · FastAPI`

- 58,000+ delivery hours (since January 2020) with incremental dbt models and revision-aware reprocessing
- Model contracts, SCD2 revision snapshots and quality tests (uniqueness, exchange limits, cross-source alignment), validated on DuckDB and PostgreSQL 17 in CI
- dbt Semantic Layer metrics and a read-only FastAPI service over the marts
- Live report: [nl-energy-warehouse](https://kaeldrin-gh.github.io/nl-energy-warehouse/report.html)

## [databricks-energy-quality](https://github.com/kaeldrin-gh/databricks-energy-quality)

Data-quality monitoring lakehouse on Databricks.

`Python · PySpark · SQL · Unity Catalog · Delta Lake · Lakeflow pipelines · Workflows · Declarative Automation Bundles · GitHub Actions`

- Medallion lakehouse with pipeline expectations and revision-aware dedupe
- Three-task workflow whose quality checks fail the job when data is unhealthy
- Everything deployed as code, dashboard included
- CI/CD in GitHub Actions: tests, bundle validate, deploy and dashboard publish on every push to main; the ingest task retries before failing
- Screenshots and architecture: [databricks-energy-quality README](https://github.com/kaeldrin-gh/databricks-energy-quality#what-it-looks-like)

## How they fit together

- Four platforms: a cloud warehouse (BigQuery), self-hosted streaming, local
  batch analytics engineering, and a managed lakehouse
- The same correctness idea everywhere: idempotent ingestion, one row per
  entity version, newest revision wins
- Real public data from the Netherlands and Germany: power markets and parliament
- MIT-licensed, no paid services, CI on every push
