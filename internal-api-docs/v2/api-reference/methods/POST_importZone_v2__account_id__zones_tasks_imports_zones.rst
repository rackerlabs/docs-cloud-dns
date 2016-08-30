.. _POST_importZone_v2__account_id__zones_tasks_imports_zones:

Create a zone import
--------------------

.. code::

    POST /v2/{TENANT_ID}/zones/tasks/imports

This operation imports a *zone file*. To import a zone file, you set the
``content-type`` header to ``text/dns``. An object is returned that can be
queried by using the ``self`` link in the ``links`` field.

.. important::

	The content type for this request is not json.  Instead, use
	``Content-type: text/dns``.

This table shows the possible response codes for this operation:

+---------+-----------------------+-------------------------------------------+
| Response| Name                  | Description                               |
| code    |                       |                                           |
+=========+=======================+===========================================+
| 202     | Accepted              | The request was accepted for              |
|         |                       | processing, but the processing has not    |
|         |                       | completed.                                |
+---------+-----------------------+-------------------------------------------+
| 415     | Unsupported Media     | The server won't service the              |
|         | Type                  | request because the entity of the request |
|         |                       | is in a format not supported by the       |
|         |                       | requested resource for the requested      |
|         |                       | method.                                   |
+---------+-----------------------+-------------------------------------------+

Request
^^^^^^^

This table shows the URI parameters for the request:

+-----------------------+---------+-------------------------------------------+
| Name                  | Type    | Description                               |
+=======================+=========+===========================================+
| ``{TENANT_ID}``       | ​String | The account ID of the account owner.      |
+-----------------------+---------+-------------------------------------------+


**Example: Create a zone import, request**

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

The body parameters for this operation are the contents of the zone file that you want to
import.

Response
^^^^^^^^

This table shows the body parameters for the response:

+--------------------------------+---------------------+----------------------+
|Name                            |Type                 |Description           |
+================================+=====================+======================+
|**id**                          |Uuid                 |The ID of the zone    |
|                                |                     |import.               |
+--------------------------------+---------------------+----------------------+
|**zone_id**                     |Uuid                 |The ID of the zone.   |
+--------------------------------+---------------------+----------------------+
|**project_id**                  |Integer              |The project, account, |
|                                |                     |or tenant ID.         |
+--------------------------------+---------------------+----------------------+
|**message**                     |String               |A description of the  |
|                                |                     |zone import.          |
+--------------------------------+---------------------+----------------------+
|**version**                     |Integer              |The version of the    |
|                                |                     |zone import.          |
+--------------------------------+---------------------+----------------------+
|**created_at**                  |Datestamp            |The time stamp        |
|                                |                     |indicating the        |
|                                |                     |creation date of the  |
|                                |                     |zone import.          |
+--------------------------------+---------------------+----------------------+
|**updated_at**                  |Datestamp            |The time stamp        |
|                                |                     |indicating the date   |
|                                |                     |that the zone import  |
|                                |                     |was last updated.     |
+--------------------------------+---------------------+----------------------+
|**links**                       |Object               |A container with the  |
|                                |                     |links to the zone.    |
+--------------------------------+---------------------+----------------------+
|links.\ **self**                |Uuid                 |The link to the zone  |
|                                |                     |import (self).        |
+--------------------------------+---------------------+----------------------+

**Example: Create a zone import, response**

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
