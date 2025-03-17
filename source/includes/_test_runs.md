# Test runs
## Get test runs of a project

```http
GET https://studio.cucumberstudio.com/api/projects/<project_id>/test_runs HTTP/1.1
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
curl "https://studio.cucumberstudio.com/api/projects/<project_id>/test_runs" \
    -H 'accept: application/vnd.api+json; version=1' \
    -H 'access-token: <your access token>' \
    -H 'uid: <your uid>' \
    -H 'client: <your client id>'
```

```json
{
  "data": [
    {
      "type": "test-runs",
      "id": "1",
      "attributes": {
        "created-at" : "2017-02-28T11:39:08.281Z",
        "updated-at" : "2017-02-28T11:39:08.281Z",
        "last-author" : "harry@example.org",
        "name": "Sprint 1",
        "description": "Wandering in the countryside, doing boring stuff",
        "statuses": {
          "passed": 0,
          "failed": 0,
          "retest": 0,
          "undefined": 765,
          "blocked": 0,
          "skipped": 0,
          "wip": 0
        },
        "archived": false,
        "external": false
      },
      "links": {
        "self": "/test-runs/1"
      },
      "relationships": {
        "tags": {}
      }
    },
    {
      "type": "test-runs",
      "id": "2",
      "attributes": {
        "name": "Sprint 2",
        "description": "Bank robbery and blowing up things",
        "statuses": {
          "passed": 15,
          "failed": 42,
          "retest": 0,
          "undefined": 0,
          "blocked": 0,
          "skipped": 0,
          "wip": 0
        },
        "archived": true,
        "external": false
      },
      "links": {
        "self": "/test-runs/2"
      },
      "relationships": {
        "tags": {}
      }
    }
  ]
}
```

This endpoint retrieves all test runs of a given project. The order is undefined.

<aside class="notice">
<p>Note: you can use the "filter[status]" parameter to only fetch archived or active test runs
as a query string of the request:</p>
<code>
https://studio.cucumberstudio.com/api/projects/&lt;project_id&gt;/test_runs?filter[status]=active
</code><br /><code>
https://studio.cucumberstudio.com/api/projects/&lt;project_id&gt;/test_runs?filter[status]=archived
</code>
</aside>

### URL Parameters

Parameter          | Description
------------------ | -----------
project_id         | The ID of the project you want to retrieve the test runs from
filter[status]     | "active" or "archived"

## Get a single test run

```http
GET https://studio.cucumberstudio.com/api/projects/<project_id>/test_runs/<test_run_id> HTTP/1.1
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
curl "https://studio.cucumberstudio.com/api/projects/<project_id>/test_runs/<test_run_id>" \
    -H 'accept: application/vnd.api+json; version=1' \
    -H 'access-token: <your access token>' \
    -H 'uid: <your uid>' \
    -H 'client: <your client id>'
```

```json
{
  "data":
    {
      "type": "test-runs",
      "id": "1",
      "attributes": {
        "created-at" : "2017-02-28T11:39:08.281Z",
        "updated-at" : "2017-02-28T11:39:08.281Z",
        "last-author" : "harry@example.org",
        "name": "Sprint 1",
        "description": "Wandering in the countryside, doing boring stuff",
        "statuses": {
          "passed": 0,
          "failed": 0,
          "retest": 0,
          "undefined": 765,
          "blocked": 0,
          "skipped": 0,
          "wip": 0
        },
        "archived": false,
        "external": false
      },
      "links": {
        "self": "/test-runs/1"
      },
      "relationships": {
        "tags": {}
      }
    }
}
```

This endpoint retrieves a single test run of a given project.

### URL Parameters

Parameter | Description
--------- | -----------
project_id | The ID of the project you want to retrieve the test run from
test_run_id | The ID of the test run you want to get

## Archive test runs

```http
POST https://studio.cucumberstudio.com/api/projects/<project_id>/test_runs/archive?older_than=2021-02-13 HTTP/1.1
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
curl -X POST "https://studio.cucumberstudio.com/api/projects/<project_id>/test_runs/archive?older_than=2021-02-13" \
    -H 'accept: application/vnd.api+json; version=1' \
    -H 'access-token: <your access token>' \
    -H 'uid: <your uid>' \
    -H 'client: <your client id>'
```

