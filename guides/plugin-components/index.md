---
layout: default
title: Add plugins to the writer
active: /guides/
---

# Add different plugin parts to the writer

All plugins must register their components when registering with the writer,  the components to be registered is specified in your `PluginPackage.js`

The example below shows the skeleton of a plugin package.

When registering with the writer, it will call the `configure` method and inject the writer configurator. The configurator has methods which allows you to register
different component, such as tools through the `addTool` method or component through the `addComponent` method.

~~~ javascript

export default {
    id: 'se.infomaker.myplugin',
    name: 'myplugin',
    configure: function(configurator) {
        
    }
}

~~~

You can read more about different components on the [basic information page]({{site.url}}{{site.baseurl}}/guides/basic-information#plugin-information)

In the following example we focus on just the configure method.

## Adding tools and commands

Tools and commands are tightly interconnected, a tool must have a command registered with the same name, a command on the other hand can be indepedent.

Tools must extend from the Tool class and Command must extend from the Command class



~~~ javascript

import {Command} from 'substance'

class MyCommandClass extends Command {
    getCommandState() {
        return {
            disabled: false
        }
    }

    execute() {
        console.log("Execute command")
    }
}

export default MyCommandClass

~~~


~~~ javascript

import {Tool} from 'substance'

class MyToolClass extends Tool {

    render($$) {
        const el = $$('span').append('click')
        el.on('click', () => {
            this.executeCommand()
        })
        return el
    }

}

export default MyToolClass

~~~


~~~ javascript

import MyToolClass from './MyToolClass'
import MyCommandClass from './MyCommandClass'

...
    configure: function(configurator) {
        configurator.addTool('mytool', MyToolClass)
        configurator.addCommand('mytool', MyCommandClass)
    }
...

~~~

## Adding Components

A component is used to render nodes inside the editor but also to render other parts, like in the sidebar, dialog, buttons etc. It's like a React component

~~~ javascript

import {Component} from 'substance'

class MyComponentClass extends Component {

    render($$) {
        el.append($$('h2').append('Hello world'))
        return el
    }
}

export default MyComponentClass

~~~ 


~~~ javascript

import MyComponentClass from './MyComponentClass'

...
    configure: function(configurator) {
        configurator.addComponent('mycomponent', MyComponentClass)
    }
...

~~~

## Adding tabs to sidebar

You can add a own tab in the sidebar, you can then add your sidebar components to that tab by referencing the Id you pass in `addSidebarTab()`

~~~ javascript

...
    configure: function(configurator) {
        configurator.addSidebarTab('myId', 'name')
    }
...

~~~


## Adding panels to a sidebar tab

When adding a component to the sidebar you must specify a tabId.

The component class is just a regular component, see ["Add component"](#adding-components) for component example

The id of the main tab is `main`

~~~ javascript

...
    configure: function(configurator) {
        configurator.addComponentToSidebarWithTabId('myPanel', 'tabId' ComponentClass)
    }
...

~~~


## Adding converters

Converters is used to transform the XML to the Node and back.

When you add a converter the first parameter specifies the format of the document, we are using newsml

~~~ javascript

export default {
    type: 'mytype',
    tagName: 'object',

    matchElement: function (el) {
        return el.is('object[type="mytype"]');
    },

    import: function (el, node) {
        // Set value on node from el
    },

    export: function (node, el, converter) {
        var $$ = converter.$$;
        el.attr({
            id: node.id,
        });
        // Create the element with values from node
    }
}

~~~


~~~ javascript

...
    configure: function(configurator) {
        configurator.addConverter('newsml', Converter)
    }
...

~~~

## Adding nodes

A node is a representation of the XML structure

The NodeClass must have a property called type to specify the type och the node. This type is matched with the converters type

~~~ javascript

import {BlockNode} from 'substance'

class MyNode extends BlockNode {}

MyNode.type = 'mytype'
MyNode.define({
    "propertyNumber": { type: "number", default: 1 },
    "propertyString": { type: "string", optional: true },
})

export default MyNode

~~~


~~~ javascript

import NodeClass from './NodeClass'

...
    configure: function(configurator) {
        configurator.addNode(MyNode)
    }
...

~~~

## Adding validation

Validator plugins is executed before the article is saved.

Validators must implement a constructor (calling the super constructor) and a validate method


__SampleValidation.js__ - *The validation class extends from writer.Validator*

~~~ javascript

import {Validator, api} from 'writer'

class SampleValidation extends Validator {

    constructor(...args) {
        super(...args)
    }

    validate() {
        // newsItem is availble as this.newsItem
        // Add messages by calling this.addError() this.addWarning() this.addInfo()
    }
}

export default SampleValidation

~~~

__PackageFile__

~~~ javascript

import SampleValidation from './SampleValidation'

...
    configure: function(configurator) {
        configurator.addValidator(SampleValidation)
    }
...

~~~