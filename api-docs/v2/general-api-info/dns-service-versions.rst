.. _cdns-dg-service-versions:

====================
DNS Service versions
====================


The |product name| Service version defines the contract and build information for the API.

Contract version
~~~~~~~~~~~~~~~~

The contract version denotes the data model and behavior that the API supports. The 
requested contract version is included in all request URLs. Different contract versions 
of the API may be available at any given time and are not guaranteed to be compatible with 
one another.

**Example: Request URL**

.. code::

    https://global.dns.api.rackspacecloud.com/v2.0/zones

.. note:: This request URL pertains to contract version 2.0.
