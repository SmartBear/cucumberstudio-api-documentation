# Folders

## Get folders of a given project

```http
GET https://studio.cucumberstudio.com/api/projects/<project_id>/folders HTTP/1.1
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
curl "https://studio.cucumberstudio.com/api/projects/<project_id>/folders" \
    -H 'accept: application/vnd.api+json; version=1' \
    -H 'access-token: <your access token>' \
    -H 'uid: <your uid>' \
    -H 'client: <your client id>'
```

```json
{
  "data": [
    {
      "type": "folders",
      "id": "1",
      "attributes": {
        "created-at" : "2017-02-28T11:39:08.281Z",
        "updated-at" : "2017-02-28T11:39:08.281Z",
        "last-author" : "harry@example.org",
        "name": "HP Saga",
        "description": "This project is designed to keep track of the evolution of the HP saga,
        in the most expressive way possible, thanks to BDD!",
        "parent-id": null
      },
      "links": {
        "self": "/folders/1"
      }
    },
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
      }
    }
  ]
}
```

This endpoint retrieves all folders of a given project.
<aside class="warning"> Note that this endpoint will only return the attributes of folders
and not their elements (scenarios and subfolders)</aside>

### URL Parameters

Parameter | Description
--------- | -----------
project_id | The ID of the project you want to retrieve the folders from

## Find folders by tags

> Find folders by tag key

```http
GET https://studio.cucumberstudio.com/api/projects/<project_id>/folders/find_by_tags?key=<tag_key> HTTP/1.1
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
curl "https://studio.cucumberstudio.com/api/projects/<project_id>/folders/find_by_tags?key=<tag_key>" \
    -H 'accept: application/vnd.api+json; version=1' \
    -H 'access-token: <your access token>' \
    -H 'uid: <your uid>' \
    -H 'client: <your client id>'
```

```json
{
    "data": [
        {
            "type": "folders",
            "id": "791625",
            "attributes": {
                "created-at": "2019-01-20T22:29:45.135Z",
                "updated-at": "2020-07-29T14:34:20.739Z",
                "last-author": "harry@example.org",
                "name": "Support internationalisation",
                "description": "As a polyglot coffee lover\nI can select the language on the coffee machine\nSo I can practice my use of greetings in several languages",
                "definition": "folder do\nend\n",
                "parent-id": 791623,
                "scenarios-count": 0,
                "feature-updated-at": "2020-07-29T14:34:20.739Z"
            },
            "links": {
                "self": "/folders/791625"
            },
            "relationships": {
                "tags": {}
            }
        },
        {
            "type": "folders",
            "id": "791626",
            "attributes": {
                "created-at": "2019-01-20T22:29:45.190Z",
                "updated-at": "2020-07-29T14:34:20.549Z",
                "last-author": "harry@example.org",
                "name": "Can be configured",
                "description": "**In order to** get the best possible coffees\n**As a** geeky coffee lover\n**I can** configure it to match my needs\n",
                "definition": "folder do\nend\n",
                "parent-id": 791623,
                "scenarios-count": 0,
                "feature-updated-at": "2020-07-29T14:34:20.549Z"
            },
            "links": {
                "self": "/folders/791626"
            },
            "relationships": {
                "tags": {}
            }
        }
    ],
    "included": []
}
```

> Find folders by tag key and value

```http
GET https://studio.cucumberstudio.com/api/projects/<project_id>/folders/find_by_tags?key=<tag_key>&value=<tag_value> HTTP/1.1
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
curl "https://studio.cucumberstudio.com/api/projects/<project_id>/folders/find_by_tags?key=<tag_key>&value=<tag_value>" \
    -H 'accept: application/vnd.api+json; version=1' \
    -H 'access-token: <your access token>' \
    -H 'uid: <your uid>' \
    -H 'client: <your client id>'
```

```json
{
    "data": [
        {
            "type": "folders",
            "id": "1245135",
            "attributes": {
                "created-at": "2020-02-11T10:42:19.094Z",
                "updated-at": "2020-07-29T14:34:20.663Z",
                "last-author": "harry@example.org",
                "name": "Serve coffee",
                "description": "As a coffee lover\nI can get coffee from the machine\nSo I can enjoy the rest of the day",
                "definition": "folder do\nend\n",
                "parent-id": 791623,
                "scenarios-count": 1,
                "feature-updated-at": "2020-07-29T14:34:20.663Z"
            },
            "links": {
                "self": "/folders/1245135"
            },
            "relationships": {
                "tags": {}
            }
        }
    ],
    "included": []
}
```

