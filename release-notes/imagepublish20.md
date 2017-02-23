---
layout: default
title: Lambda Image Publish 2.0 release
---
# Lambda Image Publish 2.0

### Table of contents
* [General changes](#general-changes)
* [Issues](#issues)

## General changes
Lambda function depends on a S3 configuration file (json) that is pointed out via the event. The structure of the 
configuration file is depicted below. Note that `accesKeyId`, `secretAccessKeyId` and `region` are optional. If not 
specified, lambda user needs permissions to access the source and target buckets.

**Configuration file**

```json
{
    "sourceBucket": "writer-internal-images-test",
    "targetBucket": "writer-public-images-test",
    "accessKeyId": "*******",
    "secretAccessKeyId": "*******",
    "region": "eu-west-1"    
}
```

## Issues  

### New Feature
* [LIP-2] - Lambda ImagePublish need to read config from S3