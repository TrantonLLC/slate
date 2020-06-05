# Key resetting

The key resetting API allows people to reset their connected bot keys by presenting you with authentication information that you 
can use to verify their ownership. To make this functional, you will need to do 3 simple things:

- Get a **key resetting API key** from us which we'll send to your endpoints
- Create a **key validation** endpoint
- Create a **key reset** endpoint

We'll require you to make endpoints have the same base_url, with the endpoints `/validity` and `/reset`. You may put anything you want before
that such as `/api/v1/scout`, `/api/scout`, or nothing at all.

The key resetting and validation API relies on status codes, and does not require you provide a body with any context.

## Key validation endpoint

> The request we'll send your endpoint to validate

```shell
curl --request GET \
  --url 'https://yourendpoint.com/validity?key=XXXXX-XXXXX-XXXXX-XXXXX&access_token=c9e035bef74b804483b7e306&discord_ids=95889183222034432,95889183222034432' \
  --header 'x-api-key: keyresettingapikey'
```

To check validation with your endpoint, we'll send a request in the format shown above. We'll send you 3 things. 

1. The `key` is the key that the user is attempting to validate
    - Return a `404` if the key specified doesn't exist
2. The `access_token` is their access token made when signing in with Scout on your application (OAuth)
    - The `access_token` should be saved to their user account in your database when they complete the OAuth flow. In this endpoint, you
      should use it to check if the key is bound to a user with this `access_token`. If so, you should return a `200`.
3. The `discord_ids` is a comma delimited list of discord accounts connected to their Scout account
    - The `discord_ids` are used in the case of a Scout user that has multiple keys of your application on different Discord accounts. If we send a `discord_id` 
    of that is bound to this key, return a `200`.
    
If checks 2 or 3 fail, return a `401` unauthorized. If everything passes, return a status `200` with an empty body.

## Key reset endpoint 

> The request we'll send your endpoint to reset

```shell
curl --request POST \
  --url https://yourendpoint.com/reset \
  --header 'content-type: application/json' \
  --header 'x-api-key: botapikey' \
  --data '{
	"key": "XXXXX-XXXXX-XXXXX-XXXXX",
	"access_token": "c9e035bef74b804483b7e306",
	"discord_ids": [
		"95889183222034432",
		"95889183222034432",
		"95889183222034432",
		"95889183222034432"
	]
}'
```

To check validation with your endpoint, we'll send a request in the format shown above. We'll send you 3 things. 

1. The `key` is the key that the user is attempting to validate
    - Return a `404` if the key specified doesn't exist
2. The `access_token` is their access token made when signing in with Scout on your application (OAuth)
    - Same as validity endpoint
3. The `discord_ids` is a comma delimited list of discord accounts connected to their Scout account
    - Same as validity endpoint
    
If checks 2 or 3 fail, return a `401` unauthorized. If everything passes, reset the key
and return a status `200` with an empty body.
