.. _index:

===========================================================
|apiservice| |contract version| )
===========================================================

*Last updated:* |today|

The |apiservice| enables developers to view and manage domains, subdomains, and
records through a simple Representational State Transfer (REST) web service
interface.

For more information about the |product name| service, see the
:how-to:`Managed DNS FAQ <managed-dns-faq>` in the Rackspace How-To.

|product name| is a globally distributed (Anycast network) service that
enables Rackspace customers to manage Domain Name System (DNS) zones and
resource records via a REepresentational State Transfer (REST) based API for
their account. Interactions with |product name| occur programmatically via the
API described in this |product name| API guide.

|product name| is powered by OpenStack Designate v2.0 (DNSaaS). Duplicate zones
and resource records may not exist between Rackspace Cloud DNS and
|product name|.

This guide is intended to assist software developers who want to develop
applications by using the |product name| service REST application programming
interface (API). It fully documents the |apiservice|, which enables developers
to interact with the components of the service.

To use the information provided here, you should have a general understanding
of the DNS service. You should also be familiar with the following
technologies:

-	DNS terminology
-  General operating principles of DNS
-  RESTful web services
-  HTTP/1.1 conventions
-  JSON data serialization format

..  note::

	-  |product name| is currently limited to Rackspace Cloud accounts.

	-  PTR records are currently supported in Rackspace Cloud DNS but will not
	   be supported by |product name| until the Unlimited Availability launch
	   phase.

	- For information about DNS propagation, see
	  :ref:`DNS propagation <propagation>`.

.. warning::

 	If you're using pyrax or ansible, see the known issue, described in
 	:ref:`v2 EA release, March 14, 2016  <RN_20160314>`.


The following figure shows an overview of the |product name| infrastructure:

.. figure:: /_images/Cloud_DNS_Infographic-1.png


Use the following links to get user and reference information for using the
|product name|  service REST API.

- :ref:`Getting Started Guide<getting-started-guide>`
- :ref:`General API information <general-api-info>`
- :ref:`API reference <api-reference>`
- :ref:`Release Notes <release-notes-collection>`

.. note::

   You can also use |product name| from the Cloud Control Panel or by using
   one of the language-specific
   :rax-devdocs:`software development kits or the rack CLI <#sdks>`.

.. toctree:: :hidden:
   :maxdepth: 3

   Managed DNS v2.0 <self>
   getting-started/index
   general-api-info/index
   api-reference/index
   release-notes/index
   service-updates
   additional-resources
   copyright
