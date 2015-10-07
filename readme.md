# ps

A Node.js module for looking up running processes.

## Install

```bash
$ npm install ps-node
```

## Usage

Lookup process with spicified `pid`:

```javascript
var ps = require('ps-node');

// A simple pid lookup
ps.lookup({ pid: 12345 }, function(err, resultList ) {
    if (err) {
        throw new Error( err );
    }

    var process = resultList[ 0 ];

    if( process ){

        console.log( 'PID: %s, COMMAND: %s', process.pid, process.command );
    }
    else {
        console.log( 'No such process found!' );
    }
});

```

Or use RegExp to filter `command`:

```javascript
var ps = require('ps-node');

// A simple pid lookup
ps.lookup({
    command: 'node',
    }, function(err, resultList ) {
    if (err) {
        throw new Error( err );
    }

    resultList.forEach(function( process ){
        if( process ){

            console.log( 'PID: %s, COMMAND: %s', process.pid, process.command );
        }
    });
});

```

Also, you can use `kill` to kill process by `pid`:

```javascript
var ps = require('ps-node');

// A simple pid lookup
ps.kill( '12345', function( err ) {
    if (err) {
        throw new Error( err );
    }
    else {
        console.log( 'Process %s has been killed!', pid );
    }
});
```

You can also pass arguments to `lookup` with `psargs` as arguments for `ps` command（Note that `psargs` is not available in windows):

```javascript
var ps = require('ps-node');

// A simple pid lookup
ps.lookup({
    command: 'node',
    psargs: 'ux'
    }, function(err, resultList ) {
    if (err) {
        throw new Error( err );
    }

    resultList.forEach(function( process ){
        if( process ){
            console.log( 'PID: %s, COMMAND: %s', process.pid, process.command );
        }
    });
});

```

Lastly, you can filter a list of items by their PPID by passing a PPID to filter on. You will need to pass in a `psarg` that provides the PPID in the results (`-l` or `-j` for instance).

```javascript
var ps = require('ps-node');

// A simple pid lookup
ps.lookup({
    command: 'mongod',
    psargs: '-l',
    ppid: 82292
    }, function(err, resultList ) {
    if (err) {
        throw new Error( err );
    }

    resultList.forEach(function( process ){
        if( process ){
            console.log( 'PID: %s, COMMAND: %s', process.pid, process.command );
        }
    });
});

```
