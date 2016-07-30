.. _curl-listing-recordset:

Getting details about a  record set with cURL
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The following example shows the cURL request for list record set operation.


**Example: List record set, cURL request**

.. code::

    curl -s \
    -H "X-Auth-Token: $AUTH_TOKEN" \
    -H "Content-Type: application/json" \
    https://global.dns.api.rackspacecloud.com/v2/$TENANT_ID/zones/{zoneId}/recordsets/{recordSetId} | python -m json.tool

Remember to replace the values in the examples with their actual respective
values:

-  **AUTH_TOKEN**

	The token that you received during authentication.  For automatic
	replacement, set your environment variables (see
	:ref:`Configure environment variables <configure-environment-variables>`).

-  **TENANT_ID**

	Your Rackspace Cloud account ID.  For automatic  replacement, set your
	environment variables (see
	:ref:`Configure environment variables <configure-environment-variables>`).

-  **zoneId**

   The zone ID returned in the ``Create zone`` response (see the examples in
   the "Create a zone" section).

-  **recordSetId**
   The ``record set ID``returned in the ``Create a record set`` response (see
   the examples in the "Create a record set" section).

The following example shows the response for the list record set operation.

**Example: List record set response**

.. code::

    HTTP/1.1 200 OK
    Vary: Accept
    Content-Type: application/json

    {
        "id": "f7b10e9b-0cae-4a91-b162-562bc6096648",
        "created_at": "2015-06-18T19:59:44.000000",
        "updated_at": null,
        "ttl": 3600,
        "name": "example.org.",
        "zone_id": "2150b1bf-dee2-4221-9d85-11f7886fb15f",
        "version": 1,
        "type": "A",
        "records": [ "10.1.0.2" ],
        "status": "ACTIVE",
        "action": "NONE",
        "description": "This is an example record set.",
        "links": {
            "self": "https://global.dns.api.rackspacecloud.com/v2/123456/zones/2150b1bf-dee2-4221-9d85-11f7886fb15f/recordsets/f7b10e9b-0cae-4a91-b162-562bc6096648"
        },
    }

The ``status`` is set to ``ACTIVE``, which indicates that the record set is now
created and active.
