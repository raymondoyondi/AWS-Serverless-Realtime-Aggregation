# 🛢️ AWS Serverless Real-time Aggregation Pipeline

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![AWS: Lambda](https://img.shields.io/badge/AWS-Lambda-orange?logo=amazon-aws)](https://aws.amazon.com/lambda/)
[![AWS: DynamoDB](https://img.shields.io/badge/AWS-DynamoDB-blue?logo=amazon-dynamodb)](https://aws.amazon.com/dynamodb/)

A near real-time, scalable, and fault-tolerant serverless data aggregation pipeline built on AWS. This project implements a **distributed Map-Reduce pattern** to process high-velocity data streams with exactly-once processing guarantees.

## 🚀 Overview

Traditional aggregation often requires persistent clusters (like EMR or Kinesis Analytics). This project offers a **100% serverless alternative** that scales to zero when idle and expands instantly to handle massive throughput.

### Key Features
* **Map-Reduce Architecture:** Leverages AWS Lambda to parallelize data processing (Map) and aggregate results (Reduce) into DynamoDB.
* **Exactly-Once Processing:** Implements idempotency logic to ensure data is neither lost nor duplicated during retries.
* **Dynamic Scaling:** Automatically adjusts to workload spikes without manual intervention.
* **Fault Tolerance:** Built-in error handling and dead-letter queues (DLQ) for resilient stream processing.

## 🏗️ Architecture

The pipeline follows a structured flow from ingestion to finalized aggregation:

1.  **Ingestion:** Data enters via Amazon Kinesis or SQS.
2.  **Mapper (Lambda):** Validates, transforms, and shards the incoming data.
3.  **Aggregation (DynamoDB):** Uses atomic counters and conditional updates to perform real-time state management.
4.  **Reducer (Lambda):** Triggered by DynamoDB Streams to finalize aggregations or move data to long-term storage (S3/Redshift).

## 🛠️ Tech Stack
* **Compute:** AWS Lambda
* **Database:** Amazon DynamoDB (with Streams enabled)
* **Orchestration:** AWS Step Functions (Optional/Configurable)
* **Messaging:** Amazon Kinesis / SQS
* **IaC:** AWS SAM / Serverless Framework

## ⚙️ Setup & Deployment

### Prerequisites
* AWS CLI configured with appropriate permissions.
* Node.js/Python (depending on your specific implementation)
* SAM CLI installed.

### Deployment Steps
1. **Clone the repository:**
   ```bash
   git clone [https://github.com/raymondoyondi/AWS-Serverless-Realtime-Aggregation.git](https://github.com/raymondoyondi/AWS-Serverless-Realtime-Aggregation.git)
   cd AWS-Serverless-Realtime-Aggregation

2. **Build the application:**
   ```bash
   sam build
   ```
   
3. **Deploy to AWS:**
   ```bash
   sam deploy --guided
   ```bash
  
## 📊 Performance & Scalability
Because the system is serverless, the throughput is primarily governed by:

*   **DynamoDB WCU/RCU:** Configure for On-Demand for maximum elasticity.
*   **Lambda Concurrency:** Ensure your account limits allow for the desired burst capacity.

## 🤝 Contributing
Contributions are what make the open-source community such an amazing place to learn, inspire, and create. Any contributions you make are **greatly appreciated**.

1.  Fork the Project
2.  Create your Feature Branch (`git checkout -b feature/AmazingFeature`)
3.  Commit your Changes (`git commit -m 'Add some AmazingFeature'`)
4.  Push to the Branch (`git push origin feature/AmazingFeature`)
5.  Open a Pull Request

## 📄 License
Distributed under the MIT License. See `LICENSE` for more information.
