.. _POST_importZone_v2__account_id__zones_tasks_imports_zones:

Create a zone import
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code::

    POST /v2/{TENANT_ID}/zones/tasks/imports

This call imports a zonefile. To import a zonefile, set the Content-type to ``text/dns``. 
The **zoneextractor.py** tool in the ``contrib`` folder can generate zonefiles that are 
suitable for DNS (without any ``$INCLUDE`` statements for example). An object will be 
returned that can be queried using the ``self`` link in the ``links`` field.

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

This table shows the URI parameters for the create a zone import
request:

+-----------------------+---------+---------------------------------------------+
| Name                  | Type    | Description                                 |
+=======================+=========+=============================================+
| ``{TENANT_ID}``       | ​String | The account ID of the owner of the          |
|                       |         | specified account.                          |
+-----------------------+---------+---------------------------------------------+

 
**Example Create zone import request**

.. code::  

    POST /v2/123456/zones/tasks/imports HTTP/1.1
    Host: global.dns.rackspacecloud.com
    Content-type: text/dns

    $ORIGIN example.com.
    example.com. 42 IN SOA ns.example.com. nsadmin.example.com. 42 42 42 42 42
    example.com. 42 IN NS ns.example.com.
    example.com. 42 IN MX 10 mail.example.com.
    ns.example.com. 42 IN A 10.0.0.1
    mail.example.com. 42 IN A 10.0.0.2

This operation does not accept a request body.

 
**Example Create zone import response**

.. code::  

    HTTP/1.1 201 Created
    Content-Type: application/json

    {
        "status": "PENDING",
        "zone_id": null,
        "links": {
            "self": "https://global.dns.rackspacecloud.com/v2/123456/zones/tasks/imports/074e805e-fe87-4cbb-b10b-21a06e215d41"
        },
        "created_at": "2015-05-08T15:43:42.000000",
        "updated_at": null,
        "version": 1,
        "message": null,
        "project_id": "123456",
        "id": "074e805e-fe87-4cbb-b10b-21a06e215d41"
    }
