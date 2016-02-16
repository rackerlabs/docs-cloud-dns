.. _cdns-paginated-collections:

Pagination and Sorting
~~~~~~~~~~~~~~~~~~~~~~

Collection responses will include a ``links`` object containing absolute URLs for the next 
and previous pages. These links may be omitted, or null, at the edges of a paginated 
collection.

Pagination and sorting is available on all collections and is controlled using a combination 
of four query parameters:

- **marker**: ID of the last item in the previous list
- **limit**: sets the page size.
- **sort_key**: attribute used for sorting
- **sort_dir**: direction (``asc`` for ascending and ``desc`` for descending)

For example: ``marker=<UUID>&limit=<INTEGER>&sort_key=<STRING>&sort_dir<STRING>``. 

To navigate the collection, the parameters ``limit`` and ``marker`` can be set in the URI 
(for example: ``?limit=100&marker=<UUID>``). Both parameters are optional.

Items are sorted by create time in descending order. When a create time is not available, 
they are sorted by ID. To sort results, set the ``sort_key`` query parameter to a valid 
attribute (e.g. ``name``or ``email``). To sort in descending order, specify add the 
``sort_dir=desc`` query parameter.

**Example Request for a paginated collection of zones**

.. code::  

    GET /v2/zones?marker=c74af170-0673-11e3-8ffd-0800200c9a66&limit=2 HTTP/1.1
     Host: global.dns.api.rackspacecloud.com
     Accept: application/json
     X-Auth-Token: ************  

 
**Example Response for a paginated collection of zones**

.. code::  

    HTTP/1.1 200 OK
    Content-Type: application/json

    {
      "zones": [{
        "status": "ACTIVE",
        "description": null,
        "updated_at": null,
        "ttl": 3600,
        "serial": 1405435156,
        "id": "c316def0-8599-4030-9dcd-2ce566348115",
        "name": "abc.example.net.",
        "created_at": "2014-07-15T14:39:16.000000",
        "pool_id": "572ba08c-d929-4c70-8e42-03824bb24ca2",
        "version": 1,
        "project_id": "123456",
        "email": "hostmaster@example.net",
        "links": {
          "self": "https://global.dns.api.rackspacecloud.com/v2/123456/zones/c316def0-8599-4030-9dcd-2ce566348115"
        }
      },
      {
        "status": "ACTIVE",
        "description": null,
        "updated_at": "2014-07-08T20:28:31.000000",
        "ttl": 86400,
        "serial": 1404851315,
        "id": "a4e29ed3-d7a4-4e4d-945d-ce64678d3b94",
        "name": "example.com.",
        "created_at": "2014-07-08T20:28:19.000000",
        "pool_id": "572ba08c-d929-4c70-8e42-03824bb24ca2",
        "version": 1,
        "project_id": "123456",
        "email": "hostmaster@example.com",
        "links": {
          "self": "https://global.dns.api.rackspacecloud.com/v2/123456/zones/a4e29ed3-d7a4-4e4d-945d-ce64678d3b94"
        }
      }
      }],
      "links": {
        "self": "https://global.dns.api.rackspacecloud.com/v2/123456/zones?sort_key=id&sort_dir=desc"
      }
    }
