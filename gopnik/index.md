---
layout: page
title: Gopnik
group: projects
---

# Gopnik

**Gopnik** is a scalable tile server and a renderer for [slippy map](http://wiki.openstreetmap.org/wiki/Slippy_map) based on [mapnik](http://mapnik.org/) library.

## Warning
Code is unstable. Current status of Gopnik is something like developer preview. Everything may change. Everything may be broken.

## Features
 * high performance tile server
 * management of dynamic rendering requests
 * tags on request, tag filtering
 * support for multiple different styles and rendering options for different zooms and tags
 * distributed render balancer
 * storage and discovery plugins
 * full support of eventually consistent storages
 * some nice utils

## Implementation
 * Gopnik is written in [Go](http://golang.org/) and C++ programming languages.
 * It supports 2.x and 3.x mapnik branches.

## Documentation
 * [Installation](installation.html)
 * [Overview](overview.html)
 * [Configuration](configuration.html)
 * [Default plugins](defplugins.html)
 * [Utils](utils.html)

## Licese
 * Code available under BSD 2-Clause License
 * See full text [here](https://github.com/sputnik-maps/gopnik/blob/master/LICENSE)

## Sources
 * [github.com/sputnik-maps/gopnik](https://github.com/sputnik-maps/gopnik)