```json
{
  "meta": {
    "archived_test_run_ids": [12, 15]
  }
}
```

This endpoint archives all test runs older than the specified date.

### URL Parameters

Parameter  | Description
---------- | -----------
older_than | An ISO 8601 date (YYYY-MM-DD). All test runs created before this date will be archived. Mandatory.

## Include tags when fetching your test run(s)

```http
GET https://studio.cucumberstudio.com/api/projects/<project_id>/test_runs?include=tags HTTP/1.1
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
curl "https://studio.cucumberstudio.com/api/projects/<project_id>/test_runs?include=tags" \
    -H 'accept: application/vnd.api+json; version=1' \
    -H 'access-token: <your access token>' \
    -H 'uid: <your uid>' \
    -H 'client: <your client id>'
```
> Also works when retrieving a single test run

You can use the JSONAPI [include syntax](http://jsonapi.org/format/#fetching-includes) to fetch the tags of your test runs

## Create a test run

```http
POST https://studio.cucumberstudio.com/api/projects/<project_id>/test_runs HTTP/1.1
Content-Type: application/json; charset=utf-8
Accept: application/vnd.api+json; version=1
access-token: <your access token>
client: <your client id>
uid: <your uid>


{
  "data": {
    "attributes": {
      "name": "Sprint 1",
      "description": "My TR description",
      "scenario_ids": [1, 2, 3]
    }
  }
}
```

```http
HTTP/1.1 201 Created
Content-Type: application/vnd.api+json
```

```shell
curl -X POST "https://studio.cucumberstudio.com/api/projects/<project_id>/test_runs" \
    -H 'Content-Type: application/json' \
    -H 'accept: application/vnd.api+json; version=1' \
    -H 'access-token: <your access token>' \
    -H 'uid: <your uid>' \
    -H 'client: <your client id>' \
    --data '{"data": {"attributes": {"name": "Sprint 1", "description": "My TR description", "scenario_ids": [1, 2, 3]} } }'
```

```json
{
  "data":
    {
      "type": "test-runs",
      "id": "1",
      "attributes": {
        "created-at" : "2017-02-28T11:39:08.281Z",
        "updated-at" : "2017-02-28T11:39:08.281Z",
        "last-author" : "harry@example.org",
        "name": "Sprint 1",
        "description": "My TR description",
        "statuses": {
          "passed": 0,
          "failed": 0,
          "retest": 0,
          "undefined": 3,
          "blocked": 0,
          "skipped": 0,
          "wip": 0
        },
        "archived": false,
        "external": false
      },
      "links": {
        "self": "/test-runs/1"
      },
      "relationships": {
        "tags": {}
      }
    }
}
```

This endpoint creates a new test run.

<aside class="notice">
If you don't specify scenario ids, you'll create a test run with all your available scenarios in the project.
</aside>

### URL Parameters

Parameter | Description
--------- | -----------
project_id | The ID of the project in which you want to create the test run.

<aside class="notice">
You can create tags alongside the test run by specifying them in the "relationship" section, as explained in the <a href="#create-tags-alongside-elements">tags creation section</a>.
</aside>

### Mandatory fields

Field | Description
--------- | -----------
name | (String) The name of the test run.

### Other fields

Field | Description
--------- | -----------
scenario_ids | (List of Integer) The ids of scenarios you want in the test run.
external | 1 or true to create an external test run.
description | (String) The description of the test run.

<aside class="notice">
You can create a test run from a subset of tests by specifying the list of scenario ids.
</aside>

<aside class="notice">
If you specify scenario ids, `external` will be ignored. External test runs will
be created empty.
</aside>

## Update test run description

```http
PATCH https://studio.cucumberstudio.com/api/projects/<project_id>/test_runs/<test_run_id> HTTP/1.1
Accept: application/vnd.api+json; version=1
access-token: <your access token>
client: <your client id>
uid: <your uid>


{
  "data": {
    "type": "test_runs",
    "id": <test_run_id>,
    "attributes": {
      "description": "My new test run description"
    }
  }
}
```

```http
HTTP/1.1 201 Created
Content-Type: application/vnd.api+json
```

```shell
curl -X PATCH "https://studio.cucumberstudio.com/api/projects/<project_id>/test_runs/<test_run_id>" \
    -H 'accept: application/vnd.api+json; version=1' \
    -H 'access-token: <your access token>' \
    -H 'uid: <your uid>' \
    -H 'client: <your client id>' \
    --data '{"data": { "type": "test_runs", "id": <test_run_id>, {"attributes": {"description": "My new test run description" } } }'
```

```json
{
  "data":
    {
      "type": "test-runs",
      "id": "3",
      "attributes": {
        "created-at": "2021-06-10T09:35:01.975Z",
        "updated-at": "2021-06-14T12:19:32.607Z",
        "last-author" : "harry@example.org",
        "name": "My new test run",
        "description": "My new test run description",
        "statuses": {},
        "archived": false,
        "external": false
      },
      "links": {
        "self": "/test-runs/3"
      },
      "relationships": {
        "tags": {}
      }
    }
}
```

This endpoint updates the description of a given test run.
## Clone a test run

```http
POST https://studio.cucumberstudio.com/api/projects/<project_id>/test_runs HTTP/1.1
Accept: application/vnd.api+json; version=1
access-token: <your access token>
client: <your client id>
uid: <your uid>


{
  "data": {
    "attributes": {
      "name": "My new test run",
      "test_run_id": 1
    }
  }
}
```

```http
HTTP/1.1 201 Created
Content-Type: application/vnd.api+json
```

```shell
curl -X POST "https://studio.cucumberstudio.com/api/projects/<project_id>/test_runs" \
    -H 'accept: application/vnd.api+json; version=1' \
    -H 'access-token: <your access token>' \
    -H 'uid: <your uid>' \
    -H 'client: <your client id>' \
    --data '{"data": {"attributes": {"name": "My new test run", "test_run_id": 1} } }'
```

```json
{
  "data":
    {
      "type": "test-runs",
      "id": "2",
      "attributes": {
        "created-at": "2019-05-23T08:30:17.398Z",
        "updated-at": "2019-05-23T08:30:17.398Z",
        "last-author" : "harry@example.org",
        "name": "My new test run",
        "description": "first test run description",
        "statuses": {},
        "archived": false,
        "external": false
      },
      "links": {
        "self": "/test-runs/2"
      },
      "relationships": {
        "tags": {}
      }
    }
}
```

This endpoint clones a test run.

### URL Parameters

Parameter | Description
--------- | -----------
project_id | The ID of the project in which you want to create the test run.

### Mandatory fields

Field | Description
--------- | -----------
name | (String) The name of the test run.
test_run_id | (Integer) The id of the source test run.

## Synchronize a test run
Synchronization give you the ability to update the tests of your test run with their last version, based on the current scenarios definitions

### Watch synchronization state
```http
GET https://studio.cucumberstudio.com/api/projects/<project_id>/test_runs/<test_run_id>?show_synchronization_information=true HTTP/1.1
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
curl "https://studio.cucumberstudio.com/api/projects/<project_id>/test_runs/<test_run_id>?show_synchronization_information=true" \
    -H 'accept: application/vnd.api+json; version=1' \
    -H 'access-token: <your access token>' \
    -H 'uid: <your uid>' \
    -H 'client: <your client id>'
```

```json
{
  "data":
    {
      "type": "test-runs",
      "id": "1",
      "attributes": {
        "created-at" : "2017-02-28T11:39:08.281Z",
        "updated-at" : "2017-02-28T11:39:08.281Z",
        "last-author" : "harry@example.org",
        "name": "Sprint 1",
        "description": "Wandering in the countryside, doing boring stuff",
        "statuses": {
          "passed": 0,
          "failed": 0,
          "retest": 0,
          "undefined": 765,
          "blocked": 0,
          "skipped": 0,
          "wip": 0
        },
        "archived": false,
        "external": false,
        "synchronization-information": {
          "synchronizable": true,
          "synchronizing": false,
          "details": {
            "deleted_folders_snapshots": [],
            "deleted_scenarios_snapshots": [],
            "deleted_tests_snapshots": []
          }
        }
      },
      "links": {
        "self": "/test-runs/1"
      },
      "relationships": {
        "tags": {}
      }
    }
}
```
This endpoint is useful to track the state of a test run synchronization.

The synchronization operation can be dangerous. If some of your test run tests and folders are based on scenarios and folders that no longer exist, they will be destroyed.
It is strongly advised to use this endpoint to get the potential impacts of a synchronization before running one.

### Synchronize the test run

```http
POST https://studio.cucumberstudio.com/api/projects/<project_id>/test_runs/<test_run_id>/synchronize HTTP/1.1
Content-Type: application/json; charset=utf-8
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
curl -X POST "https://studio.cucumberstudio.com/api/projects/<project_id>/test_runs/<test_run_id>/synchronize" \
    -H 'Content-Type: application/json' \
    -H 'accept: application/vnd.api+json; version=1' \
    -H 'access-token: <your access token>' \
    -H 'uid: <your uid>' \
    -H 'client: <your client id>'
```


```json
{
  "data":
    {
      "type": "test-runs",
      "id": "1",
      "attributes": {
        "created-at" : "2017-02-28T11:39:08.281Z",
        "updated-at" : "2017-02-28T11:39:08.281Z",
        "last-author" : "harry@example.org",
        "name": "Sprint 1",
        "description": "Wandering in the countryside, doing boring stuff",
        "statuses": {
          "passed": 0,
          "failed": 0,
          "retest": 0,
          "undefined": 765,
          "blocked": 0,
          "skipped": 0,
          "wip": 0
        },
        "archived": false,
        "external": false,
        "synchronization-information": {
          "synchronizable": true,
          "synchronizing": true,
          "details": {
            "deleted_folders_snapshots": [],
            "deleted_scenarios_snapshots": [],
            "deleted_tests_snapshots": []
          }
        }
      },
      "links": {
        "self": "/test-runs/1"
      },
      "relationships": {
        "tags": {}
      }
    }
}
```

This endpoint will start the synchronization of a given test run.

<aside class="notice">
Since this is an asynchronous operation, the synchronization might not be done when the server responds back. Use the previous endpoint to watch the state of the
synchronization before doing anything else with your test run data.
</aside>

<aside class="notice">
Only one synchronization of a test run can be run at the same time. Calling this endpoint when the test run is synchronizing won't do anything.
</aside>

<aside class="notice">
Only 10 synchronizations of test runs per project can be run at the same time.
</aside>

### URL Parameters

Parameter | Description
--------- | -----------
project_id | The ID of the project containing the test run
test_run_id | The ID of the test run you want to synchronize


## Get builds history of a test run

```http
GET https://studio.cucumberstudio.com/api/projects/<project_id>/test_runs/<test_run_id>/build_history HTTP/1.1
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
curl "https://studio.cucumberstudio.com/api/projects/<project_id>/test_runs/<test_run_id>/build_history" \
    -H 'accept: application/vnd.api+json; version=1' \
    -H 'access-token: <your access token>' \
    -H 'uid: <your uid>' \
    -H 'client: <your client id>'
```

```json
{
    "data": [
        {
            "id": 3,
            "date": "2018-09-12T08:19:28.446Z",
            "values": {
                "passed": 1,
                "failed": 1,
                "wip": 0,
                "retest": 1,
                "blocked": 0,
                "skipped": 0,
                "undefined": 0
            },
            "platform": "Default"
        },
        {
            "id": 2,
            "date": "2018-09-12T08:19:09.615Z",
            "values": {
                "passed": 2,
                "failed": 0,
                "wip": 1,
                "retest": 0,
                "blocked": 0,
                "skipped": 0,
                "undefined": 0
            },
            "platform": "Default"
        },
        {
            "id": 1,
            "date": "2018-09-12T07:21:21.606Z",
            "values": {
                "passed": 2,
                "failed": 1,
                "wip": 0,
                "retest": 0,
                "blocked": 0,
                "skipped": 0,
                "undefined": 0
            },
            "platform": "Default"
        }
    ]
}
```

This endpoint retrieves build history of a given test run.

### URL Parameters

Parameter | Description
--------- | -----------
project_id | The ID of the project you want to retrieve the test run from
test_run_id | The ID of the test run you want to get

<aside class="notice">
By default, this endpoint will return the last 25 builds.
You can override this limit by including a query parameter ex: ?limit=10.
</aside>

## Add a scenario to an existing test run

```http
PATCH https://studio.cucumberstudio.com/api/projects/<project_id>/test_runs/<test_run_id> HTTP/1.1
Content-Type: application/json; charset=utf-8
Accept: application/vnd.api+json; version=1
access-token: <your access token>
client: <your client id>
uid: <your uid>


{
  "data": {
    "type": "test_runs",
    "id": 1,
    "attributes": {
      "scenario_id": 1
    }
  }
}
```

```http
HTTP/1.1 200 OK
Content-Type: application/vnd.api+json
```

```shell
curl -XPATCH https://studio.cucumberstudio.com/api/projects/<project_id>/test_runs/<test_run_id> \
    -H 'Content-Type: application/json' \
    -H 'accept: application/vnd.api+json; version=1' \
    -H 'access-token: <your access token>' \
    -H 'uid: <your uid>' \
    -H 'client: <your client id>' \
    --data '{"data": {"type": "test_runs", "id": 1, "attributes": {"scenario_id": 1}}}'
```

```json
{
  "data": [
    {
      "type": "test-runs",
      "id": "1",
      "attributes": {
        "created-at" : "2019-05-27T11:39:08.281Z",
        "updated-at" : "2019-05-27T11:39:08.281Z",
        "last-author" : "harry@example.org",
        "name": "Sprint 1",
        "description": "Wandering in the countryside, doing boring stuff",
        "statuses": {
          "passed": 0,
          "failed": 0,
          "retest": 0,
          "undefined": 765,
          "blocked": 0,
          "skipped": 0,
          "wip": 0
        },
        "archived": false,
        "external": false
      },
      "links": {
        "self": "/test-runs/1"
      },
      "relationships": {
        "tags": {}
      }
    }
  ]
}
```

This endpoint adds a scenario to a given test run.

## Add multiple scenarios to an existing test run

```http
PATCH https://studio.cucumberstudio.com/api/projects/<project_id>/test_runs/<test_run_id> HTTP/1.1
Content-Type: application/json; charset=utf-8
Accept: application/vnd.api+json; version=1
access-token: <your access token>
client: <your client id>
uid: <your uid>


{
  "data": {
    "type": "test_runs",
    "id": 1,
    "attributes": {
      "scenario_ids": [2233,76547]
    }
  }
}
```

```http
HTTP/1.1 200 OK
Content-Type: application/vnd.api+json
```

```shell
curl -XPATCH https://studio.cucumberstudio.com/api/projects/<project_id>/test_runs/<test_run_id> \
    -H 'Content-Type: application/json' \
    -H 'accept: application/vnd.api+json; version=1' \
    -H 'access-token: <your access token>' \
    -H 'uid: <your uid>' \
    -H 'client: <your client id>' \
    --data '{"data": {"type": "test_runs", "id": 1, "attributes": {"scenario_ids":  [2233,76547] }}}'
```

```json
{
  "data": [
    {
      "type": "test-runs",
      "id": "1",
      "attributes": {
        "created-at" : "2019-05-27T11:39:08.281Z",
        "updated-at" : "2019-05-27T11:39:08.281Z",
        "last-author" : "harry@example.org",
        "name": "Sprint 1",
        "description": "Wandering in the countryside, doing boring stuff",
        "statuses": {
          "passed": 0,
          "failed": 0,
          "retest": 0,
          "undefined": 767,
          "blocked": 0,
          "skipped": 0,
          "wip": 0
        },
        "archived": false,
        "external": false
      },
      "links": {
        "self": "/test-runs/1"
      },
      "relationships": {
        "tags": {}
      }
    }
  ]
}
```

This endpoint adds several scenarios to a given test run.

### URL Parameters

Parameter | Description
--------- | -----------
project_id | The ID of the project you want to retrieve the test run from
test_run_id | The ID of the test run you want to get

## List attachments of a given test run

```http
GET https://studio.cucumberstudio.com/api/projects/<project_id>/test_runs/<test_run_id>/attachments HTTP/1.1
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
curl -XGET "https://studio.cucumberstudio.com/api/projects/<project_id>/test_runs/<test_run_id>/attachments" \
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
        "file-url": "/api/projects/1/test_runs/1/attachments/1",
        "file-size": 100
      },
      "links": {
        "self": "/attachments/1"
      }
    }
  ]
}
```

This endpoint list all the attachments of a given test run

### URL Parameters

Parameter   | Description
---------   | -----------
project_id  | The ID of the project you want to retrieve the test run from
test_run_id | The ID of the target test run

## Get a given attachment of a given test run

```http
GET https://studio.cucumberstudio.com/api/projects/<project_id>/test_runs/<test_run_id>/attachments/<attachment_id> HTTP/1.1
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
curl -XGET -L "https://studio.cucumberstudio.com/api/projects/<project_id>/test_runs/<test_run_id>/attachments/<attachment_id>" \
    -H 'Content-Type: application/json' \
    -H 'accept: application/vnd.api+json; version=1' \
    -H 'access-token: <your access token>' \
    -H 'uid: <your uid>' \
    -H 'client: <your client id>' \
    --output my-attachment.jpg
```

This endpoint return the requested attachment of a given test run

### URL Parameters

Parameter      | Description
---------      | -----------
project_id     | The ID of the project you want to retrieve the test run from
test_run_id    | The ID of the target test run
attachment_id  | The ID of the target attachment

## Create an attachment to a given test run

```http
POST https://studio.cucumberstudio.com/api/projects/<project_id>/test_runs/<test_run_id>/attachments HTTP/1.1
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
curl -X POST "https://studio.cucumberstudio.com/api/projects/<project_id>/test_runs/<test_run_id>/attachments" \
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
      "file-url": "/api/projects/1/test_runs/1/attachments/1",
      "file-size": 100
    },
    "links": {
      "self": "/attachments/1"
    }
  }
}
```

This endpoint create an attachment to a given test run

### URL Parameters

Parameter   | Description
---------   | -----------
project_id  | The ID of the project you want to retrieve the test run from
test_run_id | The ID of the target test run

## Update an attachment to a given test run

```http
PATCH https://studio.cucumberstudio.com/api/projects/<project_id>/test_runs/<test_run_id>/attachments/<attachment_id> HTTP/1.1
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
curl -XPATCH "https://studio.cucumberstudio.com/api/projects/<project_id>/test_runs/<test_run_id>/attachments/<attachment_id>" \
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
      "file-url": "/api/projects/1/test_runs/1/attachments/1",
      "file-size": 100
    },
    "links": {
      "self": "/attachments/1"
    }
  }
}
```

This endpoint update the attachment to a given test run

### URL Parameters

Parameter     | Description
---------     | -----------
project_id    | The ID of the project you want to retrieve the test run from
test_run_id   | The ID of the target test run
attachment_id | The ID of the target attachment

## Delete an attachment to a given test run

```http
DELETE https://studio.cucumberstudio.com/api/projects/<project_id>/test_runs/<test_run_id>/attachments/<attachment_id> HTTP/1.1
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
curl -XDELETE "https://studio.cucumberstudio.com/api/projects/<project_id>/test_runs/<test_run_id>/attachments/<attachment_id>" \
    -H 'Content-Type: application/json' \
    -H 'accept: application/vnd.api+json; version=1' \
    -H 'access-token: <your access token>' \
    -H 'uid: <your uid>' \
    -H 'client: <your client id>' \
```

```json
{}
```

This endpoint delete a given attachment of a test run

### URL Parameters

Parameter     | Description
---------     | -----------
project_id    | The ID of the project you want to retrieve the test run from
test_run_id   | The ID of the target test run
attachment_id | The ID of the target attachment
