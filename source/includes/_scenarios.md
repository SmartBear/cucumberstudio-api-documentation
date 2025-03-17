# Scenarios

## Get scenarios of a given project

```http
GET https://studio.cucumberstudio.com/api/projects/<project_id>/scenarios[?include=<fields>] HTTP/1.1
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
curl "https://studio.cucumberstudio.com/api/projects/<project_id>/scenarios[?include=<fields>]" \
    -H 'accept: application/vnd.api+json; version=1' \
    -H 'access-token: <your access token>' \
    -H 'uid: <your uid>' \
    -H 'client: <your client id>'
```

```json
{
  "data": [
    {
      "type": "scenarios",
      "id": "1",
      "attributes": {
        "created-at" : "2017-02-28T11:39:08.281Z",
        "updated-at" : "2017-02-28T11:39:08.281Z",
        "last-author" : "harry@example.org",
        "name": "Find horcruxes",
        "description": "That will help to kill Voldemort",
        "folder-id": 162629,
        "definition": "scenario 'Find horcruxes' do\n  step {action: \"Find the last one\"}\n  step {result: \"Found it!\"}\nend\n"
      },
      "links": {
        "self": "/scenarios/1"
      },
      "relationships": {
          "folder": {},
          "tags": {},
          "actionwords": {},
          "test-snapshots": {}
      }
    },
    {
      "type": "scenarios",
      "id": "2",
      "attributes": {
        "created-at" : "2017-02-28T11:39:08.281Z",
        "updated-at" : "2017-02-28T11:39:08.281Z",
        "last-author" : "harry@example.org",
        "name": "Defeat Voldemort",
        "description": "And save the world, hurray !",
        "folder-id": 162629,
        "definition": "scenario 'Defeat Voldemort' do\nend\n"
      },
      "links": {
        "self": "/scenarios/2"
      },
      "relationships": {
          "folder": {},
          "tags": {},
          "actionwords": {},
          "test-snapshots": {}
      }
    }
  ]
}
```

This endpoint retrieves all scenarios of a given project.

