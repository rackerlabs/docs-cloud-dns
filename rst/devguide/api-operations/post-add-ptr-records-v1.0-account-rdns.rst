
.. THIS OUTPUT IS GENERATED FROM THE WADL. DO NOT EDIT.

=============================================================================
Add Ptr Records -  Rackspace Cloud DNS Developer Guide
=============================================================================

Add Ptr Records
~~~~~~~~~~~~~~~~~~~~~~~~~

`Request <post-add-ptr-records-v1.0-account-rdns.html#request>`__
`Response <post-add-ptr-records-v1.0-account-rdns.html#response>`__

.. code::

    POST /v1.0/{account}/rdns

Adds one or more PTR record records for a specified Cloud device.

.. note::
   This call returns an asynchronous response. Refer to `Synchronous and Asynchronous Responses <http://docs.rackspace.com/cdns/api/v1.0/cdns-devguide/content/sync_asynch_responses.html>`__ for more details and examples of the way that asynchronous responses work.
   
   

.. note::
   Notes 
   
   *  PTR records can only be added for Rackspace Cloud Servers and Load Balancers.
   *  ``id`` for the record must not be specified.
   
   
    
   
   *  For First Generation Cloud Servers, when the server is created, each public IPv4 address that comes with the server usually has a default PTR record already created for it. A request to list the PTR records associated with the server should return any PTR records for the server. If a default PTR record exists, the default PTR record can be appropriately modified or deleted and an appropriate PTR record created.
      
      If an attempt to add a PTR record for the public IP address of a newly created First Generation Cloud Server results in a 400 Bad Request error message, that is an indication that a default PTR record for the IP address already exists.
   
   
    
   
   *  Adding PTR records for IPv6 addresses is supported only for Next Generation Cloud Servers.
   
   
   

Notice in the requests below that the service and device resource URI are specified respectively as the ``rel`` and ``href`` attributes of the link element, as follows:



*  ``rel`` – this is the name of the service (as provided in the serviceCatalog from Identity) from where the device was created.
*  ``href`` – this is the URL to the device for which the PTR record is associated. It was returned when the device was created and it uniquely identifies the device.
*  ``content`` – this is currently a place holder for possible future use.




This table shows the possible response codes for this operation:


+--------------------------+-------------------------+-------------------------+
|Response Code             |Name                     |Description              |
+==========================+=========================+=========================+
|200                       |Success                  |Request succeeded.       |
+--------------------------+-------------------------+-------------------------+
|400 500                   |dnsFault                 |The DNS service has      |
|                          |                         |experienced a fault.     |
+--------------------------+-------------------------+-------------------------+
|503                       |Service Unavailable      |The service is not       |
|                          |                         |available.               |
+--------------------------+-------------------------+-------------------------+
|401                       |Unauthorized             |You are not authorized   |
|                          |                         |to complete this         |
|                          |                         |operation. This error    |
|                          |                         |can occur if the request |
|                          |                         |is submitted with an     |
|                          |                         |invalid authentication   |
|                          |                         |token.                   |
+--------------------------+-------------------------+-------------------------+
|400                       |Bad Request              |The request is missing   |
|                          |                         |one or more elements, or |
|                          |                         |the values of some       |
|                          |                         |elements are invalid.    |
+--------------------------+-------------------------+-------------------------+
|404                       |Not Found                |The requested item was   |
|                          |                         |not found.               |
+--------------------------+-------------------------+-------------------------+
|413                       |Over Limit               |The number of items      |
|                          |                         |returned is above the    |
|                          |                         |allowed limit.           |
+--------------------------+-------------------------+-------------------------+


Request
^^^^^^^^^^^^^^^^^

This table shows the URI parameters for the request:

+--------------------------+-------------------------+-------------------------+
|Name                      |Type                     |Description              |
+==========================+=========================+=========================+
|X-Auth-Token              |xs:string *(Required)*   |Arbitrary character      |
|                          |                         |string generated by the  |
|                          |                         |authentication service   |
|                          |                         |in response to valid     |
|                          |                         |credentials.             |
+--------------------------+-------------------------+-------------------------+
|{account}                 |*(Required)*             |The tenant ID.           |
+--------------------------+-------------------------+-------------------------+





This table shows the body parameters for the request:

