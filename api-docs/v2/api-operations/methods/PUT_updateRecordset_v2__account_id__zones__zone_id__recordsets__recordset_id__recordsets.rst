.. _PUT_updateRecordset_v2__account_id__zones__zone_id__recordsets__recordset_id__recordsets:

Update recordset
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code::

    PUT /v2/{account_id}/zones/{zone_id}/recordsets/{recordset_id}

This operation replaces the specified record set with the specified details.

..  note:: 

    This operation returns an asynchronous response. This call returns an
    asynchronous response. Refer to 
    :ref:`Synchronous and asynchronous responses<cdns-dg-synch-asynch>` for more 
    information about how the asynchronous call works.     

If a request cannot be fulfilled due to insufficient or invalid data, an ``HTTP 400`` 
(Bad Request) error response will be returned with information regarding the nature of the 
failure in the body of the response. Failures in the validation process are non-recoverable 
and require the caller to correct the cause of the failure and **POST** the request again.

In the example shown below, the TTL is updated to ``3600``.

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
| 409     | Already Exists        | The item already exists.                    |
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


This table shows the URI parameters for the update record set request:

+-----------------------+---------+---------------------------------------------+
| Name                  | Type    | Description                                 |
+=======================+=========+=============================================+
| ``{account_id}``      | ​String | The account ID of the owner of the          |
|                       |         | specified account.                          |
+-----------------------+---------+---------------------------------------------+
| ``{zone_id}``         | ​String | The zone ID for the specified zone.         |
+-----------------------+---------+---------------------------------------------+
| ``{recordset_id}``    | ​String | The record set ID for the specified record  |
|                       |         | set.                                        |
+-----------------------+---------+---------------------------------------------+

This list shows the body parameters for the request:

-  **name**: String. Required.

   The name for the zone (immutable). Must be a valid zone name.

-  **type**: String. Optional.

   Type of record set. Cannot be changed on update (immutable).

-  **ttl**: Integer. Optional.

   time-to-live numeric value in seconds. The default value is 300
   seconds.

-  **description**: String. Optional.

   UTF-8 text field.

-  **records**: Object. Optional.

   A list of data records.

 
**Example Update record set request**

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

 
**Example Update record set response**

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
