.. _limits:

======
Limits
======


All accounts, by default, have a preconfigured set of thresholds, or *limits*,
to manage capacity and prevent abuse of the system. The system recognizes two
kinds of limits: *rate limits* and *absolute limits*. Rate limits are
thresholds that are reset after a certain amount of time passes. Absolute
limits are fixed. Rate limits are processed via the `Repose service`_.

.. note::

    If the default limits are too low for your particular application,
    contact Rackspace Cloud support to request an increase. All requests
    require reasonable justification.

.. _Repose service: http://www.openrepose.org

.. _api-info-limits-ratelimits:

Rate limits
~~~~~~~~~~~

Rate limits are specified in terms of both a human-readable wild-card
URI and a machine-processable regular expression. The regular expression
boundary matcher ``^`` takes effect after the root URI path. For example,
the regular expression ``^/v1.0/1234/domains`` would match the
``/v1.0/1234/domains`` portion of the following URI:

``https://dns.api.rackspacecloud.com\ /v1.0/1234/domains``

The following table specifies the default rate limits for all API
operations for all ``GET``, ``POST``, ``PUT``, and ``DELETE`` calls for
domains, subdomains, or records:

.. list-table:: **Default rate limits**
   :widths: 20 40 10 20
   :header-rows: 1

   * - Method
     - URI
     - RegEx
     - Default Limit
   * - GET
     - ``/status/*``
     - ``.*/v\d+\.\d+/(\d+/status).*``
     - 5 per second
   * - GET
     - */domains/search*
     - .*/v\d+\.\d+/(\d+/domains/search).*
     - 20/minute
   * - GET
     - */domains*
     - .*/v\d+\.\d+/(\d+/domains).*
     - 60/minute
   * - POST
     - */domains*
     - .*/v\d+\.\d+/(\d+/domains).*
     - 20/minute
   * - PUT
     - */domains*
     - .*/v\d+\.\d+/(\d+/domains).*
     - 20/minute
   * - DELETE
     - */domains*
     - .*/v\d+\.\d+/(\d+/domains).*
     - 10/minute

If you exceed the thresholds established for your account, a ``413 HTTP``
response will be returned with a ``Reply-After`` header to notify the
client when it can attempt to try again. The ``Reply-After`` header is
an ISO 8601 Date/Time field, for example ``2012-10-10T21:21:15Z``.

.. note::
   The first entry in the Default Rate Limits table above is for simple
   STATUS calls after a ``POST``, ``PUT``, or ``DELETE`` to retrieve the
   status details; for example:
   https://dns.api.rackspacecloud.com/v1.0/1234/status/0062ac6e-3d07-4980-afab-5fd3a806ef4d

   This status call has a limit of 5 requests per second.

Absolute limits
~~~~~~~~~~~~~~~

``POST`` and ``PUT`` calls are limited to the creation or modification
of a maximum of 100 entities per call where an entity is defined as a
record, domain, or subdomain. For example, when using ``POST``
``/domains`` to create a new domain with nine subdomains, you could
create a maximum of ninety records across the domain and subdomains.
This would total 100 entities: 1 domain + 9 subdomains + 90 records.
Additional records or subdomains could be created for the domain in
subsequent calls.

.. list-table:: **Absolute limits**
   :widths: 20 40 10
   :header-rows: 1

   * - Name
     - Description
     - Default
   * - DOMAIN_LIMIT
     - Total number of domains per Cloud account
     - 500
   * - RECORD_LIMIT
     - Total number of records per domain
     - 500

Domain limits
^^^^^^^^^^^^^

By default users may have up to 500 domains per Cloud account (including
sub-domains). When a user submits a request to create new domains or
sub-domains, the system will only accept the request if the total number
of existing plus requested domains and sub-domains is within the account
domain limit. If the total exceeds the account domain limit, the entire
request will be rejected and the following message will be returned:

**Example: Domain limit response: XML**

.. code::

    Status: 413 Request Entity Too Large
    Date: Thu, 28 Jul 2011 21:54:21 GMT
    X-API-VERSION: 1.0.17
    Content-Type: application/xml
    Content-Length: 417

    <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
    <overlimit code="413" xmlns:ns2="http://www.w3.org/2005/Atom" xmlns="http://docs.rackspacecloud.com/dns/api/v1.0" xmlns:ns3="http://docs.rackspacecloud.com/dns/api/management/v1.0">
        <message>Your account is currently over the limit so your request could not be processed.</message>
        <details>Limit of 500 domains has been reached.</details>
    </overlimit>


**Example: Domain limit response: JSON**

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
   Any domains/sub-domains or records that are submitted in any request
   that causes domain limits to be exceeded will not be provisioned and the
   entire request will be rejected.

.. note::
   The account domain limit applies to any API request that can be used
   to create a domain or sub-domain. An account may have a non-default
   limit if determined necessary by Support.

Record limits
^^^^^^^^^^^^^

By default users may have up to 500 records per domain per Cloud
account. When a user submits a request to create one or more new
records, the system will only accept the request if the total number of
existing plus requested records is within the account record limit. If
the total number of records on a specified domain exceeds the record
limit, the entire request will be rejected and the following message
will be returned:

**Example: Domain record limit response: XML**

.. code::

    Status: 413 Request Entity Too Large
    Date: Thu, 28 Jul 2011 21:54:21 GMT
    X-API-VERSION: 1.0.17
    Content-Type: application/xml
    Content-Length: 428

    <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
    <overlimit code="413" xmlns:ns2="http://www.w3.org/2005/Atom" xmlns="http://docs.rackspacecloud.com/dns/api/v1.0" xmlns:ns3="http://docs.rackspacecloud.com/dns/api/management/v1.0">
        <message>Your account is currently over the limit so your request could not be processed.</message>
        <details>Limit of 500 records per domain has been reached.</details>
    </overlimit>


**Example: Domain record limit response: JSON**

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
   Any domains, sub-domains or records that are submitted in any request
   that causes record limits to be exceeded will not be provisioned and the
   entire request will be rejected.

.. note::
   The limits apply to any API request that can be used to create one or
   more records. An account may have a non-default record limit if
   determined necessary by Support.

.. _determine-limits:

Retrieve account limits
~~~~~~~~~~~~~~~~~~~~~~~

Applications can programmatically determine current rate limits and absolute
limits for an account as described in
:ref:`Limits operations<limits-operations>`.

