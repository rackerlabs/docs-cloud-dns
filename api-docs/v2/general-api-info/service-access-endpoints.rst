.. _service-access-endpoints:

Service Access/Endpoints
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Because |product name| service is not a regionalized service, the service is therefore 
responsible for appropriate replication, caching, and overall maintenance of DNS data 
across regional boundaries to other DNS servers.

Use the following service access/endpoint to access the |product name| service:

- ``https://global.dns.api.rackspacecloud.com/v2/123456/``

Replace the sample account ID number, ``1234``, with your Rackspace Cloud account number.

You can find your account number after the final '/' in the ``publicURL`` field found in 
the Service catalog returned in the authentication response. For an example of the service 
catalog, see the :ref:`authentication response example <review-auth-resp>`.

..  note::
    The service catalog returned in the auth response specifies the correct service access 
    endpoint for your account to use for accessing |product name|. Use the service type 
    (dns) to locate the correct endpoint in the service catalog. For an example of the 
    service catalog, see :ref:`authentication response examples <review-auth-resp>`.
