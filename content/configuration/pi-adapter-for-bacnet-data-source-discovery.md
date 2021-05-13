---
uid: PIAdapterBACnetDataSourceDiscovery
---

# BACnet data source discovery

When running a discovery against the data source of a BACnet adapter, you can specify optional query parameters. The query discovers the contents of the data source and narrows the scope of the discovery. Following a completed discovery, you can add the discovered items to the data selection.

## BACnet query string

The string of the **query** parameter must contain string items in follow form:

```text
<BACNET_QUERY_EXAMPLE>
```

String item | Required | Description
--|--|--
**<STRING_ITEM>** | Required/Optional | <DESCRIPTION_OF_STRING_ITEM>
**<STRING_ITEM>** | Required/Optional | <DESCRIPTION_OF_STRING_ITEM>
**<STRING_ITEM>** | Required/Optional | <DESCRIPTION_OF_STRING_ITEM>

### Query rules

The following rules apply for specifying the query string:

* Multiple queries are separated by a semicolon (`;`).
* Partial queries are terminated by a multi-level wildcard (`#`).
* A query cannot be terminated by a trailing slash (`/`).
* A query cannot start with a leading slash (`/`) or `$`.
* Topics are case sensitive.

**Note:** The data source may contain thousands of metrics. Therefore, follow these recommendations to return useful query results:

* Limit use of the `#` character.
* Create specific query strings or break down the query into different discoveries.

#### Wildcards

Wildcards are allowed in the query with the following specifications:

* A single-level wildcard replaces one topic level and is indicated by `+`.
* A multi-level wildcard covers many topic levels and is indicated by `#`.
* Wildcards can be combined.
* `#` must not be used more than once and can only be used at the end of the topic.
* No query, an empty string, or `null` as the query parameter is equivalent to `#`.

## Discovery query example

The query parameter of the BACnet component must be specified in the following form:

```text
<BACNET_QUERY_EXAMPLE>
```

### BACnet data source discovery initiation

```json
<EXAMPLE_JSON_FOR_DISCOVERY_POST_REQUEST_THAT_INCLUDES_BACNET_QUERY>
```

### BACnet data source discovery results

```json
<EXAMPLE_JSON_FOR_DISCOVERY_GET_REQUEST>
```
