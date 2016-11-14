---
layout: default
title: Fetch asynchronous
---

# Fetch asynchronous data in plugins

## Resource nodes

A resource node is almost like a regular node but it fetches data asynchronous och updates the node automatically.
  
A resource node must implement specific methods and properties.

A resource node must implement a fetchPayload method as well as a static property `isResource`
 and also a property named errorMessage


When the fetchPayload method is complete a callback is made with the new node values as second parameter.
The component then will be updated with values from the node.

The first parameter of the callback is if there's any errors.

~~~ javascript

class MyResourceNode extends BlockNode {
    
    fetchPayload(context, cb) {
           let url = this.url
           
           fetch('url_to_fetch')
                .then(response => response.json())
                .then(json => {
                    cb(null, {
                        nodeProperty: json.someValue,
                        nodeProperty2: json.secondValue
                    })
                })
                .catch((e) => {
                    cb(e)
                })
    }
}   

MyResourceNode.isResource = true
MyResourceNode.define({
    ...
    errorMessage: { type: 'string', optional: true },
    ...
})



~~~


## Using the API and Proxy

It's often a problem when javascript needs to fetch data from another source, so we have provided a lightweight proxy server that
you use to fetch the data you need.

We also provide a method that will the response status code to be > 199 and < 300. This is because the fetch
API doesn't reject depending on status codes.

~~~ javascript

const urlToFetch = 'http://api.krisinformation.se/v1/capmessage?format=json'

api.router.get('/api/proxy/', {url: urlToFetch})
    .then(response => api.router.checkForOKStatus(response))
    .then(response => response.json())
    .then(json => {
        console.log("Response is", json)
    })
    .catch((e) => {
        console.error(e)
    })


~~~ 


