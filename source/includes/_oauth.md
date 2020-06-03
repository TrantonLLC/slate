# OAuth

The Scout API uses an OAuth 2.0 flow in order to grant your application control of user accounts.
To use OAuth, make sure you have your Client ID, Secret Key, and have set redirect URIs in your app settings.

## Start OAuth flow

To start the OAuth flow, redirect your user to a URL in this format:

`https://scoutapp.ai/oauth/new?client_id={your client ID}&redirect_uri={your redirect uri}&scopes={comma,separated,scopes}`

If you make this request with an invalid redirect URI that hasn't been saved in your app settings, or a scope that your application is not approved for,
your will see an error message.

This will send whoever completes the flow to `https://your-redirect-uri.com/?code=adbccfe15b4da2b6050cba89` with a random code.
You will then exchange this code in the next request for an access token.


## Exchange code for access token

```shell
  curl --request POST \
    --url https://scoutapp.ai/api/v1/oauth/token \
    --header 'content-type: application/json' \
    --header 'x-api-key: yoursecretkey' \
    --data '{
  	"code": "adbccfe15b4da2b6050cba89",
  	"redirect_uri": "https://your-redirect-uri.com"
  }'
```

> The above command returns JSON structured like this:

```json
{
  "success": true,
  "user": {
    "id": 1,
    "access_token": "c9e035bef74b804483b7e306",
    "scopes": [
      "checkouts",
      "username"
    ]
  }
}
```

Exchange an OAuth code for an access token.

### HTTP Request

`POST https://scoutapp.ai/api/v1/oauth/token`

### Body Parameters

Parameter | Description
--------- | -----------
code | The OAuth code given in the `code` url parameter after finishing the OAuth flow
redirect_uri | The `redirect_uri` url parameter taht was used to begin the OAuth flow

## Get user info using access_token


```shell
curl --request GET \
  --url 'https://scoutapp.ai/api/v1/oauth/info?access_token=c9e035bef74b804483b7e306' \
  --header 'x-api-key: yoursecretkey'
```

> The above command returns JSON structured like this:

```json
{
  "success": true,
  "user": {
    "id": 1,
    "username": "shrey"
  }
}
```

Validate your stored access token by using it to get user info. If you're using this on a desktop app, we recommend that you do this on each launch of your application to ensure
that if they remove access from their account, you reflect that accurately.

### HTTP Request

`GET https://scoutapp.ai/api/v1/oauth/info`

### Query Parameters

Parameter | Description
--------- | -----------
access_token | The user's access token

