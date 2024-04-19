# postgraphile-plugin-apollo-federation

[![GitHub Workflow Status (with branch)](https://img.shields.io/github/actions/workflow/status/brooklyn-labs/postgraphile-plugin-apollo-federation/ci.yml?branch=main&label=Build)](https://github.com/brooklyn-labs/postgraphile-plugin-apollo-federation/actions/workflows/ci.yml)
[![npm (scoped)](https://img.shields.io/npm/v/@brooklyn-labs/postgraphile-plugin-apollo-federation?label=NPM)](https://www.npmjs.com/package/@brooklyn-labs/postgraphile-plugin-apollo-federation)
[![License](https://img.shields.io/github/license/brooklyn-labs/postgraphile-plugin-apollo-federation?label=License)](https://github.com/brooklyn-labs/postgraphile-plugin-apollo-federation/blob/main/LICENSE.md)

Apollo federation support for PostGraphile (or any Graphile Engine schema).

## Installation

```shell
npm install postgraphile-plugin-apollo-federation
```

## CLI usage

```shell
postgraphile --append-plugins postgraphile-plugin-apollo-federation
```

## Library usage

```js
const express = require("express");
const { postgraphile } = require("postgraphile");
const { default: postgraphile-plugin-apollo-federation } = require("postgraphile-plugin-apollo-federation");

const app = express();

app.use(
  postgraphile(process.env.DATABASE_URL, "public", {
    appendPlugins: [postgraphile-plugin-apollo-federation],
  })
);

app.listen(process.env.PORT || 3000);
```

## How?

This plugin exposes the [Global Object Identification
Specification](https://facebook.github.io/relay/graphql/objectidentification.htm)
(i.e. `Node` interface) in a way that's compatible with Apollo Federation.

Requires PostGraphile v4.14.0+

## Testing

Docker can be used to spin up a test instance for running Jest tests. The instance will be exposed at port `5432`. See `.env.example` for the exported Postgre connection.

```sh
docker compose up -d
./scripts/test
```

## Do you need this?

Only use this if you're planning to have your API consumed by Apollo
Federation; exposing these redundant interfaces to regular users may be
confusing.

## Status

Proof of concept. No tests, use at your own risk! Pull requests very welcome.
