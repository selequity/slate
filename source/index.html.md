---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - ruby
  - json

toc_footers:
  - <a href='#'>Example Link</a>
  - <a href='https://github.com/tripit/slate'>Documentation Powered by Slate</a>

search: true
---
# Context

Currently, we're at version 1 of the Selequity API. The Rails side, and the
Angular side, are deeply coupled. At some point, we'll likely want to
start moving pieces off the Angular app. And we'll certainly want to
expand our api to be consumed by other services. There's no consistent JSON schema
being served up, and large improvements to be made in logging, error
handling, and performance.

Thus, alongside other refactoring efforts, we're going to slowly
convert, piece by piece, resource by resource, the current codebase from
version 1 to our latest understanding of the domain and use cases in
version 2.

# Targets

* Build out a style guide & useful documentation here
* Make responses as flat/normalized as possible
* Where possible, copy [Stripe's](https://stripe.com/docs/api) api

# Starting Points

## Basic Request Structure

Every request will include information about the url, and the api
version.

We're thinking about maintaining major version in the url, and if
needed, smaller sub-versions in http headers.

```json
{
  apiVersion: 2.0,
  url: '/api/v2/investments'
}
```

## Error Format

```json
{
  type: 'api_error',
  message: 'human-friendly message about what went wrong',
  code: 500,
  param: {
    relevant: 'id'
  }
}
```

## Guidelines

More advanced queries on a specific resource will use query parameters.

Ex: `/api/v2/investments?status=active`

Each endpoint will, by default, give back the minimal info needed. To
request additional info, include fields:

`/api/v2/investments?fields=all`

If there's a commonly requested configuration of query parameters on a
resource, chances are we'll have a restful alias.

`/api/v2/deals/recently_funded`

If you want the response to include other associated records, use the
include parameter:

`/api/v2/investments?include=deal`
