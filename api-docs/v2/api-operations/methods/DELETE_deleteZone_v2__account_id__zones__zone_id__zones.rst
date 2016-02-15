.. _DELETE_deleteZone_v2__account_id__zones__zone_id__zones:

Delete specified zone
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code::

    DELETE /v2/{$TENANT-ID}/zones/{zone_id}

This operation deletes a specified zone. Once a zone has been deleted, all associated 
resources are destroyed, and the operation is non-recoverable.

..  note:: 

    This operation returns an asynchronous response. This call returns an asynchronous 
    response. Refer to :ref:`Synchronous and asynchronous responses<cdns-dg-synch-asynch>` 
    for more information about how the asynchronous call works. 
    
    Refer to :ref:`DNS propagation<cdns-dg-propagation>` for information about DNS 
    propagation.

..  note:: 

    This operation takes a few minutes to become effective on our name servers.

This table shows the possible response codes for this operation:

+---------+-----------------------+---------------------------------------------+
| Response| Name                  | Description                                 |
| Code    |                       |                                             |
+=========+=======================+=============================================+
| 201     | Created               | The request has been fulfilled and resulted |
|         |                       | in a new resource being created.            |
+---------+-----------------------+---------------------------------------------+
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
| 403     | Forbidden             | The server has not found anything matching  |
|         |                       | the Request-URI.                            |
+---------+-----------------------+---------------------------------------------+
| 404     | Not Found             | The requested item was not found.           |
+---------+-----------------------+---------------------------------------------+
| 405     | Method Not Allowed    | The method specified in the Request-Line is |
|         |                       | not allowed for the resource identified by  |
|         |                       | the Request-URI.                            |
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

This table shows the URI parameters for the delete zone request:

+-----------------------+---------+---------------------------------------------+
| Name                  | Type    | Description                                 |
+=======================+=========+=============================================+
| ``{$TENANT-ID}``      | ​String | The account ID of the owner of the          |
|                       |         | specified account.                          |
+-----------------------+---------+---------------------------------------------+
| ``{zone_id}``         | ​String | The zone ID for the specified zone.         |
+-----------------------+---------+---------------------------------------------+

 
**Example Delete zone request**

.. code::  

    DELETE /v2/123456/zones/a86dba58-0043-4cc6-a1bb-69d5e86f3ca3 HTTP/1.1
    Host: global.dns.rackspacecloud.com
    Accept: application/json
    Content-Type: application/json

This operation does not accept a request body.

 
**Example Delete zone response**

.. code::  

    HTTP/1.1 202 Accepted

This operation does not return a response body.
