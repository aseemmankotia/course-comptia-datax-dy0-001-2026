## Chapter 7 Cheat Sheet — Data Ingestion, Storage, Pipeline Architecture

### Storage Architecture Comparison
| Feature | Data Lake | Data Warehouse | Lakehouse |
|---|---|---|---|
| Schema | Schema-on-read | Schema-on-write | Schema-on-write (enforced) |
| Data type | Raw, any format | Structured, curated | Raw + curated |
| Cost | Low | Higher | Low-medium |
| ACID transactions | No (native) | Yes | Yes |
| Use case | ML, unstructured, future use | BI, reporting | Both |
| Example tech | S3, ADLS, GCS | Snowflake, Redshift, BigQuery | Delta Lake, Iceberg, Hudi |

### ETL vs ELT
| | ETL | ELT |
|---|---|---|
| Transform location | External engine, before load | Inside target system, after load |
| Best for | Legacy on-prem warehouses, limited target compute | Modern cloud warehouses/lakehouses |
| Load speed | Slower (transform first) | Faster (load raw immediately) |
| Flexibility | Lower (schema decided upfront) | Higher (raw data preserved) |

### Batch vs Streaming
| | Batch | Streaming |
|---|---|---|
| Latency | Minutes-hours | Sub-second to seconds |
| Tooling | Airflow, scheduled Spark jobs | Kafka, Kinesis, Flink, Spark Structured Streaming |
| Failure handling | Rerun whole batch | Checkpointing, exactly-once/at-least-once semantics |
| Use case | Reports, nightly loads | Fraud detection, monitoring, alerts |

### Schema Drift vs Schema Evolution
- **Drift** = unplanned structural change from source (new/removed/renamed field, type change).
- **Evolution** = pipeline's managed policy to absorb drift safely (additive-only rules, schema registry compatibility modes: BACKWARD / FORWARD / FULL).
- Safe drift: new nullable column. Unsafe: type change, column removal, rename without mapping.

### Pipeline Orchestration Essentials
- DAGs define task dependencies; tasks should be **idempotent** (safe to retry — use UPSERT/MERGE, not blind INSERT).
- Retries + idempotency prevent duplicate writes on failure.
- Data versioning: table format time travel (Delta Lake log retention **30 days** default; VACUUM file retention **7 days** default).

### Data Quality in Pipelines
- Embed checks at ingestion: schema validation, null-rate thresholds, uniqueness, range checks.
- Quarantine/fail bad records — never silently load invalid data downstream.
- Common framework reference: Great Expectations-style declarative checks.

### Common Exam Traps
- Choosing ETL when scenario clearly implies cloud warehouse compute (should be ELT).
- Confusing schema-on-read (lake) with schema-on-write (warehouse).
- Assuming lakehouse = just a data lake (it adds ACID + schema enforcement).
- Missing that retries without idempotency cause duplicate data, not orchestration failure.
