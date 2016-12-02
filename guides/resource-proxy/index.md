---
layout: default
title: Use the resource proxy to fetch external data
---

# Fetch external data with the resource proxy

All properties (excepts `headers` and `body`) passed to the proxy will be added to a querystring.

The `url` property is mandatory for the proxy.

For example:

~~~ javascript

{
    url: 'http://infomaker.se',
    param: 'value'
}

~~~

Will be transformed to `?url=http://infomaker.se&param=value`

## Make GET request

To pass custom headers provide a object containing a headers property.

~~~ javascript

import {api} from 'writer'

const request = {
    url: 'http://url.to.fetch',
    headers: {
        "Content-Type": "text/json",
        "x-custom-header": "this is GET",
    }
}
api.router.get('/api/resourceproxy', request)
    .then(response => response.text())
    .then(text => {
        console.log("Text", text);
    })

~~~ 


## POST Request


~~~ javascript

import {api} from 'writer'

const bodyData = {
    name: "John",
    lastname: "Doe"
}
const request = {
    url: 'http://url.to.fetch',
    headers: {
        "Content-Type": "text/json",
        "x-custom-header": "this is POST",
    },
    body: JSON.stringify(bodyData)
}
api.router.post('/api/resourceproxy', request)
    .then(response => response.text())
    .then(text => {
        console.log("Text", text);
    })

~~~ 


## PUT Request


~~~ javascript

import {api} from 'writer'

const bodyData = {
    name: "John",
    lastname: "Doe"
}
const request = {
    url: 'http://url.to.fetch',
    headers: {
        "Content-Type": "text/json",
        "x-custom-header": "this is PUT",
    },
    body: JSON.stringify(bodyData)
}
api.router.put('/api/resourceproxy', request)
    .then(response => response.text())
    .then(text => {
        console.log("Text", text);
    })

~~~ 

## DELETE Request


~~~ javascript

import {api} from 'writer'

const bodyData = {
    name: "John",
    lastname: "Doe"
}
const request = {
    url: 'http://url.to.fetch',
    headers: {
        "Content-Type": "text/json",
        "x-custom-header": "this is PUT",
    },
    body: JSON.stringify(bodyData)
}
api.router.del('/api/resourceproxy', request)
    .then(response => response.text())
    .then(text => {
        console.log("Text", text);
    })

~~~ 

  