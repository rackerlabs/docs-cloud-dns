.. _use-cloud-dns:

Use Managed DNS
-------------------------------------

The following sections show you how to use managed DNS to create and manage zones and 
record sets.

Creating DNS zones (domains)
-------------------------------------

You can use the examples in this sections to create zones (domains) by using |apiservice| 
operations.

The create zone API operation provisions one or more new DNS zones, based on the 
configuration defined in the request object. To create a zone, you send a **POST** to the 
**/zones** endpoint. 

This operation returns an *asynchronous* response. In fact, **PUT**, **POST**, and **DELETE** 
|apiservice| operations are all *asynchronous*, because they might take some time to process. 
Therefore they return ``202 ACCEPTED`` responses containing information with a link URL, 
which allows the progress, status, or response information of the operation to be
retrieved at a later point in time.

.. note::
   
   If the request cannot be fulfilled due to insufficient or invalid data, an ``HTTP 400`` 
   (Bad Request) error response will be returned with information about the nature of the 
   failure in the body of the response. Failures in the validation process are non-recoverable 
   and require you to correct the cause of the failure and resend the request.


In this case, assume that you want to create a zone by using ``name=example.org``.

..  note:: 

   When you name a zone, you can use any letter, numbers from 0 to 9, and a hyphen. Ensure 
   that you add the final period (.) at the end of your fully qualified zone name (for
   example, ``example1234.com.``).


Choose one of the following methods:

-  :ref:`Creating a zone with the CLI<cli-creating-zone>`
-  :ref:`Creating a zone with cURL<curl-creating-zone>`

.. include:: examples/cli-creating-zone.rst
.. include:: examples/curl-creating-zone.rst

Getting details about DNS zones (domains)
------------------------------------------

Use the ``list zone`` API operation or the ``zone show`` CLI command to get detailed output 
for a specific zone by using the ``zone UID``. You can query only zones that you have 
permission to query, which are ones created using your tenant ID.

Choose one of the following methods:

-  :ref:`Getting details about a zone with the CLI<cli-listing-zone>`
-  :ref:`Getting details about with cURL<curl-listing-zone>`

.. include:: examples/cli-listing-zone.rst
.. include:: examples/curl-listing-zone.rst

Create record sets
-----------------------------

A record set groups together a list of related records of the same type. It is the essential
content of your zone file. Record sets are also referred to as *Resource Record Sets* or
*RRSets*. The following examples create an A record set. An A record set is used to map a
hostname to an IP address.

Choose one of the following methods:

-  :ref:`Creating a record set with the CLI<cli-creating-recordset>`
-  :ref:`Creating a record set with cURL<curl-creating-recordset>`

.. include:: examples/cli-creating-recordset.rst
.. include:: examples/curl-creating-recordset.rst

Get details about record sets
-------------------------------------

Use the ``list record set`` API operation or the ``recordset show`` CLI command to get 
detailed output for a specific record set by using the ``recordset id``.

Choose one of the following methods:

-  :ref:`Getting details about a record set with the CLI<cli-listing-recordset>`
-  :ref:`Getting deatils about a record set with cURL<curl-listing-recordset>`

.. include:: examples/cli-listing-recordset.rst
.. include:: examples/curl-listing-recordset.rst
