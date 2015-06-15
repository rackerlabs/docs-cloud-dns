========
Concepts
========

To use the DNS API effectively, you should understand several key
concepts:

DNS
---

The Domain Name System (DNS) is a system by which internet domain
name-to-address and address-to-name resolutions are determined. All
domains and their components, such as mail servers, utilize DNS to
resolve to the appropriate locations. DNS servers are usually set up in
a master-slave relationship such that failure of the master invokes the
slave. DNS servers may also be clustered or replicated such that changes
made to one DNS server are automatically propagated to other active
servers.

.. note::
   DNS understands only ASCII, so the Cloud DNS Service provides conversion
   between UTF-8 and ASCII on all calls into the system.

Domain
------

A domain is an entity/container of all DNS-related information
containing one or more records.

Subdomain
---------

Subdomains are domains within a parent domain, and subdomains cannot be
registered. Subdomains allow you to delegate domains. Subdomains can
themselves have subdomains, so third-level, fourth-level, fifth-level,
and deeper levels of nesting are possible.

Record
------

A DNS record belongs to a particular domain and is used to specify
information about the domain. There are several types of DNS records.
Each record type contains particular information used to describe that
record's purpose. Examples include mail exchange (MX) records, which
specify the mail server for a particular domain, and name server (NS)
records, which specify the authoritative name servers for a domain.

Domain Owner
------------

Within Rackspace DNS, the account which creates the domain is the domain
owner.

.. note:: 
   Domain registration is currently outside the scope of the Rackspace DNS
   API. Any references to ownership and management of domain information is
   only relevant within the context of the Rackspace DNS system.

