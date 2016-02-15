.. _GET_listZones_v2__account_id__zones_zones:

List zones
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code::

    GET /v2/{account_id}/zones

This operation provides a list of detailed information for all zones.

A ``self`` link is included for each zone. These links point to each

This table shows the possible response codes for this operation:

+---------+-----------------------+---------------------------------------------+
| Response| Name                  | Description                                 |
| Code    |                       |                                             |
+=========+=======================+=============================================+
| 200     | Success               | Request succeeded.                          |
+---------+-----------------------+---------------------------------------------+
| 201     | Created               | The request has been fulfilled and resulted |
|         |                       | in a new resource being created.            |
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
| 403     | Forbidden             | The server has not found anything matching  |
|         |                       | the Request-URI.                            |
+---------+-----------------------+---------------------------------------------+
| 404     | Not Found             | The requested item was not found.           |
+---------+-----------------------+---------------------------------------------+
| 405     | Method Not Allowed    | The method specified in the Request-Line is |
|         |                       | not allowed for the resource identified by  |
|         |                       | the Request-URI.                            |
+---------+-----------------------+---------------------------------------------+
| 413     | Over Limit            | The number of items returned is above the   |
|         |                       | allowed limit.                              |
+---------+-----------------------+---------------------------------------------+
| 415     | Unsupported Media     | The server is refusing to service the       |
|         | Type                  | request because the entity of the request   |
|         |                       | is in a format not supported by the         |
|         |                       | requested resource for the requested        |
|         |                       | method.                                     |
+---------+-----------------------+---------------------------------------------+
| 503     | Service Unavailable   | The service is not available.               |
+---------+-----------------------+---------------------------------------------+

This table shows the URI parameters for the list zones request:

+-----------------------+---------+---------------------------------------------+
| Name                  | Type    | Description                                 |
+=======================+=========+=============================================+
| ``{account_id}``      | ​String | The account ID of the owner of the          |
|                       |         | specified account.                          |
+-----------------------+---------+---------------------------------------------+

 
**Example  List zones request**

.. code::  

    GET /v2/123456/zones HTTP/1.1
    Host: global.dns.rackspacecloud.com
    Accept: application/json
    Content-Type: application/json

This operation does not accept a request body.


**Example List zones response**

.. code::  

    HTTP/1.1 200 OK
    Vary: Accept
    Content-Type: application/json

    {
        "zones": [
            {
                "id": "a86dba58-0043-4cc6-a1bb-69d5e86f3ca3",
                "pool_id": "572ba08c-d929-4c70-8e42-03824bb24ca2",
                "project_id": "4335d1f0-f793-11e2-b778-0800200c9a66",
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
                "project_id": "4335d1f0-f793-11e2-b778-0800200c9a66",
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
