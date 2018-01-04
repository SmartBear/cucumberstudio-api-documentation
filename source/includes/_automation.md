# Test execution

## What's a build?
A build is a way to group the execution results of the tests contained in a Hiptest test run.
Even if the notion of build does not appear (for now!) in the Hiptest interface, they are used in our
database when you push the results of a test execution using the Hiptest publisher.

## List builds of a test run
```http
GET https://hiptest.net/api/projects/<project_id>/test_runs/<test_run_id>/builds HTTP/1.1
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
curl "https://hiptest.net/api/projects/<project_id>/test_runs/<test_run_id>/builds" \
    -H 'accept: application/vnd.api+json; version=1' \
    -H 'access-token: <your access token>' \
    -H 'uid: <your uid>' \
    -H 'client: <your client id>'
```

```json
{
  "data": [
    {
      "type": "builds",
      "id": "1",
      "attributes": {
        "created-at": "2017-06-13T08:15:38.607Z",
        "test-run-id": 1,
        "is-running": false,
        "closed-at": "2017-06-16T09:13:48.737Z"
      },
      "links": {
        "self": "/builds/1"
      }
    },
    {
      "type": "builds",
      "id": "2",
      "attributes": {
        "created-at": "2017-06-13T08:15:38.607Z",
        "test-run-id": 215,
        "is-running": true,
        "closed-at": nil
      },
      "links": {
        "self": "/builds/2"
      }
    }
  ]
}
```

This endpoint retrieves all builds of a given test run.
<aside class="warning"> Note that this endpoint will only return the attributes of builds
and not their test results</aside>

### URL Parameters

Parameter | Description
--------- | -----------
project_id | The ID of the project that contains the requested test run
test_run_id | The ID of the test run you want to retrieve the builds from

## Get a specific build of a test run

```http
GET https://hiptest.net/api/projects/<project_id>/test_runs/<test_run_id>/builds/<build_id>" HTTP/1.1
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
curl "https://hiptest.net/api/projects/<project_id>/test_runs/<test_run_id>/builds/<build_id>" \
    -H 'accept: application/vnd.api+json; version=1' \
    -H 'access-token: <your access token>' \
    -H 'uid: <your uid>' \
    -H 'client: <your client id>'
```

```json
{
  "data": {
    "type": "builds",
    "id": "1",
    "attributes": {
      "created-at": "2017-06-13T08:15:38.607Z",
      "test-run-id": 1,
      "is-running": false,
      "closed-at": "2017-06-16T09:13:48.737Z"
    },
    "links": {
      "self": "/builds/1"
    },
    "relationships": {
      "test-results": {
        "data": []
      }
    }
  },
  "included": []
}
```

This endpoint retrieves a specific build of a given test run.
<aside class="warning"> Note that this endpoint will only return the attributes of the build
and not their test results</aside>

### URL Parameters

Parameter | Description
--------- | -----------
project_id | The ID of the project you want to retrieve the folders from
test_run_id | The ID of the test run you want to retrieve the build from

## Get test execution results of a build

```http
GET https://hiptest.net/api/projects/<project_id>/test_runs/<test_run_id>/builds/<build_id>?include=test-results HTTP/1.1
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
curl "https://hiptest.net/api/projects/<project_id>/test_runs/<test_run_id>/builds/<build_id>?include=test-results" \
    -H 'accept: application/vnd.api+json; version=1' \
    -H 'access-token: <your access token>' \
    -H 'uid: <your uid>' \
    -H 'client: <your client id>'
```

