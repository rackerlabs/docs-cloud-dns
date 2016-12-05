.. _name-server-setup:

Set up name servers with your domain registrar
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Configure the name servers for your domain to ensure that your domain resolves
properly. You can do this through your domain name registrar or by delegating a
subzone from another zone.

.. note:: 
   Rackspace cannot automatically verify domain ownership. 
   Be sure to add the domain to your Rackspace account before adding the
   Rackspace name servers at your registrar. 
   When deleting a domain, remove the Rackspace name servers
   from your registrar prior to removing the domain from your Rackspace account.
   Contact Support with any questions or concerns.

Following are the authoritative |product name| name servers:

- ``ns.rackspace.com``
- ``ns2.rackspace.com``

Domains provisioned by using Rackspace Cloud DNS default to the
``dns1.stabletransit.com`` and ``dns2.stabletransit.com`` name servers for the
Rackspace public cloud. Because all Rackspace DNS has been consolidated under
``ns.rackspace.com`` and ``ns2.rackspace.com``, the ``stabletransit`` names now
resolve to these name servers.

When |product name| domains are provisioned, the system, by default, adds name
server records for ``ns.rackspace.com`` and ``ns2.rackspace.com`` to phase out
the ``stabletransit`` name servers. Although not required, customers can update
their older Rackspace Cloud DNS domain delegation and name server records to
specify ``ns.rackspace.com`` and ``ns2.rackspace.com``.
