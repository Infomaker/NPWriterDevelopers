---
layout: default
title: Getting started
writer: Newspilot Writer
infomaker: Infomaker
---

# {{ page.title }}

**In this article you will find instructions of how to download and start the {{ page.writer }} locally
and how to start developing your first plugin.**


## Before you start

To use  {{ page.writer }} you need to use the latest version of Google Chrome
{{ page.writer }} requires Node.js version 6.9.1

Start by installing Node.js on your machine.

- [Installing NodeJS in OS X]({{site.url}}{{site.baseurl}}/getting-started/nodejs-installations/osx.html)
- [Installing NodeJS in Windows]({{site.url}}{{site.baseurl}}/getting-started/nodejs-installations/win.html)

The code resides on github, hence you also need to have Git installed.

- [Installing Git in OS X]({{site.url}}{{site.baseurl}}/getting-started/git-installations/osx.html)
- [Installing Git in Windows]({{site.url}}{{site.baseurl}}/getting-started/git-installations/win.html)

---

## The Writer

### Get the code

In order to get access to the writer you will need to be added to the Infomaker /Writer3-Plugin-Developer/ team on Github. You will also need to obtain an API key to get access to services necessary to run the Writer.

Start by cloning the NPWriter project.

```
mkdir workshop
cd workshop
git clone https://github.com/Infomaker/NPWriter.git
```

### Prepare and start the Writer

```
cd NPWriter
npm install && npm run build-dep
```

The writer is now almost ready. The only thing we need to do now is add the API key to the server config file. Open the file `server/config.server.json` and add the obtained API key, which looks something like `fAL0FFu9kcbaUDIh4W130rOrOogkDd38YBYJJ0`, where you see `[Enter API key here]`

*The default developer usage plan allows for 10 requests per second and 5.000 requests per month.*

Now start the writer in dev mode using the default configuration.

```
npm run dev
```

This should have the Writer running and you will find it on [localhost:5000](http://localhost:5000).

## Getting on with plugin development

Get started with the dev kit
The dev kit provides everything needed to get started, including build steps and local plugin server. Start by going to the workshop directory again and clone the NPWriterDevKit project.

```
git clone https://github.com/Infomaker/NPWriterDevKit.git
cd NPWriterDevKit
rm -rf .git
npm install
npm start
```

This should have the plugin started and served by the plugin server on [localhost:3000](http://localhost:3000). Next you need to add this plugin to the Writer configuration so it loads the plugin. The configuration should look like below.

*[You can find more information on plugin configuration here]({{site.url}}{{site.baseurl}}/guides/plugin-configuration.html)*

```json
{
    "id": "se.infomaker.npwriterdevkit",
    "name": "npwriterdevkit",
    "url": "http://localhost:3000/index.js",
    "style": "http://localhost:3000/style.css",
    "mandatory": false,
    "enabled": true
}
```

Add this to the top of the plugins section in  `server/config/writer.json`. After this it should look something like

```json
{
  "newsItemTemplateId": "30eae1c0-c640-4053-b114-05c64e28bbe7",
  "language": "en_US",
  "labelLanguage": "en",
  "plugins": [
        {
            "id": "se.infomaker.npwriterdevkit",
            ...
        },
        ...
    ]
}
```

### Next… improvise!

Next up is to familiarize yourself with the [API reference]({{site.url}}{{site.baseurl}}/api-reference/), the [howto guides]({{site.url}}{{site.baseurl}}/guides/) and play around.


<!--
//~~~ javascript

// Get all nodes in the document
const nodes = api.document.getBlockNodes()
let myvar = "this"
let myvar = "this"
let myvar = "this"

~~~
-->



***

###  Discuss this

<div id="disqus_thread"></div>
<script>

var disqus_config = function () {
this.page.url = "{{ site.url }}{{ page.url }}";  
this.page.identifier = "PAGE_{{ page.url }}";
};

(function() { // DON'T EDIT BELOW THIS LINE
var d = document, s = d.createElement('script');
s.src = '//developer-portal.disqus.com/embed.js';
s.setAttribute('data-timestamp', +new Date());
(d.head || d.body).appendChild(s);
})();
</script>
<noscript>Please enable JavaScript to view the <a href="https://disqus.com/?ref_noscript">comments powered by Disqus.</a></noscript>
