.. _paginated-collections:

=====================
Paginated collections
=====================

To reduce load on the service, retrieve operations return a maximum limit of
100 items at a time. If a request supplies no limit or one that exceeds the
configured  default limit, the default limit is used instead.

This behavior is called *pagination*. Pagination gives you the ability to
limit the size of the returned data and to retrieve a specified subset of a
large data set.  Pagination has two key concepts: limit and marker.

* *Limit* is the restriction on the maximum number of items for that type that
  can be returned.

* *Marker* is a reference to an object's ID and is in the list of paged
  results for a particular resource. For example, if the resource is a load
  balancer, the marker is the load balancer ID at which to begin the list of
  the paged results.

To navigate the collection, you can set the ``limit`` and ``marker``
parameters in the URI. For example, ``?limit=10&marker=1234`` displays a
maximum of 10 domains in the paginated results, beginning with the
domain with an id of ``1234``.

If a marker beyond the end of a list is given, an empty list is returned.

You can also use the ``offset`` parameter, which is a count of the number
of objects from where the paginated list is started.

It is important to note that offset must be a multiple of the limit
(or zero), otherwise a ``Bad Request`` Exception will be thrown. Both limit
and offset are specified via request parameters on the URI. The
parameters are named ``limit`` and ``offset`` respectively, and both
apply only to **GET** calls. If unspecified, they default to
``limit=100`` and ``offset=0``. See the examples that follow.

**Examples of limits and offsets for paging calls**

.. code::

   ....\domains?limit=50              -- returns the first 50 domains, that is: 1 - 50
   ....\domains?limit=50&offset=50    -- returns the domains 51-100
   ....\domains?limit=25&offset=50    -- returns the domains 51-75
   ....\domains?limit=25              -- returns the domains 1-25
   ....\domains?limit=25&offset=5     -- returns Bad Request Exception; offset must be a multiple of the limit or 0
   ....\domains?offset=5              -- returns Bad Request Exception; offset must be a multiple of the limit or 0
   ....\domains?offset=200            -- returns back the 201-300th domains if they exist (default limit of 100 applies)
   ....\domains                       -- returns the current maximum items allowable (currently 100)


Pagination applies only to the calls listed here:

+------+------------------------------+---------------------------------------------------------------------------------------------------------------------+
| Verb | URI                          | Description                                                                                                         |
+------+------------------------------+---------------------------------------------------------------------------------------------------------------------+
| GET  | /domains/                    | List all domains manageable by the account specified.                                                               |
+------+------------------------------+---------------------------------------------------------------------------------------------------------------------+
| GET  | /domains/?name=domainName    | Filter domains by domain name: list all domains manageable by the account specified that match the name domainName. |
+------+------------------------------+---------------------------------------------------------------------------------------------------------------------+
| GET  | /domains/domainID            | List details of the specified domain. Applies to the recordsand subdomains lists.                                   |
+------+------------------------------+---------------------------------------------------------------------------------------------------------------------+
| GET  | /domains/domainID/subdomains | List domains that are subdomains of the specified domain.                                                           |
+------+------------------------------+---------------------------------------------------------------------------------------------------------------------+
| GET  | /domains/domainID/records    | List all records configured for the domain.                                                                         |
+------+------------------------------+---------------------------------------------------------------------------------------------------------------------+


See the following section for examples of paged List Domains calls.

Pagination elements and attributes
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

For any collection in a result, there is a ``totalEntries`` attribute
representing the total number of entries there are for this item type. If the
number of items requested in the ``GET`` call is less then the total number of
items for this type, then there will be pagination links ``previous`` or
``next``, specifying how to get to the previous or next set of records.

.. note::
   The ``previous`` or ``next`` link elements are displayed only if
   there are items available in the corresponding link. See the following
   examples for details.

**Example: List Domains Request with limit: XML**

.. code::

    GET https://dns.api.rackspacecloud.com/v1.0/1234/domains?limit=3
    Accept: application/xml
    X-Auth-Token: ea85e6ac-baff-4a6c-bf43-848020ea3812
    Content-Type: application/xml
    Content-Length: 0


