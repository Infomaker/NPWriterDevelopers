---
layout: default
title: Getting started
writer: Newspilot Writer
infomaker: Infomaker
---

# {{ page.title }}

{{ page.writer }} consists of two different projects, the NPWriter core 
and the NPWriterPluginBundle. One containing the writer itself and the other
one {{ page.infomaker }}s plugins.

The {{ page.writer }} is served to the browser via a node.js server. The server get the instructions of
which plugins to load from a configuration file. The easiest way to develop plugins on a local machine
is to:
 
1. Clone the {{ page.writer }} source code from github
2. Edit the configuration file and link to the new plugin
3. Start the {{ page.writer }} Node.js server

## Prerequisites

{{ page.writer }} requires Node.js version 6.9.1

Since {{ page.writer }} is served by Node.js, the first step is to install it on the local machine.

- [Installing NodeJS for OS X]({{site.url}}{{site.baseurl}}/getting-started/nodejs-installations/osx.html)
- [Installing NodeJS for Windows]({{site.url}}{{site.baseurl}}/getting-started/nodejs-installations/win.html)

---

## Clone and start Newspilot Writer

Download and clone from Github
<video src="{{site.url}}{{site.baseurl}}/getting-started/get-started.mp4" width="70%" controls="true">
</video>


~~~text

git clone git@github.com:Infomaker/NPWriter.git
cd NPWriter
npm install
npm run build-dep
npm run dev

~~~



You can now open thw writer with a demo document [localhost:5000/#demo](http://localhost:5000/#demo) or just 
[localhost:5000/](http://localhost:5000/) to create a new article


---

## Download add enable the Devkit plugin

We have provided you with a developers kit which is supplied with an example plugin.

<video src="{{site.url}}{{site.baseurl}}/getting-started/add-devkit-plugin.mp4" width="70%" controls="true">
</video>


~~~ 

git clone git@github.com:Infomaker/NPWriterDevKit.git
cd NPWriterDevKit
npm install 
npm run dev

~~~ 

Plugin server started at [localhost:3000](http://localhost:3000)


To enable plugin open NPWriter and edit server/config/writer.json








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
                                