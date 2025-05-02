# **Amazon SP-Data Engineering Project**

In this project, we designed and implemented a modern data pipeline using **Databricks**, **Azure Blob Storage**, and the **Amazon Selling Partner API (SP-API)**, structured around the **Medallion Architecture**.

---

### **Project Architecture**
![Architecture Diagram](https://github.com/Mockbee/amazon-sp-data-engineering/blob/dev/Amazon%20SP%20Data%20Architecture%20Diagram.png)

---

### **About Dataset/API Used**

This project integrates data from the **Amazon Selling Partner API (SP-API)**:

1. **SP-API Orders API**  
   - Fetches Amazon order data using access tokens, LWA authentication, and SP credentials.  
   - Contains key order metadata like purchase dates, order status, buyer info, etc.
   - API can be accessed here [here](https://developer-docs.amazon.com/sp-api)

2. **Data is fetched as JSON** and transformed through multiple pipeline layers for analytics and reporting.

---

### **Services and Tools Used**

1. **Amazon Selling Partner API (SP-API):**  
   - OAuth 2.0 and AWS Signature v4 authentication.  
   - Accessed via Postman initially, then automated with Python code in Databricks.

2. **Azure Blob Storage:**  
   - Used to store Bronze (raw), Silver (transformed), and Gold (enriched) datasets.  
   - Accessed securely via Databricks using service principal authentication.

3. **Databricks:**  
   - Notebook-based development for fetching, transforming, and structuring SP-API data.  
   - Integrated with `dbutils.secrets` for secure token handling.  
   - Implements the Medallion Architecture using PySpark.

4. **Delta Lake:**  
   - Provides ACID-compliant storage, schema evolution, and time travel for Silver/Gold tables.

---

### **Project Execution Flow**

1. **Initial Authentication & API Fetching:**  
   - Tested API calls via Postman using `client_id`, `client_secret`, `refresh_token`, and AWS credentials.  
   - Implemented token generation and SP-API fetching using Python in Databricks.

2. **Bronze Layer (Raw Data Ingestion):**  
   - JSON responses from SP-API are stored as-is in Azure Blob Storage.  
   - Includes full raw payload for traceability.

3. **Silver Layer (Data Transformation):**  
   - Parsed raw JSON into flattened tables using PySpark.  
   - Added ingestion metadata and applied type casting.

4. **Gold Layer (Data Enrichment):**  
   - Business-specific aggregates and cleaned datasets stored in Delta format.  
   - Ready for analytics or dashboarding.

5. **Databricks Orchestration:**  
   - Modular notebooks manage token generation, ingestion, transformation, and archival.  
   - Uses widgets and secrets for parameterization and security.
   - Modular notebooks manage token generation, ingestion, transformation, and archival.

Uses widgets and secrets for parameterization and security.

Scheduled and managed using Databricks Workflows for automation and reliability.
---

### **Key Features**

- **Secure Authentication:** OAuth 2.0 and AWS SigV4 implemented correctly for Amazon SP-API.  
- **Structured Pipeline:** Follows Medallion Architecture for scalable processing.  
- **Optimized Storage Formats:** Uses Delta (Bronze), Delta (Silver), and Delta (Gold).  
- **Databricks + Azure Integration:** Full lifecycle from ingestion to storage using Azure-native services.  
- **Modular Design:** Separate notebooks for each pipeline stage for flexibility and reusability.

---

This project showcases modern data engineering practices to ingest and process third-party e-commerce data into cloud-native, analytics-ready formats.
