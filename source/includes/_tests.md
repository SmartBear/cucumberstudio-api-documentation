# Tests

## Get tests of a test run

```http
GET https://studio.cucumberstudio.com/api/projects/<project_id>/test_runs/<test_run_id>/test_snapshots HTTP/1.1
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
curl "https://studio.cucumberstudio.com/api/projects/<project_id>/test_runs/<test_run_id>/test_snapshots" \
    -H 'accept: application/vnd.api+json; version=1' \
    -H 'access-token: <your access token>' \
    -H 'uid: <your uid>' \
    -H 'client: <your client id>'
```

```json

{
  "data": [
    {
      "type": "test-snapshots",
      "id": "1",
      "attributes": {
        "created-at" : "2017-02-28T11:39:08.281Z",
        "updated-at" : "2017-02-28T11:39:08.281Z",
        "last-author" : "harry@example.org",
        "name": "Find horcruxes",
        "definition-json": {
          "scenario_name": "Find horcruxes",
          "dataset_name": null,
          "dataset_id": null,
          "steps": [
            {
              "action": "Given Harry has one horcrux"
            },
            {
              "result": "Then he should destroy it"
            },
          ],
          "index": 0
        },
        "status": "failed",
        "scenario-snapshot-id": 1,
        "folder-snapshot-id": 2
      },
      "links": {
        "self": "/test-snapshots/1"
      },
      "relationships": {
        "scenario": {},
        "dataset": {},
        "last-result": {}
      }
    },
    {
      "type": "test-snapshots",
      "id": "2",
      "attributes": {
        "created-at" : "2017-02-28T11:39:08.281Z",
        "updated-at" : "2017-02-28T11:39:08.281Z",
        "last-author" : "harry@example.org",
        "name": "Defeat Voldemort",
        "definition-json": {
          "scenario_name": "Defeat Voldemort",
          "dataset_name": null,
          "dataset_id": null,
          "steps": [
            {
              "action": "Given Harry cast the Expelliarmus spell"
            },
            {
              "result": "Then Voldemort should be defeated"
            }
          ],
          "index": 0
        },
        "status": "success",
        "scenario-snapshot-id": 1,
        "folder-snapshot-id": 5
      },
      "links": {
        "self": "/test-snapshots/2"
      },
      "relationships": {
        "scenario": {},
        "dataset": {},
        "last-result": {}
      }
    }
  ]
}
```

This endpoint retrieves all test snapshots of a test run

<aside class="warning"><b>Deprecations</b>
  <br>Test status attribute is deprecated. More information <a href="#test-status">here</a>.
</aside>

### URL Parameters

Parameter | Description
--------- | -----------
project_id | The ID of the project you want to retrieve the tests from
test_run_id | The ID of the test run that contains the tests you want

<aside class="notice">
  The list of available statuses for a test are:
  <ul>
    <li>undefined</li>
    <li>passed</li>
    <li>failed</li>
    <li>retest</li>
    <li>blocked</li>
    <li>wip</li>
    <li>skipped</li>
  </ul>
</aside>

### Optional parameter

Parameter | Description
--------- | -----------
show_step_statuses (value: 'true') | Embed detailed test results including statuses per step with every tests

### Errors

If the test run has just been created and the tests generation is still in progress, this endpoint will return a **HTTP 423 Locked** error until the tests generation finishes.

## Get a test

```http
GET https://studio.cucumberstudio.com/api/projects/<project_id>/test_runs/<test_run_id>/test_snapshots/<test_snapshot_id> HTTP/1.1
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
curl "https://studio.cucumberstudio.com/api/projects/<project_id>/test_runs/<test_run_id>/test_snapshots/<test_snapshot_id>" \
    -H 'accept: application/vnd.api+json; version=1' \
    -H 'access-token: <your access token>' \
    -H 'uid: <your uid>' \
    -H 'client: <your client id>'
```

```json
{
  "data": {
    "type": "test-snapshots",
    "id": "1",
    "attributes": {
      "created-at" : "2017-02-28T11:39:08.281Z",
      "updated-at" : "2017-02-28T11:39:08.281Z",
      "last-author" : "harry@example.org",
      "name": "Find horcruxes",
      "definition-json": {
        "scenario-name": "Find horcruxes",
        "dataset_name": null,
        "dataset_id": null,
        "steps": [
          {
            "action": "Given Harry has one horcrux"
          },
          {
            "result": "Then he should destroy it"
          },
        ],
        "index": 0
      },
      "status": "failed",
      "scenario-snapshot-id": 1,
      "folder-snapshot-id": 5
    },
    "links": {
      "self": "/test-snapshots/1"
    },
    "relationships": {
      "scenario": {},
      "dataset": {},
      "last-result": {}
    }
  }
}
```

This endpoint retrieves a particular test of a test run

<aside class="warning"><b>Deprecations</b>
  <br>Test status attribute is deprecated. More information <a href="#test-status">here</a>.
</aside>

### URL Parameters

Parameter | Description
--------- | -----------
project_id | The ID of the project you want to retrieve the tests from
test_run_id | The ID of the test run that contains the test you want
test_snapshot_id | The ID of the test you want to get


## Get a test additional data