```json
{
  "data": {
    "type": "builds",
    "id": "1",
    "attributes": {
      "created-at": "2017-06-13T08:15:38.607Z",
      "test-run-id": 1,
      "is-running": false,
      "closed-at": "2017-06-16T09:13:48.737Z"
    },
    "links": {
      "self": "/builds/1"
    },
    "relationships": {
      "test-results": {
        "data": [
          {
            "type": "test-results",
            "id": "1"
          },
          {
            "type": "test-results",
            "id": "2"
          }
        ]
      }
    }
  },
  "included": [
    {
      "type": "test-results",
      "id": "1",
      "attributes": {
        "status": "passed",
        "created-at": "1980-07-01T12:00:00.350Z",
        "description": "",
        "status-author": "Jenkins",
        "step-statuses": [
          "passed",
          "passed",
          "passed"
        ],
        "test-snapshot-id": 1
      },
      "links": {
        "self": "/test-results/1"
      }
    },
    {
      "type": "test-results",
      "id": "2",
      "attributes": {
        "status": "failed",
        "created-at": "1980-07-01T12:00:00.350Z",
        "description": "Error on line 42",
        "status-author": "Jenkins",
        "step-statuses": [],
        "test-snapshot-id": 2
      },
      "links": {
        "self": "/test-results/2"
      }
    }
  ]
}
```
Use the JSONAPI [include syntax](http://jsonapi.org/format/#fetching-includes) to fetch the test execution results
of your build.

### URL Parameters

Parameter | Description
--------- | -----------
project_id | The ID of the project you want to retrieve the folders from
test_run_id | The ID of the test run you want to retrieve the build from

## Create a new build

```http
POST https://hiptest.net/api/projects/<project_id>/test_runs/<test_run_id>/builds" HTTP/1.1
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
curl "https://hiptest.net/api/projects/<project_id>/test_runs/<test_run_id>/builds" \
    -XPOST
    -H 'accept: application/vnd.api+json; version=1' \
    -H 'access-token: <your access token>' \
    -H 'uid: <your uid>' \
    -H 'client: <your client id>'
    --data '{}'
```

> A new build

```json
  {
    "data": {
      "type": "builds",
      "id": "3",
      "attributes": {
        "created-at": "now!",
        "test-run-id": 1,
        "is_running": true,
        "closed_at": nil
      },
      "links": {
        "self": "/builds/3"
      },
      "relationships": {
        "test-results": {}
      }
    }
  }
```

<aside class="notice">You MUST create a new build when you need to push the execution results of a new run of your tests</aside>

### URL Parameters

Parameter | Description
--------- | -----------
project_id | The ID of the project you want to retrieve the folders from
test_run_id | The ID of the test run you are executing


## Close a build

```http
POST https://hiptest.net/api/projects/<project_id>/test_runs/<test_run_id>/builds/<build_id>/close" HTTP/1.1
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
curl "https://hiptest.net/api/projects/<project_id>/test_runs/<test_run_id>/builds/<build_id>/close" \
    -XPOST
    -H 'accept: application/vnd.api+json; version=1' \
    -H 'access-token: <your access token>' \
    -H 'uid: <your uid>' \
    -H 'client: <your client id>'
    --data '{}'
```

> The closed build

```json
  {
    "data": {
      "type": "builds",
      "id": "3",
      "attributes": {
        "created-at": "2017-06-13T08:15:38.607Z",
        "test-run-id": 1,
        "is-running": false,
        "closed-at": "2017-06-16T09:13:48.737Z"
      },
      "links": {
        "self": "/builds/3"
      },
      "relationships": {
        "test-results": {}
      }
    }
  }
```

<aside class="notice">Closing a build will turn the flag "is_running" to false and set the "closed_at" attribute.</aside>

### URL Parameters

Parameter | Description
--------- | -----------
project_id | The ID of the project you want to retrieve the folders from
test_run_id | The ID of the test run you are executing
build_id | The ID of the build you want to close
## Assign test execution results to a build
```http
POST https://hiptest.net/api/projects/<project_id>/test_runs/<test_run_id>/builds/<build_id>/test_results HTTP/1.1


data={"data": {"type": "test-results",
  "attributes": {"status": "passed", "status-author": "Harry", "description": "All was well"},
  "relationships": {
    "test-snapshot": {
      "data": {
        "type": "test-snapshots",
        "id": 1
      }
    }
  }
}}

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
curl -XPOST "https://hiptest.net/api/projects/<project_id>/test_runs/<test_run_id>/test_snapshots/<test_snapshot_id>/test_results" \
    -H 'accept: application/vnd.api+json; version=1' \
    -H 'access-token: <your access token>' \
    -H 'uid: <your uid>' \
    -H 'client: <your client id>'
    --data '{"data": {"type": "test-results", "attributes": {"status": "passed", "status-author": "Harry", "description": "All was well"},
    "relationships": {
      "test-snapshot": {
        "data": {
          "type": "test-snapshots",
          "id": 1
        }
      }
    }}}'
```

> Newly created test result

``` json
{
  "data": {
    "type": "test-results",
    "id": "1",
    "attributes": {
      "status": "passed",
      "created-at": "Couple of miliseconds ago",
      "description": "",
      "status-author": "Harry"
    },
    "links": {
      "self": "/test-results/1"
    },
    "relationships": {
      "test-snapshot": {
        "data": {
          "type": "test-snapshots",
          "id": "1"
        },
      "build": {
        "data": {
          "type": "builds",
          "id": "1"
        }
      }
    }
  },
  "included": [
    {
      "type": "test-snapshots",
      "attributes": "test data"
    },

    {
      "type": "builds",
      "attributes": "build data"
    }
  ]
}
}
```

### URL Parameters

Parameter | Description
--------- | -----------
project_id | The ID of the project you want to retrieve the tests from
test_run_id | The ID of the test run that contains the test you want
build_id | The ID of the build whose you want add a test result to

### Mandatory fields

Field | Description
--------- | -----------
status | (String) The status of the test execution. Possible values are 'passed', 'failed', 'wip', 'retest', 'blocked', 'skipped', 'undefined'.
status-author | (String) The name of the author of the test execution
description | (String) A comment about the test execution
test-snapshot | (JSONAPI relationship) The executed test

<aside class="notice">
If the provided 'status' value does not match any of the listed possible values, the result will be set as 'undefined'
</aside>