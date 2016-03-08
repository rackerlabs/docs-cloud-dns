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

**Zone rate limits:** URIs: ``/zones/`` and ``/zones/<id>``

+--------+---------------+
| Method | Default       |
+--------+---------------+
| GET    | 420 per minute|
+--------+---------------+
| POST   | 10 per minute |
+--------+---------------+
| PATCH  | 20 per minute |
+--------+---------------+
| DELETE |  5 per minute |
+--------+---------------+

**Record set rate limits:** URI: ``/zones/<id>/recordsets/``

+--------+----------------+
| Method | Default        |
+--------+----------------+
| GET    | 420 per minute |
+--------+----------------+
| POST   | 40 per minute  |
+--------+----------------+
| PUT    | 40 per minute  |
+--------+----------------+
| DELETE | 20 per minute  |
+--------+----------------+

If you exceed the thresholds established for your account, a ``413`` HTTP response will 
be returned with a ``Reply-After`` header to notify the client when it can attempt to try 
again. The ``Reply-After`` header is an ISO 8601 date/time field, for example 
"2012-10-10T21:21:15Z".

**Global rate limit**

During periods of peak load, the system might return a ``503`` HTTP response. If this 
occurs, the request should be retried in a few minutes.

Resource quotas
~~~~~~~~~~~~~~~

**POST**, **PUT**, and **PATCH** operations are subject to quotas for the number of a 
certain resource a user is allowed to create.

Zone quotas
^^^^^^^^^^^

By default users may have up to 5000 zones per Cloud account (including sub-zones). When
a user submits a request to create new zones, the system accepts the request only if the
total number of existing plus requested zones is within the account zone limit. If the total
exceeds the account zone limit, the entire request is rejected and the following message
is returned:

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
   exceeded are not be provisioned and the entire request is rejected.

   The account zone limit applies to any API request that can be used to create a zone. An 
   account may have a nondefault limit if determined necessary by Rackspace Support.

Record set quotas and record quotas
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

By default, users may have up to 3000 record sets per zone per Cloud account and up to
3000 records per zone.

When a user submits a request to create a new record set, the system accepts the request 
only if the total number of existing plus requested records or record sets is within these
quotas. If the total number of records or record sets on a specified zone exceeds
these quotas, the entire request is rejected and the following message is returned:

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
   be exceeded are not be provisioned and the entire request is rejected.

   The limits apply to any API request that can be used to create one or more record sets. 
   An account may have a nondefault record limit if determined necessary by Rackspace Support.


