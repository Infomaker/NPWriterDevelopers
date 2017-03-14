---
layout: default
title: Writer plugins 3.0 release
---

<div class="jumbotron">
    <h1>Newspilot Writer Plugins 3.0</h1>    
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
* [WPLUG-25] - Error trying to create new position in place plugin
* [WPLUG-26] - Error handling uploading image that fails
* [WPLUG-27] - PDF plugin not able to open in external link
* [WPLUG-30] - Adding teaser headline generates error
* [WPLUG-31] - Drag and drop youtube does not work
* [WPLUG-34] - New article generates unsaved changes
* [WPLUG-38] - Edit concepts not working
* [WPLUG-39] - Cannot edit concept - Story
* [WPLUG-40] - Cannot edit concept - Funktionstagg
* [WPLUG-41] - Cannot edit concept - Place
* [WPLUG-42] - An article containing a story entity which is removed from backend breaks story item
* [WPLUG-43] - CharacterTransformationMarco throws error when pasting nodes
* [WPLUG-44] - Cannot edit concept - Tag
* [WPLUG-45] - Cannot remove byline in popup byline dialog
* [WPLUG-48] - Save timeout occurs when saving new article even though the article has been saved

### New Feature
* [WPLUG-3] - Section plugin
* [WPLUG-4] - Modify author plugin so that search for authors could be optional
* [WPLUG-6] - Implement image byline
* [WPLUG-7] - Implement support for basic authentication in np image plugin
* [WPLUG-12] - Possible to add tooltips to components
* [WPLUG-13] - Fetch Newspilot credentials in np job plugin
* [WPLUG-14] - Add possibility to login using jxbrowser extensions for newspilot job plugin
* [WPLUG-15] - Handle error when uploading image from file
* [WPLUG-17] - Conflict handler plugin
* [WPLUG-18] - New IM tags plugin
* [WPLUG-19] - Error creating concept story
* [WPLUG-20] - Migrate old se.infomaker.tags to sydsvenskans namespace
* [WPLUG-21] - Execute social embed macros on paste
* [WPLUG-23] - Implement grabFocus for plugin component
* [WPLUG-32] - UX/GUI related content
* [WPLUG-37] - Change format of image soft crops to flatter link structure
* [WPLUG-46] - Unable to open writer when articles without headline is saved in localstorage
* [WPLUG-47] - Error when undoing teaser with image
