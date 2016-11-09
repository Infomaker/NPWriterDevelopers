---
layout: default
title: Open modal dialogs
active: /guides/
---

# Open and configure a modal

Opening a modal window can be very useful when your plugins need to have more space, for example
when showing a map or browsing an image archive.

Currently there is two types of modals available, __custom dialog__ (provided by plugin developer) and a __message dialog__.

<img src="{{ site.url }}{{ site.baseurl }}/guides/open-modal/open-modal.gif" class="img-thumbnail" width="100%">


## Example
[This example code is available at Github](https://github.com/Infomaker/NPWriterExamplePlugins/tree/master/examples/open-modal)



## Create a dialog with your custom component

How to create and open a basic modal.

__Folder structure__

~~~

open-modal
    |_ DialogComponent.js
    |_ PluginComponent.js
    |_ PluginPackage.js
    |_ index.js
    
~~~



__DialogComponent.js__ - _The component that is rendered inside the modal_

~~~ javascript

import {Component} from 'substance'

class DialogComponent extends Component {
    
    render($$) {
        return $$('div').append('Hello world from DialogComponent')
    }
    
    onClose(action) { // action is save or cancel
        
    }
}
export default DialogComponent

~~~


__PluginComponent.js__ - _The main plugin components that initiate the modal open_


~~~ javascript

import {Component} from 'substance'
import {api} from 'writer'
import DialogComponent from './DialogComponent'

class PluginComponent extends Component {
    
    render($$) {
        const el = $$('div')
        
        const openDialogButton = $$('button')
                .append("Click me to open dialog")
                .on('click', () => {
                    api.ui.showDialog(DialogComponent, {}, {})
                })
        
        el.append(openDialogButton)
        
        return el
    }
    
}

export default PluginComponent

~~~

The modal is opened by calling the `api.ui.showDialog` method. 
When clicking the button the API will be called to open a new dialog containing the DialogComponent class.

__PluginPackage.js__ - 

~~~ javascript

import PluginComponent from './PluginComponent'

export default {
    name: 'open-modal',
    id: 'se.infomaker.open-modal',
    configure: function (config) {
        config.addComponentToSidebarWithTabId(this.id, 'main', PluginComponent)
    }
}

~~~

__index.js__ - The index file used to register the plugin

~~~javascript 

import {registerPlugin} from 'writer'
import PluginPackage from './PluginPackage'

(() => {
if (registerPlugin) {
        registerPlugin(PluginPackage)
    } else {
        console.error("Register method not yet available");
    }
})()

~~~


### Valid options properties

Please see the Ui section in API Reference

### Create a message dialog 