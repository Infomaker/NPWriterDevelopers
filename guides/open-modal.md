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

## Create a dialog with your custom component

How to create and open a basic modal.


_DialogComponent.js_

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

_PluginComponent.js_


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



### Valid options properties

|-----------------+------------+----------------|
| Property        |Type        | Description    | 
|-----------------|------------|----------------|
| title  | string, optional | The title for the modal  
| props             | object    | An object contain information you want to access in your dialog. 
| options           | object    | An options object for the modal. [Valid option properties](#valid-options-properties)



### Create a message dialog 