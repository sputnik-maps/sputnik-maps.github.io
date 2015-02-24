---
layout: page
title: Gopnik installation
---

# Installation

## Go SDK
 * [Go](http://golang.org/doc/install)

## Go libraries
 * [github.com/cheggaaa/pb](https://github.com/cheggaaa/pb/)
 * [github.com/davecgh/go-spew/spew](https://github.com/davecgh/go-spew/spew/)
 * [github.com/go-martini/martini](https://github.com/go-martini/martini/)
 * [github.com/martini-contrib/staticbin](https://github.com/martini-contrib/staticbin/)
 * [github.com/op/go-logging](https://github.com/op/go-logging/)
 * [github.com/orofarne/hmetrics2](https://github.com/orofarne/hmetrics2/)
 * [github.com/orofarne/hmetrics2-graphite](https://github.com/orofarne/hmetrics2-graphite/)
 * [github.com/orofarne/strict-json](https://github.com/orofarne/strict-json/)
 * [github.com/yosssi/rendergold](https://github.com/yosssi/rendergold/)
 * [gopkg.in/check.v1](https://labix.org/gocheck)
 * [github.com/stretchr/testify](https://github.com/stretchr/testify)
 * [github.com/jteeuwen/go-bindata](https://github.com/jteeuwen/go-bindata)
 * [github.com/golang/protobuf/{proto,protoc-gen-go}](https://github.com/golang/protobuf)
 * [code.google.com/p/freetype-go/freetype](https://code.google.com/p/freetype-go/)

The easiest way to get it is to setup [GOPATH](https://golang.org/doc/code.html#GOPATH) and use [go get](https://golang.org/cmd/go/#hdr-Download_and_install_packages_and_dependencies) utility.

## C++ tools and libraries
 * [cmake](http://www.cmake.org/)
 * C++11 compitible compiler
 * [mapnik](https://github.com/mapnik/mapnik/wiki/Mapnik-Installation)
 * [boost](http://www.boost.org/)

## Build
```bash
./bootstrap.bash
./build.bash
```

## External plugins
Because Gopnik is a statically linked binary, plugins should be defined at the build stage.
Use

```bash
./bootstrap.bash --plugin <plugin_package>
```

to enable a plugin.
