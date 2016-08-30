.. _DELETE_deleteZoneExport_v2__account_id__zones_tasks_exports__uuid_id__zones:

Delete a zone export
--------------------

.. code::

    DELETE /v2/{$TENANT-ID}/zones/tasks/exports/{zoneId}

This operation deletes a zone export for the specified zone export uuid ID.
This operation does not affect the zone that was exported; it simply removes
the record of the export. If the link to view the export pointed to a DNS API
endpoint, the endpoint will no longer be available.

This table shows the possible response codes for this operation:

+---------+---------------------+---------------------------------------------+
| Response| Name                | Description                                 |
| code    |                     |                                             |
+=========+=====================+=============================================+
| 204     | No Content          | The server fulfilled the request but        |
|         |                     | does not need to return an entity body, and |
|         |                     | might want to return updated                |
|         |                     | metainformation.                            |
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

Request
^^^^^^^

This table shows the URI parameters for the request:

+-----------------------+---------+-------------------------------------------+
| Name                  | Type    | Description                               |
+=======================+=========+===========================================+
| ``{TENANT_ID}``       | ​String | The account ID of the account owner.      |
+-----------------------+---------+-------------------------------------------+
| ``{zoneId}``          | ​Uuid   | The ID for the zone export to delete.     |
+-----------------------+---------+-------------------------------------------+


**Example: Delete a zone export, request**

.. code::

    DELETE /v2/123456/zones/tasks/exports/a86dba58-0043-4cc6-a1bb-69d5e86f3ca3 HTTP/1.1
    Host: global.dns.rackspacecloud.com
    Accept: application/json
    Content-Type: application/json

This operation does not accept a request body.

Response
^^^^^^^^


**Example: Delete a zone export, response**

.. code::

    HTTP/1.1 204 No Content

This operation does not return a response body.
