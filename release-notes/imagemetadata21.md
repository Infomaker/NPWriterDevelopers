---
layout: default
title: Lambda Image Metadata 2.1 release
---
# Lambda Image Metadata 2.1

### Table of contents
* [General changes](#general-changes)
* [Issues](#issues)

## General changes
Lambda function uses a configuration in S3. The `event` must contain parameter for S3 configuration file and S3 bucket 
name in which configuration resides in.

**Configuration file**  

```json
{
    "bucket": "writer-image-upload", 
    "accessKeyId": "access-key-to-s3",
    "secretAccessKeyId": "secret-access-key-to-s3",
    "region": "region-to-s3",
    "charsetLookup": [
        {
            "charset": "mac",
            "templateName": "copyrightnotice",
            "templateValue": "BILDBYRÅN"
        },
        {
            "charset": "mac",
            "templateName": "caption-abstract",
            "templateValue": "Göteborg"
        },
        {
            "charset": "utf-16",
            "templateName": "copyrightnotice",
            "templateValue": "something"
        }
    ],
    "customTagsConfigFile": "custom-tags.config",
    "customTags": [
        "-iptc:UserDefined252=true",
        "-iptc:Awesome253=splendid"
    ]
}
```
The `bucket` key specifies which S3 bucket the function should look in for getting the image to
process. 

The `charsetLookup` key (optional) specifies if there are any specific templates to look 
for and match with specified values in the image to decide which character set to use when 
extracting metadata from image. If `charsetLookup` is omitted or if specified templates have no 
match exiftool default character set is used (i.e. "UTF-8").

The `accessKeyId` and `secretAccessKeyId` (optional) should be supplied if Lambda function does not 
have access to S3 where image resides (if S3 resides on another AWS account for example).

The `region` (optional) should be used if the region for the S3 bucket is configured with. If left
blank, the same region as the Lambda function is configured with is expected for the S3 bucket.

The `customTagsConfigFile` (optional) specifies any custom _exiftool_ configuration file used
for updating/setting custom metadata tags on image. _Note_ that custom metadata tags are only
set/updated if event parameter `firstUpdate` is set to true (see below).

The `customTags` (optional) is used together with customTagsConfigFile configuration and specifies
a list of custom metadata tags to update/set on image. _Note_ that custom metadata tags are only
set/updated if event parameter `firstUpdate` is set to true (see below).

## Issues  

### New Feature
* [LIM-2] - Enable custom tags metadata update