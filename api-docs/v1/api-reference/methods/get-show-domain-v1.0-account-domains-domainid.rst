.. _get-show-domain-v1.0-account-domains-domainid:

Show domain
~~~~~~~~~~~

.. code::

    GET /v1.0/{account}/domains/{domainId}

Shows details for a specified domain. Displays details, as specified by the
``showRecords`` and ``showSubdomains`` parameters.

This call provides the detailed output for a specified domain configured and
associated with an account. This call is not capable of returning details for a
domain that has been deleted.

This call does not require a request body.

.. note::
   By default, returns a maximum of 100 items at a time if no ``limit`` is
   specified. To navigate the collection returned, the parameters ``limit`` and
   ``offset`` can be set in the URI (for example: ``limit=10 & offset=0`` ), as
   described in :ref:`Paginated collections<paginated-collections>`.

Two parameters are available to specify the information about subdomains and
records to be returned by the ``List domain details`` call:

* ``showRecords`` - if this parameter is set to ``true``, then information
   out records is returned; if this parameter is set to ``false``, then
   information about records is not returned.
* ``showSubdomains`` - if this parameter is set to ``true``, then information
   about subdomains is returned; if this parameter is set to ``false``, then
   information about subdomains is not returned.

The following examples show the parameter settings to return information for
both records and subdomains ( ``showSubdomains`` = ``true &`` ``showRecords`` =
``true`` ) for the ``List domain details`` call.

The examples also show the parameter settings to return basic information only,
without records or subdomains ( ``showRecords`` = ``false &``
``showSubdomains`` = ``false`` ) for the List domain details call.

This table shows the possible response codes for this operation:

+--------------------------+-------------------------+-------------------------+
|Response Code             |Name                     |Description              |
+==========================+=========================+=========================+
|200                       |Success                  |Request succeeded.       |
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
-------

This table shows the URI parameters for the request:

+--------------------------+-------------------------+-------------------------+
|Name                      |Type                     |Description              |
+==========================+=========================+=========================+
|{account}                 |String                   |The tenant ID.           |
+--------------------------+-------------------------+-------------------------+
|{domainId}                |String                   |ID for the domain.       |
+--------------------------+-------------------------+-------------------------+

This table shows the query parameters for the request:

+--------------------------+-------------------------+-------------------------+
|Name                      |Type                     |Description              |
+==========================+=========================+=========================+
|showRecords               |String                   |If showRecords is set to |
|                          |                         |true, information about  |
|                          |                         |records is returned. If  |
|                          |                         |showRecords is set to    |
|                          |                         |false, information about |
|                          |                         |records is not returned. |
+--------------------------+-------------------------+-------------------------+
|showSubdomains            |String                   |If showSubdomains is set |
|                          |                         |to true, information     |
|                          |                         |about subdomains is      |
|                          |                         |returned. If             |
|                          |                         |showSubdomains is set to |
|                          |                         |false, information about |
|                          |                         |subdomains is not        |
|                          |                         |returned.                |
+--------------------------+-------------------------+-------------------------+

This operation does not accept a request body.

**Example List domain details with records, no subdomains: XML request**

.. code::

   GET https://dns.api.rackspacecloud.com/v1.0/1234/domains/2725233?showRecords=true&showSubdomains=false
   Accept: application/xml
   X-Auth-Token: ea85e6ac-baff-4a6c-bf43-848020ea3812
   Content-Type: application/xml
   Content-Length: 0

**Example List domain details with records, no subdomains: JSON request**

.. code::

   GET https://dns.api.rackspacecloud.com/v1.0/1234/domains/2725233?showRecords=true&showSubdomains=false
   Accept: application/json
   X-Auth-Token: ea85e6ac-baff-4a6c-bf43-848020ea3812
   Content-Type: application/json
   Content-Length: 0

**Example List domain details with records and subdomains: XML request**

.. code::

   GET https://dns.api.rackspacecloud.com/v1.0/1234/domains/2725233?showRecords=true&showSubdomains=true
   Accept: application/xml
   X-Auth-Token: ea85e6ac-baff-4a6c-bf43-848020ea3812
   Content-Type: application/xml
   Content-Length: 0

**Example List domain details with records and subdomains: JSON request**

.. code::

   GET https://dns.api.rackspacecloud.com/v1.0/1234/domains/2725233?showRecords=true&showSubdomains=true
   Accept: application/json
   X-Auth-Token: ea85e6ac-baff-4a6c-bf43-848020ea3812
   Content-Type: application/json
   Content-Length: 0

**Example List domain details, no records, no subdomains: XML request**

