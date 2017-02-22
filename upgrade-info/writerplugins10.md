---
layout: default
title: Writer plugins 1.0 changes
---
# General changes
The plugins are no longer bundled in one file.
The list of available plugins can be found here:
[IM Dev plugins](https://s3-eu-west-1.amazonaws.com/writer-dev-plugins)

# Plugin changes
## se.infomaker.tags
This plugin has been renamed to se.infomaker.hdsds.tags

## se.infomaker.ximtags
This plugin is new and handles creation of person, organisation and topic. 
It needs configuration in the `writer-client-config` file:

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
        "x-im/channel": {
            "icon": "fa-random",
            "name": "Channel",
            "editable": false
        },
        "x-im/topic": {
            "icon": "fa-tags",
            "name": "Topic",
            "editable": true
        },
        "x-im/category": {
            "icon": "fa-tags",
            "name": "Category",
            "editable": false
        }
    }}
}
```