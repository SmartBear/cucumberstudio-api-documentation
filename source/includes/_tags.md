# Tags

## Include tags when requesting elements

```http
GET https://studio.cucumberstudio.com/api/projects/<project_id>/folders/<folder_id>?include=tags HTTP/1.1
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
curl "https://studio.cucumberstudio.com/api/projects/<project_id>/folders/<folder_id>?include=tags" \
    -H 'accept: application/vnd.api+json; version=1' \
    -H 'access-token: <your access token>' \
    -H 'uid: <your uid>' \
    -H 'client: <your client id>'
```

```json
{
  "data":
    {
      "type": "folders",
      "id": "2",
      "attributes": {
        "created-at" : "2017-02-28T11:39:08.281Z",
        "updated-at" : "2017-02-28T11:39:08.281Z",
        "last-author" : "harry@example.org",
        "name": "The Philosopher's Stone",
        "description": "",
        "parent-id": 1
      },
      "links": {
        "self": "/folders/2"
      },
      "relationships": {
        "tags": {
          "data": [
            {
              "type": "tags",
              "id": "6537"
            }
          ]
        }
      }
    },
  "included": [
    {
      "type": "tags",
      "id": "6539",
      "attributes": {
        "key": "horcruxes",
        "value": ""
      },
      "links": {
        "self": "/tags/6539"
      }
    }
  ]
}
```