This endpoint retrieves all folders of a given project and having the given tag.

Field name | Description
--------- | -----------
tag_key | The KEY of the tag you use to retrieve the folders
tag_value | The VALUE of the tag you use to retrieve the folders

### URL Parameters

Parameter | Description
--------- | -----------
project_id | The ID of the project you want to retrieve the folders from

### Request parameters

Parameter | Description
--------- | -----------
key | The key of the tag
value | The value of the tag


## Get a single folder

```http
GET https://studio.cucumberstudio.com/api/projects/<project_id>/folders/<folder_id> HTTP/1.1
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
curl "https://studio.cucumberstudio.com/api/projects/<project_id>/folders/<folder_id>" \
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
      }
    }
}
```

This endpoint retrieves a specific folder of a given project.
<aside class="warning"> Note that this endpoint will only return the attributes of the folder
and not its elements (scenarios and subfolders)</aside>

### URL Parameters

Parameter | Description
--------- | -----------
project_id | The ID of the project you want to retrieve the folders from
folder_id | The ID of the folder you want to get

## Get children of a folder

```http
GET https://studio.cucumberstudio.com/api/projects/<project_id>/folders/<folder_id>/children HTTP/1.1
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
curl "https://studio.cucumberstudio.com/api/projects/<project_id>/folders/<folder_id>/children" \
    -H 'accept: application/vnd.api+json; version=1' \
    -H 'access-token: <your access token>' \
    -H 'uid: <your uid>' \
    -H 'client: <your client id>'
```

```json
{
  "data": [
    {
      "type": "folders",
      "id": "2",
      "attributes": {
        "name": "The Philosopher's stone",
        "description": "",
        "parent-id": 1
      },
      "links": {
        "self": "/folders/2"
      }
    },
    {
      "type": "folders",
      "id": "3",
      "attributes": {
        "name": "The Chamber of Secrets",
        "description": "",
        "parent-id": 1
      },
      "links": {
        "self": "/folders/3"
      }
    }
  ]
}
```
This endpoint retrieves the subfolders of a specific folder

### URL Parameters

Parameter | Description
--------- | -----------
project_id | The ID of the project you want to retrieve the folders from
folder_id | The ID of the folder you want to get the children

## Get scenarios of a folder

```http
GET https://studio.cucumberstudio.com/api/projects/<project_id>/folders/<folder_id>/scenarios HTTP/1.1
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
curl "https://studio.cucumberstudio.com/api/projects/<project_id>/folders/<folder_id>/scenarios" \
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
        "name": "Read a Hogwarts letter"
      },
      "links": {
        "self": "/scenarios/1"
      }
    },
    {
      "type": "scenarios",
      "id": "2",
      "attributes": {
        "name": "Shopping on Diagon Alley"
      },
      "links": {
        "self": "/scenarios/2"
      }
    }
  ]
}
```

This endpoint retrieves the scenarios of a specific folder

### URL Parameters

Parameter | Description
--------- | -----------
project_id | The ID of the project you want to retrieve the folders from
folder_id | The ID of the folder you want to get the scenarios

## Create a folder

```http
POST https://studio.cucumberstudio.com/api/projects/<project_id>/folders HTTP/1.1
Content-Type: application/json; charset=utf-8
Accept: application/vnd.api+json; version=1
access-token: <your access token>
client: <your client id>
uid: <your uid>

{
  "data": {
    "attributes": {
      "name": "A new folder",
      "parent-id": 1234
    }
  }
}
```

```http
HTTP/1.1 201 Created
Content-Type: application/vnd.api+json
```

```shell
curl -XPOST "https://studio.cucumberstudio.com/api/projects/<project_id>/folders" \
    -H 'Content-Type: application/json' \
    -H 'accept: application/vnd.api+json; version=1' \
    -H 'access-token: <your access token>' \
    -H 'uid: <your uid>' \
    -H 'client: <your client id>' \
    --data '{"data": {"attributes": {"name": "A new folder", "parent-id": "1234" } } }'
```

```json
{
  "data": {
    "type": "folders",
    "id": "1235",
    "attributes": {
      "created-at": "2017-10-17T08:00:33.978Z",
      "updated-at": "2017-10-18T08:28:07.791Z",
      "last-author": "harry@example.org",
      "name": "A new folder",
      "description": "",
      "definition": "folder do\nend\n",
      "parent-id": 1234
    },
    "links": {
      "self": "/folders/1235"
    }
  }
}
```

