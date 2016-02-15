.. _POST_exportZone_v2__account_id__zones__uuid_id__tasks_export_zones:

Create a zone export
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code::

    POST /v2/{TENANT_ID}/zones/{uuid}/tasks/export

This call exports a zone in BIND9 zone file format. To export a zone in BIND9 zonefile 
format, a zone export resource must be created by initializing an export task.

This table shows the possible response codes for this operation:

+---------+-----------------------+---------------------------------------------+
| Response| Name                  | Description                                 |
| Code    |                       |                                             |
+=========+=======================+=============================================+
| 202     | Accepted              | The request has been accepted for           |
|         |                       | processing, but the processing has not been |
|         |                       | completed.                                  |
+---------+-----------------------+---------------------------------------------+
| 415     | Unsupported Media     | The server is refusing to service the       |
|         | Type                  | request because the entity of the request   |
|         |                       | is in a format not supported by the         |
|         |                       | requested resource for the requested        |
|         |                       | method.                                     |
+---------+-----------------------+---------------------------------------------+

This table shows the URI parameters for the create a zone export
request:

+-----------------------+---------+---------------------------------------------+
| Name                  | Type    | Description                                 |
+=======================+=========+=============================================+
| ``{TENANT_ID}``       | ​String | The account ID of the owner of the          |
|                       |         | specified account.                          |
+-----------------------+---------+---------------------------------------------+
| ``{uuid_id}``         | ​String | The uuid of the specified zone.             |
+-----------------------+---------+---------------------------------------------+

 
**Example Create zone export request**

.. code::  

    POST /v2/123456/zones/074e805e-fe87-4cbb-b10b-21a06e215d41/tasks/export HTTP/1.1
    Host: global.dns.rackspacecloud.com

This operation does not accept a request body.
 
**Example Create zone export response**

.. code::  

    HTTP/1.1 202 Accepted
    Content-Type: application/json

    {
        "status": "PENDING",
        "zone_id": "074e805e-fe87-4cbb-b10b-21a06e215d41",
        "links": {
            "self": "https://global.dns.rackspacecloud.com/v2/123456/zones/tasks/exports/8ec17fe1-d1f9-41b4-aa98-4eeb4c27b720"
        },
        "created_at": "2015-08-27T20:57:03.000000",
        "updated_at": null,
        "version": 1,
        "location": null,
        "message": null,
        "project_id": "1",
        "id": "8ec17fe1-d1f9-41b4-aa98-4eeb4c27b720"
    }
