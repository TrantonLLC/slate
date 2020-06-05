---
title: Scout API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell

toc_footers:
  - <a href='https://scoutapp.ai/app/apps'>Scout Developer portal</a>

includes:
  - oauth
  - checkouts
  - key_resetting
  - errors
  - brand
 

search: true
---

# Introduction

Welcome to the Scout API. The Scout API is organized around [REST](https://en.wikipedia.org/wiki/Representational_state_transfer), accepts
JSON request bodies, and returns JSON encoded responses.

The base URL is `https://scoutapp.ai/api/v1`. Any endpoints described should be appended to the base URL described here.

<br>
<br>
URL parameters and body parameters for requests are described by tables. All parameters listed are required, unless they have
the `optional` label like so:

### Example Body Parameters

Parameter | Description
--------- | -----------
order_id | The order ID of the checkout
tags | Order tags `optional`

# Authentication

> To authorize, use this code:

```shell
curl "api_endpoint_here"
  -H "x-api-key: yoursecretkey"
```

> Make sure to replace `yoursecretkey` with your application's secret key.

The Scout API uses application secret keys in request headers to authenticate requests. You can get your secret key from the
[developer page](https://scoutapp.ai/app/apps) inside Scout.

`x-api-key: yoursecretkey`

# Acceptable currencies

The following currencies are currently accepted in every request:

```json
{
   "currencies":[
      {
         "code":"usd",
         "symbol":"$"
      },
      {
         "code":"eur",
         "symbol":"€"
      },
      {
         "code":"gbp",
         "symbol":"£"
      },
      {
         "code":"cad",
         "symbol":"C$"
      },
      {
         "code":"cny",
         "symbol":"¥"
      },
      {
         "code":"hkd",
         "symbol":"HK$"
      },
      {
         "code":"aud",
         "symbol":"A$"
      },
      {
         "code":"dkk",
         "symbol":"Kr."
      },
      {
         "code":"sek",
         "symbol":"Kr"
      },
      {
         "code":"czk",
         "symbol":"Kč"
      }
   ]
}
```