.. code::

   GET https://dns.api.rackspacecloud.com/v1.0/1234/domains/2725233?showRecords=false&showSubdomains=false
   Accept: application/xml
   X-Auth-Token: ea85e6ac-baff-4a6c-bf43-848020ea3812
   Content-Type: application/xml
   Content-Length: 0

**Example List domain details, no records, no subdomains: JSON request**


.. code::

   GET https://dns.api.rackspacecloud.com/v1.0/1234/domains/2725233?showRecords=false&showSubdomains=false
   Accept: application/json
   X-Auth-Token: ea85e6ac-baff-4a6c-bf43-848020ea3812
   Content-Type: application/json
   Content-Length: 0

Response
--------

**Example List domain details with records, no subdomains: XML response**

.. code::

   Status: 200 OK
   Date: Thu, 28 Jul 2011 21:54:21 GMT
   X-API-VERSION: 1.0.17
   Content-Type: application/xml
   Content-Length: 1660

   <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
   <domain id="2725233" accountId="1234" name="example.com" ttl="3600" emailAddress="sample@rackspace.com" updated="2011-06-24T01:23:15Z" created="2011-06-24T01:12:51Z" comment="Optional domain comment..." xmlns:ns2="http://www.w3.org/2005/Atom" xmlns="http://docs.rackspacecloud.com/dns/api/v1.0" xmlns:ns3="http://docs.rackspacecloud.com/dns/api/management/v1.0">
       <nameservers>
           <nameserver name="ns.rackspace.com"/>
           <nameserver name="ns2.rackspace.com"/>
       </nameservers>
       <recordsList totalEntries="6">
           <record id="A-6817754" type="A" name="ftp.example.com" data="192.0.2.8" ttl="5771" updated="2011-05-19T08:07:08-05:00" created="2011-05-18T14:53:09-05:00"/>
           <record id="A-6822994" type="A" name="example.com" data="192.0.2.17" ttl="86400" updated="2011-06-24T01:12:52Z" created="2011-06-24T01:12:52Z"/>
           <record id="NS-6251982" type="NS" name="example.com" data="ns.rackspace.com" ttl="3600" updated="2011-06-24T01:12:51Z" created="2011-06-24T01:12:51Z"/>
           <record id="NS-6251983" type="NS" name="example.com" data="ns2.rackspace.com" ttl="3600" updated="2011-06-24T01:12:51Z" created="2011-06-24T01:12:51Z"/>
           <record id="MX-3151218" type="MX" name="example.com" data="mail.example.com" ttl="3600" priority="5" updated="2011-06-24T01:12:53Z" created="2011-06-24T01:12:53Z"/>
           <record id="CNAME-9778009" type="CNAME" name="www.example.com" data="example.com" ttl="5400" updated="2011-06-24T01:12:54Z" created="2011-06-24T01:12:54Z" comment="This is a comment on the CNAME record"/>
       </recordsList>
   </domain>

**Example List domain details with records, no subdomains: JSON response**

.. code::

   Status: 200 OK
   Date: Thu, 28 Jul 2011 21:54:21 GMT
   X-API-VERSION: 1.0.17
   Content-Type: application/json
   Content-Length: 1975

   {
     "name" : "example.com",
     "id" : 2725233,
     "comment" : "Optional domain comment...",
     "updated" : "2011-06-24T01:23:15.000+0000",
     "nameservers" : [ {
       "name" : "ns.rackspace.com"
     }, {
       "name" : "ns2.rackspace.com"
     } ],
     "accountId" : 1234,
     "recordsList" : {
       "totalEntries" : 6,
       "records" : [ {
         "name" : "ftp.example.com",
         "id" : "A-6817754",
         "type" : "A",
         "data" : "192.0.2.8",
         "updated" : "2011-05-19T13:07:08.000+0000",
         "ttl" : 5771,
         "created" : "2011-05-18T19:53:09.000+0000"
       }, {
         "name" : "example.com",
         "id" : "A-6822994",
         "type" : "A",
         "data" : "192.0.2.17",
         "updated" : "2011-06-24T01:12:52.000+0000",
         "ttl" : 86400,
         "created" : "2011-06-24T01:12:52.000+0000"
       }, {
         "name" : "example.com",
         "id" : "NS-6251982",
         "type" : "NS",
         "data" : "ns.rackspace.com",
         "updated" : "2011-06-24T01:12:51.000+0000",
         "ttl" : 3600,
         "created" : "2011-06-24T01:12:51.000+0000"
       }, {
         "name" : "example.com",
         "id" : "NS-6251983",
         "type" : "NS",
         "data" : "ns2.rackspace.com",
         "updated" : "2011-06-24T01:12:51.000+0000",
         "ttl" : 3600,
         "created" : "2011-06-24T01:12:51.000+0000"
       }, {
         "name" : "example.com",
         "priority" : 5,
         "id" : "MX-3151218",
         "type" : "MX",
         "data" : "mail.example.com",
         "updated" : "2011-06-24T01:12:53.000+0000",
         "ttl" : 3600,
         "created" : "2011-06-24T01:12:53.000+0000"
       }, {
         "name" : "www.example.com",
         "id" : "CNAME-9778009",
         "type" : "CNAME",
         "comment" : "This is a comment on the CNAME record",
         "data" : "example.com",
         "updated" : "2011-06-24T01:12:54.000+0000",
         "ttl" : 5400,
         "created" : "2011-06-24T01:12:54.000+0000"
       } ]
     },
     "ttl" : 3600,
     "emailAddress" : "sample@rackspace.com",
     "created" : "2011-06-24T01:12:51.000+0000"
   }

