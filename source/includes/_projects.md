# Projects

## Get projects
```http
GET https://studio.cucumberstudio.com/api/projects/ HTTP/1.1
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
curl "https://studio.cucumberstudio.com/api/projects/" \
    -H 'accept: application/vnd.api+json; version=1' \
    -H 'access-token: <your access token>' \
    -H 'uid: <your uid>' \
    -H 'client: <your client id>'
```

```json
{
  "data": [
    {
      "type": "projects",
      "id": "1",
      "attributes": {
        "created-at": "2017-10-02T12:01:27.125Z",
        "updated-at": "2018-01-10T14:55:49.848Z",
        "last-author": "harry@example.org",
        "name": "And the Philosopher's Stone",
        "description": "This is where all starts",
        "bdd-mode": true
      },
      "links": {
        "self": "/projects/1"
      },
      "relationships": {
        "scenarios-folder": {
          "links": {
            "self": "/projects/1/relationships/scenarios-folder",
            "related": "/projects/1/scenarios-folder"
          }
        }
      }
    },
    {
      "type": "projects",
      "id": "2",
      "attributes": {
        "created-at": "2017-10-02T12:01:27.125Z",
        "updated-at": "2018-01-10T14:55:49.848Z",
        "last-author": "harry@example.org",
        "name": "And the Chamber of Secrets",
        "description": "With douchebag Draco Malfoy...",
        "bdd-mode": false
      },
      "links": {
        "self": "/projects/2"
      },
      "relationships": {
        "scenarios-folder": {
          "links": {
            "self": "/projects/2/relationships/scenarios-folder",
            "related": "/projects/2/scenarios-folder"
          }
        }
      }
    }
  ]
}
```

This endpoint retrieves all projects of the logged-in user

## Get a particular project
```http
GET https://studio.cucumberstudio.com/api/projects/<project_id> HTTP/1.1
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
curl "https://studio.cucumberstudio.com/api/projects/<project_id>" \
    -H 'accept: application/vnd.api+json; version=1' \
    -H 'access-token: <your access token>' \
    -H 'uid: <your uid>' \
    -H 'client: <your client id>'
```

```json
{
  "data": [
    {
      "type": "projects",
      "id": "1",
      "attributes": {
        "created-at": "2017-10-02T12:01:27.125Z",
        "updated-at": "2018-01-10T14:55:49.848Z",
        "last-author": "harry@example.org",
        "name": "And the Philosopher's Stone",
        "description": "This is where all starts",
        "bdd-mode": true
      },
      "links": {
        "self": "/projects/1"
      },
      "relationships": {
        "scenarios-folder": {
          "links": {
            "self": "/projects/1/relationships/scenarios-folder",
            "related": "/projects/1/scenarios-folder"
          }
        }
      }
    }
  ]
}
```

This endpoint retrieves a specific project of the logged-in user

### URL Parameters

Parameter | Description
--------- | -----------
project_id | The ID of the project you want to retrieve

## Create a project backup

### Create the project backup

```http
POST https://studio.cucumberstudio.com/api/projects/<project_id>/backups HTTP/1.1
Accept: application/vnd.api+json; version=1
access-token: <your access token>
client: <your client id>
uid: <your uid>
```
```http
HTTP/1.1 202 Accepted
Content-Type: application/vnd.api+json
```

```shell
curl "https://studio.cucumberstudio.com/api/projects/<project_id>/backups" \
    -X POST \
    -H 'accept: application/vnd.api+json; version=1' \
    -H 'access-token: <your access token>' \
    -H 'uid: <your uid>' \
    -H 'client: <your client id>'
```

```json
{
  "data": [
    {
      "type": "projects",
      "id": "1",
      "attributes": {
        "created-at": "2017-10-02T12:01:27.125Z",
        "updated-at": "2018-01-10T14:55:49.848Z",
        "last-author": "harry@example.org",
        "name": "And the Philosopher's Stone",
        "description": "This is where all starts",
        "bdd-mode": true,
        "new-backup-in-progress": true
      },
      "links": {
        "self": "/projects/1"
      },
      "relationships": {
        "scenarios-folder": {
          "links": {
            "self": "/projects/1/relationships/scenarios-folder",
            "related": "/projects/1/scenarios-folder"
          }
        }
      }
    }
  ]
}
```

This endpoint will schedule the backup creation of a given project. The
operation is acknownledged with a 202 Accepted HTTP code. The returned project
attributes include a `"new-backup-in-progress"` field set to `true`.

<aside class="notice">
Since this is an asynchronous operation, the backup creation might not be
finished when the server responds back. Use the <tt>/projects/&lt;project_id&gt;/backups/last</tt>
endpoint to watch the state of the backup creation.
</aside>

<aside class="notice">
Only one backup of a project and between projects of the same organization can
be created at the same time. Calling this endpoint when a backup creation is in
progress will reply with a 409 Conflict HTTP code.
</aside>

### URL Parameters

Parameter | Description
--------- | -----------
project_id | The ID of the project you want to create the backup for


## Get last backup state

```http
GET https://studio.cucumberstudio.com/api/projects/<project_id>/backups/last HTTP/1.1
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
curl "https://studio.cucumberstudio.com/api/projects/<project_id>/backups/last" \
    -H 'accept: application/vnd.api+json; version=1' \
    -H 'access-token: <your access token>' \
    -H 'uid: <your uid>' \
    -H 'client: <your client id>'
```

```json
{
  "data": {
    "type": "backups",
    "id": "9876",
    "attributes": {
      "project-id": 1234,
      "new-backup-in-progress": false,
      "updated-at": "2018-06-13T13:19:28.380Z",
      "file-name": "coffee_machine__hiptest_publisher_sample_20180419.zip",
      "file-size": 33968,
      "url": "https://attachments-hiptest-production.s3.amazonaws.com/backups/backup_files/000/012/345/original/coffee_machine__hiptest_publisher_sample_20180419.zip?AWSAccessKeyId=XXXXX&Expires=1528298175&Signature=XXX"
    },
    "links": {
      "self": "/backups/9876"
    }
  }
}
```

This endpoint is useful to track the state of a project backup creation and get the last created backup URL.

If the project does not have any backups yet, or when the very first backup is in
progress, this endpoint will respond with empty data: `{ "data": null }`.

<aside class="notice">
For security reasons, the file URL is valid for only 10 minutes. Afterwards, you
will get a HTTP 403 response with "Request has expired" error.
</aside>

### URL Parameters

Parameter | Description
--------- | -----------
project_id | The ID of the project you want to see the last backup of


## Getting root scenarios folder of a project

```http
GET https://studio.cucumberstudio.com/api/projects?include=scenarios-folder HTTP/1.1
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
curl "https://studio.cucumberstudio.com/api/project?include=scenarios-folder" \
    -H 'accept: application/vnd.api+json; version=1' \
    -H 'access-token: <your access token>' \
    -H 'uid: <your uid>' \
    -H 'client: <your client id>'
```
> Also works when retrieving a single project

You can use the JSONAPI [include syntax](http://jsonapi.org/format/#fetching-includes) to fetch the scenarios root folder of your project
