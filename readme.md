# Stripe Project - OLTP, OLAP, and NoSQL Architecture

---

## 📚 Table of Contents
- [🎯 Context and Goals](#-context-and-goals)
- [🛠️ Overall Architecture](#️-overall-architecture)
- [💾 Databases and Technologies](#-databases-and-technologies)
- [🔄 Data Pipeline and Flow](#-data-pipeline-and-flow)
- [☁️ Cloud Infrastructure and Monitoring](#️-cloud-infrastructure-and-monitoring)
- [🔒 Security and Compliance](#-security-and-compliance)
- [📝 Notes and Next Steps](#-notes-and-next-steps)
- [📂 Annexes](#-annexes)

---

## 🎯 Context and Goals
Stripe processes millions of transactions daily, requiring a scalable infrastructure to handle:
- **OLTP (Online Transaction Processing):** Efficient real-time transaction processing.
- **OLAP (Online Analytical Processing):** Complex data analysis and reporting.
- **NoSQL:** Management of semi-structured and unstructured data for use cases like fraud detection and customer personalization.

This project aims to design an integrated and scalable architecture to address these needs using **PostgreSQL**, **Snowflake**, and **MongoDB** on **AWS**.

---

## 🛠️ Overall Architecture
The architecture revolves around three key components:
1. **OLTP:** PostgreSQL (or NeonDB for a managed cloud solution).
2. **OLAP:** Snowflake for advanced analytics.
3. **NoSQL:** MongoDB for semi-structured data (ML features, error logs, etc.).

### 🌟 Architecture Diagram
*[View Architecture Diagram (PDF)](STRIPE_ARCHITECTURE.pdf)*

---

## 💾 Databases and Technologies

### 1. **OLTP - PostgreSQL**
- **Purpose:** Real-time transaction management.
- **Structure:** Relational database with normalized tables (e.g., Transaction, Customer, Merchant).
- **Deployment Options:**
  - Local: Using Docker for development.
  - Cloud: Using NeonDB for a managed database.

### 2. **OLAP - Snowflake**
- **Purpose:** Historical data analysis and reporting.
- **Structure:** Star schema (fact and dimension tables).
- **Use Cases:**
  - Fact tables for transactions.
  - Dimension tables: customer, product, location, etc.

### 3. **NoSQL - MongoDB**
- **Purpose:** Storage for unstructured data.
- **Primary Collections:**
  - Transactions
  - Error logs
  - ML features for training

---

## 🔄 Data Pipeline and Flow

### **Ingestion**
- **Kafka:** Real-time event ingestion.
- **Debezium:** Change Data Capture (CDC) for syncing PostgreSQL with Snowflake and MongoDB.
- **S3:** Intermediate storage for raw data.

### **ETL Transformation**
- **Spark:** Cleaning, enrichment, and aggregation of data.
- **Airbyte:** Synchronizing data with Snowflake and MongoDB.

### **Analytics and Reporting**
- Processed data is stored in Snowflake and visualized using BI tools like Tableau or Power BI.

### **Machine Learning**
- **MLflow:** Training and tracking ML models for:
  - Fraud detection.
  - Customer personalization.
- **ML Pipeline:** Models are deployed to production and monitored with Evidently.AI.

---

## ☁️ Cloud Infrastructure and Monitoring

### **AWS Cloud**
- **S3:** Backup of raw data and ML models.
- **CloudWatch:** Performance monitoring.

### **Model Monitoring**
- **Airflow:** Workflow orchestration and alerts.
- **Evidently.AI:** Monitoring model drift in production.

---

## 🔒 Security and Compliance

### **Access Control**
- **IAM roles** for AWS resources.
- **Role-Based Access Control (RBAC)** for PostgreSQL, Snowflake, and MongoDB.
- **SSO** authentication.

### **Encryption**
- **In-transit:** TLS.
- **At-rest:** AES-256 encryption.

### **Compliance**
- User action logging.
- Automatic backups and Point-In-Time Recovery (PITR).

---

## 📝 Notes and Next Steps

### **Data Replication**
- Set up automatic replication in MongoDB and Snowflake.
  
### **ML Pipeline Improvement**
- Test additional models for fraud detection.

### **Production Migration**
- Migrate local PostgreSQL to NeonDB for scalability.

  ---

## 📂 Annexes

- Diagrams (achitecture, OLTP, OLAP, NoSQL)
- Notebook: Database creation and query examples.
- Technical documentation
