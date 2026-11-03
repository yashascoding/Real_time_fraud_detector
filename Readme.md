# Real-Time Fraud Detection System

![Real-time fraud detection architecture](<./WhatsApp Image 2026-11-02 at 9.46.19 PM.jpeg>)

A real-time fraud detection architecture designed for high-volume transaction monitoring. The system ingests transaction events, processes them in streaming fashion, combines ML-based anomaly detection with business rule checks, stores the results for downstream analysis, and exposes a live monitoring dashboard for fraud investigation.

## Architecture Overview

```text
PaySim Dataset
   |
   v
Apache Kafka
   |
   v
Apache Spark Structured Streaming
   |
   +------------------------------+
   |                              |
   v                              v
Fraud Detection Model          Fraud Rules
(Random Forest / XGBoost)   Unusual amounts and account behaviour
   |
   v
Fraud Risk Assessment
(Legitimate / Suspicious / High Risk)
   |
   +----------------------+
   |                      |
   v                      v
MongoDB             Hadoop HDFS
Transactions and    Historical transaction storage
fraud alerts
   |
   v
Fraud Monitoring Dashboard
Live transaction feed, fraud alerts, risk scores and analytics
```

## Data Flow

1. Historical transaction data is loaded from the PaySim dataset.
2. Streaming transaction events are published into Apache Kafka.
3. Apache Spark Structured Streaming consumes the data continuously.
4. The data is processed in real time by:
   - a machine learning fraud detection model
   - custom fraud rules based on abnormal transaction characteristics
5. Each transaction receives a fraud risk score or label such as:
   - Legitimate
   - Suspicious
   - High Risk
6. Alerts and transaction records are stored in MongoDB.
7. Historical data is retained in Hadoop HDFS for replay, training, and auditing.
8. The Fraud Monitoring Dashboard presents live metrics, risk scores, alerts, and transaction analytics.

## Core Components

### 1. PaySim Dataset
The system starts with a synthetic financial dataset representing simulated mobile money transactions. It provides large-scale historical transaction patterns needed for fraud analysis and model evaluation.

### 2. Apache Kafka
Kafka acts as the real-time event backbone. It captures incoming transaction events and allows downstream systems to process them asynchronously and at scale.

### 3. Apache Spark Structured Streaming
This layer performs continuous processing of streaming data. It cleanses, transforms, and enriches transaction records before passing them to the detection logic.

### 4. Fraud Detection Model
The fraud detection model uses supervised learning techniques such as:
- Random Forest
- XGBoost

These models learn from historical transaction patterns to identify suspicious activity based on behavior and anomaly signals.

### 5. Fraud Rules Engine
Alongside the ML model, rule-based checks detect suspicious patterns such as:
- unusual transaction amounts
- abnormal spending behavior
- account-level anomalies
- uncommon transaction sequences

### 6. Fraud Risk Assessment
This stage combines model output with rule-based findings to classify each transaction as legitimate, suspicious, or high-risk.

### 7. MongoDB
MongoDB stores:
- transaction records
- fraud alerts
- risk classifications
- investigation metadata

### 8. Hadoop HDFS
HDFS stores historical transaction data for:
- model retraining
- trend analysis
- forensic investigation
- long-term archival

### 9. Fraud Monitoring Dashboard
The dashboard provides:
- live transaction monitoring
- fraud alerts
- risk scores
- analytics summaries
- operational visibility for fraud teams

## Key Features

- Real-time transaction processing
- High-throughput streaming architecture
- Hybrid fraud detection combining ML and business rules
- Risk-based classification for each transaction
- Scalable storage using MongoDB and HDFS
- Monitoring and alerting through a centralized dashboard
- Suitable for financial services and digital payment use cases

## Benefits

- Detects fraud quickly before transactions are fully completed
- Reduces manual investigation workload
- Supports both anomaly-based and policy-based detection
- Scales to large transaction volumes
- Provides a clear operational view for fraud analysts

## Typical Use Case

This architecture is suitable for digital payment platforms, banking systems, e-wallet providers, and financial fraud operations teams that need real-time monitoring and proactive risk control.

## Summary

The project represents a modern fraud detection pipeline that brings together streaming data processing, machine learning, rule-based detection, persistent storage, and live monitoring into a single end-to-end architecture.
