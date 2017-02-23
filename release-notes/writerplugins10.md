---
layout: default
title: Writer plugins 1.0 release
---

<div class="jumbotron">
    <h1>Newspilot Writer Plugins 1.0</h1>    
    <h2>Highlights</h2>
    <ul>
        <li>The plugins are no longer bundled in one file.
                    The list of available plugins can be found here: 
                    <a href="https://s3-eu-west-1.amazonaws.com/writer-dev-plugins">IM Dev plugins</a>
        </li>
    </ul>    
    <h2>Breaking changes</h2>
    <ul>
        <li>
        Plugin <code>se.infomaker.mitm.publicationchannel</code> has been renamed to <code>se.infomaker.publicationchannel</code>
        </li>
        <li>
        Plugin <code>se.infomaker.tags</code> has been renamed to <code>se.infomaker.hdsds.tags</code>
        </li>
        <li>
        Plugin <code>se.infomaker.ximtags</code> is used instead of <code>se.infomaker.tags</code>. Configuration for this
        plugin is described in <a href="https://github.com/Infomaker/NPWriterPluginBundle/blob/master/plugins/se.infomaker.ximtags/README.md">README.md</a> on github
        </li>        
    </ul>
</div>

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