.. _cdns-dg-synch-asynch:

======================================
Synchronous and asynchronous responses
======================================

All Create, Update, and Delete operations can be either synchronous or asynchronous.

With *synchronous* requests, the caller waits until the call returns with the specified 
code and response body.

With *asynchronous* requests, the caller receives status information and can determine when 
the operation is complete at a later time. In other words, the caller does not need to wait 
for the results before continuing.

To determine whether a given API call was synchronous or asynchronous, examine the HTTP
status of the operation.

- Synchronous Create/Update/Delete API calls will return an HTTP status of 201 Created, 
  200 OK, or 204 No Content respectively. Additionally, resources which contain a ``status`` 
  property *must* have the value ``ACTIVE``.

- Asynchronous Create/Update/Delete API calls will return an HTTP status of 202 Accepted. 
  The ``status`` property *must not* have the value ``ACTIVE``.

The following two methods show how to check whether an asynchronous request is complete:

Method 1:

Query the collections link (where examples of collections include zones or recordsets). For 
example: 

.. code::

	`https://dns.api.rackspacecloud.com/v2/1234/zones <http://localhost:9001/v2/zones>`__.
	
You can filter collections by status. For example:

.. code::

	`https://dns.api.rackspacecloud.com/v2/1234/zones?status=PENDING <http://localhost:9001/v2/zones?status=PENDING>`__.
	
Method 2:

Query the ``self`` link included in a given response and check the value of the ``status`` 
property. If the job is complete, the ``status`` field will be ``ACTIVE``..  For example:

 .. code::  

    {
      "status": "ACTIVE",
      "description": null,
      "updated_at": "2014-07-08T20:28:31.000000",
      "ttl": 86400,
      "serial": 1404851315,
      "id": "a4e29ed3-d7a4-4e4d-945d-ce64678d3b94",
      "name": "example.com.",
      "created_at": "2014-07-08T20:28:19.000000",
      "pool_id": "572ba08c-d929-4c70-8e42-03824bb24ca2",
      "version": 1,
      "project_id": "noauth-project",
      "email": "hostmaster@example.com",
      "links": {
      "self": "http://dns.provider.com/v2/zones/a4e29ed3-d7a4-4e4d-945d-ce64678d3b94"
    }


