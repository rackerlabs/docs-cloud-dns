.. _POST_createRecordset_v2__account_id__zones__zone_id__recordsets_recordsets:

Create a record set
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code::

    POST /v2/{TENANT_ID}/zones/{zoneId}/recordsets

This operation creates a record set with the configuration defined by the request.

A record set groups together a list of related records. A record set is the essential 
content of your zone file and is used to define the various domain-name-to-server routes 
for your application. Record sets are also referred to as *resource record rets* or *RRSets*.

This operation provisions a new DNS record set, based on the configuration defined in the 
request object. 

If the corresponding request cannot be fulfilled because of insufficient or invalid data, 
an ``HTTP 400`` (Bad Request) error response is returned with information about the 
failure in the body of the response. Failures in the validation process are 
non-recoverable and require you to correct the cause of the failure and resend the request.

..  note:: 

   - This operation returns an asynchronous response. For information about how
     asynchronous operations work, see 
     :ref:`Synchronous and asynchronous responses<cdns-dg-synch-asynch>`.
   
   - The following examples show the final 201 Created responses for the operations and 
     indicate that the task has been completed. 


The following table shows the possible response codes for this operation.

+---------+-----------------------+---------------------------------------------+
| Response| Name                  | Description                                 |
| code    |                       |                                             |
+=========+=======================+=============================================+
| 201     | Created               | The request was fulfilled and a new resource|
|         |                       | was created.                                |
+---------+-----------------------+---------------------------------------------+
| 202     | Accepted              | The request was accepted for                |
|         |                       | processing, but the processing has not      |
|         |                       | completed.                                  |
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
| ``{zoneId}``          | ​UUID   | The ID of the zone for which you want to    |
|                       |         | create a record set.                        |
+-----------------------+---------+---------------------------------------------+

The following table shows the body parameters for the request.

+-----------------------+------------+---------------------------------------------+
| Name                  | Type       | Description                                 |
+=======================+============+=============================================+
| ``name``              | ​String    | The name for the zone, which cannot be      |
|                       | (Required) | changed. Must be a valid zone (domain) name.|
+-----------------------+------------+---------------------------------------------+
| ``type``              | ​String    | Type of record set, which cannot be         |
|                       | (Optional) | changed.                                    |
+-----------------------+------------+---------------------------------------------+
| ``ttl``               | Integer    | Time-to-live numeric value in seconds. The  |
|                       | (Optional) | default, and minimum, value is 300 seconds. |
+-----------------------+------------+---------------------------------------------+
| ``description``       | ​String    | A description of the record set (UTF-8 text |
|                       | (Optional) | field).                                     |
+-----------------------+------------+---------------------------------------------+
| ``records``           | ​Object    | An array of data records.                   |
|                       | (Optional) |                                             |
+-----------------------+------------+---------------------------------------------+

The format shown in the following examples can be used for common record set types including 
A, AAAA, CNAME, NS, and TXT. Simply replace the ``type`` and ``records`` values with the 
appropriate values.

 
**Example: Create an A record set, request**

.. code::  

    POST /v2/123456/zones/2150b1bf-dee2-4221-9d85-11f7886fb15f/recordsets HTTP/1.1
    Host: global.dns.rackspacecloud.com
    Accept: application/json
    Content-Type: application/json

    {
      "name" : "example.org.",
      "description" : "This is an example record set.",
      "type" : "A",
      "ttl" : 3600,
      "records" : [
          "10.1.0.2"
      ]
    }

 
**Example: Create an MX record set, request**

.. code::  

    POST /v2/123456/zones/2150b1bf-dee2-4221-9d85-11f7886fb15f/recordsets HTTP/1.1
    Host: global.dns.rackspacecloud.com
    Accept: application/json
    Content-Type: application/json

    {
        "name" : "mail.example.org.",
        "description" : "An MX recordset.",
        "type" : "MX",
        "ttl" : 3600,
        "records" : [
            "10 mail1.example.org.",
            "20 mail2.example.org.",
            "30 mail3.example.org.",
            "40 mail4.example.org."
        ]
    }

 
**Example: Create a CNAME record set, request**

.. code::  

    POST /v2/123456/zones/2150b1bf-dee2-4221-9d85-11f7886fb15f/recordsets HTTP/1.1
    Host: global.dns.rackspacecloud.com
    Accept: application/json
    Content-Type: application/json

    {
      "name" : "www.example.org.",
      "description" : "This is an example record set.",
      "type" : "CNAME",
      "ttl" : 3600,
      "records" : [
          "example.com."
      ]
    }

 
**Example: Create an A record set, response**

.. code::  

    HTTP/1.1 201 Created
    Content-Type: application/json

    {
        "description": "This is an example record set.",
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

 
**Example: Create an MX record set, response**

.. code::  

    HTTP/1.1 201 Created
    Content-Type: application/json

    {
        "description": "An MX recordset.",
        "links": {
            "self": "https://global.dns.rackspacecloud.com/v2/123456/zones/2150b1bf-dee2-4221-9d85-11f7886fb15f/recordsets/f7b10e9b-0cae-4a91-b162-562bc6096649"
        },
        "updated_at": null,
        "records" : [
            "10 mail1.example.org.",
            "20 mail2.example.org.",
            "30 mail3.example.org.",
            "40 mail4.example.org."
        ],
        "ttl": 3600,
        "id": "f7b10e9b-0cae-4a91-b162-562bc6096649",
        "name": "mail.example.org.",
        "zone_id": "2150b1bf-dee2-4221-9d85-11f7886fb15f",
        "created_at": "2014-10-25T19:59:44.000000",
        "version": 1,
        "type": "MX"
    }

 
**Example: Create a CNAME record set, response**

.. code::  

    HTTP/1.1 201 Created
    Content-Type: application/json

    {
        "description": "A CNAME recordset.",
        "links": {
            "self": "https://global.dns.rackspacecloud.com/v2/123456/zones/2150b1bf-dee2-4221-9d85-11f7886fb15f/recordsets/f7b10e9b-0cae-4a91-3765-562bc6096649"
        },
        "updated_at": null,
        "records" : [
            "example.com."
        ],
        "ttl": 3600,
        "id": "f7b10e9b-0cae-4a91-3765-562bc6096649",
        "name": "example.org.",
        "zone_id": "2150b1bf-dee2-4221-9d85-11f7886fb15f",
        "created_at": "2014-10-25T19:59:44.000000",
        "version": 1,
        "type": "CNAME"
    }
