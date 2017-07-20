---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - json

toc_footers:
  - <a href='#'>Example Link</a>
  - <a href='https://github.com/tripit/slate'>Documentation Powered by Slate</a>

includes:
  - authentication
  - errors
  - investments

search: true
---

# Introduction
Currently, we're at version 1 of the Selequity API. Soon, we will likely
need to integrate with external services, as well as creating greater
internal consistency. There are several tasks between here and there:

  * defining a consistent json schema
  * documentation around the api
  * building out the endpoints

Thus, alongside other refactoring efforts, we're going to slowly
convert, piece by piece, resource by resource, the current codebase from
version 1 to our latest understanding of the domain and use cases in
version 2.

This API follows the [json api](http://jsonapi.org/) specification.