This endpoint create a new folder

### URL Parameters

Parameter | Description
--------- | -----------
project_id | The ID of the project you want to retrieve the folders from

### Mandatory fields

Field | Description
--------- | -----------
name | (String) The name of the folder.

### Other fields

Field | Description
--------- | -----------
parent-id | (Integer) The id of the folder that will contain the created folder.

<aside class="notice"> If no parent folder is specified, the folder will be created inside the root folder of the project</aside>

## Update a folder

```http
PATCH https://studio.cucumberstudio.com/api/projects/<project_id>/folders/<folder_id> HTTP/1.1
Content-Type: application/json; charset=utf-8
Accept: application/vnd.api+json; version=1
access-token: <your access token>
client: <your client id>
uid: <your uid>

{
  "data": {
    "type": "folders",
    "id": "<folder_id>",
    "attributes": {
      "name": "A new folder name",
      "description": "A new description",
      "definition": "folder do end"
      "parent-id": 1233
    }
  }
}
```

```http
HTTP/1.1 200 OK
Content-Type: application/vnd.api+json
```

```shell
curl -XPATCH "https://studio.cucumberstudio.com/api/projects/<project_id>/folders/<folder_id>" \
    -H 'Content-Type: application/json' \
    -H 'accept: application/vnd.api+json; version=1' \
    -H 'access-token: <your access token>' \
    -H 'uid: <your uid>' \
    -H 'client: <your client id>' \
    --data '{"data": {"attributes": {"name": "A new folder name", "parent-id": "1233", "description: "A new description", "definition": "folder do end" } } }'
```

```json
{
  "data": {
    "type": "folders",
    "id": "1234",
    "attributes": {
      "created-at": "2017-10-17T08:00:33.978Z",
      "updated-at": "2017-10-18T08:28:07.791Z",
      "last-author": "harry@example.org",
      "name": "A new folder name",
      "description": "A new descriptio",
      "definition": "folder do\nend\n",
      "parent-id": 1233
    },
    "links": {
      "self": "/folders/1234"
    }
  }
}
```

This endpoint updates a folder

### URL Parameters

Parameter | Description
--------- | -----------
project_id | The ID of the project you want to retrieve the folders from

### Fields

Field      | Description
---------  | -----------
name       | (String) The name of the folder.
description| (String) The description of the folder.
definition | (String) The definition of the folder.
parent-id  | (Integer) The id of the parent folder.

<aside class="notice">Attributes to update are all optional. Specify only the ones you want to update.</aside>

## Delete a folder

```http
DELETE https://studio.cucumberstudio.com/api/projects/<project_id>/folders/<folder_id> HTTP/1.1
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
curl -XDELETE "https://studio.cucumberstudio.com/api/projects/<project_id>/folders/<folder_id>" \
    -H 'accept: application/vnd.api+json; version=1' \
    -H 'access-token: <your access token>' \
    -H 'uid: <your uid>' \
    -H 'client: <your client id>'
```

```json
{
  "data": {}
}
```

This endpoint destroy a folder

### URL Parameters

Parameter  | Description
---------  | -----------
project_id | The ID of the project you want to retrieve the folders from
folder_id  | The ID of the target folder

<aside class="warning"><b>Warning:</b> this action will destroy all the children and scenarios within the given folder</aside>

## Delete a folder children

```http
DELETE https://studio.cucumberstudio.com/api/projects/<project_id>/folders/<folder_id>/children HTTP/1.1
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
curl -XDELETE "https://studio.cucumberstudio.com/api/projects/<project_id>/folders/<folder_id>/children" \
    -H 'accept: application/vnd.api+json; version=1' \
    -H 'access-token: <your access token>' \
    -H 'uid: <your uid>' \
    -H 'client: <your client id>'
```

```json
{
  "data": {}
}
```

This endpoint destroys all sub-folders of the target folder

### URL Parameters

Parameter  | Description
---------  | -----------
project_id | The ID of the project you want to retrieve the folders from
folder_id  | The ID of the target folder

<aside class="warning"><b>Warning:</b> this action will destroy all the children and their scenarios</aside>

## Delete a folder scenarios

