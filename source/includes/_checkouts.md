# Checkouts

The Scout checkouts API allows you to post a user's checkout and have it be added into their Scout inventory as an item.
To post a user's checkout, you will first need to fully authenticate them using OAuth with the following scopes:

`checkouts,username`

The `username` scope is optional, but encouraged so you can display their Scout username after they sign in.


## Post a checkout

```shell
curl --request POST \
  --url https://ingest.scoutapp.ai/ingest \
  --header 'content-type: application/json' \
  --header 'x-api-key: yoursecretkey' \
  --data '{
  "order_id": "123124124",
  "purchase_currency": "usd",
  "purchase_price": 15000,
  "tax": 1500,
  "shipping_price": 1000,
  "name": "Nike Air Force 1 Low Off-White",
  "sku": "CI1173-400",
  "size": "1",
  "brand": "Nike",
  "color": "University Blue",
  "store": "Kith",
  "user_id": 1,
  "access_token": "c9e035bef74b804483b7e306 ",
  "checkout_time": 1591086812
}'
```

> The above command returns JSON structured like this:

```json
{
  "success": true
}
```

Posting a checkout should be done alongside sending any other requests you do on a successful checkout (Discord webhook, analytics webhook, etc.).
**PLEASE ONLY POST CHECKOUTS FROM YOUR SERVER, NOT FROM CLIENTS**


### HTTP Request

`POST https://ingest.scoutapp.ai/ingest`

### Body Parameters

Parameter | Description
--------- | -----------
order_id | The order ID of the purchase made
purchase_currency | The currency that the purchase was made in
purchase_price | The purchase price in cents ($15.50 purchase = 1550)
tax | The purchase tax in cents `optional`
shipping_price | The shipping price in cents `optional`
name | The name of the item
sku | The SKU or Style ID of the item `optional`
size | The purchased item's size. If item size is not present, use `OS`
brand | The purchased item's brand `optional`
color | The purchased item's color `optional`
store | The store that the item was purchased at `optional`
user_id | The Scout user's ID that checked out
access_token | The Scout user's access token
checkout_time | An epoch timestamp in **seconds** of the checkout 

