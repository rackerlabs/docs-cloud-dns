.. _GET_listExportedZone_v2__account_id__zones_tasks_exports__uuid_id__export_zones:

List exported zone
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code::

    GET /v2/{$TENANT-ID}/zones/tasks/exports/{uuid_id}/export

This call lists an exported zone for the specified zone export uuid ID. The link that is 
generated in the export field of an export resource can be followed to a DNS resource, or 
an external resource. If the link is to a DNS endpoint, the zonefile can be retrieved 
directly through the API by following that link.

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

This table shows the URI parameters for the list exported zone request:

+-----------------------+---------+---------------------------------------------+
| Name                  | Type    | Description                                 |
+=======================+=========+=============================================+
| ``{$TENANT-ID}``      | ​String | The account ID of the owner of the          |
|                       |         | specified account.                          |
+-----------------------+---------+---------------------------------------------+
| ``{uuid_id}``         | ​String | The uuid ID for the specified zone export.  |
+-----------------------+---------+---------------------------------------------+

 
**Example List exported zone request**

.. code::  

    GET /v2/123456/zones/tasks/exports/8ec17fe1-d1f9-41b4-aa98-4eeb4c27b720/export HTTP/1.1
    Host: global.dns.rackspacecloud.com
    Accept: text/dns

This operation does not accept a request body.

 
**Example List exported zone response**

.. code::  

    HTTP/1.1 200 OK
    Content-Type: text/dns

    $ORIGIN example.com.
    $TTL 42

    example.com. IN SOA ns.rackspace.com. nsadmin.example.com. (
        1394213803 ; serial
        3600 ; refresh
        600 ; retry
        86400 ; expire
        3600 ; minimum
    )

    example.com. IN NS ns.rackspace.com.
    example.com.  IN MX 10 mail.example.com.
    ns.example.com.  IN A  10.0.0.1
    mail.example.com.  IN A  10.0.0.2

Notice how the SOA and NS records are replaced with the DNS server(s).

This operation does not return a response body.
