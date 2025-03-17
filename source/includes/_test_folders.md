# Test folders

## Get test folders of a test run

```http
GET https://studio.cucumberstudio.com/api/projects/<project_id>/test_runs/<test_run_id>/folder_snapshots HTTP/1.1
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
curl "https://studio.cucumberstudio.com/api/projects/<project_id>/test_runs/<test_run_id>/folder_snapshots" \
    -H 'accept: application/vnd.api+json; version=1' \
    -H 'access-token: <your access token>' \
    -H 'uid: <your uid>' \
    -H 'client: <your client id>'
```
```json
{
"data": [
        {
                     "type": "folder-snapshots",
                       "id": "1",
               "attributes": {
                 "created-at": "2017-09-15T12:59:08.328Z",
                 "updated-at": "2017-09-15T12:59:08.710Z",
                "last-author": "HarryP",
                       "name": "A Hogwarts project",
                "description": "",
                   "statuses": {
                       "passed_count": 0,
                       "failed_count": 0,
                       "retest_count": 0,
                    "undefined_count": 3,
                      "blocked_count": 0,
                      "skipped_count": 0,
                          "wip_count": 0
                },
                  "parent-id": null,
                "test-run-id": 1
            },
                    "links": {
                "self": "/folder-snapshots/1"
            },
            "relationships": {
                        "folder": {},
                      "children": {},
                "test-snapshots": {}
            }
        },
        {
                     "type": "folder-snapshots",
                       "id": "1",
               "attributes": {
                 "created-at": "2017-09-15T12:59:08.328Z",
                 "updated-at": "2017-09-15T12:59:08.710Z",
                "last-author": "HarryP",
                       "name": "The Philosopher's Stone",
                "description": "",
                   "statuses": {
                       "passed_count": 0,
                       "failed_count": 0,
                       "retest_count": 0,
                    "undefined_count": 3,
                      "blocked_count": 0,
                      "skipped_count": 0,
                          "wip_count": 0
                },
                  "parent-id": 1,
                "test-run-id": 1
            },
                    "links": {
                "self": "/folder-snapshots/1"
            },
            "relationships": {
                        "folder": {},
                      "children": {},
                "test-snapshots": {}
            }
        }
      ]
    }
```
### URL Parameters

Parameter | Description
--------- | -----------
project_id | The ID of the project you want to retrieve the test folders from
test_run_id | The ID of the test run that contains the test folders you want

## Get a test folder

```http
GET https://studio.cucumberstudio.com/api/projects/<project_id>/test_runs/<test_run_id>/folder_snapshots/<folder_snapshot_id> HTTP/1.1
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
curl "https://studio.cucumberstudio.com/api/projects/<project_id>/test_runs/<test_run_id>/folder_snapshots/<folder_snapshot_id>" \
    -H 'accept: application/vnd.api+json; version=1' \
    -H 'access-token: <your access token>' \
    -H 'uid: <your uid>' \
    -H 'client: <your client id>'
```

```json
{
"data": [
        {
                     "type": "folder-snapshots",
                       "id": "1",
               "attributes": {
                 "created-at": "2017-09-15T12:59:08.328Z",
                 "updated-at": "2017-09-15T12:59:08.710Z",
                "last-author": "HarryP",
                       "name": "A Hogwarts project",
                "description": "",
                   "statuses": {
                       "passed_count": 0,
                       "failed_count": 0,
                       "retest_count": 0,
                    "undefined_count": 3,
                      "blocked_count": 0,
                      "skipped_count": 0,
                          "wip_count": 0
                },
                  "parent-id": null,
                "test-run-id": 1
            },
                    "links": {
                "self": "/folder-snapshots/1"
            },
            "relationships": {
                        "folder": {},
                      "children": {},
                "test-snapshots": {}
            }
        }
      ]
    }
```
### URL Parameters

Parameter | Description
--------- | -----------
project_id | The ID of the project you want to retrieve the test folders from
test_run_id | The ID of the test run that contains the test folders you want
folder_snapshot_id | The ID of the test folder you want to get

## Get a test folder additional data
```http
GET https://studio.cucumberstudio.com/api/projects/<project_id>/test_runs/<test_run_id>/folder_snapshots/<folder_snapshot_id>?include=<fields> HTTP/1.1
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
curl "https://studio.cucumberstudio.com/api/projects/<project_id>/test_runs/<test_run_id>/folder_snapshots/<folder_snapshot_id>?include=<fields>" \
    -H 'accept: application/vnd.api+json; version=1' \
    -H 'access-token: <your access token>' \
    -H 'uid: <your uid>' \
    -H 'client: <your client id>'
```

> The data you want to include in the response must be comma-separated

You can use the JSONAPI [include syntax](http://jsonapi.org/format/#fetching-includes) to fetch additional data
about your tests.

The available additional data are the following:

Field name | Description
-----------| -----------
folder | The original folder that produced the test folder
children | The subfolders of the test folder
test-snapshots | The tests contained by the test folder

```http
GET https://studio.cucumberstudio.com/api/projects/<project_id>/test_runs/<test_run_id>/folder_snapshots/<folder_snapshot_id>?include=folder HTTP/1.1
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
curl "https://studio.cucumberstudio.com/api/projects/<project_id>/test_runs/<test_run_id>/folder_snapshots/<folder_snapshot_id>?include=folder" \
    -H 'accept: application/vnd.api+json; version=1' \
    -H 'access-token: <your access token>' \
    -H 'uid: <your uid>' \
    -H 'client: <your client id>'
```

> Get a test folder original scenario folder

```http
GET https://studio.cucumberstudio.com/api/projects/<project_id>/test_runs/<test_run_id>/folder_snapshots/<folder_snapshot_id>?include=children HTTP/1.1
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
curl "https://studio.cucumberstudio.com/api/projects/<project_id>/test_runs/<test_run_id>/folder_snapshots/<folder_snapshot_id>?include=children" \
    -H 'accept: application/vnd.api+json; version=1' \
    -H 'access-token: <your access token>' \
    -H 'uid: <your uid>' \
    -H 'client: <your client id>'
```

> Get the subfolders of a test folder

```http
GET https://studio.cucumberstudio.com/api/projects/<project_id>/test_runs/<test_run_id>/folder_snapshots/<folder_snapshot_id>?include=test-snapshots HTTP/1.1
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
curl "https://studio.cucumberstudio.com/api/projects/<project_id>/test_runs/<test_run_id>/folder_snapshots/<folder_snapshot_id>?include=test-snapshots" \
    -H 'accept: application/vnd.api+json; version=1' \
    -H 'access-token: <your access token>' \
    -H 'uid: <your uid>' \
    -H 'client: <your client id>'
```

> Get the tests of a test folder

### URL Parameters

Parameter | Description
--------- | -----------
project_id | The ID of the project you want to retrieve the test folders from
test_run_id | The ID of the test run that contains the test folders you want
folder_snapshot_id | The ID of the test folder you want to get

### Request parameters

Parameter | Description
----------|------------
include | The data to include in the test JSON response. Fields must be comma-separated
