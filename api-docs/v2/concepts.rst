.. _concepts:

=========
Concepts
=========

To use the |apiservice| effectively, you should understand the following key concepts:

.. _concept-DNS:

DNS
----

The Domain Name System (DNS) is a system by which internet domain name-to-address and 
address-to-name resolutions are determined. All domains and their components, such as mail 
servers, utilize DNS to resolve to the appropriate locations. DNS servers are usually set 
up in a master-slave relationship such that failure of the master invokes the slave. DNS 
servers may also be clustered or replicated such that changes made to one DNS server are 
automatically propagated to other active servers.

.. note::
   DNS supports ASCII characters. For non ASCII characters, Punycode must be used.

.. _concept-zone:

Zone (Domain)
-------------

A zone is an entity, or container, of all DNS-related information containing one or more 
records. Zones may also be referred to as domains.

.. _concept-subzone:

Subzone
-------

Also known as second level or child zones, a subzone is any zone that is part of a larger
zone. Subzones allow you to divide and delegate a zone, also called a parent zone. Subzones 
cannot be registered and are controlled by the parent zone.

.. _concept-record:

Record
------

A DNS record belongs to a particular zone and is used to specify information about the 
zone. There are several types of DNS records. Each record type contains particular 
information used to describe that record's purpose. Examples include mail exchange (MX) 
records, which specify the mail server for a particular internet domain, and name server 
(NS) records, which specify the authoritative name servers for a domain.

.. _concept-record-set:

Record set
----------

A record set groups together a list of related records of the same type and is the essential
content of your zone file. All records in a single record set must share the same type and 
name (e.g. 'MX' and 'mydomainname.com'). Record sets are also referred to as *Resource 
Record Sets* or *RRSets*.

.. _concept-zone-owner:

Zone owner
------------

Within Rackspace Managed DNS, the account which creates the zone is the zone owner.

.. note:: 
   Internet Domain registration is currently outside the scope of the |apiservice|. Any 
   references to ownership and management of zone information is only relevant within the 
   context of the |product name| system.

