.. _service-access:

========================
Service access endpoints
========================

The |apiservice| service is not a regionalized service. Therefore, the service
is responsible for appropriate replication, caching, and overall maintenance
of DNS data across regional boundaries to other DNS servers.

Use the following service access endpoint to access the |product name| service.
Replace the $TENANT_ID variable with your Rackspace Cloud account number
(for example, 123456).

- ``https://global.dns.api.rackspacecloud.com/v2/$TENANT_ID/``

You can find your account number after the final slash(/) in the ``publicURL``
field found in the service catalog that isreturned in the authentication
response. For an example of the service catalog, see the
:ref:`authentication response example <review-auth-resp>`.

The service catalog returned in the authentication response specifies the
correct service access endpoint for your account to use for accessing
|product name|. Use the service type (``managedDNS``) to locate the
correct endpoint in the service catalog. For an example of the service
catalog, see
:ref:`authentication response examples <authentication-response-examples>`.