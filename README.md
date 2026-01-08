An automated pipeline for Spotify Analysis, where every component runs on its own from data ingestion all the way to data updates. We get the raw data, store it in data warehouse
which we will use Snowflake. We clean the data in three stages using the Medallion Architecture. Then we connect everything to Power BI to build a dashboard for real insights. 
We will use Kafka for streaming, MinIO for data lake storage, airflow for orchestration dbt for transformation and docker to containerize the whole architecture. 
* We will use a Python code simulator to generate our data where every 1 second a new row is generated to simulate realtime data.
