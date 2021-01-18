# Client-Server Overview

## Web servers and HTTP(a primer)

web browsers communicate with web servers using **HyperText Transfer Protocol(HTTP)**. the browser sends HTTP Request to server.

this request includes:

* URL
* method
  - GET
  - POST
  - HEAD
  - PUT
  - DELETE
  - TRACE
  - OPTIONS
  - CONNECT
  - PATCH
* additional information can be encoded
  - URL Parameters
  - POST data encoded in request body
  - Client-side Cookies. contain session data about the client.

Web servers wait for client's request message, process them when they arrive, and reply with HTTP Response message.

the response contains:
- HTTP Response status code
- the response data

## Static Sites

one that returns the same hard coded content from the server whenever a particular resource is requested.

the same page will be returned to every user from the same url.

this is inefficient for when we need to use the same type of page with different context.

## Dynamic Sites

one that can generate and return content based on the specific request URL and data.

the data is stored in a database.