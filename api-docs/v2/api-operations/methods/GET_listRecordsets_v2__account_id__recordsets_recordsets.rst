.. _GET_listRecordsets_v2__account_id__recordsets_recordsets:

List all record sets
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code::

    GET /v2/{TENANT_ID}/recordsets

This operation provides detailed information for all record sets for the
specified zone.

This table shows the possible response codes for this operation:

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

Request
""""""""""""""""

This table shows the URI parameters for the request:

+-----------------------+---------+---------------------------------------------+
| Name                  | Type    | Description                                 |
+=======================+=========+=============================================+
| ``{TENANT_ID}``       | ​String | The account ID of the account owner.        |
+-----------------------+---------+---------------------------------------------+


**Example: List all record sets, request**

.. code::

    GET /v2/123456/recordsets HTTP/1.1
    Host: global.dns.rackspacecloud.com
    Accept: application/json
    Content-Type: application/json

This operation does not accept a request body.

Response
""""""""""""""""

This table shows the body parameters for the response:

+--------------------------------+----------------------+----------------------+
|Name                            |Type                  |Description           |
+================================+======================+======================+
|**recordsets**                  |Array                 |An array of           |
|                                |                      |recordsets.           |
+--------------------------------+----------------------+----------------------+
|recordsets.\ **id**             |Uuid                  |The ID of the         |
|                                |                      |record.               |
+--------------------------------+----------------------+----------------------+
|recordsets.\ **zone_id**        |Uuid                  |The ID of the zone.   |
+--------------------------------+----------------------+----------------------+
|recordsets.\ **name**           |String                |The name of the       |
|                                |                      |record.               |
+--------------------------------+----------------------+----------------------+
|recordsets.\ **ttl**            |Integer               |The time to live for  |
|                                |                      |the record.           |
+--------------------------------+----------------------+----------------------+
|recordsets.\ **description**    |String                |The description       |
|                                |                      |of the record.        |
+--------------------------------+----------------------+----------------------+
|recordsets.\ **records**        |Array                 |An array of record    |
|                                |                      |IP addresses.         |
+--------------------------------+----------------------+----------------------+
|recordsets.\ **type**           |String                |The record type.      |
+--------------------------------+----------------------+----------------------+
|recordsets.\ **version**        |Integer               |The version of the    |
|                                |                      |record.               |
+--------------------------------+----------------------+----------------------+
|recordsets.\ **created_at**     |Datestamp             |The time stamp        |
|                                |                      |indicating the        |
|                                |                      |creation date of the  |
|                                |                      |record.               |
+--------------------------------+----------------------+----------------------+
|recordsets.\ **updated_at**     |Datestamp             |The time stamp        |
|                                |                      |indicating the date   |
|                                |                      |that the record was   |
|                                |                      |last updated.         |
+--------------------------------+----------------------+----------------------+
|recordsets.\ **links**          |Object                |A container with the  |
|                                |                      |links to the record.  |
+--------------------------------+----------------------+----------------------+
|recordsets.links.\ **self**     |Uuid                  |The link to the       |
|                                |                      |record.               |
+--------------------------------+----------------------+----------------------+
|**links**                       |Object                |A container with the  |
|                                |                      |links to the          |
|                                |                      |recordsets.           |
+--------------------------------+----------------------+----------------------+
|links.\ **self**                |Uuid                  |The link to the       |
|                                |                      |recordsets.           |
+--------------------------------+----------------------+----------------------+
|**metadata**                    |Object                |Any metadata key and  |
|                                |                      |value pairs.          |
+--------------------------------+----------------------+----------------------+
|metadata.\ **total_count**      |Integer               |The number of records |
|                                |                      |in the array.         |
+--------------------------------+----------------------+----------------------+

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
               "self": "https://127.0.0.1:9001/v2/zones/2150b1bf-dee2-4221-9d85-11f7886fb15f/recordsets/65ee6b49-bb4c-4e52-9799-31330c94161f"
           },
           "updated_at": null,
           "records": [
               "ns1.devstack.org."
           ],
           "action": "NONE",
           "ttl": null,
           "status": "ACTIVE",
           "id": "65ee6b49-bb4c-4e52-9799-31330c94161f",
           "name": "example.org.",
           "zone_id": "2150b1bf-dee2-4221-9d85-11f7886fb15f",
           "zone_name": "example.org.",
           "created_at": "2014-10-24T19:59:11.000000",
           "version": 1,
           "type": "NS"
        },
        {
           "description": null,
           "links": {
               "self": "https://127.0.0.1:9001/v2/zones/2150b1bf-dee2-4221-9d85-11f7886fb15f/recordsets/14500cf9-bdff-48f6-b06b-5fc7491ffd9e"
           },
           "updated_at": "2014-10-24T19:59:46.000000",
           "records": [
               "ns1.devstack.org. jli.ex.com. 1458666091 3502 600 86400 3600"
           ],
           "action": "NONE",
           "ttl": null,
           "status": "ACTIVE",
           "id": "14500cf9-bdff-48f6-b06b-5fc7491ffd9e",
           "name": "example.org.",
           "zone_id": "2150b1bf-dee2-4221-9d85-11f7886fb15f",
           "zone_name": "example.org.",
           "created_at": "2014-10-24T19:59:12.000000",
           "version": 1,
           "type": "SOA"
        },
        {
           "name": "example.com.",
           "id": "12caacfd-f0fc-4bcb-aa24-c42769897822",
           "type": "SOA",
           "zone_name": "example.com.",
           "action": "NONE",
           "ttl": null,
           "status": "ACTIVE",
           "description": null,
           "links": {
               "self": "http://127.0.0.1:9001/v2/zones/b8d7eaf1-e5c7-4b15-be6e-4b2809f47ec3/recordsets/12caacfd-f0fc-4bcb-aa24-c42769897822"
           },
           "created_at": "2016-03-22T16:12:35.000000",
           "updated_at": "2016-03-22T17:01:31.000000",
           "records": [
               "ns1.devstack.org. jli.ex.com. 1458666091 3502 600 86400 3600"
           ],
           "zone_id": "b8d7eaf1-e5c7-4b15-be6e-4b2809f47ec3",
           "version": 2
        }
     ],
     "metadata": {
       "total_count": 3
     },
     "links": {
       "self": "https://127.0.0.1:9001/v2/recordsets"
     }
   }
