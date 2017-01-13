---
layout: default
title: Register event listeners
active: /guides/
---

# Adding and removing event listeners

Newspilot Writer triggers events when different actions occur. This means that you as a plugin developer can listen on these event and perform
appropriate actions


## Newspilot Writer Events

Here's a list of the events fired by the Writer. You can also see all events contants by typing `writer.events` in developer console in the Writer 
check them out at [Github](https://github.com/Infomaker/NPWriter/blob/develop/writer/utils/Event.js)

To get access to these event constants you can import those in your plugin: 
`import {events} from 'writer`

* DOCUMENT_SAVED
* DOCUMENT_SAVE_FAILED
* DOCUMENT_CHANGED
* DIALOG_CLOSE
* NOTIFICATION_ADD
* HISTORY_SAVED
* HISTORY_CLEARED
* USERACTION_SAVE
* USERACTION_KEY_ESCAPE
* USERACTION_CANCEL_SAVE

## Adding an event listener

To register a listener you should use the `api.events.on` method, this method accepts three arguments
`pluginname`, `eventType`, `callback`

~~~ javascript

import {Component} from 'substance'
import {api, event} from 'writer'

class PluginComponent extends Component {
   constructor(...args) {
       super(...args)
       
       api.events.on('myplugin', event.DOCUMENT_CHANGED, (event) => {
           //Perform some action
       })
   }
}

~~~

## Removing an event listener

It's also important to remove you event listeners when the component is disposed. The `api.events.off` should be called in your
components `dispose` method.

~~~ javascript

import {Component} from 'substance'
import {api, event} from 'writer'

class PluginComponent extends Component {
   dispose() {
        api.events.off('myplugin', event.DOCUMENT_CHANGED);
   }
}

~~~


## Complete example

~~~ javascript

import {Component} from 'substance'
import {api, event} from 'writer'

class PluginComponent extends Component {

   constructor(...args) {
       super(...args)
       api.events.on('myplugin', event.DOCUMENT_CHANGED, (event) => {
            //Perform some action
       })
   }
   dispose() {
        api.events.off('myplugin', event.DOCUMENT_CHANGED);
   }
}

~~~

