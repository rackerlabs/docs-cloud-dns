.. _DELETE_deleteZoneImport_v2__account_id__zones_tasks_imports__zone_id__zones:

Delete a zone import
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code::

    DELETE /v2/{$TENANT-ID}/zones/tasks/imports/{zoneId}

This operation deletes a zone import with the specified zone import ID.
The operation does not affect the zone that was imported; it simply removes the
record of the import.

The following table shows the possible response codes for this operation.

+---------+-----------------------+---------------------------------------------+
| Response| Name                  | Description                                 |
| code    |                       |                                             |
+=========+=======================+=============================================+
| 204     | No Content            | The server has fulfilled the request but    |
|         |                       | does not need to return an entity-body, and |
|         |                       | might want to return updated                |
|         |                       | meta-information.                           |
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

The following table shows the URI parameters for the request.

+-----------------------+---------+---------------------------------------------+
| Name                  | Type    | Description                                 |
+=======================+=========+=============================================+
| ``{$TENANT-ID}``      | ​String | The account ID of the account owner.        |
+-----------------------+---------+---------------------------------------------+
| ``{zoneId}``          | ​UUID   | The ID of the zone import to delete.        |
+-----------------------+---------+---------------------------------------------+

 
**Example: Delete a zone import, request**

.. code::  

    DELETE /v2/123456/zones/tasks/imports/a86dba58-0043-4cc6-a1bb-69d5e86f3ca3 HTTP/1.1
    Host: global.dns.rackspacecloud.com
    Accept: application/json
    Content-Type: application/json

This operation does not accept a request body.

 
**Example: Delete a zone import, response**

.. code::  

    HTTP/1.1 204 No Content

This operation does not return a response body.
