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

Rate limits are specified in terms of both a human-readable wild-card URI and a 
machine-processable regular expression. The regular expression boundary matcher '^' takes 
effect after the root URI path. For example, the regular expression ^/v1.0/1234/domains 
matches the bolded portion of the following URI:
https://dns.api.rackspacecloud.com\ **/v1.0/1234/domains**.

The following table specifies the default rate limits for the **GET**, **POST**, **PUT**, 
**PATCH**, and **DELETE** calls for zone API operations:

**Default rate limits**

+--------+----------------+-----------+
| Verb   | URI            | Default   |
+--------+----------------+-----------+
| GET    | \*/zones/\*    | 420/minute|
+--------+----------------+-----------+
| POST   | \*/zones\*     | 40/minute |
+--------+----------------+-----------+
| PUT    | \*/zones\*     | 40/minute |
+--------+----------------+-----------+
| PATCH  | \*/zones*\     | 40/minute |
+--------+----------------+-----------+
| DELETE | \*/zones*\     | 10/minute |
+--------+----------------+-----------+


If you exceed the thresholds established for your account, a ``413`` HTTP response will 
be returned with a ``Reply-After`` header to notify the client when it can attempt to try 
again. The ``Reply-After`` header is an ISO 8601 Date/Time field, for example 
"2012-10-10T21:21:15Z".

.. note::
   The first entry in the Default Rate Limits table above is for simple
   STATUS calls after a **POST**, **PUT**, or **DELETE** to retrieve the
   status details. For example, the following status call has a limit of 5 requests per 
   second:
   
   .. code::
   
      https://dns.api.rackspacecloud.com/v1.0/1234/status/0062ac6e-3d07-4980-afab-5fd3a806ef4d

Resource Quotas
~~~~~~~~~~~~~~~

**POST**, **PUT**, and **PATCH** ccalls are subject to quotas for the number of a certain 
resource a user is allowed to create.

Zone quotas
^^^^^^^^^^^

By default users may have up to 500 zones per Cloud account (including sub-zones). When
a user submits a request to create new zones, the system will only accept the request if the
total number of existing plus requested zones is within the account zone limit. If the total
exceeds the account zone limit, the entire request will be rejected and the following message
will be returned:

**Example: Domain limit rejection response:**

.. code::

    Status: 413 Request Entity Too Large
    Date: Thu, 28 Jul 2011 21:54:21 GMT
    X-API-VERSION: 1.0.17
    Content-Type: application/json
    Content-Length: 172

    {
      "message" : "Your account is currently over the limit so your request could not be processed.",
      "code" : 413,
      "details" : "Limit of 500 domains has been reached."
    }



.. note::
   Any zones or recordsets that are submitted in any request that causes zone quotas to be 
   exceeded will not be provisioned and the entire request will be rejected.

   The account zone limit applies to any API request that can be used to create a zone. An 
   account may have a non-default limit if determined necessary by Rackspace Support.

Recordset and Record quotas
^^^^^^^^^^^^^^^^^^^^^^^^^^^

By default, users may have up to 500 recordsets total per zone per Cloud account and up to
50 records per recordset.

When a user submits a request to create a new recordset, the system will only accept the
request if the total number of existing plus requested record or recordset is within these
quotas. If the total number of recordsets or recordsets on a specified zone exceeds
these quotas, the entire request will be rejected and the following message will be returned:

**Example: Recordset limit rejection response:**

.. code::

    Status: 413 Request Entity Too Large
    Date: Thu, 28 Jul 2011 21:54:21 GMT
    X-API-VERSION: 1.0.17
    Content-Type: application/json
    Content-Length: 183

    {
      "message" : "Your account is currently over the limit so your request could not be processed.",
      "code" : 413,
      "details" : "Limit of 500 records per domain has been reached."
    }

.. note::
   Any zones recordsets that are submitted in any request that causes recordset limits to 
   be exceeded will not be provisioned and the entire request will be rejected.

   The limits apply to any API request that can be used to create one or more recordsets. 
   An account may have a non-default record limit if determined necessary by Rackspace Support.

