.. _overview:

About the Rackspace Managed DNS API
-----------------------------------------

|product name| is a globally distributed (Anycast network) service that 
allows Rackspace customers to manage Domain Name System (DNS) zones and resource records 
via a REST-based API for their account. Interactions with |product name| occur 
programmatically via the API described in this |product name| Developer Guide.

|product name| is powered by OpenStack Designate v2.0 (DNSaaS). Duplicate zones and 
resource records may not exist between Rackspace Cloud DNS and |product name|.

..  note:: 

	-  |product name| is currently limited to Rackspace Cloud accounts.

	-  PTR records are currently supported in Rackspace Cloud DNS, but will not be supported 
	   by |product name| until the Unlimited Availability launch phase.

	- See :ref:`DNS propagation <cdns-dg-propagation>` for information about DNS propagation.

.. warning::

 	If you're using pyrax or ansible, see known issue (see 
 	:ref:`v2 EA release, March 14, 2016  <RN_20160314>`).


The following figure shows an overview of the |product name| Infrastructure:

.. figure:: /_images/Cloud_DNS_Infographic-1.png

.. toctree:: :hidden:
   :maxdepth: 3

   additional-resources
