---
layout: default
title: Place in Place
nav_order: 9
parent: REST
grand_parent: API
---

# Get Places Contained within Another Place

Given a list of `Place` DCIDs (e.g. `County`, `State`, `Country`, etc...),
return the DCIDs of places contained within, of a specified type.

**URL** : `/node/places-in`

**Method** : `GET`, `POST`

**Auth required** : YES
<!--- TODO: add link to instructions to get an API key --->

**Required Arguments**:

*   `key`: Your API key.
*   `dcids`: A list of (parent) places, identified by their DCIDs.
*   `placeType`: The type of the contained (child) `Place`s within the given
    DCIDs to filter by. E.g. `City` and `County` are contained within `State`.

## GET Request

**Example**

```bash
curl 'https://api.datacommons.org/node/places-in?key=API_KEY&dcids=geoId/05&dcids=geoId/06&placeType=County'
```

## POST Request

**Example**

```bash
curl -X POST 'https://api.datacommons.org/node/places-in?key=API_KEY' \
-d '{"dcids": ["geoId/05", "geoId/06"], \
     "placeType": "County"}'
```

## Success Response

### **Code** : `200 OK`

**Response content example**

```json
{
    "payload": "<payload string>",
}
```

The "`payload string`" is a string encoding of JSON object that is a list of
objects with fields `dcid` for the parent place and `place` for the contained-in
place.

```json
[
  {
    "dcid": "geoId/05",
    "place": "geoId/05001"
  },
  {
    "dcid": "geoId/05",
    "place": "geoId/05003"
  }
  {
    "dcid": "geoId/06",
    "place": "geoId/06001"
  }
  {
    "dcid": "geoId/06",
    "place": "geoId/06003"
  }
]
```

**NOTE:** Please run `JSON.parse()` on the `payload` field to retrieve the data.
For example, in JavaScript: `var data = JSON.parse(response['payload'])`.

## Error Response

### **Code**: `500 Internal Server Error`

**Request example:**

DCIDs not specified:

```bash
curl -X POST 'https://api.datacommons.org/node/places-in?key=API_KEY' \
-d '{"dcids": []}'
```

placeType not specified `bash curl -X POST
'https://api.datacommons.org/node/places-in?key=API_KEY' \ -d '{"dcids":
["geoId/06]}'`

**Response content example**

```json
{
  "code": 2,
  "message": "missing required arguments"
}
```

### **Code**: `401 Unauthorized`

**Request example:** (API key not specified)

```bash
curl -X POST 'https://api.datacommons.org/node/places-in'
```

**Response content example**

```json
{
  "code": 16,
  "message": "Method doesn't allow unregistered callers (callers without established identity). Please use API Key or other form of API consumer identity to call this API."
}
```