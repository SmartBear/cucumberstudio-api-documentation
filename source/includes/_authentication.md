# Authentication

> To get your credentials:

```http
POST https://studio.cucumberstudio.com/api/auth/sign_in HTTP/1.1
Content-Type: application/json

{"email": "my_cucumberstudio_account", "password": "my_cucumberstudio_account"}
```

```http
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
access-token: sUaWO8m8v5Lkv5pxnLCXzA
token-type: Bearer
client: AfLp4PsN9ZieqHas-X5lrA
expiry: 1486047985
uid: my_cucumberstudio_account
```

```shell
curl -XPOST \
    -H "Content-Type: application/json" \
    -d '{"email": "my_cucumberstudio_account", "password": "my_cucumberstudio_account"}' \
    -D - https://studio.cucumberstudio.com/api/auth/sign_in

HTTP/1.1 200 OK
# snip.
access-token: sUaWO8m8v5Lkv5pxnLCXzA
token-type: Bearer
client: AfLp4PsN9ZieqHas-X5lrA
expiry: 1486047985
uid: my_cucumberstudio_account
# snip.

```

> An API call example

```http
GET https://studio.cucumberstudio.com/api/<endpoint> HTTP/1.1
Accept: application/vnd.api+json; version=1
access-token: <your access token>
client: <your client id>
uid: <your uid>
```

```shell
curl https://studio.cucumberstudio.com/api/<endpoint> \
    -H 'accept: application/vnd.api+json; version=1' \
    -H 'access-token: <your access token>' \
    -H 'uid: <your uid>' \
    -H 'client: <your client id>'
```


Before sending requests to our endpoints, you need an authentication token.
This token is made up of three data:

* The access-token
* Your client id
* Your uid

You can get this authentication token using the `auth/sign_in` endpoint
(only working if you registered to CucumberStudio using your email) or directly
in your CucumberStudio profile page.

<aside class="notice">
  If you are getting your credentials through the API, your token will be set
  in the response headers
</aside>

 CucumberStudio expects for the authentication token to be included in all API requests
 to the server, in the HTTP headers of your requests

## Useful information about the access-token

* The token lifespan is set to a year. After that, you won't be able to access
  to the API anymore. Don't forget to generate a new token before the expiration
  date and to update your scripts
* The expiration date is returned on every HTTP response in the `expiry` HTTP
  header. The expiry date is in POSIX timestamp format (number of seconds
  elapsed since 1 January 1970 00:00:00 UTC). Example: `expiry: 1486047985`.
* You can use up to ten authentication tokens at the same time, with different
  clients
