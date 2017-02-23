---
layout: default
title: Newspilot Writer 3.0 release
---
<div class="jumbotron">
    <h1>Newspilot Writer 3.0</h1>
    <h2>Highlights</h2>
    <ul>
        <li>Built in spellchecking</li>
        <li>Automatic optimistic locking prevent users from overwriting each others changes</li>
        <li>Possibility to see who else has an article open</li>
        <li>New UI with top bar and drop down popovers for plugins</li>
        <li>Many squashed bugs for a better text editing experience</li>
    </ul>
    
    <h2>Breaking changes</h2>
    <ul>
        <li>Moved to ECMAScript 2015+</li>
        <li>New plugin architecture</li>
        <li>Improved drag'n drop handling</li>
        <li>New translation handling per plugin</li>
        <li>Paste handling through macros</li>
        <li>Configuration stored externally</li>
    </ul>
    
    <h2>Compatibility</h2>
    <ul>
        <li>Editor Service <code>3.0</code></li>
        <li>Concept Backend <code>2.5.5</code></li>
    </ul>
</div>

## Issues  

### Epic
* [WRIT-140] - NPWriter 3.0, upgrade to Substance beta 5

### Bug
* [WRIT-22] - Dropping a social embed link in a plugin annotated text area does not work
* [WRIT-67] - Text formatting options should not be visible in text only fields
* [WRIT-69] - It must be possible to place text cursor directly after a plugin component in the editor
* [WRIT-70] - All assets in writer should be loaded using https to avoid mixed content warnings
* [WRIT-71] - Image titles in related search should show meaningful information, not "unidentified"
* [WRIT-84] - Author links are created wrong
* [WRIT-100] - Missing image not rendered
* [WRIT-118] - Upload from URL sometimes starts many uploads for one url
* [WRIT-121] - ConceptItems created by plugins are invalid
* [WRIT-122] - Plugin "Story" creates invalid ConceptItems
* [WRIT-123] - Plugin "Tags" creates invalid ConceptItems
* [WRIT-172] - Problems with scrolling modals in win
* [WRIT-194] - Invalid teaser format
* [WRIT-224] - Pen component renders "wrong" when object in Newspilot Writer is selected
* [WRIT-230] - Strong/Italic becomes [Object Object] when used in a text property editor
* [WRIT-231] - When pasting a url and a macro handles an insertion, the url is still there
* [WRIT-233] - Notifications doesn't disappear
* [WRIT-234] - Add spinner to save button in dialog when clicking
* [WRIT-235] - Enable drop to teaser
* [WRIT-236] - It must be possible to change label of Meta-sidebar
* [WRIT-238] - Strange generated id in ximpdf plugin
* [WRIT-239] - Writer backend sometimes responds with 503 errors
* [WRIT-242] - UTF-8 control characters are not removed in image caption
* [WRIT-248] - Concept search should have behave better
* [WRIT-255] - Escaped XML characters appears escaped in document text when saving article
* [WRIT-257] - Twitter social embed does not work
* [WRIT-258] - Problem with selecting in drop down
* [WRIT-260] - Image binary caption is not automatically added to image caption when image is added to article
* [WRIT-263] - The browser tab title should be set to the article title
* [WRIT-264] - Set maximum width on the editor area (line lengths) to increase text readability
* [WRIT-266] - Populera image byline automatically from image binary
* [WRIT-269] - Spellcheck suggestions not working on Windows
* [WRIT-272] - When aborting a validation class a error is thrown
* [WRIT-277] - Concept plugin Tags have hardcoded filter
* [WRIT-279] - Problem saving pasted HTML text containing 'nbsp' entity
* [WRIT-281] - Story concept cannot be added
* [WRIT-282] - Concept place cannot be added nor created
* [WRIT-283] - When correcting a misspelled word thats a link or strong the annotation disappears
* [WRIT-286] - Article is set to invalid state if image drop from URL fails
* [WRIT-289] - It should be easier to select text in a plugin object field without initiating dragging (i e an image text field)
* [WRIT-299] - Checking for If-Match even though optimistic locking disabled
* [WRIT-301] - Writer reports that concept is already in use for all existing concepts
* [WRIT-304] - Missing If-Match header problem when saving article
* [WRIT-307] - <esc> empties, or restores, an article in the writer
* [WRIT-308] - Infinite spinner in save button when abort in conflict dialog
* [WRIT-312] - debounce-funktionen anropas fel i FormSearchComponent
* [WRIT-313] - History should be cleared and NOT save new version until document is dirty, after save
* [WRIT-316] - Link tool is not showing up or behaving weird

