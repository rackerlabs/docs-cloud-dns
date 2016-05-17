.. _POST_exportZone_v2__account_id__zones__uuid_id__tasks_export_zones:

Create a zone export
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code::

    POST /v2/{TENANT_ID}/zones/{zoneId}/tasks/export

This operation exports the specified zone in BIND9 zone file format. To export a zone in 
BIND9 zone file format, a zone export resource must be created by initializing an export 
task.

This table shows the possible response codes for this operation:

+---------+-----------------------+---------------------------------------------+
| Response| Name                  | Description                                 |
| code    |                       |                                             |
+=========+=======================+=============================================+
| 202     | Accepted              | The request was accepted for                |
|         |                       | processing, but the processing has not      |
|         |                       | completed.                                  |
+---------+-----------------------+---------------------------------------------+
| 415     | Unsupported Media     | The server won't service the                |
|         | Type                  | request because the entity of the request   |
|         |                       | is in a format not supported by the         |
|         |                       | requested resource for the requested        |
|         |                       | method.                                     |
+---------+-----------------------+---------------------------------------------+

Request
""""""""""""""""

This table shows the URI parameters for the request:

+-----------------------+---------+---------------------------------------------+
| Name                  | Type    | Description                                 |
+=======================+=========+=============================================+
| ``{TENANT_ID}``       | ​String | The account ID of the account owner.        |
+-----------------------+---------+---------------------------------------------+
| ``{zoneId}``          | ​UUID   | The zone ID for the zone that you want to   | 
|                       |         | export.                                     |
+-----------------------+---------+---------------------------------------------+

 
**Example: Create a zone export, request**

.. code::  

    POST /v2/123456/zones/074e805e-fe87-4cbb-b10b-21a06e215d41/tasks/export HTTP/1.1
    Host: global.dns.rackspacecloud.com

This operation does not accept a request body.
 
Response
""""""""""""""""
This table shows the body parameters for the response:

+--------------------------------+----------------------+----------------------+
|Name                            |Type                  |Description           |
+================================+======================+======================+
|**id**                          |Uuid                  |The ID of the zone    |
|                                |                      |export.               |
+--------------------------------+----------------------+----------------------+
|**zone_id**                     |Uuid                  |The ID of the zone.   |
+--------------------------------+----------------------+----------------------+
|**project_id**                  |Integer               |The project, account, |
|                                |                      |or tenant ID.         |
+--------------------------------+----------------------+----------------------+
|**message**                     |String                |A description of the  |
|                                |                      |zone export.          |
+--------------------------------+----------------------+----------------------+
|**version**                     |Integer               |The version of the    |
|                                |                      |zone export.          |
+--------------------------------+----------------------+----------------------+
|**created_at**                  |Datestamp             |The time stamp        |
|                                |                      |indicating the        |
|                                |                      |creation date of the  |
|                                |                      |zone export.          |
+--------------------------------+----------------------+----------------------+
|**updated_at**                  |Datestamp             |The time stamp        |
|                                |                      |indicating the date   |
|                                |                      |that the zone export  |
|                                |                      |was last updated.     |
+--------------------------------+----------------------+----------------------+
|**links**                       |Object                |A container with the  |
|                                |                      |links to the zone.    |
+--------------------------------+----------------------+----------------------+
|links.\ **self**                |Uuid                  |The link to the zone  |
|                                |                      |export (self).        |
+--------------------------------+----------------------+----------------------+

**Example: Create a zone export, response**

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
        "project_id": "123456",
        "id": "8ec17fe1-d1f9-41b4-aa98-4eeb4c27b720"
    }