**Example: List Domains Request with limit: JSON**

.. code::

    GET https://dns.api.rackspacecloud.com/v1.0/1234/domains?limit=3
    Accept: application/json
    X-Auth-Token: ea85e6ac-baff-4a6c-bf43-848020ea3812
    Content-Type: application/json
    Content-Length: 0


**Example: List Domains Response with totalEntries: XML**

.. code::

    Status: 200 OK
    Date: Thu, 28 Jul 2011 21:54:21 GMT
    X-API-VERSION: 1.0.17
    Content-Type: application/xml
    Content-Length: 934

    <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
    <domains totalEntries="114" xmlns:ns2="http://www.w3.org/2005/Atom" xmlns="http://docs.rackspacecloud.com/dns/api/v1.0" xmlns:ns3="http://docs.rackspacecloud.com/dns/api/management/v1.0">
        <domain id="2725257" accountId="1234" name="sub1.example.com" emailAddress="sample@rackspace.com" updated="2011-06-23T03:09:34Z" created="2011-06-23T03:09:33Z" comment="1st sample subdomain"/>
        <domain id="2725258" accountId="1234" name="sub2.example.com" emailAddress="sample@rackspace.com" updated="2011-06-23T03:52:55Z" created="2011-06-23T03:52:55Z" comment="1st sample subdomain"/>
        <domain id="2725260" accountId="1234" name="north.example.com" emailAddress="sample@rackspace.com" updated="2011-06-23T03:53:10Z" created="2011-06-23T03:53:09Z"/>
        <ns2:link href="https://dns.api.rackspacecloud.com/v1.0/1234/domains?limit=3&amp;offset=3" rel="next"></ns2:link>
    </domains>


**Example: List Domains Response with totalEntries: JSON**

.. code::

    Status: 200 OK
    Date: Thu, 28 Jul 2011 21:54:21 GMT
    X-API-VERSION: 1.0.17
    Content-Type: application/json
    Content-Length: 945

    {
      "domains" : [ {
        "name" : "sub1.example.com",
        "id" : 2725257,
        "comment" : "1st sample subdomain",
        "updated" : "2011-06-23T03:09:34.000+0000",
        "accountId" : 1234,
        "emailAddress" : "sample@rackspace.com",
        "created" : "2011-06-23T03:09:33.000+0000"
      }, {
        "name" : "sub2.example.com",
        "id" : 2725258,
        "comment" : "1st sample subdomain",
        "updated" : "2011-06-23T03:52:55.000+0000",
        "accountId" : 1234,
        "emailAddress" : "sample@rackspace.com",
        "created" : "2011-06-23T03:52:55.000+0000"
      }, {
        "name" : "north.example.com",
        "id" : 2725260,
        "updated" : "2011-06-23T03:53:10.000+0000",
        "accountId" : 1234,
        "emailAddress" : "sample@rackspace.com",
        "created" : "2011-06-23T03:53:09.000+0000"
      } ],
      "links" : [ {
        "content" : "",
        "href" : "https://dns.api.rackspacecloud.com/v1.0/1234/domains?limit=3&offset=3",
        "rel" : "next"
      } ],
      "totalEntries" : 114
    }

In the previous two response examples, note that ``totalEntries=112``
and that a link has been provided to retrieve the next 3 results
(``limit=3``) in the link element identified by the attribute
``rel="next"`` (XML) or ``"rel":"next"`` (JSON).

The following example shows links to both previous and next results in
the responses, since the request specified to start with the fourth item
in the collection (``offset=3``):

**Example: List Domains Request with limit and offset: XML**

.. code::

    GET https://dns.api.rackspacecloud.com/v1.0/1234/domains?limit=3&offset=3
    Accept: application/xml
    X-Auth-Token: ea85e6ac-baff-4a6c-bf43-848020ea3812
    Content-Type: application/xml
    Content-Length: 0

