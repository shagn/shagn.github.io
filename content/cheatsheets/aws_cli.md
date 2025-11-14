---
title: "AWS"
date: "2025-11-13"
tags: ["stub"]
draft: false
---

# CLI

## EC2
```bash
aws ec2 start-instances --instance-ids <instance id>
aws ec2 reboot-instances --instance-ids <instance id>
aws ec2 stop-instances --instance-ids <instance id>
```

## S3
```bash
aws s3 ls  
aws s3 sync <old_s3_uri> <new_s3_uri>  
aws s3 rm <s3_uri> # add --recursive to avoid being prompted for confirmation for every file
aws s3 rm s3://some-bucket-name/ --recursive --exclude "*" --include "*.json" --dryrun  # delete all JSON files from a bucket
```

## VPC

List all assigned IPs in subnet `subnet-abcxyz`

```bash
aws ec2 describe-network-interfaces --filters "Name=subnet-id,Values=subnet-abcxyz" --query 'NetworkInterfaces[*].PrivateIpAddress'
```

# Portal

## Cloudwatch Log Insights

**Analyze Lambda processing times**
```
filter @type = "REPORT" 
| stats round(avg(@duration)/1000) as avg_duration, round(max(@initDuration)/1000) as max_init, count(@requestId) as num_requests by bin(1h)
```
**Search for certain log message**
```
fields @timestamp, @message, @logStream, @log
| filter @message like /ERROR/
| sort @timestamp desc
| limit 10000
```

**Listing the most frequent errors**
fields @timestamp, @message
| filter level = "ERROR"
| stats count() as occurences by message
| sort occurences desc
