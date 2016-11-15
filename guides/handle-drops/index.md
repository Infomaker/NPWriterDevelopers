---
layout: default
title: Handle drops
active: /guides/
---

# Register a drag and drop handler

In the current version we support to handle drop containing URI and files.

First you need to add the drop handler in your package file.

~~~ javascript

import ContentRelationsDropHandler from './ContentRelationsDropHandler'

export default {
    name: 'myplugin',
    id: 'se.infomaker.myplugin',
    configure: function(config) {
        config.addDragAndDrop(ContentRelationsDropHandler)
    }
}

~~~


The drop handler must implement a match method that returns a boolean. It should return true is this handler wants to intercept the drop.

The drop method is executed on the drop event if match returned true

~~~ javascript

import {DragAndDropHandler} from 'substance'
import insertData from './insertData'

class MyDropHandler extends DragAndDropHandler {
    match(params) {
        if (someCondition(params.uri)) {
            return true
        }

    }

    drop(tx, params) {
         tx.insertBlockNode({
            type: 'myplugintype',
        })
               
    }
}

export default ContentRelationsDropHandler


~~~ 