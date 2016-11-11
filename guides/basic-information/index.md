---
layout: default
title: Basic information
active: /guides/
---
# Basic information

Newspilot works against a java backend called editorservice, the configuration for the backend
connection is located in server/config/server.json

The article format is based on the NewsML standard, you can more about the format here.

## Newspilot Writer Overview

Below is an overview image of different parts of the Newspilot Writer.

The areas shown is areas were you can place you plugins.

[Read instructions here on how to add your plugin components]({{site.url}}{{site.baseurl}}/guides/plugin-components/)

![Writer Overview]({{site.url}}{{site.baseurl}}/guides/basic-information/writer-overview.png){:class="img-fluid" style="border:1px solid #efefef"}

## Plugin information

### Plugin loading

This is one of the biggest improvement in Newspilot Writer 3.0.
Plugins is now loaded externally, which means you host your own plugins and can manage your own
release process and not depend on us.

### Anatomy of a plugin

A plugin may consist of several parts, depending on what kind of plugin you are building.
 
 __Node__
 
 The internal data node of an plugin object in the writer editor.
 
 __Converter__
 
 Responsible for importing the xml dom structure into an internal data node representation and export it back to the xml dom structure.
 
 `XML > Importer -> Node`
 
 `Node > Exporter > XML`
 
 __Component__
 
 A component is more or less like a react component. It's used to render items inside the text editor as well as the sidebar or any other visual components
 
 __Tool__
 
 The visualized tool button, or more advanced user interface. Tools are made available to the user in either the content tools on the left of the Writer editor area, 
 in the inline tools visible when selecting text or a supported annotation or in the context menu visible when right clicking in the editor.
 
 __Command__
 
 The actual command executed by either a content tool or inline tool.
 
 __UI Component__
 
 UI components are used to render plugins in the right sidebar in one of the available tabs.
 
 __Validation__
 
 A validation part of the plugin is called from the Writer when the user is saving. Gives the ability to validate any part of the NewsML before saving.
 
 __Macros__