.. _DELETE_deleteZoneImport_v2__account_id__zones_tasks_imports__zone_id__zones:

Delete a zone import
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code::

    DELETE /v2/{account_id}/zones/tasks/imports/{zone_id}

This call deletes a zone import with the specified zone import uuid ID.
It does not affect the zone that was imported. It simply removes the
record of the import.

This table shows the possible response codes for this operation:

+---------+-----------------------+---------------------------------------------+
| Response| Name                  | Description                                 |
| Code    |                       |                                             |
+=========+=======================+=============================================+
| 204     | No Content            | The server has fulfilled the request but    |
|         |                       | does not need to return an entity-body, and |
|         |                       | might want to return updated                |
|         |                       | metainformation.                            |
+---------+-----------------------+---------------------------------------------+
| 401     | Unauthorized          | You are not authorized to complete this     |
|         |                       | operation. This error can occur if the      |
|         |                       | request is submitted with an invalid        |
|         |                       | authentication token.                       |
+---------+-----------------------+---------------------------------------------+
| 404     | Not Found             | The requested item was not found.           |
+---------+-----------------------+---------------------------------------------+

This table shows the URI parameters for the delete a zone import request:

+-----------------------+---------+---------------------------------------------+
| Name                  | Type    | Description                                 |
+=======================+=========+=============================================+
| ``{account_id}``      | ​String | The account ID of the owner of the          |
|                       |         | specified account.                          |
+-----------------------+---------+---------------------------------------------+
| ``{uuid_id}``         | ​String | The uuid ID for the specified zone import.  |
+-----------------------+---------+---------------------------------------------+

 
**Example Delete zone import request**

.. code::  

    DELETE /v2/123456/zones/tasks/imports/a86dba58-0043-4cc6-a1bb-69d5e86f3ca3 HTTP/1.1
    Host: global.dns.rackspacecloud.com
    Accept: application/json
    Content-Type: application/json

This operation does not accept a request body.

 
**Example Delete zone import response**

.. code::  

    HTTP/1.1 204 No Content

This operation does not return a response body.
