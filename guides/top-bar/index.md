---
layout: default
title: Add plugin to topbar
---

# Add a plugin and popover 

You can add a icon and a popover by just calling addPopover in you plugin package.

`addPopover` takes three parameters, a name, an object containing information about icon and alignment, and third parameter is the component located in
the popover.

~~~ javascript 

import PopoverComponent from './PopoverComponent'

export default({
    id: 'se.infomaker.popoverplugin',
    name: 'popoverplugin',
    configure: function(config) {

        config.addPopover(
            'PopoverComponent',
            {
                icon: 'fa-history',
                align: 'right'
            },
            PopoverComponent
        )
    }
})

~~~ 