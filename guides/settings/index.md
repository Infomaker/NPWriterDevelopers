---
layout: default
title: Add plugin settings to the writer
active: /guides/
---

# Add

The writer provides basic functionality for handling plugin settings in a coherent way. Currently settings are stored per browser in local storage. This might change in the future.

This is done by providing a plugin module that can handle the settings. A plugin can register a module either for others to use, or as in this instance with a specific target.

A settings plugin module provide a component that can handle settings using for example text fields or option toggles, but can also be more advanced. The provided component is made available to the writer and then rendered in the writer settings dialog.


## Example

How to create a basic plugin that handle settings. It is of course possible to provide a settings module component in any plugin, it doesn't have to be a specialized settings plugin.

__Folder structure__

~~~

mysettings
    |_ MysettingsComponent.js
    |_ MysettingsPackage.js
    |_ index.js

~~~



__index.js__ - _The index file used to register the plugin_

~~~ javascript

import {registerPlugin} from 'writer'
import MysettingsPackage from './MysettingsPackage'

(() => {
if (registerPlugin) {
        registerPlugin(MysettingsPackage)
    } else {
        console.error("Register method not yet available");
    }
})()

~~~


__MysettingsPackage.js__ - _The plugin package_

The settings plugin module is registered through `config.addPluginModule()` that takes three parameters.
1. The namespace for the settings module, should be a full plugin id plus a name for the settings component.
2. The actual component.
3. The target id for this plugin module, ie always `se.infomaker.npwriter.settings` for settings.

~~~ javascript
import MysettingsComponent from './MysettingsComponent'

export default {
    name: 'mysettings',
    configure: function(config) {

        config.addPluginModule(
            // Namespace for this settings module
            'se.infomaker.mysettings.settings',
            // The settings component
            MysettingsComponent,
            // Target for this plugin module
            'se.infomaker.npwriter.settings'
        )
    }
}
~~~

__MysettingsComponent.js__ - _The component that is rendered inside the modal_

This example renders one toggle and one text field for the setting keys `mytoggle` and `mytext`.

The setting keys and values for the namespace the plugin module are available to the component through `this.props.properties`. The componenent does not need to bother with the namespace as the it is stripped from all the keys.

Whenever a change is made the component must call the `this.props.onChange(key, value)` callback to let the writer know that a setting has been changed.

*Note that the value is encoded internally as JSON.*

~~~ javascript

import {Component} from 'substance'

class MysettingsComponent.js extends Component {
    constructor(...args) {
        super(...args)

        // Defined fields for this extension module
        this.fields = {
            'mytoggle': "Toggle this toggle to set it to true or false",
            'mytext': "Write a string to the settings"
        }
    }

    render($$) {
        const el = $$('div').append(
            $$('h3').addClass('clear').append(
                this.getLabel('Text styles')
            )
        )

        for (var key in this.fields) {
            let value = ''

            // Incoming key/values available in this.props.properties
            if (this.props.properties && typeof this.props.properties[key] !== 'undefined') {
                value = this.props.properties[key]
            }

            // Incoming setting keys are stripped from their namespace
            if (key === 'showstuff') {
                el.append(
                    this.renderInputOption($$, key, this.fields[key], value)
                )
            }
            else if (key === 'stuffname') {
                el.append(
                    this.renderInputField($$, key, this.fields[key], value)
                )
            }
        }

        return el
    }

    /**
     * Render an input field styled for the writer
     */
    renderInputField($$, key, name, value) {
        return $$('div')
            .addClass('form-group flexible-label')
            .append (
                $$('input')
                    .ref(key)
                    .on('change', () => {
                        // Tell the writer that the value for a key have changed
                        this.props.onChange(key, this.refs[key].val())
                    })
                    .addClass('form-control')
                    .attr({
                        required: 'required',
                        type: 'text',
                        id: 'imext-' + key,
                        placeholder: this.getLabel(name)
                    })
                    .val(value),
                $$('label')
                    .attr('for', 'imext-' + key)
                    .append(
                        this.getLabel(name)
                    )
            )
    }

    /**
     * Render an option toggle available within the writer
     */
    renderInputOption($$, key, name, value) {
        const Toggle = this.getComponent('toggle')

        return $$('div')
            .addClass('form-group')
            .append(
                $$(Toggle, {
                    id: 'crop-toggle',
                    label: this.getLabel(name),
                    checked: value ? true : false,
                    onToggle: (checked) => {
                        // Tell the writer that the value for a key have changed
                        this.props.onChange(key, checked)
                    }
                })
            )
    }
}

export default MysettingsComponent
~~~
