.. _cdns-dg-request-response:

Request and response types
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The |apiservice| supports the JSON data serialization formats. The request format is 
specified using the ``Content-Type`` header and is required for calls that have a request 
body. The response format can be specified in requests either by using the ``Accept`` 
header or by adding a ``.json`` extension to the request URI. If no response format is 
specified, JSON is the default. If conflicting formats are specified using both an ``Accept`` 
header and a query extension, the query extension takes precedence.

