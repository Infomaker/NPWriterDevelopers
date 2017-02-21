---
layout: default
title: Breaking changes with Substance Beta 6
active: /guides/
---
# Breaking changes and new features - Substance Beta 6

## Enable access to components with SPACE (in editor)
By default the nodes in the editor is "closed", which means you must click inside them to activate. 
This can instead be done with implementing a `grabFocus()` method that's triggered with "SPACE"-key

__Example__

When this component is selected the Space-key executes the grabFocus-method, which allows you to for example set selection or open a dialog.

~~~ javascript

class MyComponent extends Component {

    grabFocus() {
        let startTime = this.refs.startTime
        this.context.editorSession.setSelection({
            type: 'property',
            path: startTime.getPath(),
            startOffset: 0
        })
    }
}
~~~


## Don't use the addDropHandler() just yet


## No need to specify node.type

Setting the `node.type property` in a converter will result in a error. Setting the node type is not necessary, it should only be specified as a property in the
converter itself

__Example__ 
~~~ javascript

export default {
    type: 'your_node_type',
    tagName: 'object',
}

~~~ 

## Commands must implement an execute method

Commands must implement an `execute` method, instead of for example an `insertNode` or a self defined method.
 
The command is then executed with `editorSession.executeCommand(name, {})` 

