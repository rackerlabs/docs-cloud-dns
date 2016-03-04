.. _cdns-dg-limits:

======
Limits
======

All accounts, by default, have a preconfigured set of thresholds (or limits) to manage 
capacity and prevent abuse of the system. The system recognizes two kinds of limits: 
*API rate limits* and *resource quotas*, which are also known as *absolute limits*. Rate 
limits are thresholds that are reset after a certain amount of time passes. Resource quotas 
are fixed.

Rate limits
~~~~~~~~~~~

Rate limits are shown below for API operations by resource. They are displayed in a simplified, wild-card style format.

**Zone rate limits:** URIs: ``/zones/`` and ``/zones/<ID>``

+--------+-----------+
| Verb   | Default   |
+--------+-----------+
| GET    | 420/minute|
+--------+-----------+
| POST   | 10/minute |
+--------+-----------+
| PATCH  | 20/minute |
+--------+-----------+
| DELETE |  5/minute |
+--------+-----------+

**Record set rate limits:** URI: ``/zones/<ID>/recordsets/``

+--------+------------+
| Verb   | Default    |
+--------+------------+
| GET    | 420/minute |
+--------+------------+
| POST   | 40/minute  |
+--------+------------+
| PUT    | 40/minute  |
+--------+------------+
| DELETE | 20/minute  |
+--------+------------+

If you exceed the thresholds established for your account, a ``413`` HTTP response will 
be returned with a ``Reply-After`` header to notify the client when it can attempt to try 
again. The ``Reply-After`` header is an ISO 8601 Date/Time field, for example 
"2012-10-10T21:21:15Z".

**Global Rate Limit**

During periods of peak load, the system may return a ``503`` HTTP reponse. If this occurs
the request should be retried in a few minutes.

Resource Quotas
~~~~~~~~~~~~~~~

**POST**, **PUT**, and **PATCH** calls are subject to quotas for the number of a certain 
resource a user is allowed to create.

Zone quotas
^^^^^^^^^^^

By default users may have up to 5000 zones per Cloud account (including sub-zones). When
a user submits a request to create new zones, the system will only accept the request if the
total number of existing plus requested zones is within the account zone limit. If the total
exceeds the account zone limit, the entire request will be rejected and the following message
will be returned:

**Example: Zone limit rejection response:**

.. code::

    Status: 413 Request Entity Too Large
    Date: Thu, 28 Jul 2011 21:54:21 GMT
    Content-Type: application/json
    Content-Length: 172

    {
      "message" : "Your account is currently over the limit so your request could not be processed.",
      "code" : 413,
      "details" : "Limit of 500 domains has been reached."
    }



.. note::

   Any zones or record sets that are submitted in any request that causes zone quotas to be 
   exceeded will not be provisioned and the entire request will be rejected.

   The account zone limit applies to any API request that can be used to create a zone. An 
   account may have a non-default limit if determined necessary by Rackspace Support.

Record set and Record quotas
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

By default, users may have up to 3000 record sets total per zone per Cloud account and up to
3000 records per zone.

When a user submits a request to create a new record set, the system will only accept the
request if the total number of existing plus requested record or record set is within these
quotas. If the total number of records or record sets on a specified zone exceeds
these quotas, the entire request will be rejected and the following message will be returned:

**Example: Record set limit rejection response:**

.. code::

    Status: 413 Request Entity Too Large
    Date: Thu, 28 Jul 2011 21:54:21 GMT
    Content-Type: application/json
    Content-Length: 183

    {
      "message" : "Your account is currently over the limit so your request could not be processed.",
      "code" : 413,
      "details" : "Limit of 3000 records per domain has been reached."
    }

.. note::

   Any record sets or records that are submitted in any request that causes quota limits to 
   be exceeded will not be provisioned and the entire request will be rejected.

   The limits apply to any API request that can be used to create one or more record sets. 
   An account may have a non-default record limit if determined necessary by Rackspace Support.