```http
GET https://studio.cucumberstudio.com/api/projects/<project_id>/test_runs/<test_run_id>/test_snapshots/<test_snapshot_id>?include=<fields> HTTP/1.1
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
curl "https://studio.cucumberstudio.com/api/projects/<project_id>/test_runs/<test_run_id>/test_snapshots/<test_snapshot_id>?include=<fields>" \
    -H 'accept: application/vnd.api+json; version=1' \
    -H 'access-token: <your access token>' \
    -H 'uid: <your uid>' \
    -H 'client: <your client id>'
```

You can use the JSONAPI [include syntax](http://jsonapi.org/format/#fetching-includes) to fetch additional data
about your tests.

> Following example returns a test with scenario, last result and the pass rate.

```http
GET https://studio.cucumberstudio.com/api/projects/<project_id>/test_runs/<test_run_id>/test_snapshots/<test_snapshot_id>?include=dataset,scenario&show_passrate HTTP/1.1
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
curl "https://studio.cucumberstudio.com/api/projects/<project_id>/test_runs/<test_run_id>/test_snapshots/<test_snapshot_id>?include=dataset,scenario&show_passrate" \
    -H 'accept: application/vnd.api+json; version=1' \
    -H 'access-token: <your access token>' \
    -H 'uid: <your uid>' \
    -H 'client: <your client id>'
```

```json
{
  "data": {
    "type": "test-snapshots",
    "id": "1",
    "attributes": {
      "created-at" : "2017-02-28T11:39:08.281Z",
      "updated-at" : "2017-02-28T11:39:08.281Z",
      "last-author" : "harry@example.org",
      "name": "Find horcruxes",
      "definition-json": {
        "scenario-name": "Find horcruxes",
        "dataset_name": null,
        "dataset_id": null,
        "steps": [
          {
            "action": "Given Harry has one horcrux"
          },
          {
            "result": "Then he should destroy it"
          },
        ],
        "index": 0
      },
      "status": "passed",
      "scenario-snapshot-id": 1,
      "folder-snapshot-id": 5,
      "pass-rate": "75"
    },
    "links": {
      "self": "/test-snapshots/1"
    },
    "relationships": {
      "scenario": {
        "data": {
          "type": "scenarios",
          "id": "10"
        }
      },
      "dataset": {},
      "last-result": {
        "links": {
          "self": "/test-snapshots/1/relationships/last-result",
          "related": "/test-snapshots/1/last-result"
        },
        "data": {
          "type": "test-results",
          "id": "7"
        }
      }
    }
  },
  "included": [
    {
      "type": "scenarios",
      "id": "10",
      "attributes": {
        "created-at": "2017-02-26T07:10:42.651Z",
        "updated-at": "2017-02-26T10:22:23.206Z",
        "last-author": "harry@example.org",
        "name": "Find horcruxes",
        "description": "That will help to kill Voldemort",
        "folder-id": 162629,
        "definition": "scenario 'Find horcruxes' do\n  call given 'Harry has one horcrux'\n  call then 'he should destroy it\nend\n"
      },
      "links": {
        "self": "/scenarios/10"
      },
      "relationships": {
        "folder": {}
      }
    },
    {
      "type": "test-results",
      "id": "7",
      "attributes": {
        "created-at": "2017-03-01T14:38:16.612Z",
        "updated-at": "2018-03-01T14:38:16.612Z",
        "last-author": "harry@example.org",
        "status": "passed",
        "description": null,
        "status-author": "Harry",
        "step-statuses": [
          "passed",
          "passed"
        ]
      },
      "links": {
        "self": "/test-results/7"
      },
      "relationships": {
        "test-snapshot": {},
        "build": {},
        "execution-environment": {}
      }
    }
  ]
}
```

<aside class="warning"><b>Deprecations</b>
  <br>Test status attribute is deprecated. More information <a href="#test-status">here</a>.
</aside>

The available additional data are the following:

Field name | Description
-----------| -----------
scenario | The original scenario that produced the test
dataset | The dataset that produced the test (if it comes from a scenario using a datatable)
last-result | The details of the last test result of the test

`show_passrate` parameter can be added to include test pass rate in the response.

### URL Parameters

Parameter | Description
--------- | -----------
project_id | The ID of the project you want to retrieve the tests from
test_run_id | The ID of the test run that contains the test you want
test_snapshot_id | The ID of the test you want to get

### Request parameters

Parameter | Description
----------|------------
include | The data to include in the test JSON response. Fields must be comma-separated
show_passrate | Add this parameter to get the test pass rate in the data

<aside class="notice">
The pass rate is only based on three types of results: passed, failed and blocked. The pass rate is computed on the last 10 results of the test.
Note: the pass rate is expressed as a percentage (25 meaning 25% for example). If there are no usable results to compute the data, an empty string will be returned.
</aside>

## Delete a test

```http
DELETE https://studio.cucumberstudio.com/api/projects/<project_id>/test_runs/<test_run_id>/test_snapshots/<test_snapshot_id> HTTP/1.1
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
curl -XDELETE "https://studio.cucumberstudio.com/api/projects/<project_id>/test_runs/<test_run_id>/test_snapshots/<test_snapshot_id>" \
    -H 'accept: application/vnd.api+json; version=1' \
    -H 'access-token: <your access token>' \
    -H 'uid: <your uid>' \
    -H 'client: <your client id>'
```

This endpoint delete a test.

### URL Parameters

Parameter | Description
--------- | -----------
project_id | The ID of the project you want to retrieve the tests from
test_run_id | The ID of the test run that contains the test you want
test_snapshot_id | The ID of the test you want to get

<aside class="warning">
Caution: your test snapshot will be totaly and permanently removed from your project.
</aside>
