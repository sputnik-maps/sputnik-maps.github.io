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
 * [github.com/orofarne/freetype-go/freetype](github.com/orofarne/freetype-go/freetype)
 * [git.apache.org/thrift.git/lib/go/thrift](https://thrift.apache.org/)

The easiest way to get it is to use [gom](https://github.com/mattn/gom).

```bash
go get github.com/mattn/gom
gom install
```

## C++ tools and libraries
 * [cmake](http://www.cmake.org/)
 * C++11 compitible compiler
 * [mapnik](https://github.com/mapnik/mapnik/wiki/Mapnik-Installation)
 * [boost](http://www.boost.org/)

## Build
```bash
gom exec ./bootstrap.bash
gom exec ./build.bash
```

## External plugins
Because Gopnik is a statically linked binary, plugins should be defined at the build stage.
Use

```bash
./bootstrap.bash --plugin <plugin_package>
```

to enable a plugin.
