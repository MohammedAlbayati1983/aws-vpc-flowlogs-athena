# Design Decisions & Architecture Notes

## 1. Data Pipeline Design
- **CloudWatch to Kinesis:** We used a CloudWatch Subscription Filter to stream logs in near real-time to Kinesis Data Streams (KDS), avoiding the need to poll S3.
- **Kinesis Firehose:** Firehose was chosen to deliver the data to S3 without writing custom code for batching or retries.
- **Lambda Transformation:** The Lambda function is essential because CloudWatch sends logs in Base64-encoded, Gzip-compressed format. Lambda decompresses and formats them into newline-delimited text, which Athena can read directly.

## 2. S3 Bucket Strategy
- **Source Bucket:** Stores the raw flow logs in their processed text format.
- **Destination Bucket:** Used exclusively by Athena to store query results (CSV files). This separation follows the "Data Lake" best practice.

## 3. Athena Table Schema
- The Athena table was created using standard VPC Flow Log fields. We used `ROW FORMAT DELIMITED` and `FIELDS TERMINATED BY ' '` (space) because the logs are space-separated.
- The location points to the Source Bucket where Firehose delivers the logs.

## 4. Security Query Examples
- **Finding malicious IPs:** 
  ```sql
  SELECT srcaddr, COUNT(*) as request_count
  FROM flowlogs_db.vpc_flow_logs
  WHERE action = 'REJECT'
  GROUP BY srcaddr
  ORDER BY request_count DESC;