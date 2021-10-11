# SiriDB ThingsDB Module (Go)

SiriDB module written using the [Go language](https://golang.org).


## Installation

Install the module by running the following command in the `@thingsdb` scope:

```javascript
new_module('siridb', 'github.com/thingsdb/module-go-siridb');
```

Optionally, you can choose a specific version by adding a `@` followed with the release tag. For example: `@v0.1.0`.

## Configuration

The SiriDB module requires a thing a configuration with the following properties:

Property | Type            | Description
-------- | --------------- | -----------
username | str (required)  | Database user to authenticate with.
password | str (required)  | Password for the database user.
database | str (required)  | Database to connect to.
servers  | list (required) | List with tuples containing the host and client port. e.g. `[["siridb.local", 9000]]`.

> Note: if you have multiple SiriDB databases, then install one SiriDB module for each database.

Example configuration:

```javascript
set_module_conf('siridb', {
    username: 'iris',
    password: 'siri',
    database: 'dbtest',
    servers: [
        ["localhost", 9000]
    ]
});
```

## Exposed functions

Name              | Description
----------------- | -----------
[query](#query)   | Run a SiriDB query.
[insert](#insert) | Insert data into SiriDB.

### query

Syntax: `query(query_string)`

#### Arguments

- `query_string`: The query string to run.

#### Example:

```javascript
siridb.query("select * from 'my-series-001'").then(|res| {
    res;  // just return the response.
});
```


### insert

Syntax: `insert(data)`

#### Arguments

- `data`: Thing with data points to insert.

#### Example:

```javascript
data = {
    mySeries001: [
        [int(now()), 3.14]
    ]
};
siridb.insert(data);
```