**Example: List Domains Request with limit and offset: JSON**

.. code::

    GET https://dns.api.rackspacecloud.com/v1.0/1234/domains?limit=3&offset=3
    Accept: application/json
    X-Auth-Token: ea85e6ac-baff-4a6c-bf43-848020ea3812
    Content-Type: application/json
    Content-Length: 0

**Example: List Domains Response with Links to previous and next
Results: XML**

.. code::

    Status: 200 OK
    Date: Thu, 28 Jul 2011 21:54:21 GMT
    X-API-VERSION: 1.0.17
    Content-Type: application/xml
    Content-Length: 1056

    <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
    <domains totalEntries="114" xmlns:ns2="http://www.w3.org/2005/Atom" xmlns="http://docs.rackspacecloud.com/dns/api/v1.0" xmlns:ns3="http://docs.rackspacecloud.com/dns/api/management/v1.0">
        <domain id="2725257" accountId="1234" name="sub1.example.com" emailAddress="sample@rackspace.com" updated="2011-06-23T03:09:34Z" created="2011-06-23T03:09:33Z" comment="1st sample subdomain"/>
        <domain id="2725258" accountId="1234" name="sub2.example.com" emailAddress="sample@rackspace.com" updated="2011-06-23T03:52:55Z" created="2011-06-23T03:52:55Z" comment="1st sample subdomain"/>
        <domain id="2725260" accountId="1234" name="north.example.com" emailAddress="sample@rackspace.com" updated="2011-06-23T03:53:10Z" created="2011-06-23T03:53:09Z"/>
        <ns2:link href="https://dns.api.rackspacecloud.com/v1.0/1234/domains?limit=3&amp;offset=0" rel="previous"></ns2:link>
        <ns2:link href="https://dns.api.rackspacecloud.com/v1.0/1234/domains?limit=3&amp;offset=6" rel="next"></ns2:link>
    </domains>

**Example: List Domains Response with Links to previous and next
Results: JSON**

.. code::

    Status: 200 OK
    Date: Thu, 28 Jul 2011 21:54:21 GMT
    X-API-VERSION: 1.0.17
    Content-Type: application/json
    Content-Length: 1081

    {
      "domains" : [ {
        "name" : "sub1.example.com",
        "id" : 2725257,
        "comment" : "1st sample subdomain",
        "updated" : "2011-06-23T03:09:34.000+0000",
        "accountId" : 1234,
        "emailAddress" : "sample@rackspace.com",
        "created" : "2011-06-23T03:09:33.000+0000"
      }, {
        "name" : "sub2.example.com",
        "id" : 2725258,
        "comment" : "1st sample subdomain",
        "updated" : "2011-06-23T03:52:55.000+0000",
        "accountId" : 1234,
        "emailAddress" : "sample@rackspace.com",
        "created" : "2011-06-23T03:52:55.000+0000"
      }, {
        "name" : "north.example.com",
        "id" : 2725260,
        "updated" : "2011-06-23T03:53:10.000+0000",
        "accountId" : 1234,
        "emailAddress" : "sample@rackspace.com",
        "created" : "2011-06-23T03:53:09.000+0000"
      } ],
      "links" : [ {
        "content" : "",
        "href" : "https://dns.api.rackspacecloud.com/v1.0/1234/domains?limit=3&offset=0",
        "rel" : "previous"
      }, {
        "content" : "",
        "href" : "https://dns.api.rackspacecloud.com/v1.0/1234/domains?limit=3&offset=6",
        "rel" : "next"
      } ],
      "totalEntries" : 114
    }

In the previous two response examples, note that ``totalEntries=112``
and two links have been provided to:

*  Retrieve the next 3 results (``limit=3``) via the link element
   identified by the attribute ``rel="next"`` (XML) or ``"rel":"next"``
   (JSON)

*  Retrieve the previous 3 results via the link element identified by
   the attribute ``rel="previous"`` (XML) or ``"rel":"previous"`` (JSON)

