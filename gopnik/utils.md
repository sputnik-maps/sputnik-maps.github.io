---
layout: page
title: Gopnik utils
---

# Utils

## gopnikbench

Utility for map style benchmarking. Run with _-h_ for details.

## gopnikprerender

Coordinates prerendering process.
Accepts a plan (see _gopnikprerenderimport_) and a config in the following format:

```json
{
	"Prerender": {
		"UIAddr":   ":8088",
		"Logging": {
		},
		"Slaves": {
				"Plugin":       "ClusterConfigPlugin",
				"PluginConfig": {
						"Nodes":    ["localhost:8095"]
				}
		}
	},
	"MetaSize": 8,
	"TileSize": 256
}

```

Config parameters:

 Name           | Type             | Default value | Description
 -------------- | ---------------- | ------------- | ----------------------------------
 DebugAddr      | string           | ":8097"       | Address for monitoring
 UIAddr         | string           | ":8088"       | WebUI address
 Threads        | int              | 1             | set GOMAXPROCS to Threads. -1 for NumCPU
 Logging        | json.RawMessage  | nil           | Logging options. See [configuration](configuration.html) for details
 PerfLog        | string           | ""            | Performance log file
 Slaves         | app.PluginConfig | nil           | Cluster of slaves
 RequestTimeout | string           | "1h"          | Timeout for request to gopnik
 NodeQueueSize  | int              | 100           | Number of parallel requests per node

## gopnikcopy

Tiles copy utility.
Accepts a plan (same as for prerendering) and a config in the following format:

```json
{
	"Copy": {
		"From": {
			"Plugin": "...",
			"PluginConfig": {
			}
		},
		"To": {
			"Plugin": "...",
			"PluginConfig": {
			}
		},
		"Threads": 20,
		"Retries": 3,
		"SkipErrors": false,
		"Logging": {
		},
	},
	"MetaSize": 8,
	"TileSize": 256
}
```

Config parameters:

 Name        | Type             | Default value | Description
 ----------- | ---------------- | ------------- | ----------------------------------------------------------------------
 From        | app.PluginConfig | nil           | Plugin to copy from
 To          | app.PluginConfig | nil           | Plugin to copy to
 Threads     | int              | 1             | Use _Threads_ connections
 Retries     | int              | 0             | Retries on errors
 SkipErrors  | bool             | false         | Do not stop process if error occurs
 Logging     | json.RawMessage  | nil           | Logging options. See [configuration](configuration.html) for details

## gopnikperf

Performance log analyzer with web UI. Run with _-h_ for details.

## gopnikprerenderimport

Creates plan file for _gopnikprerender_. Run with _-h_ for details.
