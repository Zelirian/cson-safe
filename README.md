##### Atom and all repositories under Atom will be archived on December 15, 2022. Learn more in our [official announcement](https://github.blog/2022-06-08-sunsetting-atom/)
 # cson-safe

An alternative to [cson](https://github.com/bevry/cson).
Advantages of `cson-safe`:

* A strict subset of CSON that allows only data
* Interface is identical to JSON.{parse,stringify}
* Does not run the code, free of intermediate string representations
* Sane parse error messages with line/column

In addition of pure data it allows for simple arithmetic expressions like
addition and multiplication.
This allows more readable configuration of numbers,
the following is a valid strict CSON file:

```coffee
cachedData:
  refreshIntervalMs: 5 * 60 * 1000
```

## Install

`npm install --save cson-safe`

## Usage

```coffee
CSON = require 'cson-safe'
# This will print { a: '123' }
console.log CSON.parse "a: '123'"
```

## High-level APIs

`cson-safe` only offers basic parsing and serialization.
But there are some great tools if you want more than that:

* [`season`](https://www.npmjs.org/package/season),
  atom.io's CSON package.
  Includes CLI tool to convert CSON to JSON
* [`grunt-cson`](https://www.npmjs.org/package/grunt-cson),
  converts CSON to JSON as a grunt task
* [`load-grunt-configs`](https://www.npmjs.org/package/load-grunt-configs),
  loads grunt config from CSON files (among other formats)
* [`fetcher`](https://www.npmjs.org/package/fetcher),
  a declarative way to download (frontend) libraries, supports CSON configs
* [`csonschema`](https://www.npmjs.org/package/csonschema),
  parses [JSON Schema](http://json-schema.org) files written in CSON

You can find more on the
[npm website](https://preview.npmjs.com/browse/depended/cson-safe).

## FAQ

### Why not just use YAML?

YAML allows for some pretty complex constructs like anchor and alias,
which can behave in unexpected ways, especially with nested objects.
CSON is simpler while still offering most of the niceties of YAML.

### Why not just use JSON?

JSON doesn't offer multi-line strings and is generally a little noisier.
Also sometimes it can be nice to have comments in config files.

### Why not just use CoffeeScript directly?

You don't want data files being able to run arbitrary code.
Even when ran in a proper sandbox, `while(true)` is still possible.
