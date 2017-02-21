---
layout: default
title: Breaking changes with Substance Beta 6
active: /guides/
---
# Breaking changes with Substance Beta 6

## No need to specify node.type

Setting the ~node.type property~ in a converter will result in a error. Setting the node type is not necessary, it should only be specified as a property in the
converter itself

__Example__ 
~~~ javascript

export default {
    type: 'your_node_type',
    tagName: 'object',
}

~~~ 