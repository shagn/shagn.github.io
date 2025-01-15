---
title: "AWS CLI"
date: "2025-01-14"
tags: ["stub"]
draft: false
---

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
```

## VPC

List all assigned IPs in subnet `subnet-abcxyz`

```bash
aws ec2 describe-network-interfaces --filters "Name=subnet-id,Values=subnet-abcxyz" --query 'NetworkInterfaces[*].PrivateIpAddress'
```
