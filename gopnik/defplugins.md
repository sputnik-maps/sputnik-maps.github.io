---
layout: page
title: Gopnik default plugins
---

# Default plugins

## bboxtagfilter

Filter plugin uses bbox for tag validation.

Options:

 Name   | Type             | Default value | Description
 ------ | ---------------- | ------------- | --------------------------------------------
 Rules  | []filterItem     | nil           | Filter rules. See below

filterItem parameters:

 Name            | Type       | Default value | Description
 --------------- | ---------- | ------------- | ----------------------------------------------------------
 BBoxes          | []BBox     | nil           | List of bboxes. Rule matches if any bbox in the list matches
 Drop            | []string   | nil           | Drop all tags from list if rule matches
 Add             | []string   | nil           | Add all tags from list if rule matches
 DropOtherwise   | []string   | nil           | Drop all tags from list if rule not matches
 AddOtherwise    | []string   | nil           | Add all tags from list if rule not matches

BBox:

 Name            | Type       | Default value | Description
 --------------- | ---------- | ------------- | -----------
 MinLat          | float64    | 0.0           |
 MaxLat          | float64    | 0.0           |
 MinLon          | float64    | 0.0           |
 MaxLon          | float64    | 0.0           |
 MinZoom         | uint64     | 0             |
 MaxZoom         | uint64     | 0             |

## cacheproxy

Cache plugin that allows use of multiple backends for reading and storing tiles.

 Name            | Type          | Default value | Description
 --------------- | ------------- | ------------- | ---------------------------------------------------
 Backends        | []backendConf | nil           | Cache backends
 WriteToFirst    | bool          | false         | Store tiles in the first relevant backend if true
 ReadFromFirst   | bool          | false         | Reads tiles from the first relevant backend if true
 WriteToAny      | bool          | false         | Write is successful if set operation on any backend is successful

backendConf:

 Name            | Type                        | Default value | Description
 --------------- | --------------------------- | ------------- | -------------------------------------------------------
 Name            | string                      | ""            | Plugin name
 Plugin          | gopnik.CachePluginInterface | nil           | Plugin config
 MinZoom         | uint64                      | 0             | Minimum zoom
 MaxZoom         | uint64                      | 0             | Maximum zoom
 Tags            | []string                    | nil           | Use backend only if request has all tags from the list
 ReadOnly        | bool                        | false         | Do not use backend for set operations

## clusterconfig

Plugin for very simple cluster management.
Loads information about cluster from config.

 Name            | Type       | Default value | Description
 --------------- | ---------- | ------------- | --------------------------------------
 Nodes           | []string   | nil           | Slave addresses in format "host:port"

## emptyfilter

Stub for filter plugin. Does nothing.

## fakecache

Fake plugin for cache.

Options:

 Name            | Type       | Default value | Description
 --------------- | ---------- | ------------- | -----------------------------------
 UseStubImage    | bool       | false         | Return stab image for each request
 GetSleep        | string     | ""            | Sleep to emulate storage latency
 SetSleep        | string     | ""            | Sleep to emulate storage latency

## filecache

Cache plugin uses mod_tile file format.

 Name            | Type             | Default value | Description
 --------------- | ---------------- | ------------- | -----------------------------------
 Root            | string           | "/tmp/tiles"  | Directory for storing tiles
 UseHash         | bool             | true          | Use flat directory scheme if false

## graphite

Monitoring plugin.
Exports metrics over [graphite](http://graphite.wikidot.com/) protocol.

 Name            | Type             | Default value | Description
 --------------- | ---------------- | ------------- | -----------
 Host            | string           | ""            |
 Port            | int              | 0             |
 Prefix          | string           | ""            |

## kvcache

Cache plugin that stores tiles in key-value backend.

 Name                | Type             | Default value | Description
 ------------------- | ---------------- | ------------- | --------------------------------------------------
 Backend             | app.PluginConfig | nil           | Key-value storage backend
 UseMultilevel       | bool             | false         | Optimize one-color tiles (e.g. water, forest, etc)
 UseSecondLevelCache | bool             | false         | Cache one-color pngs in dispatchers memory
 Prefix              | string           | ""            | Key prefix

## memorykv

In-memory key-value plugin. Useful for testing. Plugin has no options.

## simplefilecache

Simple cache plugin. Tiles are saved as is. One file per tile.

 Name            | Type       | Default value | Description
 --------------- | ---------- | ------------- | -----------------------------------
 Root            | string     | "/tmp/tiles"  | Directory for storing tiles
