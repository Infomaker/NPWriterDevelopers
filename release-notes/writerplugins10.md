---
layout: default
title: Writer plugins 1.0 release
---
# Newspilot Writer Plugins 1.0

### Table of contents
* [General changes](#general-changes)  
* [Plugin changes](#plugin-changes)  
* [Issues](#issues)

## General changes
The plugins are no longer bundled in one file.
The list of available plugins can be found here:
[IM Dev plugins](https://s3-eu-west-1.amazonaws.com/writer-dev-plugins)

## Plugin changes

### se.infomaker.mitm.publicationchannel  
This plugin has been renamed to `se.infomaker.publicationchannel`.

### se.infomaker.tags
This plugin has been renamed to `se.infomaker.hdsds.tags`.

### se.infomaker.ximtags
This plugin handles searching, creating and editing "tags". What is handled by the plugin depends on the plugin
configuration (see below).

**Plugin configuration**  

```json
{
    "id": "se.infomaker.ximtags",
    "name": "ximtags",
    "url": "http://localhost:5001/index.js",
    "style": "http://localhost:5001/style.css",
    "mandatory": false,
    "enabled": true,
    "data": {"tags": {
        "x-im/person": {
            "icon": "fa-user",
            "name": "Person",
            "editable": true
        },
        "x-im/organisation": {
            "icon": "fa-sitemap",
            "name": "Organisation",
            "editable": true
        },
        "x-im/topic": {
            "icon": "fa-tags",
            "name": "Topic",
            "editable": true
        }
    }}
}
```

The `tags` config decides what types of concepts that are handled by the plugin.

Please note that `tags` must correspond with Concept backend configuration for `tags` search so that the same
concept types are used both in plugin and in Concept backend.

**Tag concept format**  
See [Concept Items](https://github.com/Infomaker/writer-format/tree/master/newsml/conceptitem).

**Tag format in article**  
When applying a tag in the article the relation will be represented as a link; 
 
```xml
<newsItem>
    <itemMeta>
        <links>
            <link title="Volvo" rel="author" type="x-im/organisation" 
                uuid="4w1653f3-6575-5cb7-8b74-qc4dea63513e"/>                
        </links>
    </itemMeta>
</newsItem>
```

## Issues  

### Bug    
* [WPLUG-8] - Error handling in Job plugin when image does not exist
* [WPLUG-11] - Split plugins into separate includes
* [WPLUG-22] - Spinner for save never stops when getting an exception
* [WPLUG-26] - Error handling uploading image that fails

### New Feature  
* [WPLUG-12] - Possible to add tooltips to components
* [WPLUG-13] - Fetch Newspilot credentials in np job plugin
* [WPLUG-14] - Add possibility to login using jxbrowser extensions for newspilot job plugin
* [WPLUG-15] - Handle error when uploading image from file
* [WPLUG-17] - Conflict handler plugin
* [WPLUG-20] - Migrate old se.infomaker.tags to sydsvenskans namespace
* [WPLUG-21] - Execute social embed macros on paste
* [WPLUG-23] - Implement grabFocus for plugin component