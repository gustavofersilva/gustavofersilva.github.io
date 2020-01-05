---
layout: post
title: Golang installation
date:   2019-03-14 16:48:00 +0100
categories: [backend, golang]
tags: [programming, backend, golang, how-to-install]
---
## Check installation
~~~ bash
go version
~~~

## Environment variables
**GOROOT**  
Folder where go was installated. It must only be set when installing to a custom location.

**GOPATH**  
Place to get, build and install packages outside the standard Go Tree.  
<!--more-->

~~~ bash
# golang
export GOPATH=/home/msanchez/go/packages
export GOROOT=/home/msanchez/Programs/go
export PATH=$PATH:$GOROOT/bin:$GOPATH/bin
~~~

[Source](https://stackoverflow.com/questions/7970390/what-should-be-the-values-of-gopath-and-goroot)

## Multiple workspaces
For a custom installation, it's possible to give more than one value to `GOPATH`.
~~~ bash
export GOPATH="/home/msanchez/go/packages/bin:/home/msanchez/Documents/Personal/Github/language_testing/golang"
~~~

The first value is used as default to install packages. The second and next ones may be used as standalone workspaces. It's important for the root of the workspace to be `/src`, otherwise it will complain and not compile into `/bin`.

## IDE preparation
I use Sublime, to get it ready:

* `ctrl + shift + p`
* `install package`  

Install the packages:
* `GoOracle`
* `All Autocomplete`

_(missing steps)_

* install [https://github.com/golang/sublime-build](https://github.com/golang/sublime-build)

To compile / build / run
* `ctrl + shift + P`
* `go install`
* `go run`
