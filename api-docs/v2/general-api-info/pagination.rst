.. _cdns-paginated-collections:

Pagination
~~~~~~~~~~~~~~

Pagination is available on all collections and is controlled using a combination of two 
query parameters: ``marker=<UUID>&limit=<INTEGER>``. Collection responses will include a 
``links`` object containing absolute URLs for the next and previous pages. These links may 
be omitted, or null, at the edges of a paginated collection.

To navigate the collection, the parameters ``limit`` and ``marker`` can be set in the URI 
(for example: ``?limit=100&marker=<UUID>``). The ``marker`` parameter is the ID of the last 
item in the previous list. Items are sorted by create time in descending order. When a 
create time is not available, they are sorted by ID. The ``limit`` parameter sets the page 
size. Both parameters are optional.


**Example Request for a paginated collection**

.. code::  

    GET /v2/examples?marker=c74af170-0673-11e3-8ffd-0800200c9a66&limit=2 HTTP/1.1
     Host: dns.provider.com
     Accept: application/json
     X-Auth-Token: ************  

 
**Example Response for a paginated collection**

.. code::  

    HTTP/1.1 200 OK
     Vary: Accept
     Content-Type: application/json  

.. code::  

     {
       "examples": [{
         "id": "a86dba58-0043-4cc6-a1bb-69d5e86f3ca3",
         "....": "...."
       }, {
         "id": "fdd7b0dc-52a3-491e-829f-41d18e1d3ada",
         "....": "...."
       }],
       "links": {
         "self": "https://dns.provider.com/v2/examples?marker=e728bfe0-0673-11e3-8ffd-0800200c9a66&limit=2",
         "next": "https://dns.provider.com/v2/examples?marker=fdd7b0dc-52a3-491e-829f-41d18e1d3ada&limit=2",
         "previous": "https://dns.provider.com/v2/examples?marker=d9890c50-0673-11e3-8ffd-0800200c9a66&limit=2" 
       }
     }  