You can use the JSONAPI [include syntax](http://jsonapi.org/format/#fetching-includes) to fetch tags
alongside parent elements. Elements can be scenarios, actionwords, folders, test runs, tests and test folders.
This is working when requesting for a list of elements, and for a single element.


## Get tags of a given action word

```http
GET https://studio.cucumberstudio.com/api/projects/<project_id>/actionwords/<actionword_id>/tags HTTP/1.1
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
curl "https://studio.cucumberstudio.com/api/projects/<project_id>/actionwords/<actionword_id>/tags" \
    -H 'accept: application/vnd.api+json; version=1' \
    -H 'access-token: <your access token>' \
    -H 'uid: <your uid>' \
    -H 'client: <your client id>'
```

```json
{
  "data": [
    {
      "type": "tags",
      "id": "1",
      "attributes": {
        "key": "platform",
        "value": "Android"
      },
      "links": {
        "self": "/tags/1"
      }
    },
    {
      "type": "tags",
      "id": "2",
      "attributes": {
        "key": "automated",
        "value": "yes"
      },
      "links": {
        "self": "/tags/2"
      }
    }
  ]
}
```

This endpoint retrieves all tags of a given action word.

### URL Parameters

Parameter | Description
--------- | -----------
project_id | The ID of the project that contains the wanted action word
actionword_id | The ID of the action word you want to retrieve the tags from


## Get tags of a given scenario

```http
GET https://studio.cucumberstudio.com/api/projects/<project_id>/scenarios/<scenario_id>/tags HTTP/1.1
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
curl "https://studio.cucumberstudio.com/api/projects/<project_id>/scenarios/<scenario_id>/tags" \
    -H 'accept: application/vnd.api+json; version=1' \
    -H 'access-token: <your access token>' \
    -H 'uid: <your uid>' \
    -H 'client: <your client id>'
```

```json
{
  "data": [
    {
      "type": "tags",
      "id": "1",
      "attributes": {
        "key": "Status",
        "value": "InProgress"
      },
      "links": {
        "self": "/tags/1"
      }
    },
    {
      "type": "tags",
      "id": "2",
      "attributes": {
        "key": "Priority",
        "value": "Over9000"
      },
      "links": {
        "self": "/tags/2"
      }
    }
  ]
}
```
This endpoint retrieves all tags of a given scenario.

### URL Parameters

Parameter | Description
--------- | -----------
project_id | The ID of the project that contains the wanted scenario
scenario_id | The ID of the scenario you want to retrieve the tags from

## Get tags of a given folder

```http
GET https://studio.cucumberstudio.com/api/projects/<project_id>/folders/<folder_id>/tags HTTP/1.1
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
curl "https://studio.cucumberstudio.com/api/projects/<project_id>/folders/<folder_id>/tags" \
    -H 'accept: application/vnd.api+json; version=1' \
    -H 'access-token: <your access token>' \
    -H 'uid: <your uid>' \
    -H 'client: <your client id>'
```

```json
{
  "data": [
    {
      "type": "tags",
      "id": "1",
      "attributes": {
        "key": "Javascript",
        "value": ""
      },
      "links": {
        "self": "/tags/1"
      }
    },
    {
      "type": "tags",
      "id": "2",
      "attributes": {
        "key": "Sprint",
        "value": "1"
      },
      "links": {
        "self": "/tags/2"
      }
    }
  ]
}
```
This endpoint retrieves all tags of a given folder.

### URL Parameters

Parameter | Description
--------- | -----------
project_id | The ID of the project that contains the wanted folder
folder_id | The ID of the folder you want to retrieve the tags from

## Get tags of a given test run

```http
GET https://studio.cucumberstudio.com/api/projects/<project_id>/test_runs/<test_run_id>/tags HTTP/1.1
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
curl "https://studio.cucumberstudio.com/api/projects/<project_id>/test_runs/<test_run_id>/tags" \
    -H 'accept: application/vnd.api+json; version=1' \
    -H 'access-token: <your access token>' \
    -H 'uid: <your uid>' \
    -H 'client: <your client id>'
```

```json
{
  "data": [
    {
      "type": "tags",
      "id": "1",
      "attributes": {
        "key": "priority",
        "value": "high"
      },
      "links": {
        "self": "/tags/1"
      }
    },
    {
      "type": "tags",
      "id": "2",
      "attributes": {
        "key": "jira",
        "value": "test"
      },
      "links": {
        "self": "/tags/2"
      }
    }
  ]
}
```
This endpoint retrieves all tags of a given test run.

### URL Parameters

Parameter | Description
--------- | -----------
project_id | The ID of the project that contains the wanted test run
test_run_id | The ID of the test run you want to retrieve the tags from

## Get tags of a given test

```http
GET https://studio.cucumberstudio.com/api/projects/<project_id>/test_runs/<test_run_id>/test_snapshots/<test_snapshot_id>/tags HTTP/1.1
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
curl "https://studio.cucumberstudio.com/api/projects/<project_id>/test_runs/<test_run_id>/test_snapshots/<test_snapshot_id>/tags" \
    -H 'accept: application/vnd.api+json; version=1' \
    -H 'access-token: <your access token>' \
    -H 'uid: <your uid>' \
    -H 'client: <your client id>'
```

```json
{
  "data": [
    {
      "type": "tags",
      "id": "1",
      "attributes": {
        "key": "priority",
        "value": "high"
      },
      "links": {
        "self": "/tags/1"
      }
    },
    {
      "type": "tags",
      "id": "2",
      "attributes": {
        "key": "jira",
        "value": "test"
      },
      "links": {
        "self": "/tags/2"
      }
    }
  ]
}
```
This endpoint retrieves all tags of a given test.

### URL Parameters

Parameter | Description
--------- | -----------
project_id | The ID of the project that contains the wanted test run
test_run_id | The ID of the test run where the test is
test_snapshot_id | The ID of the test in the test-run you want to retrieve the tags from

## Create tag in a scenario

```http
POST https://studio.cucumberstudio.com/api/projects/<project_id>/scenarios/<scenario_id>/tags HTTP/1.1
Accept: application/vnd.api+json; version=1
access-token: <your access token>
client: <your client id>
uid: <your uid>

{
  "data": {
    "attributes": {
      "key": "priority",
      "value": "high"
    }
  }
}
```

```http
HTTP/1.1 201 Created
Content-Type: application/vnd.api+json
```

```shell
curl -X POST "https://studio.cucumberstudio.com/api/projects/<project_id>/scenarios/<scenario_id>/tags" \
    -H 'accept: application/vnd.api+json; version=1' \
    -H 'access-token: <your access token>' \
    -H 'uid: <your uid>' \
    -H 'client: <your client id>'
```

```json
{
  "data": [
    {
      "type": "tags",
      "id": "1",
      "attributes": {
        "key": "priority",
        "value": "high"
      },
      "links": {
        "self": "/tags/1"
      }
    }
  ]
}
```
This endpoint creates a new tag in a scenario.

Parameter | Description
--------- | -----------
project_id | The ID of the project that contains the wanted scenario
scenario_id | The ID of the scenario where you want to create the tag

## Create tag in a test run

```http
POST https://studio.cucumberstudio.com/api/projects/<project_id>/test_runs/<test_run_id>/tags HTTP/1.1
Accept: application/vnd.api+json; version=1
access-token: <your access token>
client: <your client id>
uid: <your uid>

{
  "data": {
    "attributes": {
      "key": "priority",
      "value": "high"
    }
  }
}
```

```http
HTTP/1.1 201 Created
Content-Type: application/vnd.api+json
```

```shell
curl -X POST "https://studio.cucumberstudio.com/api/projects/<project_id>/test_runs/<test_run_id>/tags" \
    -H 'accept: application/vnd.api+json; version=1' \
    -H 'access-token: <your access token>' \
    -H 'uid: <your uid>' \
    -H 'client: <your client id>'
```

```json
{
  "data": [
    {
      "type": "tags",
      "id": "1",
      "attributes": {
        "key": "priority",
        "value": "high"
      },
      "links": {
        "self": "/tags/1"
      }
    }
  ]
}
```
This endpoint creates a new tag in a test run.

Parameter | Description
--------- | -----------
project_id | The ID of the project that contains the wanted test run
test_run_id | The ID of the test run where you want to create the tag

## Create tag in a test

```http
POST https://studio.cucumberstudio.com/api/projects/<project_id>/test_runs/<test_run_id>/test_snapshots/<test_snapshot_id>/tags HTTP/1.1
Accept: application/vnd.api+json; version=1
access-token: <your access token>
client: <your client id>
uid: <your uid>

{
  "data": {
    "attributes": {
      "key": "priority",
      "value": "high"
    }
  }
}
```

```http
HTTP/1.1 201 Created
Content-Type: application/vnd.api+json
```

```shell
curl -X POST "https://studio.cucumberstudio.com/api/projects/<project_id>/test_runs/<test_run_id>/test_snapshots/<test_snapshot_id>/tags" \
    -H 'accept: application/vnd.api+json; version=1' \
    -H 'access-token: <your access token>' \
    -H 'uid: <your uid>' \
    -H 'client: <your client id>'
```

```json
{
  "data": [
    {
      "type": "tags",
      "id": "1",
      "attributes": {
        "key": "priority",
        "value": "high"
      },
      "links": {
        "self": "/tags/1"
      }
    }
  ]
}
```

This endpoint creates a new tag in a test.

Parameter | Description
--------- | -----------
project_id | The ID of the project that contains the wanted test run
test_run_id | The ID of the test run where the test is
test_snapshot_id | The ID of the test in the test-run where you want to create the tag

## Update a tag in a scenario

```http
PATCH https://studio.cucumberstudio.com/api/projects/<project_id>/scenarios/<scenario_id>/tags/<tag_id> HTTP/1.1
Content-Type: application/json; charset=utf-8
Accept: application/vnd.api+json; version=1
access-token: <your access token>
client: <your client id>
uid: <your uid>

{
  "data": {
    "type": "tags",
    "id": 5,
    "attributes": {
      "key": "priority",
      "value": "low"
    }
  }
}
```

```http
HTTP/1.1 200 OK
Content-Type: application/vnd.api+json
```

```shell
curl -XPATCH "https://studio.cucumberstudio.com/api/projects/<project_id>/scenarios/<scenario_id>/tags/<tag_id>" \
    -H 'Content-Type: application/json' \
    -H 'accept: application/vnd.api+json; version=1' \
    -H 'access-token: <your access token>' \
    -H 'uid: <your uid>' \
    -H 'client: <your client id>' \
    --data '{"data": {"type": "tags","id": 5,"attributes": {"key": "priority","value": "low"}}}'
```

```json
{
  "data": [
    {
      "type": "tags",
      "id": "5",
      "attributes": {
        "key": "priority",
        "value": "low"
      },
      "links": {
        "self": "/tags/1"
      }
    }
  ]
}
```

This endpoint updates a tag in a scenario.

Parameter | Description
--------- | -----------
project_id | The ID of the project that contains the wanted scenario
scenario_id | The ID of the scenario where you want to update the tag
tag_id | The ID of the tag you want to update

## Update a tag in a test run

```http
PATCH https://studio.cucumberstudio.com/api/projects/<project_id>/test_runs/<test_run_id>/tags/<tag_id> HTTP/1.1
Content-Type: application/json; charset=utf-8
Accept: application/vnd.api+json; version=1
access-token: <your access token>
client: <your client id>
uid: <your uid>

{
  "data": {
    "type": "tags",
    "id": 5,
    "attributes": {
      "key": "priority",
      "value": "low"
    }
  }
}
```

```http
HTTP/1.1 200 OK
Content-Type: application/vnd.api+json
```

```shell
curl -XPATCH "https://studio.cucumberstudio.com/api/projects/<project_id>/test_runs/<test_run_id>/tags/<tag_id>" \
    -H 'Content-Type: application/json' \
    -H 'accept: application/vnd.api+json; version=1' \
    -H 'access-token: <your access token>' \
    -H 'uid: <your uid>' \
    -H 'client: <your client id>' \
    --data '{"data": {"type": "tags","id": 5,"attributes": {"key": "priority","value": "low"}}}'
```

```json
{
  "data": [
    {
      "type": "tags",
      "id": "5",
      "attributes": {
        "key": "priority",
        "value": "low"
      },
      "links": {
        "self": "/tags/1"
      }
    }
  ]
}
```

This endpoint updates a tag in a test run.

Parameter | Description
--------- | -----------
project_id | The ID of the project that contains the wanted test run
test_run_id | The ID of the test run where you want to update the tag
tag_id | The ID of the tag you want to update

## Update a tag in a test

```http
PATCH https://studio.cucumberstudio.com/api/projects/<project_id>/test_runs/<test_run_id>/test_snapshots/<test_snapshot_id>/tags/<tag_id> HTTP/1.1
Content-Type: application/json; charset=utf-8
Accept: application/vnd.api+json; version=1
access-token: <your access token>
client: <your client id>
uid: <your uid>

{
  "data": {
    "type": "tags",
    "id": 5,
    "attributes": {
      "key": "priority",
      "value": "low"
    }
  }
}
```

```http
HTTP/1.1 200 OK
Content-Type: application/vnd.api+json
```

```shell
curl -XPATCH "https://studio.cucumberstudio.com/api/projects/<project_id>/test_runs/<test_run_id>/test_snapshots/<test_snapshot_id>/tags/<tag_id>" \
    -H 'Content-Type: application/json' \
    -H 'accept: application/vnd.api+json; version=1' \
    -H 'access-token: <your access token>' \
    -H 'uid: <your uid>' \
    -H 'client: <your client id>' \
    --data '{"data": {"type": "tags","id": 5,"attributes": {"key": "priority","value": "low"}}}'
```

```json
{
  "data": [
    {
      "type": "tags",
      "id": "5",
      "attributes": {
        "key": "priority",
        "value": "low"
      },
      "links": {
        "self": "/tags/1"
      }
    }
  ]
}
```

This endpoint updates a tag in a test run.


Parameter | Description
--------- | -----------
project_id | The ID of the project that contains the wanted test run
test_run_id | The ID of the test run where the test is
test_snapshot_id | The ID of the test you want to update the tag
tag_id | The ID of the tag you want to update

## Delete a tag in a scenario

```http
DELETE https://studio.cucumberstudio.com/api/projects/<project_id>/scenarios/<scenario_id>/tags/<tag_id> HTTP/1.1
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
curl -XDELETE "https://studio.cucumberstudio.com/api/projects/<project_id>/scenarios/<scenario_id>/tags<tag_id>" \
    -H 'accept: application/vnd.api+json; version=1' \
    -H 'access-token: <your access token>' \
    -H 'uid: <your uid>' \
    -H 'client: <your client id>'
```

```json
{}
```

This endpoint deletes a tag in a scenario.


Parameter | Description
--------- | -----------
project_id | The ID of the project that contains the wanted scenario
scenario_id | The ID of the scenario where you want to delete the tag
tag_id | The ID of the tag you want to delete

## Delete a tag in a test run

```http
DELETE https://studio.cucumberstudio.com/api/projects/<project_id>/test_runs/<test_run_id>/tags/<tag_id> HTTP/1.1
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
curl -XDELETE "https://studio.cucumberstudio.com/api/projects/<project_id>/test_runs/<test_run_id>/tags<tag_id>" \
    -H 'accept: application/vnd.api+json; version=1' \
    -H 'access-token: <your access token>' \
    -H 'uid: <your uid>' \
    -H 'client: <your client id>'
```

```json
{}
```

This endpoint deletes a tag in a test run.


Parameter | Description
--------- | -----------
project_id | The ID of the project that contains the wanted test run
test_run_id | The ID of the test run where you want to delete the tag
tag_id | The ID of the tag you want to delete

## Delete a tag in a test

```http
DELETE https://studio.cucumberstudio.com/api/projects/<project_id>/test_runs/<test_run_id>/test_snapshots/<test_snapshot_id>/tags/<tag_id> HTTP/1.1
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
curl -XDELETE "https://studio.cucumberstudio.com/api/projects/<project_id>/test_runs/<test_run_id>/test_snapshots/<test_snapshot_id>/tags<tag_id>" \
    -H 'accept: application/vnd.api+json; version=1' \
    -H 'access-token: <your access token>' \
    -H 'uid: <your uid>' \
    -H 'client: <your client id>'
```

```json
{}
```

This endpoint deletes a tag in a test run.


Parameter | Description
--------- | -----------
project_id | The ID of the project that contains the wanted test run
test_run_id | The ID of the test run where the test is
test_snapshot_id | The ID of the test where you want to delete the tag
tag_id | The ID of the tag you want to delete

## Create tags alongside elements

```http
POST https://studio.cucumberstudio.com/api/projects/<project_id>/<element_type> HTTP/1.1
Content-Type: application/json; charset=utf-8
Accept: application/vnd.api+json; version=1
access-token: <your access token>
client: <your client id>
uid: <your uid>

{
  "data": {
    "attributes": {
      ...
    },
    "relationships": {
      "tags": {
        "data": [
          { "type": "tag", "key": "automated" },
          { "type": "tag", "key": "sprint", value: "2" },
          { "type": "tag", "key": "priority", value: "high" }
        ]
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
curl -XPOST "https://studio.cucumberstudio.com/api/projects/<project_id>/<element_type>" \
    -H 'Content-Type: application/json' \
    -H 'accept: application/vnd.api+json; version=1' \
    -H 'access-token: <your access token>' \
    -H 'uid: <your uid>' \
    -H 'client: <your client id>' \
    --data '{"data": {"attributes": {}, "relationships": { "tags": { "data": [ { "type": "tag", "key": "automated" }, { "type": "tag", "key": "sprint", "value": "2" }, { "type": "tag", "key": "priority", "value": "high" }] } }}'
```

```json
{
  "data":
    {
      "type": "test-runs",
      "id": "1",
      "attributes": {
        ...
      },
      "links": {
        "self": "/test-runs/1"
      },
      "included": [
        { "type": "tags", "id": "1", "attributes": { "key": "automated", "value": "" }, "links": { "self": "/tags/1" } },
        { "type": "tags", "id": "2", "attributes": { "key": "sprint", "value": "2" }, "links": { "self": "/tags/2" } },
        { "type": "tags", "id": "3", "attributes": { "key": "priority", "value": "high" }, "links": { "self": "/tags/3" } }
      ]
    }
}
```

With some elements (such as the test runs and scenarios), you can create one or multiple tags linked to the created element.
This can be done by specifying the "relationships" element.

Parameter    | Description
---------    | -----------
project_id   | The ID of the project in wich you want to create the actionword
element_type | The type of element you want to create (scenarios, test_runs)
