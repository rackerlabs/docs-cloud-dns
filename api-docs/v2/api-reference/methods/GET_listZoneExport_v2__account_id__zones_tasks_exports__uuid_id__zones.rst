.. _GET_listZoneExport_v2__account_id__zones_tasks_exports__uuid_id__zones:

List a zone export record
-------------------------

.. code::

    GET /v2/{TENANT_ID}/zones/tasks/exports/{zoneId}

This operation lists the zone export record for the specified zone export uuid
ID. Returned objects can be queried by using the links in the ``links`` field.

This table shows the possible response codes for this operation:

+---------+---------------------+---------------------------------------------+
| Response| Name                | Description                                 |
| code    |                     |                                             |
+=========+=====================+=============================================+
| 200     | Accepted            | The request was accepted for processing,    |
|         |                     | but the processing has not completed.       |
+---------+---------------------+---------------------------------------------+
| 401     | Unauthorized        | You are not authorized to complete this     |
|         |                     | operation. This error can occur if the      |
|         |                     | request is submitted with an invalid        |
|         |                     | authentication token.                       |
+---------+---------------------+---------------------------------------------+
| 404     | Not Found           | The requested item was not found.           |
+---------+---------------------+---------------------------------------------+

Request
^^^^^^^

This table shows the URI parameters for the request:

+---------------------+---------+---------------------------------------------+
| Name                | Type    | Description                                 |
+=====================+=========+=============================================+
| ``{TENANT_ID}``     | ​String | The account ID of the account owner.        |
+---------------------+---------+---------------------------------------------+
| ``{zoneId}``        | ​UUID   | The ID of the zone export for which you want|
|                     |         | to list the record.                         |
+---------------------+---------+---------------------------------------------+


**Example: List a zone export record, request**

.. code::

    GET /v2/123456/zones/tasks/exports/a86dba58-0043-4cc6-a1bb-69d5e86f3ca3 HTTP/1.1
    Host: global.dns.rackspacecloud.com
    Accept: application/json

This operation does not accept a request body.

Response
^^^^^^^^

This table shows the body parameters for the response:

+------------------------------+----------------------+----------------------+
|Name                          |Type                  |Description           |
+==============================+======================+======================+
|**id**                        |Uuid                  |The ID of the zone    |
|                              |                      |export.               |
+------------------------------+----------------------+----------------------+
|**zone_id**                   |Uuid                  |The ID of the zone.   |
+------------------------------+----------------------+----------------------+
|**project_id**                |Integer               |The project, account, |
|                              |                      |or tenant ID.         |
+------------------------------+----------------------+----------------------+
|**location**                  |String                |The location of the   |
|                              |                      |zone export.          |
+------------------------------+----------------------+----------------------+
|**message**                   |String                |A description of the  |
|                              |                      |zone export.          |
+------------------------------+----------------------+----------------------+
|**version**                   |Integer               |The version of the    |
|                              |                      |zone export.          |
+------------------------------+----------------------+----------------------+
|**created_at**                |Datestamp             |The time stamp        |
|                              |                      |indicating the        |
|                              |                      |creation date of the  |
|                              |                      |zone export.          |
+------------------------------+----------------------+----------------------+
|**updated_at**                |Datestamp             |The time stamp        |
|                              |                      |indicating the date   |
|                              |                      |that the zone export  |
|                              |                      |was last updated.     |
+------------------------------+----------------------+----------------------+
|**links**                     |Object                |A container with the  |
|                              |                      |links to the exports. |
+------------------------------+----------------------+----------------------+
|links.\ **self**              |Uuid                  |The link to the       |
|                              |                      |zone exports (self).  |
+------------------------------+----------------------+----------------------+
|links.\ **export**            |Uuid                  |The link to the       |
|                              |                      |zone export (export). |
+------------------------------+----------------------+----------------------+



**Example: List a zone export record, response**

.. code::

    HTTP/1.1 200 OK
    Content-Type: application/json

    {
        "status": "COMPLETE",
        "zone_id": "a86dba58-0043-4cc6-a1bb-69d5e86f3ca3",
        "links": {
            "self": "https://global.dns.rackspacecloud.com/v2/123456/zones/tasks/exports/8ec17fe1-d1f9-41b4-aa98-4eeb4c27b720",
            "export": "https://global.dns.rackspacecloud.com/v2/123456/zones/tasks/exports/8ec17fe1-d1f9-41b4-aa98-4eeb4c27b720/export"
        },
        "created_at": "2015-08-27T20:57:03.000000",
        "updated_at": "2015-08-27T20:57:03.000000",
        "version": 2,
        "location": "https://global.dns.rackspacecloud.com/v2/123456/zones/tasks/exports/8ec17fe1-d1f9-41b4-aa98-4eeb4c27b720/export",
        "message": null,
        "project_id": "123456",
        "id": "8ec17fe1-d1f9-41b4-aa98-4eeb4c27b720"
    }

Notice that the status is ``COMPLETE`` and the ``links`` field contains an
``export`` entry that provides a link where the export (zone file) can be
accessed.
