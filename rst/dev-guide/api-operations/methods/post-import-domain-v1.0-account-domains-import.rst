
.. THIS OUTPUT IS GENERATED FROM THE WADL. DO NOT EDIT.

.. _post-import-domain-v1.0-account-domains-import:

Import domain
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code::

    POST /v1.0/{account}/domains/import

Imports a new domain with the configuration specified by the request.

.. note::
   This call returns an asynchronous response, as described in `Synchronous and Asynchronous Responses <http://docs.rackspace.com/cdns/api/v1.0/cdns-devguide/content/sync_asynch_responses.html>`__.
   
   

This call provisions a new DNS domain under the account specified by the BIND 9 formatted file configuration contents defined in the request object.  If the corresponding request cannot be fulfilled due to insufficient or invalid data, an ``HTTP`` 400 (Bad Request) error response will be returned with information regarding the nature of the failure in the body of the response. Failures in the validation process are non-recoverable and require the caller to correct the cause of the failure and ``POST`` the request again.

For all practical purposes, a successful Import domain call creates a domain, and is therefore similar in response to a Create domain call.

.. note::
   This process allows multiple records to be created along with the domain. This is an atomic operation, so if there is a failure in the creation of even a single record, the entire process will fail.
   
   

Ensure that the BIND 9 formatted file configuration contents are valid by adhering to the following rules: 

* Each record starts on a new line and on the first column. If a record will not fit on one line, use the BIND_9 line continuation convention where you put a left parenthesis and continue the one record on the next line and put a right parenthesis when the record ends. For example,
* The attribute values of a record must be separated by a single blank or tab. No other white space characters.
* If there are any NS records, the data field should not be dns1.stabletransit.com or dns2.stabletransit.com. They will result in "duplicate record" errors.




Not following the above rules strictly will result in an HTTP 400 (Bad Request) error response with messages such as the following: "The request could not be understood by the server due to malformed syntax."

.. note::
   
   
   *  If you attempt to import a domain that already exists, the API will return an exception saying that the domain already exists. This is the same behavior as when you attempt to create a domain that already exists.
   *  The domain can have a comment attribute specified in the import domain request, and that comment is transferred to the new domain. However the domain contents cannot have comments specified in them. For example, no record level comments can be used in the import domain request.
   *  The normal bind rules apply to any imported bind file, and in particular, records without a specified TTL will receive the domain TTL as the default. If the domain TTL is not specified, the SOA minTTL (3600 seconds) is used as the default instead.
   
   
   

.. note::
   The following examples show the final successful response for the asynchronous call.
   
   



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
|FIXME/@\ **contentType**  |String *(Required)*      |The content type for the |
|                          |                         |bind file. Must be       |
|                          |                         |specified as "BIND_9".   |
+--------------------------+-------------------------+-------------------------+
|FIXME/@\ **contents**     |String *(Required)*      |The valid configuration  |
|                          |                         |contents for the domain  |
|                          |                         |to be imported.          |
+--------------------------+-------------------------+-------------------------+





**Example Import domain: XML request**


.. code::

   POST https://dns.api.rackspacecloud.com/v1.0/1234/domains/import
   Accept: application/xml
   X-Auth-Token: ea85e6ac-baff-4a6c-bf43-848020ea3812
   Content-Type: application/xml
   Content-Length: 543
   
   <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
   <domains xmlns:ns2="http://www.w3.org/2005/Atom" xmlns="http://docs.rackspacecloud.com/dns/api/v1.0" xmlns:ns3="http://docs.rackspacecloud.com/dns/api/management/v1.0">
       <domain contentType="BIND_9">
           <contents>
   example.net. 3600 IN SOA dns1.stabletransit.com. sample@rackspace.com. 1308874739 3600 3600 3600 3600
   example.net. 86400 IN A 110.11.12.16
   example.net. 3600 IN MX 5 mail2.example.net.
   www.example.net. 5400 IN CNAME example.net.
   </contents>
       </domain>
   </domains>
   





**Example Import domain: JSON request**


.. code::

   POST https://dns.api.rackspacecloud.com/v1.0/1234/domains/import
   Accept: application/json
   X-Auth-Token: ea85e6ac-baff-4a6c-bf43-848020ea3812
   Content-Type: application/json
   Content-Length: 311
   
   {
     "domains" : [ {
       "contentType" : "BIND_9",
       "contents" : "\nexample.net. 3600 IN SOA dns1.stabletransit.com. sample@rackspace.com. 1308874739 3600 3600 3600 3600\nexample.net. 86400 IN A 110.11.12.16\nexample.net. 3600 IN MX 5 mail2.example.net.\nwww.example.net. 5400 IN CNAME example.net.\n"
     } ]
   }





Response
""""""""""""""""










**Example Import domain: XML response**


.. code::

   Status: 202 Accepted
   Date: Thu, 28 Jul 2011 21:54:21 GMT
   X-API-VERSION: 1.0.17
   Content-Type: application/xml
   Content-Length: 855
   
   <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
   <domains xmlns:ns2="http://www.w3.org/2005/Atom" xmlns="http://docs.rackspacecloud.com/dns/api/v1.0" xmlns:ns3="http://docs.rackspacecloud.com/dns/api/management/v1.0">
       <domain name="example.net" ttl="3600" emailAddress="sample@rackspace.com" comment="Optional domain comment...">
           <nameservers>
               <nameserver name="dns1.stabletransit.com"/>
               <nameserver name="dns2.stabletransit.com"/>
           </nameservers>
           <recordsList totalEntries="3">
               <record type="A" name="example.net" data="110.11.12.16" ttl="86400"/>
               <record type="MX" name="example.net" data="mail2.example.net" ttl="3600" priority="5"/>
               <record type="CNAME" name="www.example.net" data="example.net" ttl="5400"/>
           </recordsList>
       </domain>
   </domains>
   





**Example Import domain: JSON response**


.. code::

   Status: 202 Accepted
   Date: Thu, 28 Jul 2011 21:54:21 GMT
   X-API-VERSION: 1.0.17
   Content-Type: application/json
   Content-Length: 756
   
   {
     "domains" : [ {
       "name" : "example.net",
       "comment" : "Optional domain comment...",
       "nameservers" : [ {
         "name" : "dns1.stabletransit.com"
       }, {
         "name" : "dns2.stabletransit.com"
       } ],
       "recordsList" : {
         "totalEntries" : 3,
         "records" : [ {
           "name" : "example.net",
           "type" : "A",
           "data" : "110.11.12.16",
           "ttl" : 86400
         }, {
           "name" : "example.net",
           "priority" : 5,
           "type" : "MX",
           "data" : "mail2.example.net",
           "ttl" : 3600
         }, {
           "name" : "www.example.net",
           "type" : "CNAME",
           "data" : "example.net",
           "ttl" : 5400
         } ]
       },
       "ttl" : 3600,
       "emailAddress" : "sample@rackspace.com"
     } ]
   }




