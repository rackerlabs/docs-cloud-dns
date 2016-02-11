.. _GET_listZoneImport_v2__account_id__zones_tasks_imports__zone_id__zones:

List a zone import
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code::

    GET /v2/{account_id}/zones/tasks/imports/{zone_id}

This call lists the status of a zone import by querying the uuid ID that was returned when 
the request was created. Objects will be returned that can be queried using the links in 
the ``links`` field.

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

This table shows the URI parameters for the list a zone import request:

+-----------------------+---------+---------------------------------------------+
| Name                  | Type    | Description                                 |
+=======================+=========+=============================================+
| ``{account_id}``      | ​String | The account ID of the owner of the          |
|                       |         | specified account.                          |
+-----------------------+---------+---------------------------------------------+
| ``{uuid_id}``         | ​String | The uuid ID for the specified zone import.  |
+-----------------------+---------+---------------------------------------------+

 
**Example List zone import request**

.. code::  

    GET /v2/1234/zones/tasks/imports/a86dba58-0043-4cc6-a1bb-69d5e86f3ca3 HTTP/1.1
    Host: 127.0.0.1:9001
    Accept: application/json

This operation does not accept a request body.

 
**Example List zone import response**

.. code::  

    HTTP/1.1 200 OK
    Content-Type: application/json

    {
        "status": "COMPLETE",
        "zone_id": "6625198b-d67d-47dc-8d29-f90bd60f3ac4",
        "links": {
            "self": "http://127.0.0.1:9001/v2/zones/tasks/imports/074e805e-fe87-4cbb-b10b-21a06e215d41",
            "href": "http://127.0.0.1:9001/v2/zones/6625198b-d67d-47dc-8d29-f90bd60f3ac4"
        },
        "created_at": "2015-05-08T15:43:42.000000",
        "updated_at": "2015-05-08T15:43:42.000000",
        "version": 2,
        "message": "example.com. imported",
        "project_id": "noauth-project",
        "id": "074e805e-fe87-4cbb-b10b-21a06e215d41"
    }

Notice that the status has been updated, the message field shows that the zone was successfully 
imported, and there now an ``href`` in the ``links`` field pointing to the new zone.