You can use the JSONAPI [include syntax](http://jsonapi.org/format/#fetching-includes) to fetch additional data
about your tests.

The available additional data are the following:

Field name | Description
-----------| -----------
folder | The folder scenarios belongs to
tags | The tags of the scenarios
actionwords | Actionwords used by the scenarios
test-snapshots | All linked test-snapshots in test runs including their last test results

### URL Parameters

Parameter | Description
--------- | -----------
project_id | The ID of the project you want to retrieve the scenarios from

## Find scenarios by tags

> Find scenarios by tags key

```http
GET https://studio.cucumberstudio.com/api/projects/<project_id>/scenarios/find_by_tags?key=<tag_key> HTTP/1.1
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
curl "https://studio.cucumberstudio.com/api/projects/<project_id>/scenarios/find_by_tags?key=<tag_key>" \
    -H 'accept: application/vnd.api+json; version=1' \
    -H 'access-token: <your access token>' \
    -H 'uid: <your uid>' \
    -H 'client: <your client id>'
```

```json
{
  "data": [
    {
      "type": "scenarios",
      "id": "1",
      "attributes": {
        "created-at" : "2018-01-31T16:03:45.387Z",
        "updated-at" : "2018-02-05T14:54:50.826Z",
        "last-author" : "harry@example.org",
        "name": "Find horcruxes",
        "description": "That will help to kill Voldemort",
        "folder-id": 162629,
        "definition": "scenario 'Find horcruxes' do\n  step {action: \"Find the last one\"}\n  step {result: \"Found it!\"}\nend\n"
      },
      "links": {
        "self": "/scenarios/1"
      },
      "relationships": {
        "folder": {}
      }
    },
    {
      "type": "scenarios",
      "id": "2",
      "attributes": {
        "created-at" : "2018-02-05T13:15:13.285Z",
        "updated-at" : "2018-02-05T13:18:19.397Z",
        "last-author" : "harry@example.org",
        "name": "Defeat Voldemort",
        "description": "And save the world, hurray !",
        "folder-id": 162629,
        "definition": "scenario 'Defeat Voldemort' do\nend\n"
      },
      "links": {
        "self": "/scenarios/2"
      },
      "relationships": {
        "folder": {}
      }
    }
  ],
  "included": []
}
```

> Find scenarios by tags key and value

```http
GET https://studio.cucumberstudio.com/api/projects/<project_id>/scenarios/find_by_tags?key=<tag_key>&value=<tag_value> HTTP/1.1
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
curl "https://studio.cucumberstudio.com/api/projects/<project_id>/scenarios/find_by_tags?key=<tag_key>&value=<tag_value>" \
    -H 'accept: application/vnd.api+json; version=1' \
    -H 'access-token: <your access token>' \
    -H 'uid: <your uid>' \
    -H 'client: <your client id>'
```

```json
{
  "data": [
    {
      "type": "scenarios",
      "id": "1",
      "attributes": {
        "created-at" : "2018-01-31T16:03:45.387Z",
        "updated-at" : "2018-02-05T14:54:50.826Z",
        "last-author" : "harry@example.org",
        "name": "Find horcruxes",
        "description": "That will help to kill Voldemort",
        "folder-id": 162629,
        "definition": "scenario 'Find horcruxes' do\n  step {action: \"Find the last one\"}\n  step {result: \"Found it!\"}\nend\n"
      },
      "links": {
        "self": "/scenarios/1"
      },
      "relationships": {
        "folder": {}
      }
    }
  ],
  "included": []
}
```

This endpoint retrieves all scenarios of a given project and having the given tag.

Field name | Description
--------- | -----------
tag_key | The KEY of the tag you use to retrieve the scenarios
tag_value | The VALUE of the tag you use to retrieve the scenarios

### URL Parameters

Parameter | Description
--------- | -----------
project_id | The ID of the project you want to retrieve the scenarios from

### Request parameters

Parameter | Description
--------- | -----------
key | The key of the tag
value | The value of the tag

## Get a single scenario

```http
GET https://studio.cucumberstudio.com/api/projects/<project_id>/scenarios/<scenario_id>[?include=<fields>] HTTP/1.1
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
curl "https://studio.cucumberstudio.com/api/projects/<project_id>/scenarios/<scenario_id>[?include=<fields>]" \
    -H 'accept: application/vnd.api+json; version=1' \
    -H 'access-token: <your access token>' \
    -H 'uid: <your uid>' \
    -H 'client: <your client id>'
```

```json
{
  "data":
    {
      "type": "scenarios",
      "id": "1",
      "attributes": {
        "created-at" : "2017-02-28T11:39:08.281Z",
        "updated-at" : "2017-02-28T11:39:08.281Z",
        "last-author" : "harry@example.org",
        "name": "Find horcruxes",
        "description": "That will help to kill Voldemort",
        "folder-id": 162629,
        "definition": "scenario 'Find horcruxes' do\n  step {action: \"Find the last one\"}\n  step {result: \"Found it!\"}\nend\n",
        "errors": []
      },
      "links": {
        "self": "/scenarios/1"
      },
      "relationships": {
        "folder": {}
      }
    }
}
```
This endpoint retrieves a single scenario of a given project.

You can use the JSONAPI [include syntax](http://jsonapi.org/format/#fetching-includes) to fetch additional data
about your tests.

The available additional data are the following:

Field name | Description
-----------| -----------
folder | The folder the scenario belongs to
tags | The tags of the scenario
actionwords | Actionwords used by the scenario

### URL Parameters

Parameter | Description
--------- | -----------
project_id | The ID of the project you want to retrieve the scenario from
scenario_id | The ID of the scenario you want to get

## Create a scenario

```http
POST https://studio.cucumberstudio.com/api/projects/<project_id>/scenarios HTTP/1.1
Content-Type: application/json; charset=utf-8
Accept: application/vnd.api+json; version=1
access-token: <your access token>
client: <your client id>
uid: <your uid>

{
  "data": {
    "attributes": {
      "name": "Find horcruxes",
      "folder-id": 1234
    }
  }
}
```

```http
HTTP/1.1 201 Created
Content-Type: application/vnd.api+json
```

```shell
curl -XPOST "https://studio.cucumberstudio.com/api/projects/<project_id>/scenarios" \
    -H 'Content-Type: application/json' \
    -H 'accept: application/vnd.api+json; version=1' \
    -H 'access-token: <your access token>' \
    -H 'uid: <your uid>' \
    -H 'client: <your client id>' \
    --data '{"data": {"attributes": {"name": "Find horcruxes", "folder-id": "1234" } } }'
```

```json
{
  "data":
    {
      "type": "scenarios",
      "id": "1",
      "attributes": {
        "created-at" : "2017-02-28T11:39:08.281Z",
        "updated-at" : "2017-02-28T11:39:08.281Z",
        "last-author" : "harry@example.org",
        "name": "Find horcruxes",
        "description": "",
        "folder-id": "1234",
        "definition": "",
        "errors": []
      },
      "links": {
        "self": "/scenarios/1"
      },
      "relationships": {
        "folder": {}
      }
    }
}
```

This endpoint create a new scenario.

### URL Parameters

Parameter | Description
--------- | -----------
project_id | The ID of the project in which you want to create the scenario

### Mandatory fields

Field | Description
--------- | -----------
name | (String) The name of the scenario

### Other fields

Field | Description
--------- | -----------
folder-id | (Integer) The id of the folder containing the scenario

<aside class="notice">
The description and the definition of a scenario cannot yet be set at creation
time. To set a proper description and definition to a scenario update it after
it has been created.
</aside>

<aside class="notice">
You can create tags alongside the scenario by specifying them in the "relationship" section, as explained in the <a href="#create-tags-alongside-elements">tags creation section</a>.
</aside>

## Update a scenario

```http
PATCH https://studio.cucumberstudio.com/api/projects/<project_id>/scenarios/<scenario_id> HTTP/1.1
Content-Type: application/json; charset=utf-8
Accept: application/vnd.api+json; version=1
access-token: <your access token>
client: <your client id>
uid: <your uid>

{
  "data": {
    "type": "scenarios",
    "id": <scenario_id>,
    "attributes": {
      "name": "The new name of the scenario",
      "description": "The new description of the scenario",
      "definition": "scenario 'The new definition of the scenario' do\nend\n",
      "folder-id": "162630"
    }
  }
}
```

```http
HTTP/1.1 200 OK
Content-Type: application/vnd.api+json
```

```shell
curl -XPATCH "https://studio.cucumberstudio.com/api/projects/<project_id>/scenarios/<scenario_id>" \
    -H 'Content-Type: application/json' \
    -H 'accept: application/vnd.api+json; version=1' \
    -H 'access-token: <your access token>' \
    -H 'uid: <your uid>' \
    -H 'client: <your client id>' \
    --data '{"data": {"type": "scenarios", "id": <scenario_id>, "attributes": {"name": "The new name of the scenario", "description": "The new description of the scenario", "definition": "scenario \'The new definition of the scenario\' do\\nend\\n", "folder-id": "162630" }}}'
```

```json
{
  "data":
    {
      "type": "scenarios",
      "id": "1",
      "attributes": {
        "name": "The new definition of the scenario",
        "description": "The new description of the scenario",
        "folder-id": "162630",
        "definition": "scenario 'The new definition of the scenario' do\nend\n"
      },
      "links": {
        "self": "/scenarios/1"
      },
      "relationships": {
        "folder": {}
      }
    }
}
```

This endpoint updates the name, descrpition, folder and definition of a single scenario of a given project.
Note that the attributes are all optional, you can update only one of them if wanted, just don't set the key in the "attributes" hash.

### URL Parameters

Parameter | Description
--------- | -----------
project_id | The ID of the project you want to retrieve the scenario from
scenario_id | The ID of the scenario you want to update

<aside class="notice">
Attributes to update are all optional. Specify only the ones you want to update.
</aside>
<aside class="warning">
Don't update name and definition attributes at the same time to avoid 409/conflict errors.
You can rename a scenario and update its definition by specifying the new name in the new definition.
</aside>

## Delete a scenario

```http
DELETE https://studio.cucumberstudio.com/api/projects/<project_id>/scenarios/<scenario_id> HTTP/1.1
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
curl -XDELETE "https://studio.cucumberstudio.com/api/projects/<project_id>/scenarios/<scenario_id>" \
    -H 'accept: application/vnd.api+json; version=1' \
    -H 'access-token: <your access token>' \
    -H 'uid: <your uid>' \
    -H 'client: <your client id>'
```

This endpoint delete a scenario.

### URL Parameters

Parameter | Description
--------- | -----------
project_id | The ID of the project you want to retrieve the scenario from
scenario_id | The ID of the scenario you want to delete

<aside class="warning">
Caution: your scenario will be totaly and permanently removed from your project.
</aside>

## List attachments of a given scenario

```http
GET https://studio.cucumberstudio.com/api/projects/<project_id>/scenarios/<scenario_id>/attachments HTTP/1.1
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
curl -XGET "https://studio.cucumberstudio.com/api/projects/<project_id>/scenarios/<scenario_id>/attachments" \
    -H 'Content-Type: application/json' \
    -H 'accept: application/vnd.api+json; version=1' \
    -H 'access-token: <your access token>' \
    -H 'uid: <your uid>' \
    -H 'client: <your client id>'
```

```json
{
  "data": [
    {
      "type": "attachments",
      "id": "1",
      "attributes": {
        "id": 1,
        "file-name": "my-attachment.jpg",
        "file-url": "/api/projects/1/scenarios/1/attachments/1",
        "file-size": 100
      },
      "links": {
        "self": "/attachments/1"
      }
    }
  ]
}
```

This endpoint list all the attachments of a given scenario

### URL Parameters

Parameter  | Description
---------  | -----------
project_id | The ID of the project you want to retrieve the scenarios from
scenario_id  | The ID of the target scenario

## Get a given attachment of a given scenario

```http
GET https://studio.cucumberstudio.com/api/projects/<project_id>/scenarios/<scenario_id>/attachments/<attachment_id> HTTP/1.1
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
curl -XGET -L "https://studio.cucumberstudio.com/api/projects/<project_id>/scenarios/<scenario_id>/attachments/<attachment_id>" \
    -H 'Content-Type: application/json' \
    -H 'accept: application/vnd.api+json; version=1' \
    -H 'access-token: <your access token>' \
    -H 'uid: <your uid>' \
    -H 'client: <your client id>' \
    --output my-attachment.jpg
```

This endpoint return the requested attachment of a given scenario

### URL Parameters

Parameter  | Description
---------  | -----------
project_id | The ID of the project you want to retrieve the scenarios from
scenario_id  | The ID of the target scenario
attachment_id  | The ID of the target attachment

## Create an attachment to a given scenario

```http
POST https://studio.cucumberstudio.com/api/projects/<project_id>/scenarios/<scenario_id>/attachments HTTP/1.1
Accept: application/vnd.api+json; version=1
access-token: <your access token>
client: <your client id>
uid: <your uid>
Content-Disposition: form-data; name="file"; filename="my-attachment.jpg"

(data)
```

```http
HTTP/1.1 200 OK
Content-Type: application/vnd.api+json
```

```shell
curl -XPOST "https://studio.cucumberstudio.com/api/projects/<project_id>/scenarios/<scenario_id>/attachments" \
    -H 'accept: application/vnd.api+json; version=1' \
    -H 'access-token: <your access token>' \
    -H 'uid: <your uid>' \
    -H 'client: <your client id>' \
    --form 'file=@./my-attachment.jpg'
```

```json
{
  "data": {
    "type": "attachments",
    "id": "1",
    "attributes": {
      "id": 1,
      "file-name": "my-attachment.jpg",
      "file-url": "/api/projects/1/scenarios/1/attachments/1",
      "file-size": 100
    },
    "links": {
      "self": "/attachments/1"
    }
  }
}
```

This endpoint create an attachment to a given scenario

### URL Parameters

Parameter  | Description
---------  | -----------
project_id | The ID of the project you want to retrieve the scenarios from
scenario_id  | The ID of the target scenario

## Update an attachment to a given scenario

```http
PATCH https://studio.cucumberstudio.com/api/projects/<project_id>/scenarios/<scenario_id>/attachments/<attachment_id> HTTP/1.1
Accept: application/vnd.api+json; version=1
access-token: <your access token>
client: <your client id>
uid: <your uid>
Content-Disposition: form-data; name="file"; filename="my-attachment.jpg"

(data)
```

```http
HTTP/1.1 200 OK
Content-Type: application/vnd.api+json
```

```shell
curl -XPATCH "https://studio.cucumberstudio.com/api/projects/<project_id>/scenarios/<scenario_id>/attachments/<attachment_id>" \
    -H 'accept: application/vnd.api+json; version=1' \
    -H 'access-token: <your access token>' \
    -H 'uid: <your uid>' \
    -H 'client: <your client id>' \
    --form 'file=@./my-attachment.jpg'
```

```json
{
  "data": {
    "type": "attachments",
    "id": "1",
    "attributes": {
      "id": 1,
      "file-name": "my-attachment.jpg",
      "file-url": "/api/projects/1/scenarios/1/attachments/1",
      "file-size": 100
    },
    "links": {
      "self": "/attachments/1"
    }
  }
}
```

This endpoint update the attachment to a given scenario

### URL Parameters

Parameter  | Description
---------  | -----------
project_id | The ID of the project you want to retrieve the scenarios from
scenario_id  | The ID of the target scenario
attachment_id  | The ID of the target attachment

## Delete an attachment to a given scenario

```http
DELETE https://studio.cucumberstudio.com/api/projects/<project_id>/scenarios/<scenario_id>/attachments/<attachment_id> HTTP/1.1
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
curl -XDELETE "https://studio.cucumberstudio.com/api/projects/<project_id>/scenarios/<scenario_id>/attachments/<attachment_id>" \
    -H 'Content-Type: application/json' \
    -H 'accept: application/vnd.api+json; version=1' \
    -H 'access-token: <your access token>' \
    -H 'uid: <your uid>' \
    -H 'client: <your client id>' \
```

```json
{}
```

This endpoint delete a given attachment of a given scenario

### URL Parameters

Parameter  | Description
---------  | -----------
project_id | The ID of the project you want to retrieve the scenarios from
scenario_id  | The ID of the target scenario
attachment_id  | The ID of the target attachment