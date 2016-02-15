.. _PATCH_updateZone_v2__account_id__zones__zone_id__zones:

Update zone
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code::

    PATCH /v2/{TENANT_ID}/zones/{zone_id}

This call modifies DNS zone attributes only. Records cannot be added,
modified, or Deleted. Only the TTL, email address and comment attributes
of a zone can be modified.

..  note:: 

    This operation returns an asynchronous response. This call returns an
    asynchronous response. Refer to 
    :ref:`Synchronous and asynchronous responses<cdns-dg-synch-asynch>` for more 
    information about how the asynchronous call works. 

If the corresponding request cannot be fulfilled due to insufficient or invalid data, an 
``HTTP 400`` (Bad Request) error response will be returned with information regarding the 
nature of the failure in the body of the response. Failures in the validation process are 
non-recoverable and require the caller to correct the cause of the failure and **POST** 
the request again.

..  note:: 

    -  Refer to :ref:`DNS propagation<cdns-dg-propagation>` for information about DNS 
       propagation.

    -  A zone's ``id`` is immutable.

    -  When the zone TTL is supplied by the user, either via a create or update call, the 
       TTL values must be 300 seconds or more.

    -  ``name`` cannot be specified, because the zone name cannot be
       modified.

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
| 413     | Over Limit            | Request exceeds rate limit or quota         |
+---------+-----------------------+---------------------------------------------+
| 415     | Unsupported Media     | The server is refusing to service the       |
|         | Type                  | request because the entity of the request   |
|         |                       | is in a format not supported by the         |
|         |                       | requested resource for the requested        |
|         |                       | method.                                     |
+---------+-----------------------+---------------------------------------------+
| 503     | Service Unavailable   | The service is not available.               |
+---------+-----------------------+---------------------------------------------+

This table shows the URI parameters for the update zone request:

+-----------------------+---------+---------------------------------------------+
| Name                  | Type    | Description                                 |
+=======================+=========+=============================================+
| ``{TENANT_ID}``       | ​String | The account ID of the owner of the          |
|                       |         | specified account.                          |
+-----------------------+---------+---------------------------------------------+
| ``{zone_id}``         | ​String | The zone ID for the specified zone.         |
+-----------------------+---------+---------------------------------------------+

This list shows the body parameters for the request:

-  **name**: String. Required.

   The name for the zone (immutable). Must be a valid zone name.

-  **type**: String. Optional.

   Enum PRIMARY/SECONDARY, default PRIMARY (immutable).

-  **email**: String. Required.

   Email address to use for contacting the zone administrator.

-  **ttl**: Integer. Optional.

   time-to-live numeric value in seconds. The default value is 300
   seconds.

-  **description**: String. Optional.

   UTF-8 text field.

-  **masters**: Object. Optional.

   Array of master nameservers. (NULL for type PRIMARY, required for
   SECONDARY otherwise zone will not be transferred before set.)

 
**Example Update zone request**

.. code::  

    PATCH /v2/123456/zones/a86dba58-0043-4cc6-a1bb-69d5e86f3ca3 HTTP/1.1
    Host: global.dns.rackspacecloud.com
    Accept: application/json
    Content-Type: application/json

    {
        "ttl": 3600
    }

 
**Example  Update zone response**

.. code::  

    HTTP/1.1 200 OK
    Content-Type: application/json

    {
        "id": "a86dba58-0043-4cc6-a1bb-69d5e86f3ca3",
        "pool_id": "572ba08c-d929-4c70-8e42-03824bb24ca2",
        "project_id": "123456",
        "name": "example.org.",
        "email": "joe@example.org.",
        "ttl": 3600,
        "serial": 1404760160,
        "status": "ACTIVE",
        "description": "This is an example zone.",
        "masters": [],
        "type": "PRIMARY",
        "transferred_at": null,
        "version": 1,
        "created_at": "2014-07-07T18:25:31.275934",
        "updated_at": "2014-07-07T19:09:20.876366",
        "links": {
          "self": "https://global.dns.api.rackspacecloud.com/v2/123456/zones/a86dba58-0043-4cc6-a1bb-69d5e86f3ca3"
        }
    }
