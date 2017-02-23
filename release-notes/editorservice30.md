---
layout: default
title: Editor Service 3.0 release
---
# Editor Service 3.0

### Table of contents
* [Breaking changes](#breaking-changes)
* [General changes](#general-changes)
* [Compatibility](#compatibility)
* [Issues](#issues)

## Breaking changes

### Version 1 of endpoints removed
Endpoint `commands` is no longer supported. Instead `v2/commands` should be used. 

## General changes

### ETag 
 
If "Optimistic locking" is not disabled update endpoint will not work (since it expects an "If-Match" header).

## Compatibility

| Service                              | Version |
| ------------------------------------ | ------- |
| Lambda - Image Metadata              | 2.1     |
| Lambda - Image Publish               | 2.0     |
| Newspilot Writer Integration Service | 1.3     |

## Issues  

### Bug
* [COBA-9] - Byline twitter images does not get rendered in Writer

### Bug    
* [EDSE-66] - Update metadata fails for new images that do not contain an author

### New Feature
* [EDSE-64] - Create thumb and preview
* [EDSE-65] - Implement optimistic locking

### Task
* [EDSE-60] - Enable HTTPS connections to OC