### New Feature
* [WRIT-137] - Add spellchecking capabilities to NPWriter
* [WRIT-148] - Plugin should be able to load own stylesheet
* [WRIT-150] - Create plugin bundle for our plugins
* [WRIT-151] - Statusbar for UI tools like messages, local versioning etc
* [WRIT-152] - Specify and load a template
* [WRIT-158] - Implement support for validator registration in configurator
* [WRIT-159] - Implement Save Article
* [WRIT-161] - Enable config loading from S3
* [WRIT-163] - Implement support for local versioning
* [WRIT-164] - Allow plugins to register tools and commands
* [WRIT-165] - Create build and deploy script
* [WRIT-166] - Implement top bar for icons, buttons and information
* [WRIT-167] - Implement spellchecker backend handling
* [WRIT-168] - Configure i18n translation overrides
* [WRIT-169] - Implement support for dialogs
* [WRIT-170] - Use bootstrap 4
* [WRIT-173] - Add a window.writer manager
* [WRIT-174] - Implement publish plugin in new top bar
* [WRIT-176] - Load plugin multiple times
* [WRIT-178] - Expose lodash through API
* [WRIT-179] - Port notifications to Writer 3
* [WRIT-181] - Trigger document changed event when changing newsItem
* [WRIT-185] - Don't reload writer when creating new article
* [WRIT-189] - Fix HTTPS for plugins on S3
* [WRIT-190] - Plugin - Finish social embed plugin with fb, instagram, twitter
* [WRIT-195] - Migrate pdf plugin to Newspilot 3.0
* [WRIT-197] - Possible to provide a css class when opening a dialog
* [WRIT-198] - Add support for textfields in header-group
* [WRIT-199] - Plugin - Finish relation plugin
* [WRIT-200] - Create/Move modal dialog component
* [WRIT-201] - Add bootstrap css to project
* [WRIT-203] - Port image plugin with meta data and crop dialogs
* [WRIT-204] - Plugin - Port youtube plugin
* [WRIT-205] - Plugin - Port MM Tag plugin
* [WRIT-206] - Plugin - Port html embed plugin
* [WRIT-207] - Plugin - port teaser plugin
* [WRIT-208] - Style newvalue and news lifetime plugin
* [WRIT-209] - Plugin - Port SDS main channel concept plugin
* [WRIT-210] - Plugin - Port category plugin
* [WRIT-211] - Plugin - Port tag concept plugin
* [WRIT-212] - Plugin - finish place concept plugin
* [WRIT-213] - Plugin - port story plugin
* [WRIT-214] - Plugin - port content profile plugin
* [WRIT-218] - Create plugin bundle for each customer
* [WRIT-220] - Wrtier backend proxy should handle auth header
* [WRIT-222] - Add title attribute to tools - in content menu, overlay and context menu,(not on text items)
* [WRIT-223] - Multiple calls to addSidebarTab should result in just one tab
* [WRIT-225] - Clean up console log in plugins
* [WRIT-232] - Port ximtags plugin
* [WRIT-246] - Improve publishing channel and deprecate old channel selector
* [WRIT-256] - Allow Writer node server to start in standby mode
* [WRIT-267] - ImageDisplayComponent should be added to registry
* [WRIT-273] - Improve error pages
* [WRIT-274] - Add email to author link in article
* [WRIT-275] - Imagextension for drops should be configurable in the writer config
* [WRIT-285] - Show icons for image even when it's selected
* [WRIT-288] - Handle ETag and If-Match for all Editor Service requests
* [WRIT-295] - Conflict handling due to optimistic lock
* [WRIT-314] - Set initial selection when opening writer

### Task
* [WRIT-196] - Plugin - Add Bootstrap list-groups for sds channel plugin
* [WRIT-318] - Add plugins.writer.infomaker.io domain to cloudfront
