
.. THIS OUTPUT IS GENERATED FROM THE WADL. DO NOT EDIT.

.. _post-create-domain-v1.0-account-domains:

Create domain
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code::

    POST /v1.0/{account}/domains

Creates a domain with the configuration defined by the request.

.. note::
   This call returns an asynchronous response. Refer to 
   :rax-devdocs:`Synchronous and asynchronous responses 
   <cloud-dns/v1/developer-guide/#document-general-api-info/synchronous-and-asynchronous-responses>`
   for more details and examples of the way that asynchronous responses work. 
   
   

.. note::
   Subdomains are also created the same way as domains.
   
   

This call provisions one or more new DNS domains under the account specified, based on the configuration defined in the request object. If the corresponding request cannot be fulfilled due to insufficient or invalid data, an ``HTTP`` 400 (Bad Request) error response will be returned with information regarding the nature of the failure in the body of the response. Failures in the validation process are non-recoverable and require the caller to correct the cause of the failure and ``POST`` the request again. 

.. note::
   
   
   *  Refer to :rax-devdocs:`DNS propagation <cloud-dns/v1/developer-guide/#document-general-api-info/dns-propagation>`
      for information about DNS propagation.
   *  If you attempt to create a domain that already exists, the API will return an exception saying that the domain already exists.
   *  This process allows multiple records to be created along with the domain. This is an atomic operation: if there is a failure in creation of even a single record, the entire process will fail.
   *  When a domain is created, and no Time To Live (TTL) is specified, the SOA minTTL (3600 seconds) is used as the default. When a record is added without a specified TTL, it will receive the domain TTL by default. When the domain and/or record TTL is supplied by the user, either via a create or update call, the TTL values must be 300 seconds or more.
   *  Subdomains are managed in separate zone files in the DNS system and will add some overhead to domain management.
   
   
   

The following examples show the Create domains requests:

.. note::
   The following examples show the initial 202 Accepted response for the asynchronous call and indicate that the task has been accepted for processing. Refer to 
   :rax-devdocs:`Synchronous and asynchronous responses 
   <cloud-dns/v1/developer-guide/#document-general-api-info/synchronous-and-asynchronous-responses>`
   for a description of how the asynchronous call works. 
   See 
   <http://docs.rackspace.com/cdns/api/v1.0/cdns-getting-started/content/Create_Domain.html>`__ for a detailed example of processing the Create domain call, including the final successful responses for create domain.
   
   



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
|409                       |Already Exists           |The item already exists. |
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


This table shows the header parameters for the request:

+--------------------------+-------------------------+-------------------------+
|Name                      |Type                     |Description              |
+==========================+=========================+=========================+
|X-Auth-Token              |String *(Required)*      |Arbitrary character      |
|                          |                         |string generated by the  |
|                          |                         |authentication service   |
|                          |                         |in response to valid     |
|                          |                         |credentials.             |
+--------------------------+-------------------------+-------------------------+




This table shows the URI parameters for the request:

+--------------------------+-------------------------+-------------------------+
|Name                      |Type                     |Description              |
+==========================+=========================+=========================+
|{account}                 |String *(Required)*      |The tenant ID.           |
+--------------------------+-------------------------+-------------------------+





This table shows the body parameters for the request:

+--------------------------+-------------------------+-------------------------+
|Name                      |Type                     |Description              |
+==========================+=========================+=========================+
|domains[*].\ **name**     |String *(Required)*      |The name for the domain  |
|                          |                         |or subdomain. Must be a  |
|                          |                         |valid domain name.       |
+--------------------------+-------------------------+-------------------------+
|domains[*].\              |String *(Required)*      |Email address to use for |
|**emailAddress**          |                         |contacting the domain    |
|                          |                         |administrator.           |
+--------------------------+-------------------------+-------------------------+
|domains[*].\ **ttl**      |String *(Optional)*      |If specified, must be    |
|                          |                         |greater than or equal to |
|                          |                         |300. The default value,  |
|                          |                         |if not specified, is     |
|                          |                         |``3600``.                |
+--------------------------+-------------------------+-------------------------+
|domains[*].\ **comment**  |String *(Optional)*      |If included, its length  |
|                          |                         |must be less than or     |
|                          |                         |equal to 160 characters. |
+--------------------------+-------------------------+-------------------------+





