---
layout: default
titlt: Documentation to be categorized
---


# Stuff to be categorized

The following stuff is just added while developing some of the features so we dont forget to write it down.
It will later be categorized in to different guides or pages.


## Writer API Endpoints



#### Available third party libraries

__lodash__

~~~ javascript

const {lodash} = writer
console.log(lodash.isObject({})) // true

~~~

~~~ javascript

const {isObject, isEmpty} = writer.lodash
console.log(isObject({})) // true
console.log(isEmpty(null)) // true

~~~


__moment.js__

[Moment.js](http://momentjs.com/) is library for parsing, manipulating, validating and displaying dates and time.

~~~ javascript

const {moment} = writer.moment

moment().format() //"2016-10-31T15:14:37+01:00"

~~~


## How to add labels to plugins

Since version 2 of Newspilot writer the label system have had a make over.

The plugin itself is now responsible for providing its own label.

This is made in the package.

~~~ javascript

config.addLabel('my-label-key', {
en: 'The english label',
sv: 'Den svenska titeln'
})

~~~

To later retrieve the label in your component just use `getLabel`

~~~ javascript

render($$) {
return $$('div').append(this.getLabel('my-label-key'))
}

~~~ 
