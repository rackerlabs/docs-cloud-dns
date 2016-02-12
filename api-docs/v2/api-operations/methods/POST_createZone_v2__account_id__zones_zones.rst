.. _POST_createZone_v2__account_id__zones_zones:

Create zone
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code::

    POST /v2/{account_id}/zones

This call provisions a new DNS zone, based on the configuration defined
in the request object. 

If the corresponding request cannot be fulfilled due to insufficient or invalid data, an 
``HTTP 400`` (Bad Request) error response will be returned with information regarding the 
nature of the failure in the body of the response. Failures in the validation process are 
non-recoverable and require the caller to correct the cause of the failure and **POST** 
the request again.

..  note:: 

    This operation returns an asynchronous response. This call returns an
    asynchronous response. Refer to 
    :ref:`Synchronous and asynchronous responses<cdns-dg-synch-asynch>` for more 
    information about how the asynchronous call works. 

..  note:: 

    This operation takes a few minutes to become effective on our name servers.

    Refer to :ref:`DNS propagation<cdns-dg-propagation>` for information about DNS 
    propagation.

If you attempt to create a zone that already exists, the API will return an exception 
saying that the zone already exists.

When a zone is created, and no Time To Live (TTL) is specified, the SOA minTTL (3600 
seconds) is used as the default. When a record is added without a specified TTL, the TTL 
will show as empty. When the zone and/or record TTL is supplied by the user, either via a 
create or update call, the TTL values must be 300 seconds or more.

The following examples show the Create zone request:

..  note:: 

    When executed, this operation will show the *initial* ``202 Accepted`` response for 
    the asynchronous call and indicate that the task has been accepted for processing. 
    This operation returns an asynchronous response. This call returns an
    asynchronous response. Refer to 
    :ref:`Synchronous and asynchronous responses<cdns-dg-synch-asynch>` for more 
    information about how the asynchronous call works. 

This table shows the possible response codes for this operation:

+---------+-----------------------+---------------------------------------------+
| Response| Name                  | Description                                 |
| Code    |                       |                                             |
+=========+=======================+=============================================+
| 202     | Accepted              | The request has been accepted for           |
|         |                       | processing, but the processing has not been |
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
| 404     | Not Found             | The requested item was not found.           |
+---------+-----------------------+---------------------------------------------+
| 409     | Already Exists        | The item already exists.                    |
+---------+-----------------------+---------------------------------------------+
| 413     | Over Limit            | The number of items returned is above the   |
|         |                       | allowed limit.                              |
+---------+-----------------------+---------------------------------------------+
| 503     | Service Unavailable   | The service is not available.               |
+---------+-----------------------+---------------------------------------------+
| 513     | Global Rate Limit     | The service is under high load and the      |
|         |                       | request was rate limited. Try again in a    |
|         |                       | few minutes.                                |
+---------+-----------------------+---------------------------------------------+

This table shows the URI parameters for the create zone request:

+-----------------------+---------+---------------------------------------------+
| Name                  | Type    | Description                                 |
+=======================+=========+=============================================+
| ``{account_id}``      | ​String | The account ID of the owner of the          |
|                       |         | specified account.                          |
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

 
**Example Create zone request**

.. code::  

    POST /v2/1234/zones HTTP/1.1
    Host: 127.0.0.1:9001
    Accept: application/json
    Content-Type: application/json

    {
        "name": "example.org.",
        "email": "joe@example.org",
        "ttl": 7200,
        "description": "This is an example zone."
    }

 
**Example Create zone response**

.. code::  

    HTTP/1.1 201 Created
    Content-Type: application/json

    {
        "id": "a86dba58-0043-4cc6-a1bb-69d5e86f3ca3",
        "pool_id": "572ba08c-d929-4c70-8e42-03824bb24ca2",
        "project_id": "4335d1f0-f793-11e2-b778-0800200c9a66",
        "name": "example.org.",
        "email": "joe@example.org",
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
          "self": "https://127.0.0.1:9001/v2/1234/zones/a86dba58-0043-4cc6-a1bb-69d5e86f3ca3"
        }
    }
