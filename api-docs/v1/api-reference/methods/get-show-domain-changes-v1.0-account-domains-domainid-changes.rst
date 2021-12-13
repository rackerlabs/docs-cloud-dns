.. _get-show-domain-changes-v1.0-account-domains-domainid-changes:

Show domain changes
~~~~~~~~~~~~~~~~~~~

.. code::

    GET /v1.0/{account}/domains/{domainId}/changes

Shows all changes to a specified domain ``since`` a specified ``date/time``.

This call shows all changes to a specified domain ``since`` a specified
date/time. The ``since`` parameter is optional and defaults to midnight of the
current day. See :ref:`Date/Time format <date-time>` for details on how
to specify this parameter's value.

The examples below show the requests and corresponding responses to list the
domain changes since midnight, GMT-5, on September 13, 2011.

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
|since                     |String                   |The Date/Time from which |
|                          |                         |the domain changes       |
|                          |                         |should be shown.         |
+--------------------------+-------------------------+-------------------------+

This operation does not accept a request body.

**Example List domain Changes: XML request**


.. code::

   GET https://dns.api.rackspacecloud.com/v1.0/1234/domains/45678/changes?since=2011-09-13T00:00:00-0500
   Accept: application/xml
   X-Auth-Token: ea85e6ac-baff-4a6c-bf43-848020ea3812
   Content-Type: application/xml
   Content-Length: 0

**Example List domain Changes: JSON request**

.. code::

   GET https://dns.api.rackspacecloud.com/v1.0/1234/domains/45678/changes?since=2011-09-13T00:00:00-0500
   Accept: application/json
   X-Auth-Token: ea85e6ac-baff-4a6c-bf43-848020ea3812
   Content-Type: application/json
   Content-Length: 0

Response
--------

**Example List domain Changes: XML response**

.. code::

   Status: 200 OK
   Date: Thu, 28 Jul 2011 21:54:21 GMT
   X-API-VERSION: 1.0.17
   Content-Type: application/xml
   Content-Length: 2460

   <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
   <changes totalEntries="4" from="2011-09-13T00:00:00-05:00" to="2011-09-19T16:36:01-05:00" xmlns:ns2="http://www.w3.org/2005/Atom" xmlns="http://docs.rackspacecloud.com/dns/api/v1.0" xmlns:ns3="http://docs.rackspacecloud.com/dns/api/management/v1.0">
       <change accountId="1234" domain="rs.example.com" targetId="45678" targetType="Domain" action="update">
           <changeDetail field="serial_number" originalValue="1315927395" newValue="1315930302"/>
           <changeDetail field="updated_at" originalValue="Tue Sep 13 15:23:15 UTC 2011" newValue="Tue Sep 13 16:11:42 UTC 2011"/>
       </change>
       <change domain="rs.example.com" targetId="222222" targetType="MX Record" action="create">
           <changeDetail field="created_at" originalValue="" newValue="Tue Sep 13 16:11:42 UTC 2011"/>
           <changeDetail field="ttl" originalValue="" newValue="3600"/>
           <changeDetail field="fqdn" originalValue="" newValue="rs.example.com"/>
           <changeDetail field="updated_at" originalValue="" newValue="Tue Sep 13 16:11:42 UTC 2011"/>
           <changeDetail field="destination" originalValue="" newValue="mail.rs.example.com"/>
           <changeDetail field="priority" originalValue="" newValue="1"/>
           <changeDetail field="id" originalValue="" newValue="222222"/>
           <changeDetail field="zone_id" originalValue="" newValue="45678"/>
       </change>
       <change accountId="1234" domain="rs.example.com" targetId="45678" targetType="Domain" action="update">
           <changeDetail field="serial_number" originalValue="1310656481" newValue="1315927395"/>
           <changeDetail field="updated_at" originalValue="Thu Jul 14 15:14:41 UTC 2011" newValue="Tue Sep 13 15:23:15 UTC 2011"/>
       </change>
       <change domain="rs.example.com" targetId="87654" targetType="CNAME Record" action="create">
           <changeDetail field="created_at" originalValue="" newValue="Tue Sep 13 15:23:15 UTC 2011"/>
           <changeDetail field="ttl" originalValue="" newValue="3600"/>
           <changeDetail field="fqdn" originalValue="" newValue="*.rs.example.com"/>
           <changeDetail field="updated_at" originalValue="" newValue="Tue Sep 13 15:23:15 UTC 2011"/>
           <changeDetail field="destination" originalValue="" newValue="rs.example.com"/>
           <changeDetail field="id" originalValue="" newValue="87654"/>
           <changeDetail field="zone_id" originalValue="" newValue="45678"/>
       </change>
   </changes>

