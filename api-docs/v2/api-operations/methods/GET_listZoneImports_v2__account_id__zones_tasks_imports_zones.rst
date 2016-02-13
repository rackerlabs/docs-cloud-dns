.. _GET_listZoneImports_v2__account_id__zones_tasks_imports_zones:

List zone imports
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code::

    GET /v2/{account_id}/zones/tasks/imports

This call lists all of the zone imports created by this project. Objects will be returned 
that can be queried using the links in the ``links`` field.

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

This table shows the URI parameters for the list zone imports request:

+-----------------------+---------+---------------------------------------------+
| Name                  | Type    | Description                                 |
+=======================+=========+=============================================+
| ``{account_id}``      | ​String | The account ID of the owner of the          |
|                       |         | specified account.                          |
+-----------------------+---------+---------------------------------------------+

 
**Example List zone imports request**

.. code::  

    GET /v2/123456/zones/tasks/imports/ HTTP/1.1
    Host: global.dns.rackspacecloud.com
    Accept: application/json

This operation does not accept a request body.

 
**Example List zone imports response**

.. code::  

    HTTP/1.1 200 OK
    Content-Type: application/json

    {
        "imports": [
            {
                "status": "COMPLETE",
                "zone_id": "ea2fd415-dc6d-401c-a8af-90a89d7efcf9",
                "links": {
                    "self": "https://global.dns.rackspacecloud.com/v2/123456/zones/tasks/imports/fb47a23e-eb97-4c86-a3d4-f3e1a4ca9f5e",
                    "href": "https://global.dns.rackspacecloud.com/v2/123456/zones/ea2fd415-dc6d-401c-a8af-90a89d7efcf9"
                },
                "created_at": "2015-05-08T15:22:50.000000",
                "updated_at": "2015-05-08T15:22:50.000000",
                "version": 2,
                "message": "example.com. imported",
                "project_id": "noauth-project",
                "id": "fb47a23e-eb97-4c86-a3d4-f3e1a4ca9f5e"
            },
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
                "project_id": "noauth-project",
                "id": "074e805e-fe87-4cbb-b10b-21a06e215d41"
            }
        ],
        "links": {
            "self": "https://global.dns.rackspacecloud.com/v2/123456/zones/tasks/imports"
        },
        "metadata": {
            "total_count": 2
        }
    }
