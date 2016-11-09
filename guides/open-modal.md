---
layout: default
title: Open modal dialogs
active: /guides/
---

# Open and configure a modal

<!--<img src="{{ site.url }}{{ site.baseurl }}/assets/open_modal.png" class="img-thumbnail float-xs-right" width="50%">-->

Opening a modal window can be very useful when your plugins need to have more space, for example
when showing a map or browsing an image archive.

Currently there is two types of modals available, __custom dialog__ (provided by plugin developer) and a __message dialog__.

__Folder structure__

~~~

Myplugin
    |_ DialogComponent.js
    |_ PluginComponent.js
    |_ PluginPackage.js
    |_ index.js
    
~~~

## Create a dialog with your custom component

How to create and open a basic modal.


__DialogComponent.js__ - _The component that is rendered inside the modal_

~~~ javascript

import {Component} from 'substance'

class DialogComponent extends Component {
    
    render($$) {
        return $$('div').append('Hello world')
    }
    
    onClose(action) { // action is save or cancel
        
    }
}

~~~


__PluginComponent.js__ - _The main plugin components that initiate the modal open_


~~~ javascript

import {Component} from 'substance'
import {api} from 'writer'
import DialogComponent from './DialogComponent'

class PluginComponent extends Component {
    
    render($$) {
        const el = $$('div')
        
        const openDialogButton = $$('button').on('click', () => {
            api.ui.showDialog(DialogComponent, {}, {})   
        }
        
        el.append(openDialogButton)
        
        return el
    }
    
}

~~~

The modal is opened by calling the `api.ui.showDialog` method. 
When clicking the button the API will be called to open a new dialog containing the DialogComponent class.

__PluginPackage.js__ - 

~~~ javascript

import PluginComponent from './PluginComponent'

export default {
    name: 'myplugin',
    id: 'se.infomaker.myplugin',
    configure: function (config) {
        config.addComponentToSidebarWithTabId(this.id, 'main', PluginComponent)
    }
}

~~~

__index.js__ - The index file used to register the plugin

~~~javascript 

import PluginPackage from './PluginPackage'

(() => {
if (registerPlugin) {
        registerPlugin(DevkitPackage)
    } else {
        console.error("Register method not yet available");
    }
})()

~~~


### Valid options properties

|-----------------+------------+----------------|
| Property        |Type        | Description    | 
|-----------------|------------|----------------|
| title  | string, optional | The title for the modal  
| props             | object    | An object contain information you want to access in your dialog. 
| options           | object    | An options object for the modal. [Valid option properties](#valid-options-properties)



### Create a message dialog 