**Example List domain Changes: JSON response**

.. code::

   Status: 200 OK
   Date: Thu, 28 Jul 2011 21:54:21 GMT
   X-API-VERSION: 1.0.17
   Content-Type: application/json
   Content-Length: 2762

   {
     "from" : "2011-09-13T05:00:00.000+0000",
     "to" : "2011-09-19T21:36:01.000+0000",
     "totalEntries" : 4,
     "changes" : [ {
       "domain" : "rs.example.com",
       "targetType" : "Domain",
       "action" : "update",
       "changeDetails" : [ {
         "field" : "serial_number",
         "newValue" : "1315930302",
         "originalValue" : "1315927395"
       }, {
         "field" : "updated_at",
         "newValue" : "Tue Sep 13 16:11:42 UTC 2011",
         "originalValue" : "Tue Sep 13 15:23:15 UTC 2011"
       } ],
       "accountId" : 1234,
       "targetId" : "45678"
     }, {
       "domain" : "rs.example.com",
       "targetType" : "MX Record",
       "action" : "create",
       "changeDetails" : [ {
         "field" : "created_at",
         "newValue" : "Tue Sep 13 16:11:42 UTC 2011",
         "originalValue" : ""
       }, {
         "field" : "ttl",
         "newValue" : "3600",
         "originalValue" : ""
       }, {
         "field" : "fqdn",
         "newValue" : "rs.example.com",
         "originalValue" : ""
       }, {
         "field" : "updated_at",
         "newValue" : "Tue Sep 13 16:11:42 UTC 2011",
         "originalValue" : ""
       }, {
         "field" : "destination",
         "newValue" : "mail.rs.example.com",
         "originalValue" : ""
       }, {
         "field" : "priority",
         "newValue" : "1",
         "originalValue" : ""
       }, {
         "field" : "id",
         "newValue" : "222222",
         "originalValue" : ""
       }, {
         "field" : "zone_id",
         "newValue" : "45678",
         "originalValue" : ""
       } ],
       "targetId" : "222222"
     }, {
       "domain" : "rs.example.com",
       "targetType" : "Domain",
       "action" : "update",
       "changeDetails" : [ {
         "field" : "serial_number",
         "newValue" : "1315927395",
         "originalValue" : "1310656481"
       }, {
         "field" : "updated_at",
         "newValue" : "Tue Sep 13 15:23:15 UTC 2011",
         "originalValue" : "Thu Jul 14 15:14:41 UTC 2011"
       } ],
       "accountId" : 1234,
       "targetId" : "45678"
     }, {
       "domain" : "rs.example.com",
       "targetType" : "CNAME Record",
       "action" : "create",
       "changeDetails" : [ {
         "field" : "created_at",
         "newValue" : "Tue Sep 13 15:23:15 UTC 2011",
         "originalValue" : ""
       }, {
         "field" : "ttl",
         "newValue" : "3600",
         "originalValue" : ""
       }, {
         "field" : "fqdn",
         "newValue" : "*.rs.example.com",
         "originalValue" : ""
       }, {
         "field" : "updated_at",
         "newValue" : "Tue Sep 13 15:23:15 UTC 2011",
         "originalValue" : ""
       }, {
         "field" : "destination",
         "newValue" : "rs.example.com",
         "originalValue" : ""
       }, {
         "field" : "id",
         "newValue" : "87654",
         "originalValue" : ""
       }, {
         "field" : "zone_id",
         "newValue" : "45678",
         "originalValue" : ""
       } ],
       "targetId" : "87654"
     } ]
   }




