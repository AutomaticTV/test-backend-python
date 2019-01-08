# Backend Software Engineer (Python) Test

## Task
SCHEDULER API:

Python web-service that provides a Restful API to manage the tasks of a scheduler. Tasks can carry application data within its payload. The API should provide CRUD for the scheduler tasks.

## Data model
The 'task' is a scheduled job that is executed by a concrete worker. You can change the field's names if you want.

```
task: {id, start, title, worker, status, payload}
```

* **start** (required) is of type datetime with seconds resolutions at least
* **title** (optional) is of type string
* **worke**r (required) is of type string and is the name of the worker which runs the task
* **status** (required) is of type string and the allowed values are: "SCHEDULED" or "RUNNING" or "SUCCEEDED" or "FAILED"
* **payload** (optional) is of type dictionary and stores application layer data

## API REST
* GET /api/tasks
    * retrieves all tasks
    * optional query filters:
        * worker
        * status
        * from: tasks which begin after 'from'
        * to: tasks which start before 'to'
* POST /api/tasks
    * creates a new task, 'start' must be a future datetime.
* GET /api/tasks/<id>
    * retrieves a certain task
* PATCH /api/tasks/<id>
    * modifies a certain task
* DELETE /api/tasks/<id>
    * delete a certain task in case that is not running
* PATCH /api/tasks/<id>/payload
    * adds or replace payload first level dictionary key, and returns the modified task
    * For example:

### Examples

#### Update a task payload
``` javascript
// before
{"id":"eea97a6", start:"20160718T01", "status": "SCHEDULED", "payload": {"key1": "value1", "key2" = [1,2,3]}}
```
*`PATCH /api/task/eea97a6/payload {"key3":{"key3_1":"value3_1"}}`*

``` javascript
// after
{"id":"eea97a6", start:"20160718T01", "status": "SCHEDULED", "payload": {"key1": "value1", "key2" = [1,2,3], "key3":{"key3_1":"value3_1"}}}
```
#### Delete a key in the task

``` javascript
// before
{"id":"eea97a6", start:"20160718T01", "status": "SCHEDULED", "payload": {"key1": "value1", "key2" = [1,2,3]}}
```
*`DELETE /api/task/eea97a6/payload/key1`*

``` javascript
// after
{"id":"eea97a6", start:"20160718T01", "status": "SCHEDULED", "payload": {"key2" = [1,2,3]}}
```

## Aspects to evaluate

### Language and libraries
* Python
* any available package on PyPi

### Deliverables
* source code
* requirements.txt `pip freeze` with all the used python PyPi packages
* deploy instructions

### What we value
* Coding structure and habits
* Solvency given a problem

### What we don't assess
* Concurrency control
* High availability
* Which version of Python is used
* Which database is chosen, if any
* What packages are chosen, if any

### Recommendations:
* using unit test
* using documentation
* using PEP8 coding style
* using logger output
