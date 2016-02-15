.. _GET_listRecordsets_v2__account_id__zones__zone_id__recordsets_recordsets:

List all recordsets for a specified zone
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code::

    GET /v2/{account_id}/zones/{zone_id}/recordsets
 
This operation provides detailed information for all record sets for the
specified zone id.

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

This table shows the URI parameters for the list all record sets for a specified zone request:

+-----------------------+---------+---------------------------------------------+
| Name                  | Type    | Description                                 |
+=======================+=========+=============================================+
| ``{account_id}``      | ​String | The account ID of the owner of the          |
|                       |         | specified account.                          |
+-----------------------+---------+---------------------------------------------+
| ``{zone_id}``         | ​String | The zone ID for the specified zone.         |
+-----------------------+---------+---------------------------------------------+

 
**Example List all record sets request**

.. code::  

    GET /v2/123456/zones/2150b1bf-dee2-4221-9d85-11f7886fb15f/recordsets HTTP/1.1
    Host: global.dns.rackspacecloud.com
    Accept: application/json
    Content-Type: application/json

This operation does not accept a request body.


 
**Example List all record sets response**

.. code::  

    HTTP/1.1 200 OK
    Vary: Accept
    Content-Type: application/json

    {
        "recordsets": [
            {
                "description": null,
                "links": {
                    "self": "https://global.dns.api.rackspacecloud.com/v2/123456/zones/2150b1bf-dee2-4221-9d85-11f7886fb15f/recordsets/65ee6b49-bb4c-4e52-9799-31330c94161f"
                },
                "updated_at": null,
                "records": [
                    "ns2.example.com."
                ],
                "ttl": null,
                "id": "65ee6b49-bb4c-4e52-9799-31330c94161f",
                "name": "example.org.",
                "zone_id": "2150b1bf-dee2-4221-9d85-11f7886fb15f",
                "created_at": "2014-10-24T19:59:11.000000",
                "version": 1,
                "type": "NS"
            },
            {
                "description": null,
                "links": {
                    "self": "https://global.dns.api.rackspacecloud.com/v2/123456/zones/2150b1bf-dee2-4221-9d85-11f7886fb15f/recordsets/14500cf9-bdff-48f6-b06b-5fc7491ffd9e"
                },
                "updated_at": "2014-10-24T19:59:46.000000",
                "records": [
                    "ns2.example.com. joe.example.org. 1414180785 3600 600 86400 3600"
                ],
                "ttl": null,
                "id": "14500cf9-bdff-48f6-b06b-5fc7491ffd9e",
                "name": "example.org.",
                "zone_id": "2150b1bf-dee2-4221-9d85-11f7886fb15f",
                "created_at": "2014-10-24T19:59:12.000000",
                "version": 1,
                "type": "SOA"
            },
            {
                "description": "This is an example recordset.",
                "links": {
                    "self": "https://global.dns.api.rackspacecloud.com/v2/123456/zones/2150b1bf-dee2-4221-9d85-11f7886fb15f/recordsets/f7b10e9b-0cae-4a91-b162-562bc6096648"
                },
                "updated_at": null,
                "records": [
                    "10.1.0.2"
                ],
                "ttl": 3600,
                "id": "f7b10e9b-0cae-4a91-b162-562bc6096648",
                "name": "example.org.",
                "zone_id": "2150b1bf-dee2-4221-9d85-11f7886fb15f",
                "created_at": "2014-10-24T19:59:44.000000",
                "version": 1,
                "type": "A"
            }
        ],
        "links": {
            "self": "https://global.dns.api.rackspacecloud.com/v2/123456/zones/2150b1bf-dee2-4221-9d85-11f7886fb15f/recordsets"
        },
        "metadata": {
            "total_count": 3
        }
    }
