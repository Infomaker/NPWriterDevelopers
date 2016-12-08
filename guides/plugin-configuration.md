---
layout: default
title: Add your plugin it the configuration file
active: /guides/
---

# Add your plugin it the configuration file


Below is the section for a plugin, in this case the __npwriterdevkit__.

{% assign config = site.data.vars['config'] %} 
This is configured in the writer configuration file, located in {{config.writer_config_path}}

~~~ json

plugins: [
    ...
    {
        "id": "se.infomaker.npwriterdevkit",
        "name": "npwriterdevkit",
        "url": "http://localhost:3000/index.js",
        "style": "http://localhost:3000/style.css",
        "mandatory": false,
        "enabled": false,
        "data": {
            "foo": "bar"
    },
    ...
}

~~~

|-----------------+------------|
| Property name                 | Description|
|-----------------              |------------|
| id                |The id of the plugin, must be an unique value. Recommended is to use Reverse domain name notation |
| name              |The name of plugin         |
| url               |Url to the location of the plugin and the file executing the registerPlugin method |
| style             |Url to the location to the stylesheet |
| mandatory             |{bool} If the plugin is mandatory the writer fails to load if the plugins should fail to load |
| enabled             |{bool} Should the plugin be loaded |
|-----------------+------------+
| data              | Data is a javascript object containing data or configuration properties for your plugin            |
|-----------------+------------+


### Disable use of annotations - bold, italic link etc

You can disable the use of annotation tools, (like strong and italic) in the configuration for the writer.

You can choose to disable for the whole plugin or just for one field, (TextPropertyEditor)

__Disable for multiple fields. Title and subject in this case__ - disableUseOfAnnotationToolsForFields is used to disable per field

~~~ json

 {
    "id": "se.infomaker.npwriterdevkit",
    "name": "npwriterdevkit",
    "url": "http://localhost:3000/index.js",
    "style": "http://localhost:3000/style.css",
    "mandatory": false,
    "enabled": false,
    "data": {
        "disableUseOfAnnotationToolsForFields": [
          "title",
          "subject"
        ],
},



~~~


__Disable for plugin__ - disableUseOfAnnotationTools is used to disable tools

~~~ json

 {
    "id": "se.infomaker.npwriterdevkit",
    "name": "npwriterdevkit",
    "url": "http://localhost:3000/index.js",
    "style": "http://localhost:3000/style.css",
    "mandatory": false,
    "enabled": false,
    "data": {
        "disableUseOfAnnotationTools": true
    }
}


~~~