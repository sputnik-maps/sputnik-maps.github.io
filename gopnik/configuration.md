---
layout: page
title: Gopnik configuration
---

# Gopnik configuration

## Config format
Gopnik uses [JSON](http://json.org/) format for config files with
[strict-json](https://github.com/orofarne/strict-json) parsing library.
This library disallows unexpected fields inside config sections;
fileds starting with # are treated as comments:

```json
{
	"Normal section": {
		"some": "values"
	},
	"#Ignored section": {
		"some": "values"
	}
}
```

One config can be used for all daemons and utilities, or separate configs can be specified. General config structure is:

```json
{
	"#Daemons configuration": null,
	"Dispatcher": {
		"..."
	},
	"Render": {
		"..."
	},
	"Prerender": {
		"..."
	},
	"PrerenderSlave": {
		"..."
	},

	"#Common configuration": null,
	"MetaSize": 8,
	"TileSize": 256,
	"CachePlugin": {
		"Plugin": "CacheProxyPlugin",
		"PluginConfig": {
			"..."
		}
	},
	"RenderPools": [
		"..."
	]
}
```

## Common options
 * MetaSize - tiles per [metatile](http://wiki.openstreetmap.org/wiki/Meta_tiles).
See also [nice article](https://www.mapbox.com/tilemill/docs/guides/metatiles/)
about metatiles from [MapBox](https://www.mapbox.com/).
 * TileSize - "base" size of tiles. Commonly is 256.
 * CachePlugin - pluggable tile storage. See below how to use the plugin system.
 * RenderPools - configuration of render pools. See details below.
 * MonitoringPlugins - metric exporters. See details below.

## Dispatcher

Dispatcher parameters:

 Name             | Type             | Default value | Description
 ---------------- | ---------------- | ------------- | --------------------------------------------
 Addr             | string           | ":8080"       | Main address
 DebugAddr        | string           | ":9080"       | Address for monitoring
 HTTPReadTimeout  | string           | "60s"         | HTTP client read timeout
 HTTPWriteTimeout | string           | "60s"         | HTTP client write timeout
 RequestTimeout   | string           | "600s"        | Timeout for dynamic rendering request
 PingPeriod       | string           | "30s"         | Ping gopniks every PingPeriod
 Threads          | int              | _NumCPU_      | set GOMAXPROCS to Threads. -1 for NumCPU
 Logging          | json.RawMessage  | nil           | see logging section below
 ClusterPlugin    | app.PluginConfig | nil           | dynamic rendering cluster plugin
 FilterPlugin     | app.PluginConfig | nil           | filter plugin for tags

## Render

 Name             | Type             | Default value | Description
 ---------------- | ---------------- | ------------- | ---------------------------------------------------------------
 Addr             | string           | ":8090"       | Main address
 DebugAddr        | string           | ":9090"       | Address for monitoring
 HTTPReadTimeout  | string           | "60s"         | HTTP client read timeout
 HTTPWriteTimeout | string           | "60s"         | HTTP client write timeout
 Threads          | int              | 1             | set GOMAXPROCS to Threads. -1 for NumCPU
 HotCacheDelay    | string           | "0s"          | Time period after cache set is done and before hot cache drop
 Logging          | json.RawMessage  | nil           | see logging section below


## Prerender

 Name      | Type             | Default value | Description
 --------- | ---------------- | ------------- | ----------------------------------
 DebugAddr | string           | ":8097"       | Address for monitoring
 UIAddr    | string           | ":8088"       | WebUI address
 Threads   | int              | 1             | set GOMAXPROCS to Threads. -1 for NumCPU
 Logging   | json.RawMessage  | nil           | see logging section below
 PerfLog   | string           | ""            | Performance log file
 Slaves    | app.PluginConfig | nil           | Cluster of slaves

## PrerenderSlave

 Name          | Type             | Default value | Description
 ------------- | ---------------- | ------------- | ----------------------------------
 RPCAddr       | string           | ":8095"       | RPC address
 DebugAddr     | string           | ":8096"       | Address for monitoring
 SaverPoolSize | int              | _NumCPU_      | Size of savers pool
 Threads       | int              | 1             | set GOMAXPROCS to Threads. -1 means NumCPU
 Logging       | json.RawMessage  | nil           | see logging section below
 PerfLog       | string           | ""            | Performance log file

## Plugins

//There are some kind of plugins: cache, cluster, tag filter and monitoring.
//Options requires plugin look like this:

Different kinds of plugins are: cache, cluster, tag filter and monitoring.
Some options require plugins to be used. They have the following fields:

```json
{
	"Plugin": "...",
	"PluginConfig": {
		"..."
	}
}
```

See [default plugins description](defplugins.html) for details.

## Render pools

RenderPools section is a list of different renders configuration.
Gopnik will use first relevant render from top.
Each render pool is discribed by the following parameters:

 Name      | Type     | Default value  | Description
 --------  | -------- | -------------- | --------------------------------------------------------
 Cmd       | []string | nil            | Slave render command line. See details below
 MinZoom   | uint     | 0              | Minimum allowed zoom
 MaxZoom   | uint     | 0              | Maximum allowed zoom
 Tags      | []string | nil            | Render to be used only when request have _all_ tags from list
 PoolSize  | uint     | 0              | Number of render instances
 QueueSize | uint     | 0              | Size of task queue
 RenderTTL | uint     | 0              | Restart render after RenderTTL completed tasks

## Slave options

Command line options for default render slave:

 Argument     | Type      | Default value  | Description
 ------------ | --------- | -------------- | -----------------------------------------------------------------------
 -stylesheet  | string    | ""             | Path to mapnik xml stylesheet
 -tileSize    | uint      | 256            | Tile size in pixels
 -bufferSize  | int       | -1             | Size of metatile buffer
 -fontsPath   | []string  | nil            | List of font paths
 -pluginsPath | string    | nil            | Mapnik plugins path
 -scaleFactor | float64   | 1.0            | Scale factor. Commonly equals _(slave tile size) / (gopnik's tile size)_

## Logging

Each daemon has logging section with followig options:

 Name     | Type             | Default value            | Description
 -------- | ---------------- | ------------------------ | --------------------------------------------------------------------------------
 Backend  | string           | ""                       | Backend for loggin ("Console", "Syslog" or empty)
 Level    | string           | ""                       | Log level ("Critical", "Error", "Warning", "Notice", "Info", "Debug")
 Format   | string           | "[%{level}] %{message}"  | Log format. See [go-logging page](https://github.com/op/go-logging) for details
 Options  | json.RawMessage  | nil                      | Backend options

### Console backend

Console backend writes log direct to stderr.

 Name     | Type    | Default value  | Description
 -------- | ------- | -------------- | -----------------
 Color    | bool    | false          | Use color output

### Syslog backend

Syslog logger backend connects to the syslog daemon using UNIX sockets
with given prefix. If prefix is not specified, it will be derived
from the launched command.

 Name     | Type    | Default value  | Description
 -------- | ------- | -------------- | -----------------
 Prefix   | string  | ""             | Syslog prefix

## Monitoring exporters

In common section of config you can set list of metric exporters.

```json
{
	"MonitoringPlugins": [
		{
			"..."
		},
		{
			"..."
		}
	]
}
```

Only graphite exporter are available by default.
Check [default plugins description](defplugins.html) page for details.
