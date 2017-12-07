---
layout: default
title: Substance tips
active: /guides/
---

# Substace tips



## Selections
There are a few different type of selections in Substance:
 - `Selection`
 - `ContainerSelection`
 - `CustomSelection`
 - `NodeSelection`
 - `PropertySelection`


### Selection
The base selection class. Refers to a Substance document model, not to the DOM. All other selection types inherit from this class.


### ContainerSelection
A selection that spans multiple nodes.

When selecting two or more nodes, e.g. a paragraph node and a headline node, a container selection is created.


### CustomSelection
A selection that can be set when focusing on a custom surface.
Contains the properties `customType`, `surfaceId`, and `data`.

`customType` should describe the type of selection so that the surface or component it refers to can handle it and disregard any other custom selections.

`surfaceId` must be provided as Substance uses it to send the selection to the right surface.

`data` is an object containing arbitrary data for the custom selection type which can then be used by the surface that handles the selection.


### NodeSelection
A selection of a single node/component on the body surface.

When clicking on an isolated node it is highlighted, set in a `selected` state, and a NodeSelection is created.



## Surfaces
Note: The only two surfaces in Substance as of now are ContainerEditor and TextPropertyEditor

***Any custom editors such as inputs should be implemented as custom surfaces***

Surfaces are components that implement a few special methods and are registered to the surface manager.
As of Substance beta 6.5 there is still no CustomSurface class (introduced in beta 7 preview 9?) to inherit from but they can be created by implementing the surface methods on a component and registering it with the surface manager. To see exactly which methods have to be implemented see [substance/ui/CustomSurface.js](https://github.com/substance/substance/blob/92365bccd7fe74bf3f63393675e9be83f7afff19/ui/CustomSurface.js).


### Summary of the added and modified component methods:

`didMount()` registers the surface with the surfaceManager.

`dispose()` unregisters the surface with the surfaceManager.

`renderDOMSelection()` does nothing by default but should set a native browser selection or focus on an element.

`_focus()` does nothing by default but should set a CustomSelection on the surfaces editor component. ContainerEditor and TextPropertyEditor selects the first (only?) editor in the surface. Not sure if it's called in beta 6.5, might have to implement a `focus()` method that calls it.

`_createSurfaceId()` creates a unique ID for the surface that is used when registering.

`_getCustomResourceId())` becomes the name of the surface. Could probably return the surface ID? Not sure if it has to be unique per instance or only unique for the surface type.



## Isolated nodes


### Blocking mode
Isolated nodes have two different types of blocking modes: **Open**, and ***Closed***. They refer to the type of isolated node. Open nodes never render a blocker element and are not draggable by default.
Closed nodes will render a blocker that prevents any clicks from propagating to the content component.

To choose the type of node you want to create, set the `noBlocker` property on your content component.

- `MyComponent.noBlocker = true` will create an isolated node with blocking mode `closed`.
- `MyComponent.noBlocker = false` will create an isolated node with blocking mode `open`.


### Stepping into an isolated node
One method to focus on an isolated node is to select it and press <kbd>Tab</kbd> which will call the `grabFocus()` method on the content component if it is implemented, or it will find the first `TextPropertyEditor` and select it.

The `grabFocus()` method, when implemented, should either set the selection into one of the surfaces of the content component, or set a `CustomSelection`.


#### Example grabFocus()
This will set a selection in the beginning of the `TextPropertyEditor`
```js
grabFocus() {
    const firstTextPropertyEditor = this.refs.text

    this.context.editorSession.setSelection({
        type: 'property',
        path: firstTextPropertyEditor.getPath(),
        startOffset: 0,
        surfaceId: firstTextPropertyEditor.id
    })
}
```

***Note that `grabFocus()` will only be run when pressing <kbd>Tab</kbd>.***

Another method is to click inside a `TextPropertyEditor` which will handle setting it's own selection.

By default, the isolated node will not be focused by clicking inside it unless you click inside a component that sets a selection. If you want the node to be focused no matter where the user clicks inside it, the following is a simple way to handle it:

```js
render() {
    return $$('div').append([
        ...
    ]).on('click', () => {
        setTimeout(this.focusOnIsolatedNode.bind(this))
    })
}

focusOnIsolatedNode() {
    const isolatedNode = this.context.isolatedNodeComponent

    // Make sure that the node is not already focused yet
    if (isolatedNode.state.mode !== 'focused') {
        isolatedNode.extendState({
            mode: 'focused',
            unblocked: true
        })
    }
}
```
