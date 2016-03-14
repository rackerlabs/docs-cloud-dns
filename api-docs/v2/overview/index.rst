.. _overview:

About the Rackspace Managed DNS API
-----------------------------------------

The |apiservice| enables developers to view and manage domains, subdomains, and records 
through a simple Representational State Transfer (REST) web service interface.

For more information about the |product name| service, see the :how-to:`Managed DNS FAQ <managed-dns-faq>`
in the Rackspace How-To. 

|product name| is a globally distributed (Anycast network) service that 
enables Rackspace customers to manage Domain Name System (DNS) zones and resource records 
via a REepresentational State Transfer (REST) based API for their account. Interactions with |product name| occur 
programmatically via the API described in this |product name| Developer guide.

|product name| is powered by OpenStack Designate v2.0 (DNSaaS). Duplicate zones and 
resource records may not exist between Rackspace Cloud DNS and |product name|.

..  note:: 

	-  |product name| is currently limited to Rackspace Cloud accounts.

	-  PTR records are currently supported in Rackspace Cloud DNS but will not be supported 
	   by |product name| until the Unlimited Availability launch phase.

	- For information about DNS propagation, see :ref:`DNS propagation <cdns-dg-propagation>`.

.. warning::

 	If you're using pyrax or ansible, see the known issue, described in 
 	:ref:`v2 EA release, March 14, 2016  <RN_20160314>`.


The following figure shows an overview of the |product name| infrastructure:

.. figure:: /_images/Cloud_DNS_Infographic-1.png

.. toctree:: :hidden:
   :maxdepth: 3

   additional-resources
