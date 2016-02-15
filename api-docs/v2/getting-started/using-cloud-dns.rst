.. _using-cloud-dns:

Create and manage DNS zones (domains)
-------------------------------------

You can use the examples in the following sections to create and manage zones (domains)
by using |apiservice| operations.

The Create zone API call provisions one or more new DNS zones, based on the configuration 
defined in the request object. To create a zone, you need to post to the **/zones** 
endpoint. If the corresponding request cannot be fulfilled due to insufficient or invalid 
data, an ``HTTP 400`` (Bad Request) error response will be returned with information 
regarding the nature of the failure in the body of the response. Failures in the
validation process are non-recoverable and require the caller to correct the cause of the 
failure and **POST** the request again.

This call returns an *asynchronous* response. In fact, **PUT**, **POST**, and **DELETE** 
|apiservice| calls are all *asynchronous*, since they may take some time to process. 
Therefore they return ``202 ACCEPTED`` responses containing information with a link URL, 
which allows the progress, status, and/or response information of the call to be
retrieved at a later point in time.

In this case, assume that you want to create a zone using ``name=example.org``.

..  note:: 

   **Zone naming** You can use any letter, number from 0 to 9, and the character 
   `-`. Ensure that you add the final period (.) at the end of your fully qualified 
   zone name (e.g. `example1234.com.`).


Choose one of the following methods:

-  :ref:`Creating a zone with the CLI<cli-create-zone>`
-  :ref:`Creating a zone with cURL<curl-create-zone>`

.. include:: examples/cli-create-zone.rst
.. include:: examples/curl-create-zone.rst

The List API call provides detailed output for a specific zone. You can only query for 
zones that you have permission to query, which are ones created using your tenant ID.

Choose one of the following methods:

-  :ref:`Listing a zone with the CLI<cli-list-zone>`
-  :ref:`Listing a zone with cURL<curl-list-zone>`

.. include:: examples/cli-list-zone.rst
.. include:: examples/curl-list-zone.rst

Create and manage record sets
-----------------------------

A record set groups together a list of related records of the same type. It is the essential
content of your zone file. Record sets are also referred to as “Resource Record Sets” or
“RRSets”. The following example creates an 'A' record set. An 'A' record set is used to map a
hostname to an IP address.

Choose one of the following methods:

-  :ref:`Creating a record set with the CLI<cli-create-recordset>`
-  :ref:`Creating a record set with cURL<curl-create-recordset>`

.. include:: examples/cli-create-recordset.rst
.. include:: examples/curl-create-recordset.rst

The List record set API call provides detailed output for a specific record set using the 
``recordset id``.

Choose one of the following methods:

-  :ref:`Listing a record set with the CLI<cli-list-recordset>`
-  :ref:`Listing a record set with cURL<curl-list-recordset>`

.. include:: examples/cli-list-recordset.rst
.. include:: examples/curl-list-recordset.rst