**Example Create domains: XML request**


.. code::

   POST https://dns.api.rackspacecloud.com/v1.0/1234/domains
   Accept: application/xml
   X-Auth-Token: ea85e6ac-baff-4a6c-bf43-848020ea3812
   Content-Type: application/xml
   Content-Length: 1460
   
   <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
   <domains xmlns:ns2="http://www.w3.org/2005/Atom" xmlns="http://docs.rackspacecloud.com/dns/api/v1.0" xmlns:ns3="http://docs.rackspacecloud.com/dns/api/management/v1.0">
       <domain name="example.com" ttl="3600" emailAddress="sample@rackspace.com" comment="Optional domain comment...">
           <recordsList>
               <record type="A" name="ftp.example.com" data="192.0.2.8" ttl="5771"/>
               <record type="A" name="example.com" data="192.0.2.17" ttl="86400"/>
               <record type="NS" name="example.com" data="dns1.stabletransit.com" ttl="3600"/>
               <record type="NS" name="example.com" data="dns2.stabletransit.com" ttl="3600"/>
               <record type="MX" name="example.com" data="mail.example.com" ttl="3600" priority="5"/>
               <record type="CNAME" name="www.example.com" data="example.com" ttl="5400" comment="This is a comment on the CNAME record"/>
           </recordsList>
           <subdomains>
               <domain name="sub1.example.com" emailAddress="sample@rackspace.com" comment="1st sample subdomain"/>
               <domain name="sub2.example.com" emailAddress="sample@rackspace.com" comment="1st sample subdomain"/>
               <domain name="north.example.com" emailAddress="sample@rackspace.com"/>
               <domain name="south.example.com" emailAddress="sample@rackspace.com" comment="Final sample subdomain"/>
           </subdomains>
       </domain>
   </domains>
   





**Example Create domains: JSON request**


.. code::

   POST https://dns.api.rackspacecloud.com/v1.0/1234/domains
   Accept: application/json
   X-Auth-Token: ea85e6ac-baff-4a6c-bf43-848020ea3812
   Content-Type: application/json
   Content-Length: 1615
   
   {
     "domains" : [ {
       "name" : "example.com",
       "comment" : "Optional domain comment...",
       "recordsList" : {
         "records" : [ {
           "name" : "ftp.example.com",
           "type" : "A",
           "data" : "192.0.2.8",
           "ttl" : 5771
         }, {
           "name" : "example.com",
           "type" : "A",
           "data" : "192.0.2.17",
           "ttl" : 86400
         }, {
           "name" : "example.com",
           "type" : "NS",
           "data" : "dns1.stabletransit.com",
           "ttl" : 3600
         }, {
           "name" : "example.com",
           "type" : "NS",
           "data" : "dns2.stabletransit.com",
           "ttl" : 3600
         }, {
           "name" : "example.com",
           "priority" : 5,
           "type" : "MX",
           "data" : "mail.example.com",
           "ttl" : 3600
         }, {
           "name" : "www.example.com",
           "type" : "CNAME",
           "comment" : "This is a comment on the CNAME record",
           "data" : "example.com",
           "ttl" : 5400
         } ]
       },
       "subdomains" : {
         "domains" : [ {
           "name" : "sub1.example.com",
           "comment" : "1st sample subdomain",
           "emailAddress" : "sample@rackspace.com"
         }, {
           "name" : "sub2.example.com",
           "comment" : "1st sample subdomain",
           "emailAddress" : "sample@rackspace.com"
         }, {
           "name" : "north.example.com",
           "emailAddress" : "sample@rackspace.com"
         }, {
           "name" : "south.example.com",
           "comment" : "Final sample subdomain",
           "emailAddress" : "sample@rackspace.com"
         } ]
       },
       "ttl" : 3600,
       "emailAddress" : "sample@rackspace.com"
     } ]
   }





