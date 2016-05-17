.. _GET_listZoneImport_v2__account_id__zones_tasks_imports__zone_id__zones:

List a zone import
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code::

    GET /v2/{TENANT_ID}/zones/tasks/imports/{zoneId}

This operation lists the status of a zone import by querying the UUID that was returned 
when the zone import request was created. Objects are returned that can be queried by 
using the links in the ``links`` field.

This table shows the possible response codes for this operation:

+---------+-----------------------+---------------------------------------------+
| Response| Name                  | Description                                 |
| code    |                       |                                             |
+=========+=======================+=============================================+
| 200     | Accepted              | The request was accepted for processing,    |
|         |                       | but the processing has not completed.       |
+---------+-----------------------+---------------------------------------------+
| 401     | Unauthorized          | You are not authorized to complete this     |
|         |                       | operation. This error can occur if the      |
|         |                       | request is submitted with an invalid        |
|         |                       | authentication token.                       |
+---------+-----------------------+---------------------------------------------+
| 404     | Not Found             | The requested item was not found.           |
+---------+-----------------------+---------------------------------------------+

Request
""""""""""""""""

This table shows the URI parameters for the request:

+-----------------------+---------+---------------------------------------------+
| Name                  | Type    | Description                                 |
+=======================+=========+=============================================+
| ``{TENANT_ID}``       | ​String | The account ID of the account owner.        |
+-----------------------+---------+---------------------------------------------+
| ``{zoneId}``          | ​UUID   | The zone ID of the zone import for which you|
|                       |         | wan to list the status.                     |
+-----------------------+---------+---------------------------------------------+

 
**Example: List a zone import, request**

.. code::  

    GET /v2/123456/zones/tasks/imports/a86dba58-0043-4cc6-a1bb-69d5e86f3ca3 HTTP/1.1
    Host: global.dns.rackspacecloud.com
    Accept: application/json

This operation does not accept a request body.

Response
""""""""""""""""

This table shows the body parameters for the response:

+--------------------------------+----------------------+----------------------+
|Name                            |Type                  |Description           |
+================================+======================+======================+
|**id**                          |Uuid                  |The ID of the zone    |
|                                |                      |import.               |
+--------------------------------+----------------------+----------------------+
|**zone_id**                     |Uuid                  |The ID of the zone.   |
+--------------------------------+----------------------+----------------------+
|**project_id**                  |Integer               |The project, account, |
|                                |                      |or tenant ID.         |
+--------------------------------+----------------------+----------------------+
|**message**                     |String                |A description of the  |
|                                |                      |zone import.          |
+--------------------------------+----------------------+----------------------+
|**version**                     |Integer               |The version of the    |
|                                |                      |zone import.          |
+--------------------------------+----------------------+----------------------+
|**created_at**                  |Datestamp             |The time stamp        |
|                                |                      |indicating the        |
|                                |                      |creation date of the  |
|                                |                      |zone import.          |
+--------------------------------+----------------------+----------------------+
|**updated_at**                  |Datestamp             |The time stamp        |
|                                |                      |indicating the date   |
|                                |                      |that the zone import  |
|                                |                      |was last updated.     |
+--------------------------------+----------------------+----------------------+
|**links**                       |Object                |A container with the  |
|                                |                      |links to the zone.    |
+--------------------------------+----------------------+----------------------+
|links.\ **self**                |Uuid                  |The link to the zone  |
|                                |                      |import (self).        |
+--------------------------------+----------------------+----------------------+
|links.\ **href**                |Uuid                  |The link to the zone  |
|                                |                      |import (href).        |
+--------------------------------+----------------------+----------------------+
 
**Example: List a zone import, response**

.. code::  

    HTTP/1.1 200 OK
    Content-Type: application/json

    {
        "status": "COMPLETE",
        "zone_id": "6625198b-d67d-47dc-8d29-f90bd60f3ac4",
        "links": {
            "self": "https://global.dns.rackspacecloud.com/v2/123456/zones/tasks/imports/074e805e-fe87-4cbb-b10b-21a06e215d41",
            "href": "https://global.dns.rackspacecloud.com/v2/123456/zones/6625198b-d67d-47dc-8d29-f90bd60f3ac4"
        },
        "created_at": "2015-05-08T15:43:42.000000",
        "updated_at": "2015-05-08T15:43:42.000000",
        "version": 2,
        "message": "example.com. imported",
        "project_id": "123456",
        "id": "074e805e-fe87-4cbb-b10b-21a06e215d41"
    }

Notice that the status is ``COMPLETE``, the message field shows that the zone was successfully 
imported, and the ``links`` field contains an ``href`` that pointsto the new zone.
