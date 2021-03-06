---
layout: default
title: Migration guide for plugin
active: /guides/
---
# Migration from version 1 to 3

## TOC

* [ES5 to ES6](#from-es5-to-es6)
* [Dependency imports](#dependency-imports)
* [Name changes](#name-changes)
* [Plugin registration](#registering-a-plugin)
* [Validator](#validator)
* [API changes](#api-changes)
* [Node changes](#changes-in-nodes)
* [Component changes](#changes-in-components)


## From ES5 to ES6

The biggest work to be done is to migrate your plugins to ES6 with the new class system

__An ES5 component__ - *Preamble component in ES5*

~~~ javascript

'use strict';

var Component = require('substance/ui/Component');
var $$ = Component.$$;
var TextProperty = require('substance/ui/TextPropertyComponent');

function PreambleComponent() {
    Component.apply(this, arguments);
}

PreambleComponent.Prototype = function() {

    this.render = function() {
        return $$('div')
            .addClass('sc-preamble')
            .attr('data-id', this.props.node.id)
            .append($$(TextProperty, {
                path: [this.props.node.id, 'content']
            }));
    };
};
Component.extend(PreambleComponent);
module.exports = PreambleComponent;

~~~ 


__An ES6 Component__ - *Preamble component in ES6*

~~~ javascript

const {Component, TextPropertyComponent} = substance

class PreambleComponent extends Component {

    render($$) {
        return $$('div')
            .addClass('sc-preamble')
            .attr('data-id', this.props.node.id)
            .append($$(TextPropertyComponent, {
                path: [this.props.node.id, 'content']
            }));
    }
}

export default PreambleComponent;

~~~




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

~~~ javascript

export default {
    name: 'preamble',
    id: 'se.infomaker.preamble',
    ...

~~~

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

## Validator

The validation plugins has changed. The validation plugins must now extend writer.Validator class and implement a constructor and a `validate` method

The newsItem is accessible by using `this.newsItem`

To add messages you call the function for the type of message you want to add.

`this.addError({string})` - *Adds a message of type error*

`this.addWarning({string})` - *Adds a message of type warning*

`this.addInfo({string})` - *Adds a message of type info*

~~~ javascript 

import {Validator, api} from 'writer'
class AuthorValidation extends Validator {

    constructor(...args) {
        super(...args)
    }

    validate() {
    }
}
export default AuthorValidation

~~~

## API changes

We have made some changes to the API. Mostly it's just the method that's changed and not the signatures.

[Here is the full API Reference]({{site.url}}{{site.baseurl}}/api-reference)

New endpoints in the API

### Dialog

The dialog methods has moved to:

`api.ui.showDialog` *(was api.showDialog)*

`api.ui.showMessageDialog` *(was api.showMessageDialog)*

### Events

New endpoint calling on/off for Events

`api.events.on()` *(was api.on)*

`api.events.off()` *(was api.off)*

`api.events.triggerEvent()` *(was api.triggerEvent)*

### Newsitem

The endpoints used to manipulate the newsItem has moved to `api.newsItem`. Those method was previously directly under `api`

For example `api.getGuid` has now been moved to `api.newsItem.getGuid`

To avoid confusion with the newsItem endpoint and the actual newsItem article we now have different name.

The newsitem article is now located under `api.newsItemArticle`


### Document

`api.document.getDocumentNodes()` *(was api.getDocumentNodes)*

`api.document.insertInlineNode` *(was api.insertInlineNode)*

## Changes in Nodes

There is very small changes in the node. 

The needed information is still the same.

__Version 1__

~~~ javascript

'use strict';
var TextBlock = require('substance/model/TextBlock');
function Preamble() {
    Preamble.super.apply(this, arguments);
}
TextBlock.extend(Preamble);
Preamble.static.name = "preamble";
Preamble.static.defineSchema({
    "id": { type: 'string' }
});

module.exports = Preamble;

~~~

__Version 3__

~~~ javascript 

import {TextBlock} from 'substance'

class PreambleNode extends TextBlock {}

PreambleNode.type = 'preamble'
PreambleNode.define({
    "id": {type: 'string'}
})

export default PreambleNode

~~~

## Changes in components

The `$$` function is now passed to the component in the `render` method

~~~ javascript

render($$) {
    return $$('div')
}

~~~