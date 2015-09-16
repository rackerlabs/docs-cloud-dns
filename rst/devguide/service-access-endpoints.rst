.. _cdns-dg-service-endpoints:

=========================
Service Access/Endpoints 
=========================

The DNS service is not a regionalized service. DNS is therefore
responsible for appropriate replication, caching, and overall
maintenance of DNS data across regional boundaries to other DNS servers.

You can find the service access/endpoint examples for Cloud DNS in the
table below.

Table. Service Access/Endpoint Examples

+-------------------------------------------------------+
| Endpoint                                              |
+=======================================================+
| ``https://dns.api.rackspacecloud.com/v1.0/1234/``     |
+-------------------------------------------------------+
| ``https://lon.dns.api.rackspacecloud.com/v1.0/1234/`` |
+-------------------------------------------------------+

..  note:: 

Replace the sample account ID number shown above, ``1234``, with your actual
Rackspace Cloud account number.

The service catalog returned in the auth response specifies the correct
service access endpoint for your account to use for accessing DNS. Use
the service name (cloudDNS) to locate the correct endpoint in the
service catalog. 

See the auth response examples in :ref:`cdns-dg-authentication`.
You will find the actual account number after the final '/' in the
``publicURL`` field returned by the authentication response. See the
example "Authenticate: JSON Response". For example, you can
see from the ``publicURL`` field for cloudServers
("https://servers.api.rackspacecloud.com/v1.0/010101") that the account
number is 010101.