Response
""""""""""""""""










**Example Create domains: XML response**


.. code::

   Status: 202 Accepted
   Date: Thu, 28 Jul 2011 21:54:21 GMT
   X-API-VERSION: 1.0.17
   Content-Type: application/xml
   Content-Length: 1636
   
   <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
   <domains totalEntries="114" xmlns:ns2="http://www.w3.org/2005/Atom" xmlns="http://docs.rackspacecloud.com/dns/api/v1.0" xmlns:ns3="http://docs.rackspacecloud.com/dns/api/management/v1.0">
       <domain name="example.com" ttl="3600" emailAddress="sample@rackspace.com" comment="Optional domain comment...">
           <nameservers>
               <nameserver name="dns1.stabletransit.com"/>
               <nameserver name="dns2.stabletransit.com"/>
           </nameservers>
           <recordsList>
               <record type="A" name="ftp.example.com" data="192.0.2.8" ttl="5771"/>
               <record type="A" name="example.com" data="192.0.2.17" ttl="86400"/>
               <record type="NS" name="example.com" data="dns1.stabletransit.com" ttl="3600"/>
               <record type="NS" name="example.com" data="dns2.stabletransit.com" ttl="3600"/>
               <record type="MX" name="example.com" data="mail.example.com" ttl="3600" priority="5"/>
               <record type="CNAME" name="www.example.com" data="example.com" ttl="5400" comment="This is a comment on the CNAME record"/>
           </recordsList>
           <subdomains>
               <domain name="sub1.example.com" emailAddress="sample@rackspace.com" comment="1st sample subdomain"/>
               <domain name="sub2.example.com" emailAddress="sample@rackspace.com" comment="1st sample subdomain"/>
               <domain name="north.example.com" emailAddress="sample@rackspace.com"/>
               <domain name="south.example.com" emailAddress="sample@rackspace.com" comment="Final sample subdomain"/>
           </subdomains>
       </domain>
   </domains>
   





**Example Create domains: JSON response**


.. code::

   Status: 202 Accepted
   Date: Thu, 28 Jul 2011 21:54:21 GMT
   X-API-VERSION: 1.0.17
   Content-Type: application/json
   Content-Length: 1761
   
   {
     "domains" : [ {
       "name" : "example.com",
       "comment" : "Optional domain comment...",
       "nameservers" : [ {
         "name" : "dns1.stabletransit.com"
       }, {
         "name" : "dns2.stabletransit.com"
       } ],
       "recordsList" : {
         "records" : [ {
           "name" : "ftp.example.com",
           "type" : "A",
           "data" : "192.0.2.8",
           "ttl" : 5771
         }, {
           "name" : "example.com",
           "type" : "A",
           "data" : "192.0.2.17",
           "ttl" : 86400
         }, {
           "name" : "example.com",
           "type" : "NS",
           "data" : "dns1.stabletransit.com",
           "ttl" : 3600
         }, {
           "name" : "example.com",
           "type" : "NS",
           "data" : "dns2.stabletransit.com",
           "ttl" : 3600
         }, {
           "name" : "example.com",
           "priority" : 5,
           "type" : "MX",
           "data" : "mail.example.com",
           "ttl" : 3600
         }, {
           "name" : "www.example.com",
           "type" : "CNAME",
           "comment" : "This is a comment on the CNAME record",
           "data" : "example.com",
           "ttl" : 5400
         } ]
       },
       "subdomains" : {
         "domains" : [ {
           "name" : "sub1.example.com",
           "comment" : "1st sample subdomain",
           "emailAddress" : "sample@rackspace.com"
         }, {
           "name" : "sub2.example.com",
           "comment" : "1st sample subdomain",
           "emailAddress" : "sample@rackspace.com"
         }, {
           "name" : "north.example.com",
           "emailAddress" : "sample@rackspace.com"
         }, {
           "name" : "south.example.com",
           "comment" : "Final sample subdomain",
           "emailAddress" : "sample@rackspace.com"
         } ]
       },
       "ttl" : 3600,
       "emailAddress" : "sample@rackspace.com"
     } ],
     "totalEntries" : 114
   }




