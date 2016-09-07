.. _using-cloud-dns:

Create and manage DNS domains
-----------------------------

You can use the examples in the following sections to create and manage domains
by using Cloud DNS API operations.

You will perform the following tasks:

- Creating two Cloud Servers
- Creating a DNS domain
- Listing domain details
- Adding records to your domains

The DNS service is not a regionalized service. DNS is therefore responsible for
appropriate replication, caching, and overall maintenance of DNS data across
regional boundaries to other DNS servers. The followings are examples
of service access endpoints for Cloud DNS.

- ``https://dns.api.rackspacecloud.com/v1.0/1234/``
- ``https://lon.dns.api.rackspacecloud.com/v1.0/1234/``

When making a Cloud DNS API call call, place the endpoint at the beginning of
the request URL,for example:
``https://dns.api.rackspacecloud.com/v1.0/**your_acct_id**``, as you can see in
cURL request examples for this guide.

.. note::
     These examples use the ``$API_ENDPOINT``, ``$AUTH_TOKEN``, and
     ``$TENANT_ID`` environment variables to specify the API endpoint,
     authentication token, and project ID values for accessing the service.
     Make sure you
     :ref:`configure these variables<configure-environment-variables>` before
     running the code samples.

.. note::
   All examples in this guide assume that you are operating against the US
   region.

.. include:: examples/gs-create-server.rst
.. include:: examples/gs-create-domain.rst
.. include:: examples/gs-list-domain.rst
.. include:: examples/gs-add-records.rst