```http
DELETE https://studio.cucumberstudio.com/api/projects/<project_id>/folders/<folder_id>/scenarios HTTP/1.1
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
curl -XDELETE "https://studio.cucumberstudio.com/api/projects/<project_id>/folders/<folder_id>/scenarios" \
    -H 'accept: application/vnd.api+json; version=1' \
    -H 'access-token: <your access token>' \
    -H 'uid: <your uid>' \
    -H 'client: <your client id>'
```

```json
{
  "data": {}
}
```

This endpoint destroy a folder scenarios

### URL Parameters

Parameter  | Description
---------  | -----------
project_id | The ID of the project you want to retrieve the folders from
folder_id  | The ID of the target folder

<aside class="warning"><b>Warning:</b> this action will destroy all the scenarios of the given folder</aside>

## List attachments of a given folder

```http
GET https://studio.cucumberstudio.com/api/projects/<project_id>/folders/<folder_id>/attachments HTTP/1.1
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
curl -XGET "https://studio.cucumberstudio.com/api/projects/<project_id>/folders/<folder_id>/attachments" \
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
        "file-url": "/api/projects/1/folders/1/attachments/1",
        "file-size": 100
      },
      "links": {
        "self": "/attachments/1"
      }
    }
  ]
}
```

This endpoint list all the attachments of a given folder

### URL Parameters

Parameter  | Description
---------  | -----------
project_id | The ID of the project you want to retrieve the folders from
folder_id  | The ID of the target folder

## Get a given attachment of a given folder

```http
GET https://studio.cucumberstudio.com/api/projects/<project_id>/folders/<folder_id>/attachments/<attachment_id> HTTP/1.1
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
curl -XGET -L "https://studio.cucumberstudio.com/api/projects/<project_id>/folders/<folder_id>/attachments/<attachment_id>" \
    -H 'Content-Type: application/json' \
    -H 'accept: application/vnd.api+json; version=1' \
    -H 'access-token: <your access token>' \
    -H 'uid: <your uid>' \
    -H 'client: <your client id>' \
    --output my-attachment.jpg
```

This endpoint return the requested attachment of a given folder

### URL Parameters

Parameter  | Description
---------  | -----------
project_id | The ID of the project you want to retrieve the folders from
folder_id  | The ID of the target folder
attachment_id  | The ID of the target attachment

## Create an attachment to a given folder

```http
POST https://studio.cucumberstudio.com/api/projects/<project_id>/folders/<folder_id>/attachments HTTP/1.1
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
curl -XPOST "https://studio.cucumberstudio.com/api/projects/<project_id>/folders/<folder_id>/attachments" \
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
      "file-url": "/api/projects/1/folders/1/attachments/1",
      "file-size": 100
    },
    "links": {
      "self": "/attachments/1"
    }
  }
}
```

This endpoint create an attachment to a given folder

### URL Parameters

Parameter  | Description
---------  | -----------
project_id | The ID of the project you want to retrieve the folders from
folder_id  | The ID of the target folder

## Update an attachment to a given folder

```http
PATCH https://studio.cucumberstudio.com/api/projects/<project_id>/folders/<folder_id>/attachments/<attachment_id> HTTP/1.1
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
curl -XPATCH "https://studio.cucumberstudio.com/api/projects/<project_id>/folders/<folder_id>/attachments/<attachment_id>" \
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
      "file-url": "/api/projects/1/folders/1/attachments/1",
      "file-size": 100
    },
    "links": {
      "self": "/attachments/1"
    }
  }
}
```

This endpoint update the attachment to a given folder

### URL Parameters

Parameter  | Description
---------  | -----------
project_id | The ID of the project you want to retrieve the folders from
folder_id  | The ID of the target folder
attachment_id  | The ID of the target attachment

## Delete an attachment to a given folder

```http
DELETE https://studio.cucumberstudio.com/api/projects/<project_id>/folders/<folder_id>/attachments/<attachment_id> HTTP/1.1
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
curl -XDELETE "https://studio.cucumberstudio.com/api/projects/<project_id>/folders/<folder_id>/attachments/<attachment_id>" \
    -H 'Content-Type: application/json' \
    -H 'accept: application/vnd.api+json; version=1' \
    -H 'access-token: <your access token>' \
    -H 'uid: <your uid>' \
    -H 'client: <your client id>' \
```

```json
{}
```

This endpoint delete a given attachment of a given folder

### URL Parameters

Parameter  | Description
---------  | -----------
project_id | The ID of the project you want to retrieve the folders from
folder_id  | The ID of the target folder
attachment_id  | The ID of the target attachment
