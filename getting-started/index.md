---
layout: default
title: Getting started
writer: Newspilot Writer
infomaker: Infomaker
---

# {{ page.title }}

**{{ page.writer }} consists of the NPWriter core project, which provides core editing functionality,
and optional plugin projects that extends the functionality of the writer.
In this article you will find instructions of how to download and start the {{ page.writer }} locally
and how to start developing your first plugin.**


## Prerequisites

To use  {{ page.writer }} you need to use the latest version of Google Chrome 

{{ page.writer }} requires Node.js version 6.9.1

Start by installing Node.js on your machine.

- [Installing NodeJS in OS X]({{site.url}}{{site.baseurl}}/getting-started/nodejs-installations/osx.html)
- [Installing NodeJS in Windows]({{site.url}}{{site.baseurl}}/getting-started/nodejs-installations/win.html)

The code resides on github, hence you also need to have Git installed.

- [Installing Git in OS X]({{site.url}}{{site.baseurl}}/getting-started/git-installations/osx.html)
- [Installing Git in Windows]({{site.url}}{{site.baseurl}}/getting-started/git-installations/win.html)

---

## Clone and start Newspilot Writer

Download and clone from Github
<video src="{{site.url}}{{site.baseurl}}/getting-started/get-started.mp4" width="70%" controls="true">
</video>


~~~text

git clone https://github.com/Infomaker/NPWriter.git
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

git clone https://github.com/Infomaker/NPWriterDevKit.git
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
                                