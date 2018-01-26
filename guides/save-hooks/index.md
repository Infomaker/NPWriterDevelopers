---
layout: default
title: Validation and execute hooks when saving
active: /guides/
---

# Execute hooks before and after save

## Overview
It is possible to add hooks in various stages of the saving process. There are three general hooks that as well as the more special validation hook. All hooks must return a `Promise()` that is either resolved or reject by the hook. Any `reject()` will cancel the process and show an error message to the user.

*Any plugin can provide hooks or validation. The order of multiple hooks in the same stage is not guaranteed so no assumption should be made on the execution order.*

All plugins must register their hooks and validations in `PluginPackage.js` when the plugin registers.

The general stages of the saving process is

1. Before Validation hooks
2. Validation
3. Before save hooks
4. _Saving..._
5. After save hooks

### Before validation
In the before validation hooks it is allowed to alter the article programmatically through the API. This is useful if you want to change something automatically before the validation and saving process continues.

### Validation
These are not technically hooks. The NPWriter executes one or many provided validation methods. These methods add messages, warnings and errors which are then presented to the user. Any error message will stop the process.

*Any changes done programmatically to the article in the validation process - or later - will not be saves and potentially lost.*

### Before save hook
Before save hooks are executed After potential changes of the article and when the valitation passed.

### After save hook
When the article has been successfully saved the after save hooks are executed.


## Example

A compact example with one hook of each type and a validation in one package file.

~~~ javascript
import {hook} from 'writer'
import {Validator, api} from 'writer'

class MyValidation extends Validator {
    // Required
    constructor(...args) {
        super(...args)
    }

    validate() {
        const headlines = this.newsItem.querySelectorAll('idf > group element[type="headline"]')
        const headline = headlines[0].childNodes.length === 0 ? '' : headlines[0].firstChild.textContent.trim()

        if (headlines.length === 0) {
            // Informative message
            this.addValidationMessage('The article is missing a headline!')
        }
        else if (headline === '') {
            // Warning
            this.addWarning('The article has an empty headline')
        }

        if (api.newsItem.getAuthors().length === 0) {
            // Error - will cancel saving
            this.addError('The article must have an author')
        }
    }
}

class MyHookBeforeValidate {
    execute(type) {
        return new Promise((resolve, reject) => {
            // Do something, async or not
            resolve()
        })
    }
}

class MyHookBeforeSave {
    execute(type) {
        return new Promise((resolve, reject) => {
            // Do something, async or not
            resolve()
        })
    }
}

class MyHookAfterSave {
    execute(type) {
        return new Promise((resolve, reject) => {
            // Do something, async or not
            resolve()
        })
    }
}

export default {
    name: 'myplugin',
    version: '1.0',
    configure: function (config, configObject) {

        config.addValidator(MyValidation)

        config.addHook(hook.BEFORE_VALIDATE, MyHookBeforeValidate)
        config.addHook(hook.BEFORE_SAVE, MyHookBeforeSave)
        config.addHook(hook.AFTER_SAVE, MyHookAfterSave)
    }
}

~~~
