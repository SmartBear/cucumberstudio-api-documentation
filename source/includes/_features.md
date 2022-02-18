# Features

## Get feature from a given folder

```http
GET https://app.hiptest.com/api/projects/<project_id>/folders/<folder_id>/feature HTTP/1.1
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
curl "https://app.hiptest.com/api/projects/<project_id>/folders</folder_id>/feature" \
    -H 'accept: application/vnd.api+json; version=1' \
    -H 'access-token: <your access token>' \
    -H 'uid: <your uid>' \
    -H 'client: <your client id>'
```

```json
{
    "data": {
        "type": "folders",
        "id": "1",
        "attributes": {
            "created-at": "2018-05-22T09:15:01.430Z",
            "updated-at": "2018-10-08T14:42:00.688Z",
            "last-author": "harry@example.org",
            "name": "HP Saga",
            "description": "This project is designed to keep track of the evolution of the HP saga,
            in the most expressive way possible, thanks to BDD!",
            "definition": "folder do\nend\n",
            "parent-id": null,
            "feature": "Feature: The Philosopher's Stone\n\nScenario: Read a Hogwarts letter"
        },
        "links": {
            "self": "/folders/1"
        },
        "relationships": {
            "tags": {}
        }
    },
    "included": []
}
```

This endpoint retrieves Gherkin formatted feature from a specific folder.


### URL Parameters

Parameter | Description
--------- | -----------
project_id | The ID of the project you want to retrieve the folders from
folder_id | The ID of the folder you want to get




## Create from feature

```http
POST https://app.hiptest.com/api/projects/<project_id>/folders/<folder_id>/create_from_feature HTTP/1.1
Accept: application/vnd.api+json; version=1
access-token: <your access token>
client: <your client id>
uid: <your uid>

{ 
    "data": { 
        "attributes": { 
            "feature": "Feature: The Chamber of Secrets\n\nScenario: Shopping on Diagon Alley"
        }
    }
}
```

```http
HTTP/1.1 200 OK
Content-Type: application/vnd.api+json
```

```shell
curl -XPOST "https://app.hiptest.com/api/projects/<project_id>/folders</folder_id>/create_from_feature" \
    -H 'accept: application/vnd.api+json; version=1' \
    -H 'access-token: <your access token>' \
    -H 'uid: <your uid>' \
    -H 'client: <your client id>' \
    --data '{ "data": { "attributes": { "feature": "Feature: The Chamber of Secrets\n\nScenario: Shopping on Diagon Alley" } } }'
```

```json
{
    "data": {
        "type": "folders",
        "id": "2",
        "attributes": {
            "created-at": "2018-05-22T09:15:01.430Z",
            "updated-at": "2018-10-08T14:42:00.688Z",
            "last-author": "harry@example.org",
            "name": "HP Saga",
            "description": "This project is designed to keep track of the evolution of the HP saga,
            in the most expressive way possible, thanks to BDD!",
            "definition": "folder do\nend\n",
            "parent-id": null,
            "running-feature-imports": [
                "the_chamber_of_secrets"
            ]
        },
        "links": {
            "self": "/folders/2"
        },
        "relationships": {
            "tags": {}
        }
    },
    "included": []
}
```

This endpoint creates every resources from the feature into a specific folder.

### URL Parameters

Parameter | Description
--------- | -----------
project_id | The ID of the project you want to retrieve the folders from
folder_id | The ID of the folder you want to get

### Mandatory fields

Field | Description
--------- | -----------
feature   | (String) The gherkin formatted feature text.