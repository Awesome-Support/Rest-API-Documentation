---
title: Glossary
---

New to REST APIs? Get up to speed with phrases used throughout our documentation.

## Controller

[Model-View-Controller][MVC] is a standard pattern in software development. If
you aren't already familiar it, you should do a bit of reading to get up
to speed.

Within the Awesome Support API, we've adopted the controller concept to have a standard pattern
for the classes representing our resource endpoints. All resource endpoints
extend `WP_REST_Controller` to ensure they implement common methods.

[MVC]: http://en.wikipedia.org/wiki/Model-view-controller

## HEAD, GET, POST, PUT, and DELETE Requests

These "HTTP verbs" represent the _type_ of action a HTTP client might perform
against a resource. For instance, `GET` requests are used to fetch a Tickets's
data, whereas `DELETE` requests are used to delete a Ticket. They're
collectively called "HTTP verbs" because they're standardized across the web.

## HTTP Client

The phrase "HTTP Client" refers to the tool you use to interact with the Awesome Support API.
You might use [Postman][] (Chrome) or [REST Easy][] (Firefox) to test requests
in your browser, or [httpie][] to test requests at the commandline.

[Postman]: https://chrome.google.com/webstore/detail/postman-rest-client/fdmmgilgnpjigdojojpjoooidkmcomcm?hl=en
[REST Easy]: https://github.com/nathan-osman/REST-Easy
[httpie]: https://github.com/jakubroztocil/httpie

## Resource

A "Resource" is a _discrete entity_ within WordPress. You may know these
resources already as Posts, Pages, Comments, Users, Terms, and so on. WP-API
permits HTTP clients to perform CRUD operations against resources (CRUD
stands for Create, Read, Update, and Delete).

Pragmatically, here's how you'd typically interact with WP-API resources:

* `GET /wp-json/wpas-api/v1/tickets` to get a collection of Tickets. 

* `GET /wp-json/wpas-api/v1/tickets/123` to get a single Ticket with ID 123.

* `POST /wp-json/wpas-api/v1/tickets` to create a new Ticket.

* `DELETE /wp-json/wpas-api/v1/tickets/123` to delete Ticket with ID 123.

## Routes / Endpoints

Endpoints are functions available through the API. This can be things like
retrieving the API index, updating a ticket, or deleting a reply. Endpoints
perform a specific function, taking some number of parameters and return data
to the client.

A route is the "name" you use to access endpoints, used in the URL. A route
can have multiple endpoints associated with it, and which is used depends on
the HTTP verb.

For example, with the URL `http://example.com/wp-json/wpas-api/v1/tickets/123`:

* The "route" is `wpas-api/v1/tickets/123` - The route doesn't include `wp-json`
  because `wp-json` is the base path for the API itself.

* This route has 3 endpoints:

  * `GET` triggers a `get_item` method, returning the ticket data to the client.
  * `PUT` triggers an `update_item` method, taking the data to update, and
    returning the updated ticket data.
  * `DELETE` triggers a `delete_item` method, returning the now-deleted ticket
    data to the client.

**Note:** On sites without pretty permalinks, the route is instead added to
the URL as the `rest_route` parameter. For the above example, the full URL
would then be `http://example.com/?rest_route=wpas-api/v1/tickets/123`

## Schema

A "schema" is a representation of the format for Awesome Support's API response data. For
instance, the Ticket schema communicates that a request to get a Ticket will
return `id`, `title`, `content`, `author`, and other fields. Our schemas also
indicate the type each field is, provide a human-readable description, and
show which contexts the field will be returned in.
