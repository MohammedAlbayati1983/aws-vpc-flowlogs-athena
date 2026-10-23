# Project Requirements

Creating a Data Ingestion and Delivery Stream to Store and Search VPC Flow Logs for Monitoring/Security Purposes.

### Extended Requirements (Based on Architecture Design):
- **VPC Flow Logs:** Capture all network traffic in a specific VPC.
- **Streaming Pipeline:** Send logs to CloudWatch, then to Kinesis Data Streams, and finally to Kinesis Firehose.
- **Data Transformation:** Use a Lambda function to decompress and format the logs for Athena compatibility.
- **Storage:** Store the processed logs in an S3 Source Bucket.
- **Security Analytics:** Use Amazon Athena to query the logs for IPs with repeated rejected connections, excessive SSH attempts, or other security anomalies.