.. _GET_listZones_v2__account_id__zones_zones:

List zones
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code::

    GET /v2/{TENANT_ID}/zones

This operation provides a list of detailed information for all zones.

A ``self`` link is included for each zone.

The following table shows the possible response codes for this operation.

+---------+-----------------------+---------------------------------------------+
| Response| Name                  | Description                                 |
| code    |                       |                                             |
+=========+=======================+=============================================+
| 200     | Success               | The request succeeded.                      |
+---------+-----------------------+---------------------------------------------+
| 400     | Bad Request           | The request is missing one or more          |
|         |                       | elements, or the values of some elements    |
|         |                       | are invalid.                                |
+---------+-----------------------+---------------------------------------------+
| 401     | Unauthorized          | You are not authorized to complete this     |
|         |                       | operation. This error can occur if the      |
|         |                       | request is submitted with an invalid        |
|         |                       | authentication token.                       |
+---------+-----------------------+---------------------------------------------+
| 403     | Forbidden             | The server did not find anything matching   |
|         |                       | the request URI.                            |
+---------+-----------------------+---------------------------------------------+
| 404     | Not Found             | The requested item was not found.           |
+---------+-----------------------+---------------------------------------------+
| 405     | Method Not Allowed    | The method specified in the request is      |
|         |                       | not allowed for the resource identified by  |
|         |                       | the request URI.                            |
+---------+-----------------------+---------------------------------------------+
| 413     | Over Limit            | The request exceeds the rate limit or quota.|
+---------+-----------------------+---------------------------------------------+
| 415     | Unsupported Media     | The server won't service the                |
|         | Type                  | request because the entity of the request   |
|         |                       | is in a format not supported by the         |
|         |                       | requested resource for the requested        |
|         |                       | method.                                     |
+---------+-----------------------+---------------------------------------------+
| 503     | Service Unavailable   | The service is not available.               |
+---------+-----------------------+---------------------------------------------+

The following table shows the URI parameters for the request.

+-----------------------+---------+---------------------------------------------+
| Name                  | Type    | Description                                 |
+=======================+=========+=============================================+
| ``{TENANT_ID}``       | ​String | The account ID of the account owner.        |
+-----------------------+---------+---------------------------------------------+

 
**Example:  List zones, request**

.. code::  

    GET /v2/123456/zones HTTP/1.1
    Host: global.dns.rackspacecloud.com
    Accept: application/json
    Content-Type: application/json

This operation does not accept a request body.


**Example: List zones, response**

.. code::  

    HTTP/1.1 200 OK
    Vary: Accept
    Content-Type: application/json

    {
        "zones": [
            {
                "id": "a86dba58-0043-4cc6-a1bb-69d5e86f3ca3",
                "pool_id": "572ba08c-d929-4c70-8e42-03824bb24ca2",
                "project_id": "123456",
                "name": "example.org.",
                "email": "joe@example.org.",
                "ttl": 7200,
                "serial": 1404757531,
                "status": "ACTIVE",
                "description": "This is an example zone.",
                "masters": [],
                "type": "PRIMARY",
                "transferred_at": null,
                "version": 1,
                "created_at": "2014-07-07T18:25:31.275934",
                "updated_at": null,
                "links": {
                    "self": "https://global.dns.api.rackspacecloud.com/v2/123456/zones/a86dba58-0043-4cc6-a1bb-69d5e86f3ca3"
                }
            },
            {
                "id": "fdd7b0dc-52a3-491e-829f-41d18e1d3ada",
                "pool_id": "572ba08c-d929-4c70-8e42-03824bb24ca2",
                "project_id": "123456",
                "name": "example.net.",
                "email": "joe@example.net.",
                "ttl": 7200,
                "serial": 1404756682,
                "status": "ACTIVE",
                "description": "This is another example zone.",
                "masters": [],
                "type": "PRIMARY",
                "transferred_at": null,
                "version": 1,
                "created_at": "2014-07-07T18:22:08.287743",
                "updated_at": null,
                "links": {
                    "self": "https://global.dns.api.rackspacecloud.com/v2/123456/zones/fdd7b0dc-52a3-491e-829f-41d18e1d3ada"
                }
            }
        ],
        "links": {
            "self": "https://global.dns.api.rackspacecloud.com/v2/123456/zones"
        },
        "metadata": {
            "total_count": 2
        }
    }
