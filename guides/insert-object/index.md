---
layout: default
title: "Insert a node"
---

# Insert a node via the API

This example shows you how to insert a node, render it, edit the value inside the editor, import and export it.

![Writer Overview]({{site.url}}{{site.baseurl}}/guides/insert-object/insertNode.gif){:class="img-fluid" style="border:1px solid #efefef"}


[The example code can be found at Github](https://github.com/Infomaker/NPWriterExamplePlugins/tree/master/examples/insertnode)


So in this example our XML for insert node plugin looks lite this

~~~ xml

...
 <object id="" type="insertnode">
       <data>
           <text>this is the text</text>
      </data>
 </object>
...

~~~


__Folder structure__

This plugins contains six files.

~~~

insertnode
    |_ index.js
    |_ InsertNodeComponent.js
    |_ InsertNodeCoverter.js
    |_ InsertNodeNode.js
    |_ InsertNodePackage.js
    |_ InsertNodeSidebarComponent.js

~~~

__index.js__ File used to register the plugin package with the writer

~~~ javascript

import {registerPlugin} from 'writer'
import InsertNodePackage from './InsertNodePackage'

(() => {
    if (registerPlugin) {
        registerPlugin(InsertNodePackage)
    } else {
        console.error("Register method not yet available");
    }
})()

~~~



__InserNodeComponent.js__ - Renders the node inside the editor

This component is the one that's in the editor. 

You can access your node (InsertNodeNode.js) through the this.props.node

In this example we are using the TextPropertyEditor which allows us to edit the text property directly in the writer.

~~~ javascript

import {Component, TextPropertyEditor} from 'substance'

class InsertNodeComponent extends Component {
    render($$) {
        const node = this.props.node // You can access the node through the props
        const el = $$('div')
        const textField = $$(TextPropertyEditor, {
            tagName: 'div',
            path: [this.props.node.id, 'text'],
            doc: this.props.doc
        }).ref('text')

        el.append(textField)
        return el
    }

}

export default InsertNodeComponent

~~~



__InsertNodeConverter.js__ - Converter to the insertnode object

The converter is responsible for converting the XML to a node and back.

The matchElement method gets an element and should evaluate if it should handle this element, 

In the example example below we handle `<objec type="insertnode">`

~~~ javascript


export default {
    type: 'insertnode',
    tagName: 'object',

    matchElement: function (el) {
        return el.is('object[type="insertnode"]');
    },

    import: function (el, node, converter) {
        node.id = el.attr('id')
        node.dataType = el.attr('type') // type is reserved so we use dataType
        const text =  el.find('data>text')
        node.text = converter.annotatedText(text, [node.id, 'text']);
    },

    export: function (node, el, converter) {
        var $$ = converter.$$;
        el.attr({
            id: node.id,
            type: node.dataType,
        });
        var data = $$('data').append(
            $$('text').append(converter.annotatedText([node.id, 'text']))
        )
        el.append(data)
    }
}

~~~


__InsertNodeNode.js__ 

This file describe which properties, and their type we want to have on our node.

Properties can also be optional or have a default value. `text: {type: 'string', default: 'edit me'}`

~~~ javascript

import {BlockNode} from 'substance'
class InsertNodeNode extends BlockNode { }

InsertNodeNode.define({
    type: 'insertnode',
    dataType: 'string',
    text: 'string'
})

export default InsertNodeNode

~~~

__InsertNodePackage.js__


The package that's importing all of our components to the configurator

~~~ javascript

import InsertNodeSidebarComponent from './InsertNodeSidebarComponent'
import InsertNodeNode from './InsertNodeNode'
import InsertNodeConverter from './InsertNodeConverter'
import InsertNodeComponent from './InsertNodeComponent'

export default {
    name: 'insertnode',
    id: 'se.infomaker.insertnode',
    configure: function (config) {

        config.addNode(InsertNodeNode)
        config.addConverter('newsml', InsertNodeConverter)
        config.addComponent('insertnode', InsertNodeComponent)
        config.addComponentToSidebarWithTabId(this.id, 'main', InsertNodeSidebarComponent)
    }
}

~~~


__InsertNodeSidebarComponent.js__

This is a component in the sidebar containing a button, when clicked it's inserting a new node

~~~ javascript

import {Component} from 'substance'
import {api, idGenerator} from 'writer'

class InsertNodeSidebarComponent extends Component {

    render($$) {
        return $$('button')
            .addClass('sc-np-btn btn-primary')
            .append('InsertNode')
            .on('click', this.insertNode)
    }

    insertNode() {
        var node = {
            id: idGenerator(),
            type: 'insertnode',
            dataType: 'insertnode',
            text: "Edit me...",
        }
        api.document.insertBlockNode(node.type, node)
    }
}

export default InsertNodeSidebarComponent

~~~