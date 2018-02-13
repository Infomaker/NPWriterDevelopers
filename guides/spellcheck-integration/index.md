---
layout: default
title: Integrating External Spell Checking
active: /guides/
---

# Integrating External Spell Checking

## Overview
The Writer comes with a built in spell checker for swedish, english, and dutch. It's possible to create 
API endpoints and integrate your own spell checking and suggestions into the Writer.

It's not necessary to implement both spell-checking and suggestions, since both are optional. 

## Writer Configuration
In order to enable the spellcheck integration, the Writer's server-config needs to be edited. The following should be 
added to your server-config's `external`-config object:

~~~json

"spellcheck": {
    "check": {
        "url": "[your-spellcheck-endpoint]",
        "headers": {
        	"x-foo": "bar"
        }
    },
    "suggestion": {
        "url": "[your-suggestion-endpoint]",
        "headers": {
        	"x-foo": "bar"
        }
    }
}

~~~

### Fields Explanation

| Field                                    | Description  |
| ---------------------------------------- | ------------ |
| `external.spellcheck`                    | Contains the configuration for external spellchecking endpoints. |
| `external.spellcheck.check`              | **Optional** Object containing configuration for external spellcheck requests. |
| `external.spellcheck.check.url`          | **Required** Full url and path to your check request implementation. |
| `external.spellcheck.check.headers`      | **Optional** Key-value object with extra header's which will be used in the request to your API. |
| `external.spellcheck.suggestion`         | **Optional** Object containing configuration for external suggestion requests. |
| `external.spellcheck.suggestion.url`     | **Required** Full url and path to your suggestion request implementation. |
| `external.spellcheck.suggestion.headers` | **Optional** Key-value object with extra header's which will be used in the request to your API. |

The `headers`-properties are useful if you need to send additional headers to your API.

## API Specification
Your API needs to be able to handle the following requests to integrate with spell checking and suggestion.

### Language Codes
Language codes from the writer are sent in the format `[language-identifier]_[region_identifier]`. Where `[language-identifier]` follows
the [ISO 639-1](https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes) standard, which is two letters, lowercased.
The `[region-identifier]` follows the [ISO 3166-2](https://en.wikipedia.org/wiki/ISO_3166-2) standard, which is two letters, uppercased.

Examples:
`sv_SE`, `en_GB`, `en_US`, `nl_NL`

### SpellCheck Request
The API must be able to receive the following request on an endpoint you define:

#### Request

~~~

    POST [your-spellcheck-endpoint]
    headers
        Accept: application/json
        Content-Type: application/json 
    body
        {
            "lang": "sv_SE",
            "words": [
                { "start": 0, "end": 5, "text": "Lorem" },
                { "start": 6, "end": 11, "text": "ipsum" },
                { "start": 12, "end": 17, "text": "dolor" },
                { "start": 18, "end": 21, "text": "sit" },
                { "start": 22, "end": 26, "text": "amet" },
                { "start": 28, "end": 39, "text": "consectetur" },
                { "start": 40, "end": 50, "text": "adipiscing" },
                { "start": 51, "end": 55, "text": "elit" },
                { "start": 57, "end": 60, "text": "sed" },
                { "start": 61, "end": 63, "text": "do" },
                { "start": 64, "end": 71, "text": "eiusmod" },
                { "start": 72, "end": 78, "text": "tempor" }
            ]
        }

~~~

#### Response
The API should respond with a single array containing the misspelled words in the same json-format as 
they were sent, if no words were misspelled, response should contain an empty array.

**Response Format**

~~~

headers
    Content-Type: application/json 
body
    [
      { "start": 0, "end": 5, "text": "Lorem" },
      { "start": 6, "end": 11, "text": "ipsum" },
      { "start": 12, "end": 17, "text": "dolor" },
      { "start": 61, "end": 63, "text": "do" },
      { "start": 64, "end": 71, "text": "eiusmod" }
    ]

~~~

#### Example Request
Your API should be able to perform the call below, and output an array of the misspelled words, or an empty array.

~~~javascript

fetch("[your-spellcheck-endpoint]", {
    method: 'post',
    headers: {'Accept': 'application/json', 'Content-Type': 'application/json'},
    body: JSON.stringify({
        "lang": "[language_code]",
        "words": [
            { "start": 0, "end": 5, "text": "Lorem" },
            { "start": 6, "end": 11, "text": "ipsum" },
            { "start": 12, "end": 17, "text": "dolor" },
            { "start": 61, "end": 63, "text": "do" },
            { "start": 64, "end": 71, "text": "eiusmod" }
        ]
    })
})
    .then((res) => res.json())
    .then((json) => console.log(json))

~~~

Output:

~~~json

    [
        {"start":0,"end":5,"text":"Lorem"},
        {"start":6,"end":11,"text":"ipsum"},
        {"start":64,"end":71,"text":"eiusmod"}
    ]

~~~

### Suggestions
The API must be able to receive the following request on an endpoint you define:

#### Request

~~~

    POST [your-suggestion-endpoint]
    headers
        Accept: application/json
        Content-Type: application/json
    URL Params
        word=String
        lang=[language_code]

~~~

#### Response
The API should respond with a single array containing the misspelled words in the same json-format as 
they were sent, if no words were misspelled, response should be an empty array.

**Response Format**

~~~

    headers
        Content-Type: application/json
    body
        [
            "tempot",
            "tempo",
            "tempon",
            "tempos",
            "teorem"
        ]

~~~

#### Example Request
Your API should be able to perform the call below, and output an array of words, or an empty array.

~~~javascript

fetch("[your-suggestion-endpoint]?word=tempor&lang=en_US", {
    headers: {'Accept': 'application/json', 'Content-Type': 'application/json'}
})
    .then((res) => res.json())
    .then((json) => console.log(json))

~~~

Output

~~~json

    ["tempo", "temper", "tempos", "temp or", "temp-or", "tempo r"]

~~~