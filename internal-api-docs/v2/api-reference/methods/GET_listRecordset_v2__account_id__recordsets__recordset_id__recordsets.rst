.. _GET_listRecordset_v2__account_id__recordsets__recordset_id__recordsets:

List a record set
-----------------

.. code::

    GET /v2/{TENANT_ID}/recordsets/{recordsetId}

This operation retrieves a record set with the specified record set ID.

If the corresponding request cannot be fulfilled because of insufficient or
invalid data, an ``HTTP 400`` (Bad Request) error response is returned with
information about the failure in the body of the response. Failures in the
validation process are non-recoverable and require you to correct the cause of
the failure and resend the request.


This table shows the possible response codes for this operation:

+---------+---------------------+---------------------------------------------+
| Response| Name                | Description                                 |
| code    |                     |                                             |
+=========+=====================+=============================================+
| 200     | Success             | The request succeeded.                      |
+---------+---------------------+---------------------------------------------+
| 301     | Moved Permanently   | Moved Permanently. The canonical location of|
|         |                     | the requested recordset is provided.        |
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
| 409     | Already Exists      | The item already exists.                    |
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
| ``{recordsetId}``     | ​String | The ID of the record set to list.         |
+-----------------------+---------+-------------------------------------------+


**Example: List a record set, request**

.. code::

    GET /v2/123456/recordsets/f7b10e9b-0cae-4a91-b162-562bc6096648 HTTP/1.1
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
|**id**                          |Uuid                 |The ID of the         |
|                                |                     |record set.           |
+--------------------------------+---------------------+----------------------+
|**zone_id**                     |Uuid                 |The ID of the zone.   |
+--------------------------------+---------------------+----------------------+
|**name**                        |String               |The name of the       |
|                                |                     |record set.           |
+--------------------------------+---------------------+----------------------+
|**ttl**                         |Integer              |The time to live for  |
|                                |                     |the record set.       |
+--------------------------------+---------------------+----------------------+
|**description**                 |String               |The description       |
|                                |                     |of the record set.    |
+--------------------------------+---------------------+----------------------+
|**records**                     |Array                |An array of record    |
|                                |                     |IP addresses.         |
+--------------------------------+---------------------+----------------------+
|**type**                        |String               |The record type.      |
+--------------------------------+---------------------+----------------------+
|**version**                     |Integer              |The version of the    |
|                                |                     |record set.           |
+--------------------------------+---------------------+----------------------+
|**created_at**                  |Datestamp            |The time stamp        |
|                                |                     |indicating the        |
|                                |                     |creation date of the  |
|                                |                     |record set.           |
+--------------------------------+---------------------+----------------------+
|**updated_at**                  |Datestamp            |The time stamp        |
|                                |                     |indicating the last   |
|                                |                     |update date of the    |
|                                |                     |record set.           |
+--------------------------------+---------------------+----------------------+
|**links**                       |Object               |A container with the  |
|                                |                     |links to the          |
|                                |                     |record set.           |
+--------------------------------+---------------------+----------------------+
|links.\ **self**                |Uuid                 |The link to the       |
|                                |                     |record set.           |
+--------------------------------+---------------------+----------------------+


**Example: List a record set, response**

.. code::

    HTTP/1.1 200 OK
    Vary: Accept
    Content-Type: application/json

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
