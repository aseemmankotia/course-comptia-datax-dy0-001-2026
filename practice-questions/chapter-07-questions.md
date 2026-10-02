## Chapter 7: Data Ingestion, Storage, and Pipeline Architecture — Practice Questions

**Q1.** A company ingests raw JSON clickstream data into cloud storage, then loads it unchanged into a cloud data warehouse where analysts write SQL to transform it into fact tables. Which pattern does this describe?

A) ETL
B) CDC
C) Lambda architecture
D) ELT

<details>
<summary>Answer</summary>

**Correct: D**

Extract and Load happen first with no transformation, and Transform happens inside the warehouse using its compute — this is the defining trait of ELT.

**Why the others are wrong:**
- ETL requires transformation before loading into the target system, which did not happen here.
- CDC refers to capturing row-level changes from a source database, not a general load-then-transform pattern.
- Lambda architecture refers to combining batch and speed layers, unrelated to this transform-location question.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q2.** A fraud detection system must flag suspicious transactions within 2 seconds of occurrence. Which ingestion approach BEST meets this requirement?

A) Nightly batch load into a data warehouse
B) Streaming ingestion with a message broker and stream processor
C) Micro-batch ETL job scheduled every hour
D) Manual CSV export and load

<details>
<summary>Answer</summary>

**Correct: B**

Sub-second to few-second latency requirements require continuous streaming ingestion (e.g., Kafka/Kinesis + stream processing), not scheduled batch windows.

**Why the others are wrong:**
- Nightly batch introduces up to 24 hours of latency, far exceeding the 2-second requirement.
- Hourly micro-batch still introduces minutes of latency, failing the near-real-time requirement.
- Manual export cannot meet any real-time SLA and is not a scalable pattern.

</details>

---

**Q3.** A source system adds a new optional field to its event payload. The pipeline currently fails validation because the field is unrecognized. Which is the BEST fix for handling this going forward?

A) Hardcode the pipeline to reject any payload with unknown fields
B) Manually edit the raw files to remove the new field before ingestion
C) Implement schema evolution rules that allow additive, backward-compatible changes
D) Switch the pipeline from streaming to batch to avoid the issue

<details>
<summary>Answer</summary>

**Correct: C**

Schema evolution policies (e.g., allow new nullable columns, use a schema registry with backward compatibility mode) let pipelines gracefully absorb additive schema drift.

**Why the others are wrong:**
- Rejecting unknown fields is what caused the failure in the first place — not a fix.
- Manually editing raw files does not scale and destroys source fidelity.
- Switching processing mode does not address the underlying schema compatibility problem.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q4.** A team needs to store petabytes of raw video, log, and JSON files cheaply for future, not-yet-defined ML use cases, with no need for immediate schema enforcement. Which storage architecture BEST fits?

A) Data warehouse
B) Data lake
C) Relational OLTP database
D) Lakehouse with strict ACID enforcement

<details>
<summary>Answer</summary>

**Correct: B**

Data lakes store raw, schema-less data of any type cheaply using schema-on-read, ideal for undefined future analytics/ML use cases.

**Why the others are wrong:**
- A data warehouse requires structured schema-on-write and is optimized for BI, not raw multi-format storage.
- OLTP databases are built for transactional workloads, not bulk raw file storage.
- A lakehouse adds transactional/ACID structure which isn't needed when no schema is defined yet, and adds unnecessary overhead.

</details>

---

**Q5.** A team wants file-based storage that supports ACID transactions, time travel, and direct BI tool queries without a separate warehouse. Which architecture BEST satisfies this?

A) Traditional data lake
B) OLTP relational database
C) NoSQL document store
D) Data lakehouse (e.g., Delta Lake/Iceberg)

<details>
<summary>Answer</summary>

**Correct: D**

A lakehouse combines lake-style cheap file storage with warehouse-style ACID transactions, schema enforcement, and BI query support — exactly the stated requirements.

**Why the others are wrong:**
- A traditional data lake lacks native ACID guarantees and time travel.
- OLTP databases aren't designed for large-scale analytical file storage at this scale.
- NoSQL document stores don't provide ACID multi-table transactions or native BI query time-travel features.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q6.** In a data lake using schema-on-read, when is the schema actually applied to the data?

A) At write time, before the file lands in storage
B) At query/read time, when the data is accessed
C) Never — data lakes do not support schema
D) Only during nightly batch compaction jobs

<details>
<summary>Answer</summary>

**Correct: B**

Schema-on-read means raw files are stored as-is, and structure/schema is inferred or applied only when a query engine reads the data.

**Why the others are wrong:**
- Schema-on-write is the opposite pattern, used by warehouses, not lakes.
- Data lakes can and do support schema, just applied later than write time.
- Compaction jobs may rewrite files but schema application still happens at read/query time, not tied specifically to compaction.

</details>

---

**Q7.** A pipeline orchestration DAG has a task that writes to a target table. On failure and automatic retry, the task runs again and produces duplicate rows. What design flaw does this indicate?

A) The DAG scheduler is misconfigured
B) The source system has schema drift
C) The task is not idempotent
D) The pipeline is using ELT instead of ETL

<details>
<summary>Answer</summary>

**Correct: C**

Idempotent tasks produce the same result even if executed multiple times (e.g., via upsert/merge). Lack of idempotency is why retries cause duplicates.

**Why the others are wrong:**
- The scheduler correctly retrying the task is expected behavior, not a misconfiguration.
- Schema drift causes schema mismatch errors, not duplicate row insertion.
- ETL vs ELT choice does not determine whether retries cause duplication; idempotency does.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

**Q8.** What is the key distinction between schema drift and schema evolution in a data pipeline?

A) Schema drift is planned and managed change; schema evolution is unplanned and breaks pipelines
B) They are identical terms describing the same concept
C) Schema drift is unplanned/unexpected change from the source; schema evolution is the pipeline's managed process for handling such changes
D) Schema drift only applies to streaming; schema evolution only applies to batch

<details>
<summary>Answer</summary>

**Correct: C**

Schema drift refers to unexpected, uncontrolled changes to source data structure over time; schema evolution is the deliberate mechanism/policy a pipeline uses to accommodate such changes safely.

**Why the others are wrong:**
- This reverses the definitions — drift is the problem, evolution is the solution.
- They are related but distinct concepts, not synonyms.
- Both concepts apply regardless of batch or streaming processing mode.

> ⚠️ Frequently missed on the exam — read the options carefully.

</details>

---

