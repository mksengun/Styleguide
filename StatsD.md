

# Metrics styleguide

## Incoming API requests

Statistics for requests handled by the service.

Type: `statsd timing`

Stat name: `incoming_request`

Creates: count, 95p, max, min, avg

Tags:

- `service` // Name of the service sending the statistic
- `method`
- `path` // Path should not include ID's of resources. In Hapi use `request.route.path`
- `statuscode`

## Outgoing requests

Statistics for requests going from the service to another service

Type: `statsd timing`

Stat name: `outgoing_request`

Creates: count, 95p, max, min, avg

Tags:

- `service` // Name of the service sending the statistic
- `external_service` // Name of external service 
- `method`
- `url`
- `statuscode`
- `result`
  result of the request, (badrequest, failed, internal, success)
  The result is based on statuscode. If no response is received (timeout or socket hangup) result should be failed.

## Queries

statsd timing for queries, (MongoDB, Couchbase, or other databases)

type: `statsd timing`

Stat name: `query`

Creates: count, 95p, max, min, avg

Tags:

- `service` // Name of the service sending the statistic
- `database_type`
- `database_name` // Is this necessary?
- `query_type`
  eq: find, create, select, getall, update, findAll. Different query names per different database
- `result` // succes, failed