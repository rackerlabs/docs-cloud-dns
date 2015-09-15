
.. THIS OUTPUT IS GENERATED FROM THE WADL. DO NOT EDIT.

.. _delete-delete-ptr-records-v1.0-account-rdns-service-name:

Delete PTR records
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code::

    DELETE /v1.0/{account}/rdns/{service-name}

Deletes one or all PTR records associated with a Rackspace Cloud device. Use the optional ``ip`` query parameter to specify a specified record to delete. Omitting this parameter Deletes all PTR records associated with a specified device.

.. note::
   This call returns an asynchronous response. Refer to `Synchronous and Asynchronous Responses <http://docs.rackspace.com/cdns/api/v1.0/cdns-devguide/content/sync_asynch_responses.html>`__ for more details and examples of the way that asynchronous responses work.
   
   



This table shows the possible response codes for this operation:


+--------------------------+-------------------------+-------------------------+
|Response Code             |Name                     |Description              |
+==========================+=========================+=========================+
|202                       |Accepted                 |Request is accepted.     |
+--------------------------+-------------------------+-------------------------+
|400                       |Bad Request              |The request is missing   |
|                          |                         |one or more elements, or |
|                          |                         |the values of some       |
|                          |                         |elements are invalid.    |
+--------------------------+-------------------------+-------------------------+
|400 500                   |dnsFault                 |The DNS service has      |
|                          |                         |experienced a fault.     |
+--------------------------+-------------------------+-------------------------+
|401                       |Unauthorized             |You are not authorized   |
|                          |                         |to complete this         |
|                          |                         |operation. This error    |
|                          |                         |can occur if the request |
|                          |                         |is submitted with an     |
|                          |                         |invalid authentication   |
|                          |                         |token.                   |
+--------------------------+-------------------------+-------------------------+
|404                       |Not Found                |The requested item was   |
|                          |                         |not found.               |
+--------------------------+-------------------------+-------------------------+
|413                       |Over Limit               |The number of items      |
|                          |                         |returned is above the    |
|                          |                         |allowed limit.           |
+--------------------------+-------------------------+-------------------------+
|503                       |Service Unavailable      |The service is not       |
|                          |                         |available.               |
+--------------------------+-------------------------+-------------------------+


Request
""""""""""""""""




This table shows the URI parameters for the request:

+--------------------------+-------------------------+-------------------------+
|Name                      |Type                     |Description              |
+==========================+=========================+=========================+
|{account}                 |*(Required)*             |The tenant ID.           |
+--------------------------+-------------------------+-------------------------+
|{service-name}            |String *(Required)*      |Name of the Cloud        |
|                          |                         |service.                 |
+--------------------------+-------------------------+-------------------------+



This table shows the query parameters for the request:

+--------------------------+-------------------------+-------------------------+
|Name                      |Type                     |Description              |
+==========================+=========================+=========================+
|href                      |String *(Optional)*      |Device-resource-uri for  |
|                          |                         |the specified Cloud      |
|                          |                         |device.                  |
+--------------------------+-------------------------+-------------------------+
|ip                        |String *(Optional)*      |IP address for the       |
|                          |                         |specified Cloud device.  |
+--------------------------+-------------------------+-------------------------+




This operation does not accept a request body.




**Example Delete PTR records: XML request**


.. code::

    DELETE https://dns.api.rackspacecloud.com/v1.0/1234/rdns/cloudServersOpenStack?href=https://dfw.servers.api.rackspacecloud.com/v2/1234/servers/0987654321
    Accept: application/xml
    X-Auth-Token: ea85e6ac-baff-4a6c-bf43-848020ea3812
    Content-Type: application/xml
    Content-Length: 0
    


**Example Delete PTR records: JSON request**


.. code::

    DELETE https://dns.api.rackspacecloud.com/v1.0/1234/rdns/cloudServersOpenStack?href=https://dfw.servers.api.rackspacecloud.com/v2/1234/servers/0987654321
    Accept: application/json
    X-Auth-Token: ea85e6ac-baff-4a6c-bf43-848020ea3812
    Content-Type: application/json
    Content-Length: 0
    


**Example Delete PTR record: XML request**


.. code::

    DELETE https://dns.api.rackspacecloud.com/v1.0/1234/rdns/cloudServersOpenStack?href=https://dfw.servers.api.rackspacecloud.com/v2/1234/servers/0987654321&ip=2001:db8::6
    Accept: application/xml
    X-Auth-Token: ea85e6ac-baff-4a6c-bf43-848020ea3812
    Content-Type: application/xml
    Content-Length: 0
    


**Example Delete PTR record: JSON request**


.. code::

    DELETE https://dns.api.rackspacecloud.com/v1.0/1234/rdns/cloudServersOpenStack?href=https://dfw.servers.api.rackspacecloud.com/v2/1234/servers/0987654321&ip=2001:db8::6
    Accept: application/json
    X-Auth-Token: ea85e6ac-baff-4a6c-bf43-848020ea3812
    Content-Type: application/json
    Content-Length: 0
    


Response
""""""""""""""""










