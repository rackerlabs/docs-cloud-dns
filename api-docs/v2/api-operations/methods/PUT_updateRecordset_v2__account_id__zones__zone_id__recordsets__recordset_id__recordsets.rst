.. _PUT_updateRecordset_v2__account_id__zones__zone_id__recordsets__recordset_id__recordsets:

Update a record set
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code::

    PUT /v2/{TENANT_ID}/zones/{zoneId}/recordsets/{recordsetId}

This operation updates the specified record set with the specified details. NS record sets 
cannot be updated.

..  note:: 

    - This operation returns an asynchronous response. For information about how
      asynchronous operations work, see 
      :ref:`Synchronous and asynchronous responses<cdns-dg-synch-asynch>`.  

If the corresponding request cannot be fulfilled because of insufficient or invalid data, 
an ``HTTP 400`` (Bad Request) error response is returned with information about the 
failure in the body of the response. Failures in the validation process are 
non-recoverable and require you to correct the cause of the failure and resend the request.

The following table shows the possible response codes for this operation.

+---------+-----------------------+---------------------------------------------+
| Response| Name                  | Description                                 |
| code    |                       |                                             |
+=========+=======================+=============================================+
| 200     | Success               | The request succeeded.                      |
+---------+-----------------------+---------------------------------------------+
| 201     | Created               | The request was fulfilled and a new resource|
|         |                       | was created.                                |
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
| 409     | Already Exists        | The item already exists.                    |
+---------+-----------------------+---------------------------------------------+
| 413     | Over Limit            |The request exceeds the rate limit or quota. |
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
| ``{zoneId}``          | ​String | The ID of the zone with the record set to   |
|                       |         | update.                                     |
+-----------------------+---------+---------------------------------------------+
| ``{recordsetId}``     | ​String | The ID of the record set to update.         |
+-----------------------+---------+---------------------------------------------+

The following table shows the body parameters for the request.

+-----------------------+------------+---------------------------------------------+
| Name                  | Type       | Description                                 |
+=======================+============+=============================================+
| ``name``              | ​String    | The name for the zone, which cannot be      |
|                       |            | changed. Must be a valid zone (domain) name.|
+-----------------------+------------+---------------------------------------------+
| ``type``              | ​String    | Type of record set, which cannot be         |
|                       | (Optional) | changed.                                    |
+-----------------------+------------+---------------------------------------------+
| ``ttl``               | Integer    | Time-to-live numeric value in seconds. The  |
|                       | (Optional) | default value is 300 seconds.               |
+-----------------------+------------+---------------------------------------------+
| ``description``       | ​String    | A description of the record set (UTF-8 text |
|                       | (Optional) | field).                                     |
+-----------------------+------------+---------------------------------------------+
| ``records``           | ​Object    | An array of data records.                   |
|                       | (Optional) |                                             |
+-----------------------+------------+---------------------------------------------+

 
**Example: Update a record set, request**

.. code::  

    PUT /v2/123456/zones/2150b1bf-dee2-4221-9d85-11f7886fb15f/recordsets/f7b10e9b-0cae-4a91-b162-562bc6096648 HTTP/1.1
    Host: global.dns.rackspacecloud.com
    Accept: application/json
    Content-Type: application/json

     {
        "description" : "I updated this example.",
        "ttl" : 3600,
        "records" : [
           "10.1.0.2"
        ]
     }

In this example, the TTL is updated to ``3600``.

**Example: Update a record set, response**

.. code::  

    HTTP/1.1 200 OK
    Content-Type: application/json

    {
        "description": "I updated this example.",
        "ttl": 3600,
        "records": [
            "10.1.0.2"
        ],
        "links": {
            "self": "https://global.dns.api.rackspacecloud.com/v2/123456/zones/2150b1bf-dee2-4221-9d85-11f7886fb15f/recordsets/f7b10e9b-0cae-4a91-b162-562bc6096648"
        },
        "updated_at": "2014-10-24T20:15:27.000000",
        "id": "f7b10e9b-0cae-4a91-b162-562bc6096648",
        "name": "example.org.",
        "zone_id": "2150b1bf-dee2-4221-9d85-11f7886fb15f",
        "created_at": "2014-10-24T19:59:44.000000",
        "version": 2,
        "type": "A"
    }
