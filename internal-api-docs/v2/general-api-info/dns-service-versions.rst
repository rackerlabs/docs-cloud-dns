.. _service-versions:

====================
DNS service versions
====================


The |product name| service version defines the contract and build information
for the API.

Contract version
~~~~~~~~~~~~~~~~

The contract version denotes the data model and behavior that the API supports.
The requested contract version is included in all request URLs. Different
contract versions of the API might be available at any given time and are not
guaranteed to be compatible with one another.

In the following example, the request URL pertains to contract version 2.0.

**Example: Request URL**

.. code::

    https://global.dns.api.rackspacecloud.com/v2/$TENANT_ID/zones
