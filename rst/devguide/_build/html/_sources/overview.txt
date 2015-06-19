========
Overview
========

Rackspace Cloud *DNS* is a Domain Name System (DNS) available to
Rackspace Cloud customers. Interactions with Rackspace Cloud DNS occur
programmatically via the Rackspace Cloud DNS API as described in this
Cloud DNS Developer Guide.

.. note::

   See :ref:`DNS propagation <cdns-dg-propagation>` for information about DNS propagation.

The following figure shows an overview of Cloud DNS Infrastructure:

.. figure:: /_images/Cloud_DNS_Infographic-1.png

We welcome feedback, comments, and bug reports at `Product Feedback
Forum <http://feedback.rackspace.com>`_.

Issues and bug reports can be directed to your support team via ticket,
chat, email, or phone.

Intended audience
~~~~~~~~~~~~~~~~~

This Guide is intended to assist software developers who want to develop
applications using the Cloud DNS Service API. To use the information
provided here, you should first have a general understanding of the DNS
service. You should also be familiar with:

-  DNS terminology

-  General operating principles of DNS

-  ReSTful web services

-  HTTP/1.1 conventions

-  JSON and/or XML data serialization formats

Document change history
~~~~~~~~~~~~~~~~~~~~~~~

This version of the Developer Guide replaces and obsolesces all previous versions. The most recent changes are described in the table below:

May 15, 2015
--------------

Added note about using special characters in record searches. See http://docs.rackspace.com/cdns/api/v1.0/cdns-devguide/content/GET_searchRecords_v1.0__account__domains__domainId__records_records.html.

March 30, 2015
-----------------

Added note for exporting domain with more than 300 records. See http://docs.rackspace.com/cdns/api/v1.0/cdns-devguide/content/GET_exportDomain_v1.0__account__domains__domainId__export_domains.html.

February 25, 2015
----------------

Removed London endpoint, since we now have one global endpoint for the Rackspace Authentication
Service. See :ref:`Identity service endpoints <cdns-dg-authentication-endpoints>`.

Additional resources
~~~~~~~~~~~~~~~~~~~~

You can download the most current versions of other API-related documents from http://docs.rackspace.com/.

For more details about Rackspace Cloud DNS, refer to http://www.rackspace.com/cloud/dns. This site also offers links to Rackspace's official support channels, including knowledge center articles, forums, phone, chat, and email.

Using this API document, your Rackspace Cloud account, and at least two cloud servers, you can get started whenever you'd like. See the *Getting Started with Rackspace Cloud DNS* at http://docs.rackspace.com/ for information about getting started using the API.

Please visit our `Product Feedback Forum`_ and let us know what you think about Cloud DNS!

You can also follow Rackspace updates and announcements via `Twitter`_.

This API uses standard HTTP 1.1 response codes as documented at http://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html.

.. _Product Feedback Forum: http://feedback.rackspace.com
.. _Twitter: https://twitter.com/rackspace
