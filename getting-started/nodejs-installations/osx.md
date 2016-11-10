---
layout: default
title: Installing nodejs in OS X
---

# {{ page.title }}

## Using an installer package
Download the installer package from the [Node.js site](https://nodejs.org/en/download/). 

After the installation finishes, please close and re-open Terminal to allow environment variable changes to kick in.

## Using Homebrew

If you are using [Homebrew](http://brew.sh) on OS X, you may install Node.js by issuing:

    $ brew install homebrew/versions/node6-lts 

After the installation finishes, please close and re-open Terminal to allow environment variable changes to kick in.

## Test the installation

Open up the Terminal and type

    $ node --version
    v6.9.1
    
    $ npm --version
    3.10.8


