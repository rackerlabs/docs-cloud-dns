.. _req-resp-types:

==========================
Request and response types
==========================

The |apiservice| supports the JSON data serialization formats. The request
format is specified by using the ``Content-Type`` header and is required for
operations that have a request body. The response format can be specified in
requests by using the ``Accept`` header. If no response format is specified,
JSON is the default.

