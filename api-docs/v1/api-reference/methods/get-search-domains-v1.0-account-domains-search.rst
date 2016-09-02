.. _get-search-domains-v1.0-account-domains-search:

Search domains
~~~~~~~~~~~~~~

.. code::

    GET /v1.0/{account}/domains/search

Searches domains by domain name: lists all names manageable by the specified
account that have the value of the ``name`` parameter as part of their name.

.. note::


   *  Use the query parameter ``name`` to search domains by domain name. This
      lists all names manageable by the specified account that have the value
      of the ``name`` parameter as part of their name.
   *  The value specified for the ``name`` parameter must contain at least 3
      characters or nothing will be returned by the search.

Filter criteria may consist of:

* Any letter (A-Za-z)
* Numbers (0-9)
* Hyphen ("-")
* 3 to 63 characters

Filter criteria should not include any of the following characters: ' +, | ! "
£ $ % & / ( ) = ? ^ * ç ° § ; : _ > ] [ @ à, é, ò

.. note::
   This call returns by default a maximum of 100 items at a time if no
   ``limit`` is specified. To navigate the collection returned, the parameters
   ``limit`` and ``offset`` can be set in the URI (for example: ``limit=10 &
   offset=0`` ), as described at
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

This table shows the URI parameters for the request:

+--------------------------+-------------------------+-------------------------+
|Name                      |Type                     |Description              |
+==========================+=========================+=========================+
|{account}                 |String                   |The tenant ID.           |
+--------------------------+-------------------------+-------------------------+

This table shows the query parameters for the request:

+--------------------------+-------------------------+-------------------------+
|Name                      |Type                     |Description              |
+==========================+=========================+=========================+
|name                      |String                   |Name of the domain to    |
|                          |                         |find.                    |
+--------------------------+-------------------------+-------------------------+

This operation does not accept a request body.

**Example Filter by Partial Name: XML request**

.. code::

   GET https://dns.api.rackspacecloud.com/v1.0/1234/domains/search?name=sub1.exam
   Accept: application/xml
   X-Auth-Token: ea85e6ac-baff-4a6c-bf43-848020ea3812
   Content-Type: application/xml
   Content-Length: 0

**Example Filter by Partial Name: JSON request**

.. code::

   GET https://dns.api.rackspacecloud.com/v1.0/1234/domains/search?name=sub1.exam
   Accept: application/json
   X-Auth-Token: ea85e6ac-baff-4a6c-bf43-848020ea3812
   Content-Type: application/json
   Content-Length: 0

Response
--------

**Example Filter by Partial Name: XML response**

.. code::

   Status: 200 OK
   Date: Thu, 28 Jul 2011 21:54:21 GMT
   X-API-VERSION: 1.0.17
   Content-Type: application/xml
   Content-Length: 435

   <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
   <domains totalEntries="114" xmlns:ns2="http://www.w3.org/2005/Atom" xmlns="http://docs.rackspacecloud.com/dns/api/v1.0" xmlns:ns3="http://docs.rackspacecloud.com/dns/api/management/v1.0">
       <domain id="2725257" name="sub1.example.com" emailAddress="sample@rackspace.com" updated="2011-06-23T03:09:34Z" created="2011-06-23T03:09:33Z" comment="1st sample subdomain"/>
   </domains>

**Example Filter by Partial Name: JSON response**

.. code::

   Status: 200 OK
   Date: Thu, 28 Jul 2011 21:54:21 GMT
   X-API-VERSION: 1.0.17
   Content-Type: application/json
   Content-Length: 284

   {
     "domains" : [ {
       "name" : "sub1.example.com",
       "id" : 2725257,
       "comment" : "1st sample subdomain",
       "updated" : "2011-06-23T03:09:34.000+0000",
       "emailAddress" : "sample@rackspace.com",
       "created" : "2011-06-23T03:09:33.000+0000"
     } ],
     "totalEntries" : 114
   }




