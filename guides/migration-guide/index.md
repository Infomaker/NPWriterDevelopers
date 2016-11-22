---
layout: default
title: Basic information
active: /guides/
---
# Migration from version 1 to 3

## From ES5 to ES6

The biggest work to be done is to migrate your plugins to ES6 with the new class system

## Dependency imports

In the first version we used `require` to add dependencies. In the new version we are using the ES6 `import` statement.

__Version 1__

~~~ javascript

var Component = require('substance/ui/Component')

~~~

__Version 3__

Plugins is hosted seperated from the Writer so `substance` and `writer` is available on the window object. 
If you are using our devkit you can use the import statement because webpack
is treating substance and writer as externals.

If you are using vanilla js or using different build system you can either specify writer and substance as external or you can import the dependencies as regular variables.


~~~ javascript

import {Component} from 'substance'
import {api} from 'writer'

// OR

const {Component} = substance
const {api} = writer // equal to const api = window.writer.api

~~~


## Name changes

We have made some changes regarding the names of plugins.

We used to have a name and a vendor but that has now changed to `name` and `id`

For the id we recommend you use the reverse domain notation, for example the id for our plugins starts with `se.infomaker`



## Registering a plugin

__Version 1__ - *The old schema*

~~~ javascript

function Preamble() {
}

Preamble.prototype.schema = {
    name: 'preamble',
    vendor: 'infomaker.se',

    node: require('./PreambleNode'),

    converter: require('./PreambleXMLConverter'),

    component: require('./PreambleComponent')
};

module.exports = Preamble;


~~~

__Version 3__ - *The new package registration*

~~~ javascript

import PreambleNode from './PreambleNode'
import PreambleXMLConverter from './PreambleXMLConverter'
import PreambleComponent from './PreambleComponent'

export default {
    name: 'preamble',
    id: 'se.infomaker.preamble',
    configure: function(config) {
        
        config.addNode(PreambleNode)
        config.addConverter('newsml', PreambleXMLConverter)
        config.addComponent('preamble', PreambleComponent)
    }
}


~~~

## Changes in Nodes

## Changes in components

