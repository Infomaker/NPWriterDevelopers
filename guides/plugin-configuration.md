---
layout: default
title: Add your plugin it the configuration file
active: /guides/
---

# Add your plugin it the configuration file


Below is the section for a plugin, in this case the __npwriterdevkit__.

~~~ json

{
    "id": "se.infomaker.npwriterdevkit",
    "name": "npwriterdevkit",
    "url": "http://localhost:3000/index.js",
    "mandatory": false,
    "enabled": false,
    "data": {
        "foo": "bar"
    }
}

~~~

* __id__: *The id of the plugin, must be an unique value. Recommended is to use Reverse domain name notation*