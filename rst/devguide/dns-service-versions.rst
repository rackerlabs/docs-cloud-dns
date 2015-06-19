====================
DNS Service versions
====================

The Cloud DNS Service version defines the contract and build
information for the API.

Contract version
~~~~~~~~~~~~~~~~

The contract version denotes the data model and behavior that the API
supports. The requested contract version is included in all request
URLs. Different contract versions of the API may be available at any
given time and are not guaranteed to be compatible with one another.

**Example: Request URL (contract version is 1.0)**

.. code::

    https://dns.api.rackspacecloud.com/v1.0/1234/domains

.. note:: This document pertains to contract version 1.0.

API version headers
~~~~~~~~~~~~~~~~~~~

Every response from the Cloud DNS Service includes custom headers that
identify the specific release version of the API that is in use. This
information is used to assist in diagnosing issues and should be
included in any support request.

**API Version Headers**

X-API-VERSION
   The deployed version of the Cloud DNS Service. This is used to identify
   releases, and it should correspond to the contract version in the URL
   (that is, v1.0). Example value: ``X-API-VERSION=1.0.8``

