.. _GET_listZoneExport_v2__account_id__zones_tasks_exports__uuid_id__zones: 

List a zone export record
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code::

    GET /v2/{TENANT_ID}/zones/tasks/exports/{uuid_id}

This call lists the zone export record for the specified zone export uuid ID. Returned 
objects can be queried using the links in the ``links`` field.

This table shows the possible response codes for this operation:

+---------+-----------------------+---------------------------------------------+
| Response| Name                  | Description                                 |
| Code    |                       |                                             |
+=========+=======================+=============================================+
| 200     | Accepted              | The request has been accepted for           |
|         |                       | processing, but the processing has not been |
|         |                       | completed.                                  |
+---------+-----------------------+---------------------------------------------+
| 401     | Unauthorized          | You are not authorized to complete this     |
|         |                       | operation. This error can occur if the      |
|         |                       | request is submitted with an invalid        |
|         |                       | authentication token.                       |
+---------+-----------------------+---------------------------------------------+
| 404     | Not Found             | The requested item was not found.           |
+---------+-----------------------+---------------------------------------------+

This table shows the URI parameters for the list a zone export record
request:

+-----------------------+---------+---------------------------------------------+
| Name                  | Type    | Description                                 |
+=======================+=========+=============================================+
| ``{TENANT_ID}``       | ​String | The account ID of the owner of the          |
|                       |         | specified account.                          |
+-----------------------+---------+---------------------------------------------+
| ``{uuid_id}``         | ​String | The uuid ID for the specified zone export.  |
+-----------------------+---------+---------------------------------------------+

 
**Example List zone export record request**

.. code::  

    GET /v2/123456/zones/tasks/exports/a86dba58-0043-4cc6-a1bb-69d5e86f3ca3 HTTP/1.1
    Host: global.dns.rackspacecloud.com
    Accept: application/json

This operation does not accept a request body.
 
**Example List zone export record response**

.. code::  

    HTTP/1.1 200 OK
    Content-Type: application/json

    {
        "status": "COMPLETE",
        "zone_id": "6625198b-d67d-47dc-8d29-f90bd60f3ac4",
        "links": {
            "self": "https://global.dns.rackspacecloud.com/v2/123456/zones/tasks/exports/8ec17fe1-d1f9-41b4-aa98-4eeb4c27b720",
            "export": "https://global.dns.rackspacecloud.com/v2/123456/zones/tasks/exports/8ec17fe1-d1f9-41b4-aa98-4eeb4c27b720/export"
        },
        "created_at": "2015-08-27T20:57:03.000000",
        "updated_at": "2015-08-27T20:57:03.000000",
        "version": 2,
        "location": "https://global.dns.rackspacecloud.com/v2/123456/zones/tasks/exports/8ec17fe1-d1f9-41b4-aa98-4eeb4c27b720/export",
        "message": null,
        "project_id": "noauth-project",
        "id": "8ec17fe1-d1f9-41b4-aa98-4eeb4c27b720"
    }

Notice that the status has been updated and there is now an ``export`` in the ``links`` 
field that points to a link where the export (zonefile) can be accessed.
