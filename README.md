# AWS VPC Flow Logs & Athena Security Analytics

## 📌 Overview
A comprehensive security and monitoring project that captures VPC Flow Logs, streams them through Kinesis, and uses AWS Lambda to transform the data before storing it in Amazon S3. Finally, Amazon Athena is used to query the logs for security insights, such as identifying malicious IPs and repeated rejected connections.

## 🏗️ Architecture Diagram
![Architecture Diagram](./architecture/architecture-diagram.png)

## 🎯 Requirements Covered
1. **Data Ingestion:** Capturing VPC Flow Logs and sending them to CloudWatch Logs.
2. **Data Streaming:** Using CloudWatch Subscription Filters to stream logs to Amazon Kinesis Data Streams (KDS).
3. **Data Transformation:** Using Amazon Data Firehose with an AWS Lambda function to decompress and format the data (Base64 to JSON/Text).
4. **Data Storage:** Storing the processed logs in an Amazon S3 Source Bucket.
5. **Security Analytics (Athena):** Creating an external table in Athena to query the logs and identify:
   - IP addresses with repeated rejected connections (e.g., port scanning or DDoS attempts).
   - Excessive SSH login attempts (if applicable).
   - General network traffic patterns.

## 🔧 AWS Services Used
| Service | Purpose |
|---------|---------|
| Amazon VPC | Network isolation and Flow Logs generation |
| Amazon EC2 | Web server generating network traffic |
| Amazon CloudWatch | Log group for Flow Logs & Subscription Filter |
| Amazon Kinesis Data Streams | Real-time data streaming |
| Amazon Data Firehose | Data delivery to S3 with Lambda transformation |
| AWS Lambda | Decompressing and formatting logs |
| Amazon S3 (Source & Dest) | Storing raw logs and Athena query results |
| AWS IAM | Roles for VPC, CloudWatch, Firehose, and Lambda |
| Amazon Athena | Serverless SQL query service for log analysis |

## 📂 Repository Structure
```text
.
├── architecture/          # Architecture diagrams
├── screenshots/           # AWS Console screenshots
├── documentation/         # Requirements & design decisions
├── testing/               # Connectivity & validation tests
└── infrastructure-as-code/ # (Planned) Terraform implementation

```

