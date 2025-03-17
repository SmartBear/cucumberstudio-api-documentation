# Parameters
## Get parameters of a given scenario

```http
GET https://studio.cucumberstudio.com/api/projects/<project_id>/scenarios/<scenario_id>/parameters HTTP/1.1
Accept: application/vnd.api+json; version=1
access-token: <your access token>
client: <your client id>
uid: <your uid>
```
```http
HTTP/1.1 200 OK
Content-Type: application/vnd.api+json
```

```shell
curl "https://studio.cucumberstudio.com/api/projects/<project_id>/scenarios/<scenario_id>/parameters" \
    -H 'accept: application/vnd.api+json; version=1' \
    -H 'access-token: <your access token>' \
    -H 'uid: <your uid>' \
    -H 'client: <your client id>'
```

```json
{
  "data": [
    {
      "type": "parameters",
      "id": "1",
      "attributes": {
        "name": "parameter-1"
      },
      "links": {
        "self": "/parameters/1"
      }
    },
    {
      "type": "parameters",
      "id": "2",
      "attributes": {
        "name": "parameter-2"
      },
      "links": {
        "self": "/parameters/2"
      }
    }
  ]
}
```
This endpoint retrieves all parameters of a given scenario.

### URL Parameters

Parameter | Description
--------- | -----------
project_id | The ID of the project that contains the wanted scenario
scenario_id | The ID of the scenario you want to retrieve the parameters from

## Get a given parameter

```http
GET https://studio.cucumberstudio.com/api/projects/<project_id>/scenarios/<scenario_id>/parameters/<parameter_id> HTTP/1.1
Accept: application/vnd.api+json; version=1
access-token: <your access token>
client: <your client id>
uid: <your uid>
```
```http
HTTP/1.1 200 OK
Content-Type: application/vnd.api+json
```

```shell
curl "https://studio.cucumberstudio.com/api/projects/<project_id>/scenarios/<scenario_id>/parameters/<parameter_id>" \
    -H 'accept: application/vnd.api+json; version=1' \
    -H 'access-token: <your access token>' \
    -H 'uid: <your uid>' \
    -H 'client: <your client id>'
```

```json
{
  "data": {
      "type": "parameters",
      "id": "1",
      "attributes": {
          "name": "parameter-1"
      },
      "links": {
          "self": "/parameters/1"
      }
  }
}
```

### URL Parameters

Parameter | Description
--------- | -----------
project_id | The ID of the project that contains the wanted scenario
scenario_id | The ID of the scenario you want to retrieve the parameters from
parameter_id | The ID of the parameter you want to show

## Create a parameter

```http
POST https://studio.cucumberstudio.com/api/projects/<project_id>/scenarios/<scenario_id>/parameters HTTP/1.1
Content-Type: application/json; charset=utf-8
Accept: application/vnd.api+json; version=1
access-token: <your access token>
client: <your client id>
uid: <your uid>

{
  "data": {
    "attributes": {
      "name": "parameter-3"
    }
  }
}

```

```http
HTTP/1.1 201 Created
Content-Type: application/vnd.api+json
```

```shell
curl -XPOST "https://studio.cucumberstudio.com/api/projects/<project_id>/scenarios/<scenario_id>/parameters" \
    -H 'Content-Type: application/json' \
    -H 'accept: application/vnd.api+json; version=1' \
    -H 'access-token: <your access token>' \
    -H 'uid: <your uid>' \
    -H 'client: <your client id>' \
    --data '{"data": {"attributes": {"name": "parameter-3"}}}'
```

```json
{
  "data": {
      "type": "parameters",
      "id": "3",
      "attributes": {
          "name": "parameter-3"
      },
      "links": {
          "self": "/parameters/3"
      }
  }
}
```

### URL Parameters

Parameter | Description
--------- | -----------
project_id | The ID of the project that contains the wanted scenario
scenario_id | The ID of the scenario you want to retrieve the parameters from

<aside class="notice">
Please notice that parameter name will get normalized.
</aside>

## Update a parameter

```http
PATCH https://studio.cucumberstudio.com/api/projects/<project_id>/scenarios/<scenario_id>/parameters/<parameter_id> HTTP/1.1
Content-Type: application/json; charset=utf-8
Accept: application/vnd.api+json; version=1
access-token: <your access token>
client: <your client id>
uid: <your uid>

{
  "data": {
      "type": "parameters",
      "id": "3",
      "attributes": {
          "name": "new parameter-3 name"
      }
  }
}

```

```http
HTTP/1.1 200 OK
Content-Type: application/vnd.api+json
```

```shell
curl -XPATCH "https://studio.cucumberstudio.com/api/projects/<project_id>/scenarios/<scenario_id>/parameters/<parameter_id>" \
    -H 'Content-Type: application/json' \
    -H 'accept: application/vnd.api+json; version=1' \
    -H 'access-token: <your access token>' \
    -H 'uid: <your uid>' \
    -H 'client: <your client id>' \
    --data '{"data": { "type": "parameters", "id": "3", "attributes": {"name": "new parameter-3 name"}}}'
```

```json
{
    "data": {
        "type": "parameters",
        "id": "3",
        "attributes": {
            "name": "new_parameter-3_name"
        },
        "links": {
            "self": "/parameters/3"
        }
    }
}
```

### URL Parameters

Parameter | Description
--------- | -----------
project_id | The ID of the project that contains the wanted scenario
scenario_id | The ID of the scenario you want to retrieve the parameters from
parameter_id | The ID of the parameter you want to update

<aside class="notice">
Please notice that parameter name will get normalized.
</aside>

## Delete a parameter

```http
DELETE https://studio.cucumberstudio.com/api/projects/<project_id>/scenarios/<scenario_id>/parameters/<parameter_id> HTTP/1.1
Accept: application/vnd.api+json; version=1
access-token: <your access token>
client: <your client id>
uid: <your uid>
```

```http
HTTP/1.1 200 OK
Content-Type: application/vnd.api+json
```

```shell
curl -XDELETE "https://studio.cucumberstudio.com/api/projects/<project_id>/scenarios/<scenario_id>/parameters/<parameter_id>" \
    -H 'accept: application/vnd.api+json; version=1' \
    -H 'access-token: <your access token>' \
    -H 'uid: <your uid>' \
    -H 'client: <your client id>'
```

```json
{}
```

### URL Parameters

Parameter | Description
--------- | -----------
project_id | The ID of the project that contains the wanted scenario
scenario_id | The ID of the scenario you want to retrieve the parameters from
parameter_id | The ID of the parameter you want to destroy
