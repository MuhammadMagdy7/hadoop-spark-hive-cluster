# hadoop-spark-hive-cluster 🚀

## Overview
This project is a fully integrated, simulated Big Data cluster running entirely on local machines using `Docker Compose`. This environment is designed to be ready for testing data pipelines, performing batch processing, and applying data engineering concepts.

## Tech Stack
* **Storage:** Hadoop Distributed File System (HDFS)
* **Resource Management:** YARN (Yet Another Resource Negotiator)
* **Data Warehouse:** Apache Hive 4
* **Metadata Database:** PostgreSQL (for Hive Metastore)
* **Processing Engine:** Apache Spark (Master, Workers, & History Server)

## Prerequisites
* Docker and Docker Compose installed on your machine.
* An operating system that supports PowerShell or Bash commands.

## Setup & Installation

**1. Download the PostgreSQL JDBC Driver:**
You must download the driver and place it in the `lib` directory for the `hive-metastore` service to start successfully.

```bash
mkdir lib
Invoke-WebRequest -Uri "[https://jdbc.postgresql.org/download/postgresql-42.7.3.jar](https://jdbc.postgresql.org/download/postgresql-42.7.3.jar)" -OutFile "lib\postgresql-42.7.3.jar"

(Note: If you are using Linux/Mac, you can use wget instead of Invoke-WebRequest).
```
2. Start the Cluster:
```bash
Bash
docker compose up -d
3. Initialize Spark Logs Directory:
On the first run, you need to create a dedicated directory inside HDFS so the spark-history-server can read logs without crashing:
```
```bash
Bash
docker exec -it namenode hdfs dfs -mkdir -p /spark-logs
docker compose up -d --force-recreate spark-history-server
```

Web UIs
Once all containers are up and running, you can monitor your cluster via the following links in your browser:


Hadoop NameNode: http://localhost:9870

YARN ResourceManager: http://localhost:8088

Spark Master: http://localhost:8080

Spark History Server: http://localhost:18080