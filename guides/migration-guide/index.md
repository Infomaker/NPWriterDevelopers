---
layout: default
title: Basic information
active: /guides/
---
# Migration from version 1 to 3

## Dependency imports

In the first version we used `require` to add dependencies. In the new version we are using the ES6 `import` statement.

~~~ javascript

import {Component} from 'substance'
import {api, NilUUID, event, moment, idGenerator, lodash, jxon} from 'writer' 

~~~