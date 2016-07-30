.. _synch-asynch:

======================================
Synchronous and asynchronous responses
======================================

All create, update, and delete operations can be either synchronous or
asynchronous.

With *synchronous* requests, the user waits until the operation returns with
the specified code and response body.

With *asynchronous* requests, the user receives status information and can
determine when the operation is complete at a later time. In other words, the
user does not need to wait for the results before continuing.

To determine whether a given API operation was synchronous or asynchronous,
examine the HTTP status of the operation.

- Synchronous create, update, or delete API operations return an HTTP status of
  ``201 Created``, ``200 OK``, or ``204 No Content``, respectively.
  Additionally, resources that contain a ``status`` property *must* have the
  value ``ACTIVE``.

- Asynchronous create, update, or delete API operation return an HTTP status
  of ``202 Accepted``. The ``status`` property *must not* have the value
  ``ACTIVE``.

You can use the following two methods to check whether an asynchronous request
is complete.

Query the collections link method:
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Query the collections link (where examples of collections include zones or
record sets). For example:

.. code::

	`https://global.dns.api.rackspacecloud.com/v2/123456/zones`.

You can filter collections by status. For example:

.. code::

	`https://global.dns.api.rackspacecloud.com/v2/123456/zones?status=PENDING`.

Query the self link method:
~~~~~~~~~~~~~~~~~~~~~~~~~~~

Query the ``self`` link included in a given response and check the value of the
``status`` property. If the job is complete, the ``status`` field is
``ACTIVE``.  For example:

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
      "project_id": "123456",
      "email": "hostmaster@example.com",
      "links": {
      "self": "https://global.dns.api.rackspacecloud.com/v2/123456/zones/a4e29ed3-d7a4-4e4d-945d-ce64678d3b94"
    }
