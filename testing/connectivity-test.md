# Validation & Security Analytics Tests

| # | Test Description | Expected Result | Status |
|---|------------------|-----------------|--------|
| 1 | EC2 Instance Ping | Timeout (ICMP blocked by SG) | ✅ Passed |
| 2 | EC2 SSH Connection (Port 22) | Success (when SG allows) | ✅ Passed |
| 3 | VPC Flow Logs Generation | Logs appear in CloudWatch Log Group | ✅ Passed |
| 4 | CloudWatch to Kinesis | Subscription filter streams data | ✅ Passed |
| 5 | Firehose to S3 | Data appears in Source Bucket | ✅ Passed |
| 6 | Lambda Transformation | Logs are decompressed and formatted | ✅ Passed |
| 7 | Athena Query (Rejected IPs) | Successfully lists IPs with 'REJECT' action | ✅ Passed |