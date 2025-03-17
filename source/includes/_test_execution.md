# Test execution

## Getting started with test executions

Test execution results in CucumberStudio are organized in the following way:

* Test execution results are grouped into builds
* Each build belongs to an execution environment
* A test run can contain multiple execution environments, each containing their own builds of test execution results.

**The notion of execution environments is entirely optional.**
You can use them if you have several environments on which you want to execute your tests.
If you do not wish to have specific environments, you can ignore them and work directly with builds at test run level.

<aside class="notice">
If no environment is specified, test runs will always have a default environment in which all builds are created.
At any moment it is possible to start working with multiple environments
by <a href="#create-a-new-execution-environment">creating new ones</a>.
All existing builds will still exist in the first, default execution environment.
</aside>

The [Builds section](#builds) specifies all operations that can be performed without execution environments.

The [Execution environments section](#execution-environments) specifies how to work with multiple environments.

Each entry in the Builds section has a warning if an execution environment ID is mandatory
when working with multiple environments.

## Add a test execution result

```http
POST https://studio.cucumberstudio.com/api/projects/<project_id>/test_runs/<test_run_id>/test_snapshots/<test_snapshot_id>/test_results HTTP/1.1
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
      "description": "All was well",
      "step-statuses": ["passed", "passed", "passed"]
    }
  }
}
```

```http
HTTP/1.1 201 Created
Content-Type: application/vnd.api+json
```

```shell
curl -XPOST "https://studio.cucumberstudio.com/api/projects/<project_id>/test_runs/<test_run_id>/test_snapshots/<test_snapshot_id>/test_results" \
    -H 'Content-Type: application/json' \
    -H 'accept: application/vnd.api+json; version=1' \
    -H 'access-token: <your access token>' \
    -H 'uid: <your uid>' \
    -H 'client: <your client id>' \
    --data '{"data": {"type": "test-results", "attributes": {"status": "passed", "status-author": "Harry", "description": "All was well", "step-statuses": ["passed", "passed", "passed"]}}}'
```

> Newly created test result

``` json
{
  "data": {
    "type": "test-results",
    "id": "1",
    "attributes": {
      "created-at" : "2017-02-28T11:39:08.281Z",
      "updated-at" : "2017-02-28T11:39:08.281Z",
      "last-author" : "harry@example.org",
      "status": "passed",
      "created-at": "Couple of miliseconds ago",
      "description": "",
      "status-author": "Harry",
      "step-statuses": ["passed", "passed", "passed"]
    },
    "links": {
      "self": "/test-results/1"
    },
    "relationships": {
      "test-snapshot": {
        "data": {
          "type": "test-snapshots",
          "id": "1"
        }
      },
      "build": {
        "data": null
      }
    }
  },
  "included": [
    {
      "test-snapshot": "test data"
    }
  ]
}
```

### URL Parameters

Parameter | Description
--------- | -----------
project_id | The ID of the project you want to retrieve the tests from
test_run_id | The ID of the test run that contains the test you want
test_snapshot_id | The ID of the test whose you want add a test result to

### Mandatory fields

Field | Description
--------- | -----------
status | (String) The result of the test execution. Possible values are 'passed', 'failed', 'wip', 'retest', 'blocked', 'skipped', 'undefined'.
status-author | (String) The name of the author of the test execution
description | (String) A comment about the test execution

<aside class="notice">
If the provided 'status' value does not match any of the listed possible values, the result will be set as 'undefined'
</aside>

### Optional fields

Field | Description
--------- | -----------
build | (JSONAPI Relationship) The build containing your test execution result
execution-environment | (JSONAPI Relationship) The execution environment containing your test execution result
step-statuses | (String Array) The status for each individual step

If a build is provided, the test result will be created into that build.

If an execution environment is provided, the test result will be created into the current build of that execution environment

<aside class="warning">
Providing an execution environment is not needed if a build is already specified, and will return an error if it does not belong to that environment.
</aside>

If step statuses are provided, anything different from `'passed'`, `'failed'`, `'wip'`, `'retest'`, `'blocked'`, `'skipped'`, or `'undefined'` will be interpreted as `'undefined'`. If providing something else than a array of statuses, it will be interpreted as empty array, which means all step statuses are `'undefined'`.

When setting step statuses on creation, they can match the steps of the scenario, or the steps of the test. The number of steps in each case can be different because a call to an actionword step can expand into multiple steps:. So the following rules apply:

* If the given step statuses array is of the same size or bigger than the number of steps in the test, the given step statuses will be interpreted as test step statuses
* If the given step statuses array is smaller than the number of steps in the test, the given step statuses will be interpreted as scenario step statuses, and will be expanded accordingly to the scenario.

For instance, if a scenario has two steps, and each one is a call to an actionword having 2 steps, then the scenario has 2 steps and the corresponding test has 4 steps. Here are the possibilities:

* Creating a test result with step statuses being `['passed', 'failed']` will be interpreted as scenario steps and be expanded to `['passed', 'passed', 'failed', 'failed']`.
* Creating a test result with step statuses being `['passed', 'failed', 'skipped', 'skipped']` will be interpreted as test steps and used as-is.
* Creating a test result with step statuses being `['passed']` will be interpreted as scenario steps and be expanded to `['passed', 'passed']`. Unspecified statuses are always `'undefined'`.
* Creating a test result with step statuses being `['passed', 'failed', 'skipped']` will be interpreted as scenario steps and be expanded to `['passed', 'passed', 'failed', 'failed']`. The extra `'skipped'` is dropped.
* Creating a test result with step statuses being `['passed', 'failed', 'skipped', 'skipped', 'wip']` will be interpreted as test steps and used as-is. The extra `'wip'` is dropped.

```http
POST https://studio.cucumberstudio.com/api/projects/<project_id>/test_runs/<test_run_id>/test_snapshots/<test_snapshot_id>/test_results HTTP/1.1
Content-Type: application/json; charset=utf-8
Accept: application/vnd.api+json; version=1
access-token: <your access token>
client: <your client id>
uid: <your uid>

{
  "data": {
    "type": "test-results",
    "attributes": {"status": "passed", "status-author": "Harry", "description": "All was well"},
    "relationships": {
      "build": {
        "data": {
          "type": "build",
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
curl -XPOST "https://studio.cucumberstudio.com/api/projects/<project_id>/test_runs/<test_run_id>/test_snapshots/<test_snapshot_id>/test_results" \
    -H 'Content-Type: application/json' \
    -H 'accept: application/vnd.api+json; version=1' \
    -H 'access-token: <your access token>' \
    -H 'uid: <your uid>' \
    -H 'client: <your client id>' \
    --data '{
      "type": "test-results", "attributes": {"status": "passed", "status-author": "Harry", "description": "All was well"},
      "relationships": {
        "build": {
          "data": {
            "type: "build",
            "id": 1
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
        }
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
```

```http
POST https://studio.cucumberstudio.com/api/projects/<project_id>/test_runs/<test_run_id>/test_snapshots/<test_snapshot_id>/test_results HTTP/1.1
Content-Type: application/json; charset=utf-8
Accept: application/vnd.api+json; version=1
access-token: <your access token>
client: <your client id>
uid: <your uid>


{
  "data": {
    "type": "test-results",
    "attributes": {"status": "passed", "status-author": "Harry", "description": "All was well"},
    "relationships": {
      "execution-environment": {
        "data": {
          "type": "execution-environment",
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
curl -XPOST "https://studio.cucumberstudio.com/api/projects/<project_id>/test_runs/<test_run_id>/test_snapshots/<test_snapshot_id>/test_results" \
    -H 'Content-Type: application/json' \
    -H 'accept: application/vnd.api+json; version=1' \
    -H 'access-token: <your access token>' \
    -H 'uid: <your uid>' \
    -H 'client: <your client id>' \
    --data '{
      "type": "test-results", "attributes": {"status": "passed", "status-author": "Harry", "description": "All was well"},
      "relationships": {
        "execution-environment": {
          "data": {
            "type: "execution-environment",
            "id": 1
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
        }
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
```

## Update a test execution result

```http
PATCH https://studio.cucumberstudio.com/api/projects/<project_id>/test_runs/<test_run_id>/test_snapshots/<test_snapshot_id>/test_results/<test_result_id> HTTP/1.1
Content-Type: application/json; charset=utf-8
Accept: application/vnd.api+json; version=1
access-token: <your access token>
client: <your client id>
uid: <your uid>

{
  "data": {
    "type": "test-results",
    "id": <test_result_id>,
    "attributes": {
      "status": "passed",
      "status-author": "Jenkins",
      "description": "Automated jenkins job"
    }
  }
}
```

```http
HTTP/1.1 200 OK
Content-Type: application/vnd.api+json
```

```shell
curl -XPATCH "https://studio.cucumberstudio.com/api/projects/<project_id>/test_runs/<test_run_id>/test_snapshots/<test_snapshot_id>/test_results/<test_result_id>" \
    -H 'Content-Type: application/json' \
    -H 'accept: application/vnd.api+json; version=1' \
    -H 'access-token: <your access token>' \
    -H 'uid: <your uid>' \
    -H 'client: <your client id>' \
    --data '{"data": {"type": "test-results", "id": <test_result_id>, "attributes": {"status": "passed", "status-author": "Jenkins", "description": "Automated jenkins job"}}}'
```

> Updated test result

``` json
{
  "data": {
    "type": "test-results",
    "id": "<test_result_id>",
    "attributes": {
      "created-at" : "2017-02-28T11:39:08.281Z",
      "updated-at" : "2017-02-28T11:39:08.281Z",
      "last-author" : "harry@example.org",
      "status": "passed",
      "created-at": "Couple of miliseconds ago",
      "description": "Automated jenkins job",
      "status-author": "Jenkins"
    },
    "links": {
      "self": "/test-results/<test_result_id>"
    },
    "relationships": {
      "test-snapshot": {},
      "build": {}
    }
  }
}
```

The API allows you to update a test result following the
[{json:api} way to patch resources](http://jsonapi.org/format/#crud-updating).

Status, author and/or description may be updated specifying the
`status`, `status-author` and/or `description` attributes of the resource.

### URL Parameters

Parameter | Description
--------- | -----------
project_id | The ID of the project you want to retrieve the tests from
test_run_id | The ID of the test run that contains the test you want
test_snapshot_id | The ID of the test whose you want to update a test result to
test_result_id | The ID of the test result you want to update

### Attributes that may be updated

Field | Description
--------- | -----------
status | (String) The status of the test execution. Possible values are 'passed', 'failed', 'wip', 'retest', 'blocked', 'skipped', 'undefined'.
status-author | (String) The name of the author of the test execution
description | (String) A comment about the test execution

<aside class="notice">
If the provided 'status' value does not match any of the listed possible values, the result will be set as 'undefined'
</aside>

## List attachments of a given test execution result

```http
GET https://studio.cucumberstudio.com/api/projects/<project_id>/test_runs/<test_run_id>/test_snapshots/<test_snapshot_id>/test_results/<test_result_id>/attachments HTTP/1.1
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
curl -XGET "https://studio.cucumberstudio.com/api/projects/<project_id>/test_runs/<test_run_id>/test_snapshots/<test_snapshot_id>/test_results/<test_result_id>/attachments" \
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
        "file-url": "/api/projects/1/test_runs/1/test_snapshots/1/test_results/1/attachments/1",
        "file-size": 100
      },
      "links": {
        "self": "/attachments/1"
      }
    }
  ]
}
```

This endpoint list all the attachments of a given test execution result

### URL Parameters

Parameter        | Description
---------        | -----------
project_id       | The ID of the project you want to retrieve the test execution result from
test_run_id      | The ID of the test run you want to retrieve the test execution result from
test_snapshot_id | The ID of the test that you want to retrieve the test execution result from
test_result_id   | The ID of the test execution result you want

## Get a given attachment of a given test execution result

```http
GET https://studio.cucumberstudio.com/api/projects/<project_id>/test_runs/<test_run_id>/test_snapshots/<test_snapshot_id>/test_results/<test_result_id>/attachments/<attachment_id> HTTP/1.1
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
curl -XGET -L "https://studio.cucumberstudio.com/api/projects/<project_id>/test_runs/<test_run_id>/test_snapshots/<test_snapshot_id>/test_results/<test_result_id>/attachments/<attachment_id>" \
    -H 'Content-Type: application/json' \
    -H 'accept: application/vnd.api+json; version=1' \
    -H 'access-token: <your access token>' \
    -H 'uid: <your uid>' \
    -H 'client: <your client id>' \
    --output my-attachment.jpg
```

This endpoint return the requested attachment of a given test execution result

### URL Parameters

Parameter        | Description
---------        | -----------
project_id       | The ID of the project you want to retrieve the test execution result from
test_run_id      | The ID of the test run you want to retrieve the test execution result from
test_snapshot_id | The ID of the test that you want to retrieve the test execution result from
test_result_id   | The ID of the test execution result you want

## Create an attachment to a given test execution result

```http
POST https://studio.cucumberstudio.com/api/projects/<project_id>/test_runs/<test_run_id>/test_snapshots/<test_snapshot_id>/test_results/<test_result_id>/attachments HTTP/1.1
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
curl -XPOST "https://studio.cucumberstudio.com/api/projects/<project_id>/test_runs/<test_run_id>/test_snapshots/<test_snapshot_id>/test_results/<test_result_id>/attachments" \
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
      "file-url": "/api/projects/1/test_runs/1/test_snapshots/1/test_results/1/attachments/1",
      "file-size": 100
    },
    "links": {
      "self": "/attachments/1"
    }
  }
}
```

This endpoint create an attachment to a given test execution result

### URL Parameters

Parameter        | Description
---------        | -----------
project_id       | The ID of the project you want to retrieve the test execution result from
test_run_id      | The ID of the test run you want to retrieve the test execution result from
test_snapshot_id | The ID of the test that you want to retrieve the test execution result from
test_result_id   | The ID of the test execution result you want

## Update an attachment to a given test run

```http
PATCH https://studio.cucumberstudio.com/api/projects/<project_id>/test_runs/<test_run_id>/test_snapshots/<test_snapshot_id>/test_results/<test_result_id>/attachments/<attachment_id> HTTP/1.1
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
curl -XPATCH "https://studio.cucumberstudio.com/api/projects/<project_id>/test_runs/<test_run_id>/test_snapshots/<test_snapshot_id>/test_results/<test_result_id>/attachments/<attachment_id>" \
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
      "file-url": "/api/projects/1/test_runs/1/test_snapshots/1/test_results/1/attachments/1",
      "file-size": 100
    },
    "links": {
      "self": "/attachments/1"
    }
  }
}
```

This endpoint update the attachment to a given test execution result

### URL Parameters

Parameter        | Description
---------        | -----------
project_id       | The ID of the project you want to retrieve the test execution result from
test_run_id      | The ID of the test run you want to retrieve the test execution result from
test_snapshot_id | The ID of the test that you want to retrieve the test execution result from
test_result_id   | The ID of the test execution result you want
attachment_id    | The ID of the target attachment

## Delete an attachment to a given test execution result

```http
DELETE https://studio.cucumberstudio.com/api/projects/<project_id>/test_runs/<test_run_id>/test_snapshots/<test_snapshot_id>/test_results/<test_result_id>/attachments/<attachment_id> HTTP/1.1
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
curl -XDELETE "https://studio.cucumberstudio.com/api/projects/<project_id>/test_runs/<test_run_id>/test_snapshots/<test_snapshot_id>/test_results/<test_result_id>/attachments/<attachment_id>" \
    -H 'Content-Type: application/json' \
    -H 'accept: application/vnd.api+json; version=1' \
    -H 'access-token: <your access token>' \
    -H 'uid: <your uid>' \
    -H 'client: <your client id>' \
```

```json
{}
```

This endpoint delete a given attachment of a test execution result

### URL Parameters

Parameter        | Description
---------        | -----------
project_id       | The ID of the project you want to retrieve the test execution result from
test_run_id      | The ID of the test run you want to retrieve the test execution result from
test_snapshot_id | The ID of the test that you want to retrieve the test execution result from
test_result_id   | The ID of the test execution result you want
attachment_id    | The ID of the target attachment
