---
title: "AWS Portal/CLI"
description: "AWS Portal/CLI which came handy at some point"
date: "2026-01-23"
tags: ["stub"]
draft: false
---

# CLI

## Cloudtrail
Get who accessed a the value of an AWS secret in the last 7 days 
```bash
SECRET_MATCH="<secret_name>"
aws cloudtrail lookup-events \
  --region eu-central-1 \
  --lookup-attributes AttributeKey=EventName,AttributeValue=GetSecretValue \
  --start-time "$(date -u -v-7d +%Y-%m-%dT%H:%M:%SZ)" \
  --output table \
  --query "Events[?Resources[0].ResourceName!=null && contains(Resources[0].ResourceName, \`$SECRET_MATCH\`)].{Time:EventTime,User:Username,Secret:Resources[0].ResourceName}"
```

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

## Secret Manager
```bash
# List all secrets which have no custom key set
aws secretsmanager list-secrets --query 'SecretList[?KmsKeyId==null].[Name,ARN]' --output table
```

## VPC
List all assigned IPs in subnet `subnet-abcxyz`
```bash
aws ec2 describe-network-interfaces --filters "Name=subnet-id,Values=subnet-abcxyz" --query 'NetworkInterfaces[*].PrivateIpAddress'
```

# Portal

## Cloudwatch Log Insights

**Analyze Lambda processing times**
```bash
filter @type = "REPORT" 
| stats round(avg(@duration)/1000) as avg_duration, round(max(@initDuration)/1000) as max_init, count(@requestId) as num_requests by bin(1h)
```

**Search for certain log message**
```bash
fields @timestamp, @message, @logStream, @log
| filter @message like /ERROR/
| sort @timestamp desc
| limit 10000
```

**Listing the most frequent errors**
```bash
fields @timestamp, @message
| filter level = "ERROR"
| stats count() as occurences by message
| sort occurences desc
```
