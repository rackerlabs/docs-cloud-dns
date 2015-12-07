.. _service-access-endpoints:

Service Access/Endpoints
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The DNS service is not a regionalized service. DNS is therefore
responsible for appropriate replication, caching, and overall
maintenance of DNS data across regional boundaries to other DNS servers.

Use one of the following service access/endpoint to access the Rackspace Cloud DNS service:

- ``https://dns.api.rackspacecloud.com/v1.0/ 1234/``
- ``https://lon.dns.api.rackspacecloud.com/v1.0/ 1234/``

..  note::
    The service catalog returned in the auth response specifies the correct
    service access endpoint for your account to use for accessing DNS. Use
    the service name (cloudDNS) to locate the correct endpoint in the
    service catalog. For an example of the service catalog, see
    :ref:`authentication response examples <authentication-response-examples>`.

Replace the sample account ID number, ``1234``, with your Rackspace Cloud account number.

You can find the account number after the final '/' in the
``publicURL`` field found in the Service catalog returned in the authentication response. For an
example of the service catalog, see the :ref:`authentication response example <authentication-json-response>`.
