.. _GET_listRecordsets_v2__account_id__zones__zone_id__recordsets_recordsets:

List all record sets for a zone
-------------------------------

.. code::

    GET /v2/{TENANT_ID}/zones/{zoneId}/recordsets

This operation provides detailed information for all record sets for the
specified zone.

This table shows the possible response codes for this operation:

+---------+---------------------+---------------------------------------------+
| Response| Name                | Description                                 |
| code    |                     |                                             |
+=========+=====================+=============================================+
| 200     | Success             | The request succeeded.                      |
+---------+---------------------+---------------------------------------------+
| 400     | Bad Request         | The request is missing one or more          |
|         |                     | elements, or the values of some elements    |
|         |                     | are invalid.                                |
+---------+---------------------+---------------------------------------------+
| 401     | Unauthorized        | You are not authorized to complete this     |
|         |                     | operation. This error can occur if the      |
|         |                     | request is submitted with an invalid        |
|         |                     | authentication token.                       |
+---------+---------------------+---------------------------------------------+
| 403     | Forbidden           | The server did not find anything matching   |
|         |                     | the request URI.                            |
+---------+---------------------+---------------------------------------------+
| 404     | Not Found           | The requested item was not found.           |
+---------+---------------------+---------------------------------------------+
| 405     | Method Not Allowed  | The method specified in the request is      |
|         |                     | not allowed for the resource identified by  |
|         |                     | the request URI.                            |
+---------+---------------------+---------------------------------------------+
| 413     | Over Limit          | The request exceeds the rate limit or quota.|
+---------+---------------------+---------------------------------------------+
| 415     | Unsupported Media   | The server won't service the                |
|         | Type                | request because the entity of the request   |
|         |                     | is in a format not supported by the         |
|         |                     | requested resource for the requested        |
|         |                     | method.                                     |
+---------+---------------------+---------------------------------------------+
| 503     | Service Unavailable | The service is not available.               |
+---------+---------------------+---------------------------------------------+

Request
^^^^^^^

This table shows the URI parameters for the request:

+-----------------------+---------+-------------------------------------------+
| Name                  | Type    | Description                               |
+=======================+=========+===========================================+
| ``{TENANT_ID}``       | ​String | The account ID of the account owner.      |
+-----------------------+---------+-------------------------------------------+
| ``{zoneId}``          | ​UUID   | The ID of zone for which you want to list |
|                       |         | all the record sets.                      |
+-----------------------+---------+-------------------------------------------+


**Example: List all record sets, request**

.. code::

    GET /v2/123456/zones/2150b1bf-dee2-4221-9d85-11f7886fb15f/recordsets HTTP/1.1
    Host: global.dns.rackspacecloud.com
    Accept: application/json
    Content-Type: application/json

This operation does not accept a request body.

Response
^^^^^^^^

This table shows the body parameters for the response:

+--------------------------------+---------------------+----------------------+
|Name                            |Type                 |Description           |
+================================+=====================+======================+
|**recordsets**                  |Array                |An array of           |
|                                |                     |recordsets.           |
+--------------------------------+---------------------+----------------------+
|recordsets.\ **id**             |Uuid                 |The ID of the         |
|                                |                     |record.               |
+--------------------------------+---------------------+----------------------+
|recordsets.\ **zone_id**        |Uuid                 |The ID of the zone.   |
+--------------------------------+---------------------+----------------------+
|recordsets.\ **name**           |String               |The name of the       |
|                                |                     |record.               |
+--------------------------------+---------------------+----------------------+
|recordsets.\ **ttl**            |Integer              |The time to live for  |
|                                |                     |the record.           |
+--------------------------------+---------------------+----------------------+
|recordsets.\ **description**    |String               |The description       |
|                                |                     |of the record.        |
+--------------------------------+---------------------+----------------------+
|recordsets.\ **records**        |Array                |An array of record    |
|                                |                     |IP addresses.         |
+--------------------------------+---------------------+----------------------+
|recordsets.\ **type**           |String               |The record type.      |
+--------------------------------+---------------------+----------------------+
|recordsets.\ **version**        |Integer              |The version of the    |
|                                |                     |record.               |
+--------------------------------+---------------------+----------------------+
|recordsets.\ **created_at**     |Datestamp            |The time stamp        |
|                                |                     |indicating the        |
|                                |                     |creation date of the  |
|                                |                     |record.               |
+--------------------------------+---------------------+----------------------+
|recordsets.\ **updated_at**     |Datestamp            |The time stamp        |
|                                |                     |indicating the date   |
|                                |                     |that the record was   |
|                                |                     |last updated.         |
+--------------------------------+---------------------+----------------------+
|recordsets.\ **links**          |Object               |A container with the  |
|                                |                     |links to the record.  |
+--------------------------------+---------------------+----------------------+
|recordsets.links.\ **self**     |Uuid                 |The link to the       |
|                                |                     |record.               |
+--------------------------------+---------------------+----------------------+
|**links**                       |Object               |A container with the  |
|                                |                     |links to the          |
|                                |                     |recordsets.           |
+--------------------------------+---------------------+----------------------+
|links.\ **self**                |Uuid                 |The link to the       |
|                                |                     |recordsets.           |
+--------------------------------+---------------------+----------------------+
|**metadata**                    |Object               |Any metadata key and  |
|                                |                     |value pairs.          |
+--------------------------------+---------------------+----------------------+
|metadata.\ **total_count**      |Integer              |The number of records |
|                                |                     |in the array.         |
+--------------------------------+---------------------+----------------------+

**Example: List all record sets, response**

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
