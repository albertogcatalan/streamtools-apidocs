---
title: Streamtools API Docs

language_tabs: # must be one of https://git.io/vQNgJ
  - shell

toc_footers:
  - <a href='https://streamtools.com'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/slatedocs/slate'>Documentation Powered by Slate</a>

includes:
  - errors
  - changelog

search: true

code_clipboard: true
---

# Introduction

Welcome! On this page, you will find information on implementing the Streamtools API.
The API is developed in REST and all requests both returned and received are in JSON format.

We are continuously developing the project and therefore the documentation will be progressively updated. You can see the section [changelog](#changelog) to see the changes.

# Endpoint URL
All URLs start from `https://app.streamtools.com/api/v1/`.

It is necessary to specify the version number in the URL. At the moment `v1`.

# Authentication

> To authorize, use this code:

```shell
# With shell, you can just pass the correct header with each request
curl "https://app.streamtools.com/api/v1/auth/" \
  -H "X-API-KEY: apikey"
```


> Make sure to replace `apikey` with your API key.

Streamtools uses API keys to allow access to the API. You can see your personal API key at your [account](https://app.streamtools.com/account/).

Streamtools expects for the API key to be included in all API requests to the server in a header that looks like the following:

`X-API-KEY: apikey`

<aside class="notice">
You must replace <code>apikey</code> with your personal API key.
</aside>

# Zapier Alerts

## Get All Alerts

```shell
curl "https://app.streamtools.com/api/v1/getList/" \
  -H "X-API-KEY: apikey"
```

> The above command returns JSON structured like this:

```json
[
  {
        "id": 1,
        "slug": "ZA1i1234",
        "title": "Hello"
    },
    {
        "id": 2,
        "slug": "ZA1i1235",
        "title": "Hello again"
    },
]
```

This endpoint retrieves all alerts.

### HTTP Request

`GET https://app.streamtools.com/api/v1/getList/`

## Send content to Alert


```shell
curl "https://app.streamtools.com/api/v1/zapier/" \
  -X POST \
  -H "X-API-KEY: apikey"
```

> The above command returns JSON structured like this:

```json
{
    "id": "ZA_1",
    "title": "Hello",
    "type": "integration",
    "slug": "ZA1i1234",
    "status": "active",
    "content": "{content}",
    "updated": 1606469618,
    "requestContent": "my new content",
    "requestAPIStatus": true,
    "requestList": "ZA1i1234"
}
```

This endpoint send data to a specific alert.

### HTTP Request

`POST https://app.streamtools.com/api/v1/zapier/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
alert_list | The alert ID
alert_content | The content you send


# Webhooks
## Send data to Widget webhook


```shell
curl "https://app.streamtools.com/webhook/timer/OT1i2934500/" \
  -X POST \
  -H "X-API-KEY: apikey" \
  -d action="start" \
```

> The above command returns JSON structured like this:

```json
{
    "id": "OT1i2934500",
    "widgetURL": "https://app.streamtools.com/widget/timer/OT1i2934500",
    "object": "timer",
    "action": "start",
    "status": "OK"
}
```

This endpoint send data to a specific widget.

### HTTP Request

`POST https://app.streamtools.com/webhook/<WIDGET>/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
action | Action data: at the moment only accepts "start"