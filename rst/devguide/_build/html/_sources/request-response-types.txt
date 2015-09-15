.. _cdns-dg-request-response:

==========================
Request and response types
==========================

The DNS API supports both the JSON and XML data serialization formats.
The request format is specified using the ``Content-Type`` header and is
required for calls that have a request body. The response format can be
specified in requests either by using the ``Accept`` header or by adding
an ``.xml`` or ``.json`` extension to the request URI. Note that it is
possible for a response to be serialized using a format different from
the request. If no response format is specified, JSON is the default. If
conflicting formats are specified using both an ``Accept`` header and a
query extension, the query extension takes precedence.

**Table. Response formats**

+----------+---------------------+----------------------+---------+
| Format   | Accept Header       | Query Extension      | Default |
+----------+---------------------+----------------------+---------+
| JSON     | application/json    | .json                | Yes     |
+----------+---------------------+----------------------+---------+
| XML      | application/xml     | .xml                 | No      |
+----------+---------------------+----------------------+---------+

In the request example below, notice that ``Content-Type`` is set to
``application/json``, but ``application/xml`` is requested via the
``Accept`` header:

**Example: Request with headers: XML**

.. code::

    POST https://dns.api.rackspacecloud.com/v1.0/1234/domains
    Accept: application/xml
    X-Auth-Token: ea85e6ac-baff-4a6c-bf43-848020ea3812
    Content-Type: application/json
    Content-Length: 71

    {
      "name" : "example.com",
      "emailAddress" : "sample@rackspace.com"
    }

Therefore an XML response format is returned:

**Example: Response with headers: XML**

.. code::

    Status: 202 Accepted
    Date: Thu, 28 Jul 2011 21:54:21 GMT
    X-API-VERSION: 1.0.17
    Content-Type: application/xml
    Content-Length: 453

    <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
    <asyncresponse xmlns:ns2="http://www.w3.org/2005/Atom" xmlns="http://docs.rackspacecloud.com/dns/api/v1.0" xmlns:ns3="http://docs.rackspacecloud.com/dns/api/management/v1.0">
        <jobId>e63886c9-acf0-4e5d-8023-09a0fae37446</jobId>
        <callbackUrl>https://dns.api.rackspacecloud.com/v1.0/1234/status/e63886c9-acf0-4e5d-8023-09a0fae37446</callbackUrl>
        <status>RUNNING</status>
    </asyncresponse>

An alternative method of achieving the same result is illustrated below.
This time we utilize a URI extension (``.xml``) to request an XML
response format instead of an ``Accept`` header:

**Example: Extension: XML request**

.. code::

    POST https://dns.api.rackspacecloud.com/v1.0/1234/domains.xml
    X-Auth-Token: ea85e6ac-baff-4a6c-bf43-848020ea3812
    Content-Type: application/json
    Content-Length: 71

    {
      "name" : "example.com",
      "emailAddress" : "sample@rackspace.com"
    }