**Example List domain details with records and subdomains: XML response**

.. code::

   Status: 200 OK
   Date: Thu, 28 Jul 2011 21:54:21 GMT
   X-API-VERSION: 1.0.17
   Content-Type: application/xml
   Content-Length: 2421

   <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
   <domain id="2725233" accountId="1234" name="example.com" ttl="3600" emailAddress="sample@rackspace.com" updated="2011-06-24T01:23:15Z" created="2011-06-24T01:12:51Z" comment="Optional domain comment..." xmlns:ns2="http://www.w3.org/2005/Atom" xmlns="http://docs.rackspacecloud.com/dns/api/v1.0" xmlns:ns3="http://docs.rackspacecloud.com/dns/api/management/v1.0">
       <nameservers>
           <nameserver name="ns.rackspace.com"/>
           <nameserver name="ns2.rackspace.com"/>
       </nameservers>
       <recordsList totalEntries="6">
           <record id="A-6817754" type="A" name="ftp.example.com" data="192.0.2.8" ttl="5771" updated="2011-05-19T08:07:08-05:00" created="2011-05-18T14:53:09-05:00"/>
           <record id="A-6822994" type="A" name="example.com" data="192.0.2.17" ttl="86400" updated="2011-06-24T01:12:52Z" created="2011-06-24T01:12:52Z"/>
           <record id="NS-6251982" type="NS" name="example.com" data="ns.rackspace.com" ttl="3600" updated="2011-06-24T01:12:51Z" created="2011-06-24T01:12:51Z"/>
           <record id="NS-6251983" type="NS" name="example.com" data="ns2.rackspace.com" ttl="3600" updated="2011-06-24T01:12:51Z" created="2011-06-24T01:12:51Z"/>
           <record id="MX-3151218" type="MX" name="example.com" data="mail.example.com" ttl="3600" priority="5" updated="2011-06-24T01:12:53Z" created="2011-06-24T01:12:53Z"/>
           <record id="CNAME-9778009" type="CNAME" name="www.example.com" data="example.com" ttl="5400" updated="2011-06-24T01:12:54Z" created="2011-06-24T01:12:54Z" comment="This is a comment on the CNAME record"/>
       </recordsList>
       <subdomains totalEntries="4">
           <domain id="2725257" name="sub1.example.com" emailAddress="sample@rackspace.com" updated="2011-06-23T03:09:34Z" created="2011-06-23T03:09:33Z" comment="1st sample subdomain"/>
           <domain id="2725258" name="sub2.example.com" emailAddress="sample@rackspace.com" updated="2011-06-23T03:52:55Z" created="2011-06-23T03:52:55Z" comment="1st sample subdomain"/>
           <domain id="2725260" name="north.example.com" emailAddress="sample@rackspace.com" updated="2011-06-23T03:53:10Z" created="2011-06-23T03:53:09Z"/>
           <domain id="2725261" name="south.example.com" emailAddress="sample@rackspace.com" updated="2011-06-23T03:53:14Z" created="2011-06-23T03:53:14Z" comment="Final sample subdomain"/>
       </subdomains>
   </domain>

**Example List domain details with records and subdomains: JSON response**

