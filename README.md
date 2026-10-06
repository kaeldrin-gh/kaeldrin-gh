# Data engineering portfolio

Five independent, open-source projects covering the data engineering stack:
a serverless data mesh on AWS, streaming ingestion, change data capture into a
cloud warehouse, batch warehouse modeling, and a managed lakehouse with
data-quality monitoring. All of them run free - locally or on free tiers - and
all of them are CI-tested.

## [polymer-research-lakehouse](https://github.com/kaeldrin-gh/polymer-research-lakehouse)

Data mesh on AWS for polymer research and industrial emissions.

`Python · PySpark · SQL · AWS CDK · S3 · Apache Iceberg · Glue · Athena · Lambda · Step Functions · ECS Fargate · Lake Formation · dbt · Docker · GitHub Actions`

- Research and sustainability domains that own their buckets, catalogs, loads and data products; a shared product joins them
- Incremental Iceberg MERGE from the 707 GB OpenAlex snapshot that scans 8% of it (859,181 works), plus a daily API feed
- SCD Type 2 over European Environment Agency releases in a Glue PySpark job; dbt with enforced contracts on ECS Fargate
- Lake Formation tag-based access, keyless GitHub OIDC deploys, cdk-nag, and a scoped CloudFormation execution policy
- Live report: [polymer-research-lakehouse](https://kaeldrin-gh.github.io/polymer-research-lakehouse/)

## [de-energy-streaming](https://github.com/kaeldrin-gh/de-energy-streaming)

Streaming lakehouse for German day-ahead power prices.

`Python · PySpark · Spark Structured Streaming · Kafka · Apache Iceberg · Airflow · PostgreSQL · Grafana · Terraform · Docker · GitHub Actions`

- Kafka → Spark → Iceberg with revision-aware MERGE ingestion and a dead-letter queue
- Airflow orchestration, freshness SLA checks, daily Iceberg compaction and snapshot expiry, operations runbook
- 2,712 hours of real market data analyzed (duck curve, negative-price patterns)
- Live showcase: [de-energy-streaming](https://kaeldrin-gh.github.io/de-energy-streaming/)

## [nl-parliament-warehouse](https://github.com/kaeldrin-gh/nl-parliament-warehouse)

Dutch House of Representatives votes, from the parliament's own change feed.

`Python · SQL · BigQuery · dbt · DuckDB · Terraform · GitHub Actions`

- Change data capture from a public change feed: checkpoints, tombstones, and a snapshot bootstrap that loses nothing between snapshot and feed
- Append-only raw layer on the BigQuery sandbox (no DML, 60-day table expiry, lifetime storage quota) with renewal and a storage ledger
- dbt dimensional model (votes, decisions, cases, party membership over time) with enforced contracts, 108 data tests and a unit test, on DuckDB in CI and BigQuery daily
- Terraform and keyless GitHub Actions access through Workload Identity Federation
- Live report: [nl-parliament-warehouse](https://kaeldrin-gh.github.io/nl-parliament-warehouse/)

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

- Five platforms: serverless AWS, self-hosted streaming, a cloud warehouse
  (BigQuery), local batch analytics engineering, and a managed lakehouse
- The same correctness idea everywhere: idempotent ingestion, one row per
  entity version, newest revision wins
- Real public data: Dutch and German power markets, the Dutch parliament, and
  European research and industrial emissions
- MIT-licensed, no paid services, CI on every push
