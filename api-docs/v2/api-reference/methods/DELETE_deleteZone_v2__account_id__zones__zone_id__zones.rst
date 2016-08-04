.. _DELETE_deleteZone_v2__account_id__zones__zone_id__zones:

Delete a zone
-------------

.. code::

    DELETE /v2/{$TENANT-ID}/zones/{zoneId}

This operation deletes a specified zone. After a zone is deleted, all
associated resources are destroyed, and the operation is non-recoverable.

..  note::

    - This operation returns an asynchronous response. For information about
      how asynchronous operations work, see
      :ref:`Synchronous and asynchronous responses<synch-asynch>`.

   - This operation takes a few minutes to become effective on our name
     servers. For more information about DNS propagation, see
     :ref:`DNS propagation<propagation>`.

This table shows the possible response codes for this operation:

+---------+---------------------+---------------------------------------------+
| Response| Name                | Description                                 |
| code    |                     |                                             |
+=========+=====================+=============================================+
| 202     | Accepted            | The request was accepted for                |
|         |                     | processing, but the processing has not      |
|         |                     | completed.                                  |
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
| ``{$TENANT-ID}``      | ​String | The account ID of the account owner.      |
+-----------------------+---------+-------------------------------------------+
| ``{zoneId}``          | ​String | The ID for the zone to delete.            |
+-----------------------+---------+-------------------------------------------+


**Example: Delete a zone, request**

.. code::

    DELETE /v2/123456/zones/a86dba58-0043-4cc6-a1bb-69d5e86f3ca3 HTTP/1.1
    Host: global.dns.rackspacecloud.com
    Accept: application/json
    Content-Type: application/json

This operation does not accept a request body.

Response
^^^^^^^^

**Example: Delete a zone, response**

.. code::

    HTTP/1.1 202 Accepted

This operation does not return a response body.
