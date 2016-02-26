.. _name-server-setup:

Name server setup with your Domain Registrar
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Before beginning, configure the name servers for your domain to make sure your domain 
resolves properly. This can be done through your domain name registrar or by delegating a 
sub-zone from another zone. 

|product name| Name Servers
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Our official authoritative name servers are: 

- ``ns.rackspace.com``
- ``ns2.rackspace.com``

Domains provisioned using Rackspace Cloud DNS default to the ``dns1.stabletransit.com`` and 
``dns2.stabletransit.com`` name servers for our public cloud. Because all Rackspace DNS has 
since been consolidated under ``ns.rackspace.com`` and ``ns2.rackspace.com``, and the 
stabletransit names now resolve to ns/ns2 name servers as well. 

When |product name| domains are provisioned, the system will, by default, add NS records 
for ``ns.rackspace.com`` and ``ns2.rackspace.com`` to phase out the stabletransit name 
servers. While not required, customers can update their older Rackspace Cloud DNS domain 
delegation and name server records to specify ``ns.rackspace.com`` and ``ns2.rackspace.com``.