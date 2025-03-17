# Execution environments

## What's an execution environment?
An execution environment is a way to group several builds by in a CucumberStudio
test run.

You can find more details on test executions and execution environments in the [Test execution introduction section](#getting-started-with-test-executions).

## List execution environments of a test run
```http
GET https://studio.cucumberstudio.com/api/projects/<project_id>/test_runs/<test_run_id>/execution_environments HTTP/1.1
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
curl "https://studio.cucumberstudio.com/api/projects/<project_id>/test_runs/<test_run_id>/execution_environments" \
    -H 'accept: application/vnd.api+json; version=1' \
    -H 'access-token: <your access token>' \
    -H 'uid: <your uid>' \
    -H 'client: <your client id>'
```

```json
{
  "data": [
    {
      "type": "execution-environments",
      "id": "1",
      "attributes": {
        "name": "Default",
        "test-run-id": 1,
        "created-at": "2017-06-13T08:15:38.607Z",
        "updated-at": "2018-09-09T10:48:48.685Z"
      },
      "links": {
        "self": "/execution-environments/1"
      }
    },
    {
      "type": "execution-environments",
      "id": "2",
      "attributes": {
        "name": "Environment 1",
        "test-run-id": 1,
        "created-at": "2017-06-13T08:15:38.607Z",
        "updated-at": "2018-09-09T10:48:48.685Z"
      },
      "links": {
        "self": "/execution-environments/2"
      }
    }
  ]
}
```

This endpoint retrieves all execution environments of a given test run.
<aside class="warning">Note that this endpoint will only return the attributes of execution environments
and not their builds</aside>

### URL Parameters

Parameter | Description
--------- | -----------
project_id | The ID of the project that contains the requested test run
test_run_id | The ID of the test run you want to retrieve the builds from

## List builds of an execution environment
```http
GET https://studio.cucumberstudio.com/api/projects/<project_id>/test_runs/<test_run_id>/execution_environments/<execution_environment_id>/builds HTTP/1.1
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
curl "https://studio.cucumberstudio.com/api/projects/<project_id>/test_runs/<test_run_id>/execution_environments/<execution_environment_id>/builds" \
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
        "execution-environment-id": 1,
        "is-running": true,
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
        "test-run-id": 1,
        "execution-environment-id": 1,
        "is-running": false,
        "closed-at": null
      },
      "links": {
        "self": "/builds/2"
      }
    }
  ]
}
```

This endpoint retrieves all builds of a given execution environment.
<aside class="warning">Note that this endpoint will only return the attributes of builds
and not their test results</aside>

### URL Parameters

Parameter | Description
--------- | -----------
project_id | The ID of the project that contains the requested test run
test_run_id | The ID of the test run that contains the requested execution environment
execution_environment_id | The ID of the execution environment you want to retreive the builds from

## Create a new execution environment

```http
POST https://studio.cucumberstudio.com/api/projects/<project_id>/test_runs/<test_run_id>/execution_environments" HTTP/1.1
Accept: application/vnd.api+json; version=1
access-token: <your access token>
client: <your client id>
uid: <your uid>


{
  "data": {
    "attributes": {
      "name": "Execution environment 1"
    }
  }
}
```
```http
HTTP/1.1 201 Created
Content-Type: application/vnd.api+json
```

```shell
curl "https://studio.cucumberstudio.com/api/projects/<project_id>/test_runs/<test_run_id>/execution_environments" \
    -XPOST \
    -H 'accept: application/vnd.api+json; version=1' \
    -H 'access-token: <your access token>' \
    -H 'uid: <your uid>' \
    -H 'client: <your client id>' \
    --data '{"data": {"attributes": { "name": "Execution environment 1"} } }'
```

> A new execution environment

```json
  {
    "data": {
      "type": "execution-environments",
      "id": "1",
      "attributes": {
        "name": "Execution environment 1",
        "test-run-id": 29,
        "created-at": "2019-02-22T08:59:38.603Z",
        "updated-at": "2019-02-22T08:59:38.603Z"
      },
      "links": {
        "self": "/execution-environments/1"
      }
    }
  }
```

### URL Parameters

Parameter | Description
--------- | -----------
project_id | The ID of the project you want to retrieve the folders from
test_run_id | The ID of the test run you are executing

### Mandatory fields

Parameter | Description
--------- | -----------
name | The name of the execution environment. It should not be empty and uniq

## Update an execution environment name

```http
PATCH https://studio.cucumberstudio.com/api/projects/<project_id>/test_runs/<test_run_id>/execution_environments/<execution_environmnent_id> HTTP/1.1
Content-Type: application/json; charset=utf-8
Accept: application/vnd.api+json; version=1
access-token: <your access token>
client: <your client id>
uid: <your uid>


{
  "data": {
    "type": "execution-environments",
    "id": <execution_environment_id>,
    "attributes": {
      "name": "Android"
    }
  }
}
```

```http
HTTP/1.1 200 OK
Content-Type: application/vnd.api+json
```

```shell
curl -XPATCH "https://studio.cucumberstudio.com/api/projects/<project_id>/test_runs/<test_run_id>/execution_environments/<execution_environmnent_id>" \
    -H 'Content-Type: application/json' \
    -H 'accept: application/vnd.api+json; version=1' \
    -H 'access-token: <your access token>' \
    -H 'uid: <your uid>' \
    -H 'client: <your client id>' \
    --data $'{ "data": { "type": "execution-environments", "id": <execution_environment_id>, "attributes": { "name": "Android" } } }'
```

```json
{
  "data":
    {
      "type": "execution-environments",
      "id": "1",
      "attributes": {
        "created-at" : "2017-02-28T11:39:08.281Z",
        "updated-at" : "2017-02-28T11:39:08.281Z",
        "name": "Android",
        "test_run_id" : 1
      },
      "links": {
        "self": "/execution-environments/1"
      }
    }
}
```

This endpoint updates the name of an execution environment for a test run and a given project.

### URL Parameters

Parameter | Description
--------- | -----------
project_id | The ID of the project you want to retrieve the action word from
test_run_id | The ID of the test_run that the execution environment belongs to
execution_environment_id | The ID of the execution environment you want to update the name

<aside class="notice">
Specify the name you want to update.
The name is mandatory.
</aside>

## Delete an execution environment

```http
DELETE https://studio.cucumberstudio.com/api/projects/<project_id>/test_runs/<test_run_id>/execution_environments/<execution_environments_id> HTTP/1.1
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
curl -XDELETE "https://studio.cucumberstudio.com/api/projects/<project_id>/test_runs/<test_run_id>/execution_environments/<execution_environments_id>" \
    -H 'accept: application/vnd.api+json; version=1' \
    -H 'access-token: <your access token>' \
    -H 'uid: <your uid>' \
    -H 'client: <your client id>'
```

This endpoint delete an execution environment.

### URL Parameters

Parameter | Description
--------- | -----------
project_id | The ID of the project you want to retrieve the scenario from
test_run_id | The ID of the test_run that the execution environment belongs to
execution_environment_id | The ID of the execution environment to delete

<aside class="warning">
Caution: your execution environment will be totaly and permanently removed from your project.
</aside>

## Create a new build in a specific execution environment

```http
POST https://studio.cucumberstudio.com/api/projects/<project_id>/test_runs/<test_run_id>/execution_environments/<execution_environment_id>/builds" HTTP/1.1
Accept: application/vnd.api+json; version=1
access-token: <your access token>
client: <your client id>
uid: <your uid>
```
```http
HTTP/1.1 201 Created
Content-Type: application/vnd.api+json
```

```shell
curl "https://studio.cucumberstudio.com/api/projects/<project_id>/test_runs/<test_run_id>/execution_environments/<execution_environment_id>/builds" \
    -XPOST \
    -H 'accept: application/vnd.api+json; version=1' \
    -H 'access-token: <your access token>' \
    -H 'uid: <your uid>' \
    -H 'client: <your client id>' \
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
        "execution-environment-id": 29,
        "is_running": true,
        "closed_at": null
      },
      "links": {
        "self": "/builds/3"
      }
    }
  }
```

<aside class="notice">You MUST create a new build when you need to push the execution results of a new run of your tests</aside>

### URL Parameters

Parameter | Description
--------- | -----------
project_id | The ID of the project you want to retrieve the build from
test_run_id | The ID of the test run you are executing
execution_environment_id | The ID of the execution environment for your new build

## Get the current build of an execution environment

```http
GET https://studio.cucumberstudio.com/api/projects/<project_id>/test_runs/<test_run_id>/execution_environments/<execution_environment_id>/builds/current" HTTP/1.1
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
curl "https://studio.cucumberstudio.com/api/projects/<project_id>/test_runs/<test_run_id>/execution_environments/<execution_environment_id>/builds/current" \
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
      "execution-environment-id": 29,
      "is-running": false,
      "closed-at": "2017-06-16T09:13:48.737Z"
    },
    "links": {
      "self": "/builds/1"
    }
  },
  "included": []
}
```

This endpoint retrieves the current build of a given test run.
<aside class="warning">Note that this endpoint will only return the attributes of the build
and not their test results</aside>

### URL Parameters

Parameter | Description
--------- | -----------
project_id | The ID of the project you want to retrieve the build from
test_run_id | The ID of the test run you want to retrieve the build from
execution_environment_id | The ID of the execution environment you want to retrieve the build from

## Get test execution results of the current build of an execution environment

```http
GET https://studio.cucumberstudio.com/api/projects/<project_id>/test_runs/<test_run_id>/execution_environments/<execution_environment_id>/builds/current?include=test-results" HTTP/1.1
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
curl "https://studio.cucumberstudio.com/api/projects/<project_id>/test_runs/<test_run_id>/execution_environments/<execution_environment_id>/builds/current?include=test-results" \
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
      "execution-environment-id": 29,
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
        "test-snapshot-id": 1,
        "execution-environment-id": 29
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
        "test-snapshot-id": 2,
        "execution-environment-id": 29
      },
      "links": {
        "self": "/test-results/2"
      }
    }
  ]
}
```

Use the JSONAPI [include syntax](http://jsonapi.org/format/#fetching-includes) to fetch the test execution results
of the current build of a given execution environment.

### URL Parameters

Parameter | Description
--------- | -----------
project_id | The ID of the project you want to retrieve the build from
test_run_id | The ID of the test run you want to retrieve the build from
execution_environment_id | The ID of the execution environment you want to retrieve the build from

## Add a test execution result to the current build of an execution environment

```http
POST https://studio.cucumberstudio.com/api/projects/<project_id>/test_runs/<test_run_id>/execution_environments/<execution_environment_id>/test_results HTTP/1.1
Content-Type: application/json; charset=utf-8
Accept: application/vnd.api+json; version=1
access-token: <your access token>
client: <your client id>
uid: <your uid>


{
  "data": {
    "type": "test-results",
    "attributes": {
      "status": "passed",
      "status-author": "Harry",
      "description": "All was well"
    },
    "relationships": {
      "test-snapshot": {
        "data": {
          "type": "test-snapshots",
          "id": 1
        }
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
curl -XPOST "https://studio.cucumberstudio.com/api/projects/<project_id>/test_runs/<test_run_id>/execution_environments/<execution_environment_id>/test_results" \
    -H 'Content-Type: application/json' \
    -H 'accept: application/vnd.api+json; version=1' \
    -H 'access-token: <your access token>' \
    -H 'uid: <your uid>' \
    -H 'client: <your client id>' \
    --data '{
      "data": {
        "type": "test-results",
        "attributes": {
          "status": "passed",
          "status-author": "Harry",
          "description": "All was well"
        },
        "relationships": {
          "test-snapshot": {
            "data": {
              "type": "test-snapshots",
              "id": 1
            }
          }
        }
      }
    }'
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
      }
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
```

This endpoint will create a test result in the current build of the specified execution environment.

### URL Parameters

Parameter | Description
--------- | -----------
project_id | The ID of the project you want to retrieve the tests from
test_run_id | The ID of the test run that contains the test you want
execution_environment_id | The ID of the execution environment you want add a test result to

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
