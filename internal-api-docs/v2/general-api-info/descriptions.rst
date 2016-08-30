.. _descriptions:

Descriptions
~~~~~~~~~~~~

Descriptions are supported for requests and responses of zones and record sets
by using the ``description`` attribute, as demonstrated in the following
example:

**Example Response with description**

.. code::

    Status: 200 OK
    Date: Thu, 28 Jul 2011 21:54:21 GMT
    Content-Type: application/json
    Content-Length: 3020

    {
      "status": "ACTIVE",
      "masters": null,
      "name": "example.com.",
      "links": {
        "self": "https://global.dns.rackspacecloud.com/v2/123456/zones/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxxx"
      },
      "transferred_at": null,
      "created_at": "2015-07-22T15:55:47.000000",
      "pool_id": "794ccc2c-d751-44fe-b57f-8894c9f5c842",
      "updated_at": "2015-07-22T15:55:52.000000",
      "version": 2,
      "id": "12345678-90ab-cdef-0123-abcdef012345",
      "ttl": 3600,
      "action": "NONE",
      "serial": 1437580547,
      "project_id": "123456",
      "type": "PRIMARY",
      "email": "user@example.org",
      "description": "Optional zone description"
    }

Descriptions have the following characteristics:

-	Limited to 160 characters each

-	Can be any text characters

-	Are optional

Descriptions are returned on ``GET`` operations for both zones and record sets
regardless of whether the operation is a single or multiple operation, and
regardless of whether it is a detail or non-detail operation.

To remove a description, set it to an empty string, for example:
description="".