**Example Delete PTR records: XML response**


.. code::

    Status: 202 Accepted
    Date: Thu, 28 Jul 2011 21:54:21 GMT
    X-API-VERSION: 1.0.17
    Content-Type: application/xml
    Content-Length: 475
    
    <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
    <asyncresponse xmlns:ns2="http://www.w3.org/2005/Atom" xmlns="http://docs.rackspacecloud.com/dns/api/v1.0" xmlns:ns3="http://docs.rackspacecloud.com/dns/api/management/v1.0">
    <callbackUrl>https://dns.api.rackspacecloud.com/v1.0/440370/status/aad311e0-a465-4323-8d53-3d2f8ce5c372</callbackUrl>
    <jobId>aad311e0-a465-4323-8d53-3d2f8ce5c372</jobId>
        <requestUrl>https://dns.api.rackspacecloud.com/v1.0/440370/rdns/cloudServers?href=https://dfw.servers.api.rackspacecloud.com/v1.0/440370/servers/264111</requestUrl>
    <status>RUNNING</status>
    <verb>DELETE</verb>
    </asyncresponse>
    
    


**Example Delete PTR records: JSON response**


.. code::

    Status: 202 Accepted
    Date: Thu, 28 Jul 2011 21:54:21 GMT
    X-API-VERSION: 1.0.17
    Content-Type: application/json
    Content-Length: 376
    
    
    {
      "status": "RUNNING",
      "verb": "DELETE",
      "jobId": "aad311e0-a465-4323-8d53-3d2f8ce5c372",
      "callbackUrl": "https://dns.api.rackspacecloud.com/v1.0/440370/status/aad311e0-a465-4323-8d53-3d2f8ce5c372",
      "requestUrl": "https://dns.api.rackspacecloud.com/v1.0/440370/rdns/cloudServers?href=https://dfw.servers.api.rackspacecloud.com/v1.0/440370/servers/264111"
    }


**Example Delete PTR record: XML response**


.. code::

    Status: 202 Accepted
    Date: Thu, 28 Jul 2011 21:54:21 GMT
    X-API-VERSION: 1.0.17
    Content-Type: application/xml
    Content-Length: 475
    
    <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
    <asyncresponse xmlns:ns2="http://www.w3.org/2005/Atom" xmlns="http://docs.rackspacecloud.com/dns/api/v1.0" xmlns:ns3="http://docs.rackspacecloud.com/dns/api/management/v1.0">
    <callbackUrl>https://dns.api.rackspacecloud.com/v1.0/440370/status/aad311e0-a465-4323-8d53-3d2f8ce5c372</callbackUrl>
    <jobId>aad311e0-a465-4323-8d53-3d2f8ce5c372</jobId>
    <requestUrl>https://dns.api.rackspacecloud.com/v1.0/440370/rdns/cloudServers?href=https://dfw.servers.api.rackspacecloud.com/v1.0/440370/servers/264111</requestUrl>
    <status>RUNNING</status>
    <verb>DELETE</verb>
    </asyncresponse>
    
    
    


**Example Delete PTR record: JSON response**


.. code::

    Status: 202 Accepted
    Date: Thu, 28 Jul 2011 21:54:21 GMT
    X-API-VERSION: 1.0.17
    Content-Type: application/json
    Content-Length: 376
    
    
    {
      "status": "RUNNING",
      "verb": "DELETE",
      "jobId": "aad311e0-a465-4323-8d53-3d2f8ce5c372",
      "callbackUrl": "https://dns.api.rackspacecloud.com/v1.0/440370/status/aad311e0-a465-4323-8d53-3d2f8ce5c372",
      "requestUrl": "https://dns.api.rackspacecloud.com/v1.0/440370/rdns/cloudServers?href=https://dfw.servers.api.rackspacecloud.com/v1.0/440370/servers/264111"
    }

