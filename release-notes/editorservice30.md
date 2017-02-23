---
layout: default
title: Editor Service 3.0 release
---
<div class="jumbotron">
    <h1>Editor Service 3.0</h1>
    <h2>Highlights</h2>
    <ul>
        <li>Support for "optimistic locking"</li>
        <li>Support for <code>https</code> in communication with Open Content</li>
    </ul>
    
    <h2>Breaking changes</h2>
    <ul>
        <li>If "optimistic locking" is not disabled, update API endpoint will not work (since API endpoint expects an <code>If-Match</code> header)</li>
        <li>API endpoint <code>commands</code> is no longer supported. Instead <code>v2/commands</code> should be used</li>        
    </ul>
    
    <h2>Compatibility</h2>
    <ul>
        <li>Lambda - Image Metadata <code>2.1</code></li>
        <li>Lambda - Image Publish <code>2.0</code></li>
        <li>Newspilot Writer Integration Service <code>1.2</code></li>
    </ul>
</div>

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