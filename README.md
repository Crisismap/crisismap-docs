# Crisismap docs

Collection of generic docs and relevant resources: standards, examples, data sources etc.

## Generic scheme

![scheme](https://docs.google.com/drawings/d/e/2PACX-1vQaobkIUFS506kMYK2X1kW1p6wrhgPbqe5FN6H7Zit0srTPWEk8XvDh_Zwihdkz4dgxNnfsNMHFFhcx/pub?w=960&h=720)

## Glossary

(since nearly everything in here deals with data, the word **data** is intentionally omitted in definitions)

### Source

Any sort of raw data suppliers: platforms, services, publicly available APIs/DBs, aggregators over IoT sensors etc.

### Provider

Essentially, a worker (COULD be daemonized script, crawler, tiny ETL pipeline etc.) aimed to access a single **source**,
or even multiple **sources** (merging related data segments), retrieve (load, parse) raw data,
process (filter, clean, normalize) and store it accordingly.

For now, storing SHOULD happen explicitly via `INPUT` queries, accessing **back-end** potential POST API surface is left
for future considerations.

**Providers** COULD be derived from a **generic provider** (implementation details), exposing a set of templates to descendants.

Also, **providers** are about to be monitored and scheduled by an **orchestrator** - primarily a set of config declarations.

### Back-end

Ideally, "almost" a logic-less proxying service acting in the middle of DB and **clients**.

If some comprehensive business logic appears, it COULD potentially be associated with this service OR
derived into a dedicated module.

Main responsibilities:
* internally: storage accessor and data mapper, leveraged by models (representing multiple **categories**)
* externally: RESTful API wrapper (serving controllers and middlewares), together with a live update service (sockets) for **clients**

API itself acts "as a client", meaning serving JSON instead of explicit UI capabilities.

#### Categories

Existing and upcoming models/collections:
* news
  * news types
* incidents
  * incident types
* locations
* toponyms
* population
* reports

### Clients

#### Front-end

Aimed for data representation and UX/UI (map/clustering + filtering/pagination).

#### External subscribers

Any app/service/crawler authorized to access aggregated data streams.

REST and RSS services are considered as first options.
