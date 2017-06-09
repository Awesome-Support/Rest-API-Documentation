---
page: introduction
title: API Reference
layout: reference-static
---

Welcome to the API reference for the Awesome Support REST API! It's great to have you here.

The API is organized around [REST][]. Our API is designed to have predictable, resource-oriented URLs and to use HTTP response codes to indicate API errors. We use built-in HTTP features, like HTTP authentication and HTTP verbs, which can be understood by off-the-shelf HTTP clients, and we support cross-origin resource sharing to allow you to interact securely with the API from a client-side web application.

The API uses JSON exclusively as the request and response format, including error responses. It also uses the [HAL standard][] for linking, and is fully discoverable via hyperlinks in the responses.

The API provides public data accessable to any client anonymously, as well as private data only available after [authentication](/guide/authentication/). Most content management actions can be performed over the REST API, allowing you to build alternative dashboards for a site, enhance your plugins with more responsive management tools, as well as building single-page applications for a site.

This API reference provides information on what's available through the API, however common usage patterns and guides are available as part of the [general documentation](/).

[HAL standard]: http://stateless.co/hal_specification.html
[REST]: http://en.wikipedia.org/wiki/Representational_state_transfer