.. code::

   Status: 200 OK
   Date: Thu, 28 Jul 2011 21:54:21 GMT
   X-API-VERSION: 1.0.17
   Content-Type: application/json
   Content-Length: 3020

   {
     "name" : "example.com",
     "id" : 2725233,
     "comment" : "Optional domain comment...",
     "updated" : "2011-06-24T01:23:15.000+0000",
     "nameservers" : [ {
       "name" : "ns.rackspace.com"
     }, {
       "name" : "ns2.rackspace.com"
     } ],
     "accountId" : 1234,
     "recordsList" : {
       "totalEntries" : 6,
       "records" : [ {
         "name" : "ftp.example.com",
         "id" : "A-6817754",
         "type" : "A",
         "data" : "192.0.2.8",
         "updated" : "2011-05-19T13:07:08.000+0000",
         "ttl" : 5771,
         "created" : "2011-05-18T19:53:09.000+0000"
       }, {
         "name" : "example.com",
         "id" : "A-6822994",
         "type" : "A",
         "data" : "192.0.2.17",
         "updated" : "2011-06-24T01:12:52.000+0000",
         "ttl" : 86400,
         "created" : "2011-06-24T01:12:52.000+0000"
       }, {
         "name" : "example.com",
         "id" : "NS-6251982",
         "type" : "NS",
         "data" : "ns.rackspace.com",
         "updated" : "2011-06-24T01:12:51.000+0000",
         "ttl" : 3600,
         "created" : "2011-06-24T01:12:51.000+0000"
       }, {
         "name" : "example.com",
         "id" : "NS-6251983",
         "type" : "NS",
         "data" : "ns2.rackspace.com",
         "updated" : "2011-06-24T01:12:51.000+0000",
         "ttl" : 3600,
         "created" : "2011-06-24T01:12:51.000+0000"
       }, {
         "name" : "example.com",
         "priority" : 5,
         "id" : "MX-3151218",
         "type" : "MX",
         "data" : "mail.example.com",
         "updated" : "2011-06-24T01:12:53.000+0000",
         "ttl" : 3600,
         "created" : "2011-06-24T01:12:53.000+0000"
       }, {
         "name" : "www.example.com",
         "id" : "CNAME-9778009",
         "type" : "CNAME",
         "comment" : "This is a comment on the CNAME record",
         "data" : "example.com",
         "updated" : "2011-06-24T01:12:54.000+0000",
         "ttl" : 5400,
         "created" : "2011-06-24T01:12:54.000+0000"
       } ]
     },
     "subdomains" : {
       "domains" : [ {
         "name" : "sub1.example.com",
         "id" : 2725257,
         "comment" : "1st sample subdomain",
         "updated" : "2011-06-23T03:09:34.000+0000",
         "emailAddress" : "sample@rackspace.com",
         "created" : "2011-06-23T03:09:33.000+0000"
       }, {
         "name" : "sub2.example.com",
         "id" : 2725258,
         "comment" : "1st sample subdomain",
         "updated" : "2011-06-23T03:52:55.000+0000",
         "emailAddress" : "sample@rackspace.com",
         "created" : "2011-06-23T03:52:55.000+0000"
       }, {
         "name" : "north.example.com",
         "id" : 2725260,
         "updated" : "2011-06-23T03:53:10.000+0000",
         "emailAddress" : "sample@rackspace.com",
         "created" : "2011-06-23T03:53:09.000+0000"
       }, {
         "name" : "south.example.com",
         "id" : 2725261,
         "comment" : "Final sample subdomain",
         "updated" : "2011-06-23T03:53:14.000+0000",
         "emailAddress" : "sample@rackspace.com",
         "created" : "2011-06-23T03:53:14.000+0000"
       } ],
       "totalEntries" : 4
     },
     "ttl" : 3600,
     "emailAddress" : "sample@rackspace.com",
     "created" : "2011-06-24T01:12:51.000+0000"
   }

**Example List domain details, no records, no subdomains: XML response**

.. code::

   Status: 200 OK
   Date: Thu, 28 Jul 2011 21:54:21 GMT
   X-API-VERSION: 1.0.17
   Content-Type: application/xml
   Content-Length: 570

   <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
   <domain id="2725233" accountId="1234" name="example.com" ttl="3600" emailAddress="sample@rackspace.com" updated="2011-06-24T01:23:15Z" created="2011-06-24T01:12:51Z" comment="Optional domain comment..." xmlns:ns2="http://www.w3.org/2005/Atom" xmlns="http://docs.rackspacecloud.com/dns/api/v1.0" xmlns:ns3="http://docs.rackspacecloud.com/dns/api/management/v1.0">
       <nameservers>
           <nameserver name="ns.rackspace.com"/>
           <nameserver name="ns2.rackspace.com"/>
       </nameservers>
   </domain>

**Example List domain details, no records, no subdomains: JSON response**

.. code::

   Status: 200 OK
   Date: Thu, 28 Jul 2011 21:54:21 GMT
   X-API-VERSION: 1.0.17
   Content-Type: application/json
   Content-Length: 375

   {
     "name" : "example.com",
     "id" : 2725233,
     "comment" : "Optional domain comment...",
     "updated" : "2011-06-24T01:23:15.000+0000",
     "nameservers" : [ {
       "name" : "ns.rackspace.com"
     }, {
       "name" : "ns2.rackspace.com"
     } ],
     "accountId" : 1234,
     "ttl" : 3600,
     "emailAddress" : "sample@rackspace.com",
     "created" : "2011-06-24T01:12:51.000+0000"
   }




