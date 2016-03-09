.. _GET_listExportedZone_v2__account_id__zones_tasks_exports__uuid_id__export_zones:

List an exported zone
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code::

    GET /v2/{$TENANT-ID}/zones/tasks/exports/{zoneId}/export

This operation lists an exported zone for the specified zone export ID. The link that is 
generated in the export field of an export resource can be followed to a DNS resource or 
an external resource. If the link is to a DNS endpoint, the zone file can be retrieved 
directly through the API by following that link.

.. important::

	To list an exported zone file, you set the ``content-type`` header to ``text/dns``. 

The following table shows the possible response codes for this operation.

+---------+-----------------------+---------------------------------------------+
| Response| Name                  | Description                                 |
| code    |                       |                                             |
+=========+=======================+=============================================+
| 200     | Accepted              | The request was accepted for processing,    |
|         |                       |  but the processing has not completed.      |
+---------+-----------------------+---------------------------------------------+
| 401     | Unauthorized          | You are not authorized to complete this     |
|         |                       | operation. This error can occur if the      |
|         |                       | request is submitted with an invalid        |
|         |                       | authentication token.                       |
+---------+-----------------------+---------------------------------------------+
| 403     | Forbidden             | The server did not find anything matching   |
|         |                       | the request URI.                            |
+---------+-----------------------+---------------------------------------------+
| 404     | Not Found             | The requested item was not found.           |
+---------+-----------------------+---------------------------------------------+

The following table shows the URI parameters for the request.

+-----------------------+---------+---------------------------------------------+
| Name                  | Type    | Description                                 |
+=======================+=========+=============================================+
| ``{$TENANT-ID}``      | ​String | The account ID of the account owner.        |
+-----------------------+---------+---------------------------------------------+
| ``{zoneId}``          | ​UUID   | The ID for the zone export to list.         |
+-----------------------+---------+---------------------------------------------+

 
**Example: List an exported zone, request**

.. code::  

    GET /v2/123456/zones/tasks/exports/8ec17fe1-d1f9-41b4-aa98-4eeb4c27b720/export HTTP/1.1
    Host: global.dns.rackspacecloud.com
    Accept: text/dns

This operation does not accept a request body.

 
**Example: List an exported zone, response**

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

Notice that the SOA and NS records are replaced with the DNS servers.

The body returned by this operation is an exported zone file.
