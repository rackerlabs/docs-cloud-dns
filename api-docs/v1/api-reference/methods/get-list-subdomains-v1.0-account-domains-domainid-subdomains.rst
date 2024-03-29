.. _get-list-subdomains-v1.0-account-domains-domainid-subdomains:

List subdomains
~~~~~~~~~~~~~~~

.. code::

    GET /v1.0/{account}/domains/{domainId}/subdomains

Lists domains that are subdomains of the specified domain.

This call provides a list of all DNS domains that are subdomains for a
specified domain. The resulting list is flat, and does not break the domains
down hierarchically by subdomain.

.. note::
   By default, returns a maximum of 100 items at a time if no ``limit`` is
   specified. To navigate the collection returned, the parameters ``limit`` and
   ``offset`` can be set in the URI (for example: ``limit=10 & offset=0`` ).
   Refer to
   :ref:`Paginated collections<paginated-collections>`.

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

This table shows the header parameters for the request:

+--------------------------+-------------------------+-------------------------+
|Name                      |Type                     |Description              |
+==========================+=========================+=========================+
|X-Auth-Token              |String                   |Arbitrary character      |
|                          |                         |string generated by the  |
|                          |                         |authentication service   |
|                          |                         |in response to valid     |
|                          |                         |credentials.             |
+--------------------------+-------------------------+-------------------------+

This table shows the URI parameters for the request:

+--------------------------+-------------------------+-------------------------+
|Name                      |Type                     |Description              |
+==========================+=========================+=========================+
|{account}                 |String                   |The tenant ID.           |
+--------------------------+-------------------------+-------------------------+
|{domainId}                |String                   |ID for the domain.       |
+--------------------------+-------------------------+-------------------------+

This operation does not accept a request body.

**Example List subdomains: XML request**

.. code::

   GET https://dns.api.rackspacecloud.com/v1.0/1234/domains/2725233/subdomains
   Accept: application/xml
   X-Auth-Token: ea85e6ac-baff-4a6c-bf43-848020ea3812
   Content-Type: application/xml
   Content-Length: 0

**Example List subdomains: JSON request**

.. code::

   GET https://dns.api.rackspacecloud.com/v1.0/1234/domains/2725233/subdomains
   Accept: application/json
   X-Auth-Token: ea85e6ac-baff-4a6c-bf43-848020ea3812
   Content-Type: application/json
   Content-Length: 0

Response
--------

**Example List subdomains: XML response**

.. code::

   Status: 200 OK
   Date: Thu, 28 Jul 2011 21:54:21 GMT
   X-API-VERSION: 1.0.17
   Content-Type: application/xml
   Content-Length: 952

   <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
   <subdomains totalEntries="4" xmlns:ns2="http://www.w3.org/2005/Atom" xmlns="http://docs.rackspacecloud.com/dns/api/v1.0" xmlns:ns3="http://docs.rackspacecloud.com/dns/api/management/v1.0">
       <domain id="2725257" name="sub1.example.com" emailAddress="sample@rackspace.com" updated="2011-06-23T03:09:34Z" created="2011-06-23T03:09:33Z" comment="1st sample subdomain"/>
       <domain id="2725258" name="sub2.example.com" emailAddress="sample@rackspace.com" updated="2011-06-23T03:52:55Z" created="2011-06-23T03:52:55Z" comment="1st sample subdomain"/>
       <domain id="2725260" name="north.example.com" emailAddress="sample@rackspace.com" updated="2011-06-23T03:53:10Z" created="2011-06-23T03:53:09Z"/>
       <domain id="2725261" name="south.example.com" emailAddress="sample@rackspace.com" updated="2011-06-23T03:53:14Z" created="2011-06-23T03:53:14Z" comment="Final sample subdomain"/>
   </subdomains>

**Example List subdomains: JSON response**

.. code::

   Status: 200 OK
   Date: Thu, 28 Jul 2011 21:54:21 GMT
   X-API-VERSION: 1.0.17
   Content-Type: application/json
   Content-Length: 966

   {
     "domains" : [ {
       "name" : "sub1.example.com",
       "id" : "2725257",
       "comment" : "1st sample subdomain",
       "updated" : "2011-06-23T03:09:34.000+0000",
       "emailAddress" : "sample@rackspace.com",
       "created" : "2011-06-23T03:09:33.000+0000"
     }, {
       "name" : "sub2.example.com",
       "id" : "2725258",
       "comment" : "1st sample subdomain",
       "updated" : "2011-06-23T03:52:55.000+0000",
       "emailAddress" : "sample@rackspace.com",
       "created" : "2011-06-23T03:52:55.000+0000"
     }, {
       "name" : "north.example.com",
       "id" : "2725260",
       "updated" : "2011-06-23T03:53:10.000+0000",
       "emailAddress" : "sample@rackspace.com",
       "created" : "2011-06-23T03:53:09.000+0000"
     }, {
       "name" : "south.example.com",
       "id" : "2725261",
       "comment" : "Final sample subdomain",
       "updated" : "2011-06-23T03:53:14.000+0000",
       "emailAddress" : "sample@rackspace.com",
       "created" : "2011-06-23T03:53:14.000+0000"
     } ],
     "totalEntries" : 4
   }




