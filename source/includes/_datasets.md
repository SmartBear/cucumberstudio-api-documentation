# Datasets
## Get datasets of a given scenario

```http
GET https://studio.cucumberstudio.com/api/projects/<project_id>/scenarios/<scenario_id>/datasets HTTP/1.1
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
curl "https://studio.cucumberstudio.com/api/projects/<project_id>/scenarios/<scenario_id>/datasets" \
    -H 'accept: application/vnd.api+json; version=1' \
    -H 'access-token: <your access token>' \
    -H 'uid: <your uid>' \
    -H 'client: <your client id>'
```

```json
{
  "data": [
    {
      "type": "datasets",
      "id": "1",
      "attributes": {
        "name": "dataset-1",
        "data": {
          "parameter-1": "value 1-1",
          "parameter-2": "value 1-2"
        }
      },
      "links": {
        "self": "/datasets/1"
      }
    },
    {
      "type": "datasets",
      "id": "2",
      "attributes": {
        "name": "dataset-2",
        "data": {
          "parameter-1": "value 2-1",
          "parameter-2": "value 2-2"
        }
      },
      "links": {
        "self": "/datasets/2"
      }
    }
  ]
}
```
This endpoint retrieves all datasets of a given scenario.

### URL Parameters

Parameter | Description
--------- | -----------
project_id | The ID of the project that contains the wanted scenario
scenario_id | The ID of the scenario you want to retrieve the datasets from

## Get a given dataset

```http
GET https://studio.cucumberstudio.com/api/projects/<project_id>/scenarios/<scenario_id>/datasets/<dataset_id> HTTP/1.1
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
curl "https://studio.cucumberstudio.com/api/projects/<project_id>/scenarios/<scenario_id>/datasets/<dataset_id>" \
    -H 'accept: application/vnd.api+json; version=1' \
    -H 'access-token: <your access token>' \
    -H 'uid: <your uid>' \
    -H 'client: <your client id>'
```

```json
{
  "data": {
      "type": "datasets",
      "id": "1",
      "attributes": {
          "name": "dataset-1",
          "data": {
              "parameter-1": "value 1-1",
              "parameter-2": "value 1-2"
          }
      },
      "links": {
          "self": "/datasets/1"
      }
  }
}
```

### URL Parameters

Parameter | Description
--------- | -----------
project_id | The ID of the project that contains the wanted scenario
scenario_id | The ID of the scenario you want to retrieve the datasets from
dataset_id | The ID of the dataset you want to show

## Create a dataset

```http
POST https://studio.cucumberstudio.com/api/projects/<project_id>/scenarios/<scenario_id>/datasets HTTP/1.1
Content-Type: application/json; charset=utf-8
Accept: application/vnd.api+json; version=1
access-token: <your access token>
client: <your client id>
uid: <your uid>

{
  "data": {
    "attributes": {
      "name": "dataset-3",
      "data": {
        "parameter-1": "value 3-1",
        "parameter-2": "value 3-2"
      }
    }
  }
}

```

```http
HTTP/1.1 201 Created
Content-Type: application/vnd.api+json
```

```shell
curl -XPOST "https://studio.cucumberstudio.com/api/projects/<project_id>/scenarios/<scenario_id>/datasets" \
    -H 'Content-Type: application/json' \
    -H 'accept: application/vnd.api+json; version=1' \
    -H 'access-token: <your access token>' \
    -H 'uid: <your uid>' \
    -H 'client: <your client id>' \
    --data '{"data": {"attributes": {"name": "dataset-3","data": {"parameter-1": "value 3-1", "parameter-2": "value 3-2"}}}}'
```

```json
{
  "data": {
      "type": "datasets",
      "id": "3",
      "attributes": {
          "name": "dataset-3",
          "data": {
              "parameter-1": "value 3-1",
              "parameter-2": "value 3-2"
          }
      },
      "links": {
          "self": "/datasets/3"
      }
  }
}
```

### URL Parameters

Parameter | Description
--------- | -----------
project_id | The ID of the project that contains the wanted scenario
scenario_id | The ID of the scenario you want to retrieve the datasets from

## Update a dataset

```http
PATCH https://studio.cucumberstudio.com/api/projects/<project_id>/scenarios/<scenario_id>/datasets/<dataset_id> HTTP/1.1
Content-Type: application/json; charset=utf-8
Accept: application/vnd.api+json; version=1
access-token: <your access token>
client: <your client id>
uid: <your uid>

{
  "data": {
      "type": "datasets",
      "id": "3",
      "attributes": {
          "name": "new dataset-3 name",
          "data": {
              "parameter-1": "new value 3-1",
              "parameter-2": "new value 3-2"
          }
      }
  }
}

```

```http
HTTP/1.1 200 OK
Content-Type: application/vnd.api+json
```

```shell
curl -XPATCH "https://studio.cucumberstudio.com/api/projects/<project_id>/scenarios/<scenario_id>/datasets/<dataset_id>" \
    -H 'Content-Type: application/json' \
    -H 'accept: application/vnd.api+json; version=1' \
    -H 'access-token: <your access token>' \
    -H 'uid: <your uid>' \
    -H 'client: <your client id>' \
    --data '{"data": { "type": "datasets", "id": "3", "attributes": {"name": "new dataset-3 name","data": {"parameter-1": "new value 3-1", "parameter-2": "new value 3-2"}}}}'
```

```json
{
    "data": {
        "type": "datasets",
        "id": "3",
        "attributes": {
            "name": "new dataset-3 name",
            "data": {
                "parameter-1": "new value 3-1",
                "parameter-2": "new value 3-2"
            }
        },
        "links": {
            "self": "/datasets/3"
        }
    }
}
```

### URL Parameters

Parameter | Description
--------- | -----------
project_id | The ID of the project that contains the wanted scenario
scenario_id | The ID of the scenario you want to retrieve the datasets from
dataset_id | The ID of the dataset you want to update

## Delete a dataset

```http
DELETE https://studio.cucumberstudio.com/api/projects/<project_id>/scenarios/<scenario_id>/datasets/<dataset_id> HTTP/1.1
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
curl -XDELETE "https://studio.cucumberstudio.com/api/projects/<project_id>/scenarios/<scenario_id>/datasets/<dataset_id>" \
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
scenario_id | The ID of the scenario you want to retrieve the datasets from
dataset_id | The ID of the dataset you want to destroy

# Datatables

```http
GET https://studio.cucumberstudio.com/api/projects/<project_id>/scenarios/<scenario_id>/datatable HTTP/1.1
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
curl "https://studio.cucumberstudio.com/api/projects/<project_id>/scenarios/<scenario_id>/datatable" \
    -H 'accept: application/vnd.api+json; version=1' \
    -H 'access-token: <your access token>' \
    -H 'uid: <your uid>' \
    -H 'client: <your client id>'
```

```json
{
  "data": [
    {
      "type": "datasets",
      "id": "1",
      "attributes": {
        "name": "dataset-1",
        "data": {
          "parameter-1": "value 1-1",
          "parameter-2": "value 1-2"
        }
      },
      "links": {
        "self": "/datasets/1"
      }
    },
    {
      "type": "datasets",
      "id": "2",
      "attributes": {
        "name": "dataset-2",
        "data": {
          "parameter-1": "value 2-1",
          "parameter-2": "value 2-2"
        }
      },
      "links": {
        "self": "/datasets/2"
      }
    }
  ]
}
```

A `datatable` endpoint is available as an alias for the [`datasets`](#datasets)
resource.
