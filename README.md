![System Architecture](assets/Spotify_Data_Analysis.drawio.svg)
# 🎧 Real-Time Spotify Streaming Analytics Platform  
*End-to-End Streaming Data Pipeline with Kafka, Snowflake, dbt & Power BI*

---

## 1. Executive Summary

This project delivers a **fully automated, real-time analytics platform** that simulates Spotify user activity and transforms raw streaming events into **live, business-ready insights**.

The objective was to design and implement a **production-style streaming data architecture** capable of ingesting continuous event data, processing it through a structured transformation framework, and exposing real-time KPIs through an interactive **Power BI dashboard**.

The pipeline begins with a **Python-based data simulator** that generates Spotify-like streaming events at a rate of one record per second, mimicking real-world user behavior. Events are streamed via **Apache Kafka**, persisted in a **MinIO (S3-compatible) data lake**, and loaded into **Snowflake** as the analytical data warehouse. Data transformations are managed using **dbt** and structured using the **Medallion Architecture (Bronze, Silver, Gold)**. **Apache Airflow** orchestrates the entire workflow, while **Docker** containerizes all services for reproducibility and scalability.

The result is a real-time dashboard that provides visibility into **plays, user engagement, artist popularity, device usage, and geographic distribution**, demonstrating how modern data engineering tools can convert high-velocity event streams into actionable insights.

---

## 2. Business Problem

Music streaming platforms like Spotify generate **massive volumes of event data** every second—plays, skips, playlist adds, user activity, device usage, and geographic signals.

For stakeholders such as:
- Product managers  
- Marketing teams  
- Content & artist relations  
- Growth and engagement analysts  

the challenge is not data availability, but **turning continuous, raw streaming events into real-time insights** that answer questions like:

- Which artists and songs are trending *right now*?
- How are users engaging across devices (mobile, desktop, web)?
- Where is engagement geographically concentrated?
- Are users listening, skipping, or adding tracks to playlists?

Traditional batch pipelines fail to support these needs due to **latency and rigidity**.

**This project solves the problem of real-time visibility into streaming user behavior by building a scalable, automated streaming analytics pipeline.**

---

## 3. Methodology

### Real-Time Data Simulation
- Built a **Python-based Spotify event simulator**
- Generates one streaming event per second indefinitely
- Simulates:
  - User IDs
  - Song & artist metadata
  - Device types
  - Geographic locations
  - Engagement actions (plays, skips, playlist adds)

This allows realistic testing of streaming infrastructure without relying on proprietary APIs.

---

### Streaming & Data Ingestion
- Streamed simulated events into **Apache Kafka**
- Kafka acts as the real-time event backbone
- Events are serialized and published continuously to Kafka topics

---

### Data Lake Storage
- Kafka events are decoded into JSON format
- Persisted into **MinIO**, an S3-compatible object storage
- Serves as the **raw data lake layer**, enabling durability and replayability

---

### Data Architecture (Medallion Model)

Implemented a **three-layer Medallion Architecture** inside Snowflake:

#### 🥉 Bronze Layer
- Raw ingested JSON data from MinIO
- Minimal transformation
- Preserves original event structure for traceability

#### 🥈 Silver Layer
- Data cleaning and standardization using **dbt**
- Handled:
  - Schema enforcement
  - Data type casting
  - Timestamp normalization
  - Removal of malformed records

#### 🥇 Gold Layer
- Business-level aggregations and KPIs
- Optimized for analytics and BI consumption
- Metrics include:
  - Total plays
  - User engagement counts
  - Artist popularity
  - Device distribution
  - Geographic activity

---

### Orchestration
- **Apache Airflow** orchestrates:
  - Kafka → MinIO ingestion
  - MinIO → Snowflake loading
  - dbt transformations (Bronze → Silver → Gold)
- DAGs ensure:
  - Task dependencies
  - Scheduling
  - Error handling and retries

---

### Analytics & Visualization
- Gold-layer tables exposed in **Snowflake**
- Connected to **Power BI using DirectQuery**
- Enables **near real-time dashboard updates**
- Dashboard highlights:
  - Live KPIs (Plays, Users, Songs)
  - Top artists by total plays
  - Plays by device type
  - Geographic engagement map
  - Engagement behavior breakdown (plays, skips, playlist adds)

---

## 4. Tools & Skills Used

### 🐍 Python
- Real-time data simulation
- Event generation logic
- JSON serialization
- Data modeling for streaming use cases

---

### 📨 Apache Kafka
- Real-time event streaming
- Topic-based ingestion
- Decoupling producers and consumers
- High-throughput data pipelines

---

### 🪣 MinIO (S3-Compatible Data Lake)
- Object storage for raw streaming data
- Durable, scalable event persistence
- Acts as the raw data source for Snowflake ingestion

---

### 🗄️ Snowflake
- Cloud-native data warehouse
- Bronze, Silver, Gold data layers
- Scalable analytical storage
- Optimized for BI workloads

---

### 🧪 dbt
- SQL-based transformations
- Modular, version-controlled models
- Medallion Architecture implementation
- Data quality and business logic enforcement

---

### 🔄 Apache Airflow
- End-to-end pipeline orchestration
- DAG-based workflow management
- Dependency handling and scheduling
- Production-style automation

---

### 🐳 Docker
- Containerized all services:
  - Kafka
  - Airflow
  - MinIO
  - dbt
- Ensures reproducibility and environment consistency
- Simplifies local and production deployments

---

### 📊 Power BI
- DirectQuery for real-time analytics
- Data modeling and relationships
- DAX measures for KPIs
- Interactive dashboard design
- Business-focused data storytelling

---

### 🧱 Data Engineering Concepts
- Streaming data architectures
- Medallion Architecture
- Real-time analytics pipelines
- Separation of ingestion, transformation, and analytics layers
- Scalable and maintainable data systems

---

## 5. Results & Key Insights

### Dashboard Insights

- **Artist Popularity**  
  Identifies top-performing artists in real time based on total plays.

- **User Engagement Behavior**  
  Tracks how users interact with content—listening, skipping, or saving to playlists.

- **Device Usage Patterns**  
  Reveals engagement split across desktop, mobile, and web platforms.

- **Geographic Distribution**  
  Highlights regions with the highest streaming activity.

- **Live KPIs**  
  Enables stakeholders to monitor platform health and engagement as events occur.

---

## 6. Recommendations

1. **Use Real-Time Artist Metrics for Promotion Decisions**  
   Trending artists can be surfaced immediately for marketing or playlist placement.

2. **Monitor Skips vs Plays to Assess Content Quality**  
   High skip rates may indicate poor song-to-audience fit.

3. **Optimize Experiences by Device Type**  
   Device usage patterns can inform UX and feature prioritization.

4. **Extend with Time-Series Trends**  
   Adding minute-by-minute or hourly trend analysis would support anomaly detection and campaign tracking.

---

## 7. Conclusion

This project demonstrates how a **modern streaming data stack** can transform continuous event data into real-time, decision-ready insights.

By combining **Kafka, MinIO, Snowflake, dbt, Airflow, Docker, and Power BI**, the solution mirrors real-world production architectures used by data-driven companies. It showcases strong capabilities in **data engineering, analytics engineering, orchestration, and business intelligence**, while maintaining a clear focus on **business value and insight delivery**.

This platform serves as a scalable foundation for any real-time analytics use case beyond music streaming, including IoT, fintech, e-commerce, and user behavior tracking systems.