+--------------------------+-------------------------+-------------------------+
|Name                      |Type                     |Description              |
+==========================+=========================+=========================+
|type                      |xs:string *(Required)*   |The record type as       |
|                          |                         |``PTR``.                 |
+--------------------------+-------------------------+-------------------------+
|name                      |xs:string *(Required)*   |The name for the domain  |
|                          |                         |or subdomain. Must be a  |
|                          |                         |valid domain name.       |
+--------------------------+-------------------------+-------------------------+
|data                      |xs:string *(Required)*   |The data field for PTR   |
|                          |                         |records must be a valid  |
|                          |                         |IPv4 or IPv6 IP address. |
+--------------------------+-------------------------+-------------------------+
|ttl                       |xs:string *(Required)*   |If specified, must be    |
|                          |                         |greater than or equal to |
|                          |                         |300. Defaults to 3600 if |
|                          |                         |no TTL is specified.     |
+--------------------------+-------------------------+-------------------------+
|comment                   |xs:string *(Required)*   |If included, its length  |
|                          |                         |must be less than or     |
|                          |                         |equal to 160 characters. |
+--------------------------+-------------------------+-------------------------+





**Example Add PTR record: XML request**


.. code::

    POST https://dns.api.rackspacecloud.com/v1.0/1234/rdns
    Accept: application/xml
    X-Auth-Token: ea85e6ac-baff-4a6c-bf43-848020ea3812
    Content-Type: application/xml
    Content-Length: 554
    
    <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
    <rdns xmlns:ns2="http://www.w3.org/2005/Atom" xmlns="http://docs.rackspacecloud.com/dns/api/v1.0" xmlns:ns3="http://docs.rackspacecloud.com/dns/api/management/v1.0">
        <ns2:link href="https://dfw.servers.api.rackspacecloud.com/v2/1234/servers/0987654321" rel="cloudServersOpenStack"></ns2:link>
        <recordsList>
            <record type="PTR" name="example.com" data="192.0.2.7" ttl="56000"/>
            <record type="PTR" name="example.com" data="2001:db8::7" ttl="56000"/>
        </recordsList>
    </rdns>
    


**Example Add PTR record: JSON request**


.. code::

    POST https://dns.api.rackspacecloud.com/v1.0/1234/rdns
    Accept: application/json
    X-Auth-Token: ea85e6ac-baff-4a6c-bf43-848020ea3812
    Content-Type: application/json
    Content-Length: 426
    
    {
      "recordsList" : {
        "records" : [ {
          "name" : "example.com",
          "type" : "PTR",
          "data" : "192.0.2.7",
          "ttl" : 56000
        }, {
          "name" : "example.com",
          "type" : "PTR",
          "data" : "2001:db8::7",
          "ttl" : 56000
        } ]
      },
      "link" : {
        "content" : "",
        "href" : "https://dfw.servers.api.rackspacecloud.com/v2/1234/servers/0987654321",
        "rel" : "cloudServersOpenStack"
      }
    }


Response
^^^^^^^^^^^^^^^^^^





**Example Add PTR record: XML response**


.. code::

    Status: 200 OK
    Date: Thu, 28 Jul 2011 21:54:21 GMT
    X-API-VERSION: 1.0.17
    Content-Type: application/xml
    Content-Length: 710
    
    <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
    <rdns xmlns:ns2="http://www.w3.org/2005/Atom" xmlns="http://docs.rackspacecloud.com/dns/api/v1.0" xmlns:ns3="http://docs.rackspacecloud.com/dns/api/management/v1.0">
        <ns2:link href="https://dfw.servers.api.rackspacecloud.com/v2/1234/servers/0987654321" rel="cloudServersOpenStack"></ns2:link>
        <recordsList>
            <record id="PTR-000002" type="PTR" name="example.com" data="192.0.2.7" ttl="56000" updated="2011-09-24T01:12:51Z" created="2011-09-24T01:12:51Z"/>
            <record id="PTR-000003" type="PTR" name="example.com" data="2001:db8::7" ttl="56000" updated="2011-09-24T01:12:51Z" created="2011-09-24T01:12:51Z"/>
        </recordsList>
    </rdns>
    


**Example Add PTR record: JSON response**


.. code::

    Status: 200 OK
    Date: Thu, 28 Jul 2011 21:54:21 GMT
    X-API-VERSION: 1.0.17
    Content-Type: application/json
    Content-Length: 680
    
    {
      "recordsList" : {
        "records" : [ {
          "name" : "example.com",
          "id" : "PTR-000002",
          "type" : "PTR",
          "data" : "192.0.2.7",
          "updated" : "2011-09-24T01:12:51.000+0000",
          "ttl" : 56000,
          "created" : "2011-09-24T01:12:51.000+0000"
        }, {
          "name" : "example.com",
          "id" : "PTR-000003",
          "type" : "PTR",
          "data" : "2001:db8::7",
          "updated" : "2011-09-24T01:12:51.000+0000",
          "ttl" : 56000,
          "created" : "2011-09-24T01:12:51.000+0000"
        } ]
      },
      "link" : {
        "content" : "",
        "href" : "https://dfw.servers.api.rackspacecloud.com/v2/1234/servers/0987654321",
        "rel" : "cloudServersOpenStack"
      }
    }

