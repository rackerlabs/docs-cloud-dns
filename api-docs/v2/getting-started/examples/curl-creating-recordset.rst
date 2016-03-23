.. _curl-creating-recordset:

Creating a record set with cURL
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The following examples show the cURL request for create record set operation:

**Example: Create record set, cURL request**

.. code::  

    curl -s -d \
    '{
      "name" : "example.org.",
      "description" : "This is an example record set.",
      "type" : "A",
      "ttl" : 3600,
      "records" : [
          "10.1.0.2"
      ]
    }' \
    -H "X-Auth-Token: $AUTH_TOKEN" \
    -H "Content-Type: application/json" \
    https://global.dns.api.rackspacecloud.com/v2/$TENANT_ID/zones/{zoneId}/recordsets | python -m json.tool

Remember to replace the values in the example with actual respective values:

Request body:

-  **name** 

   The name you used in the create zone request (see the examples in the "Create a zone" 
   section).

-  **AUTH_TOKEN**

   The token that you received during authentication.  For automatic replacement, set your 
   environment variables (see :ref:`Configure environment variables <configure-environment-variables>`).

-  **TENANT_ID** 
   
   Your Rackspace Cloud account ID.  For automatic  replacement, set your environment 
   variables (see :ref:`Configure environment variables <configure-environment-variables>`).

-  **zoneId** 

   The ID returned in the create zone response (see the examples in the "Create a zone" 
   section).

The following example shows the response for the create record set operation:
 
**Example: Create record set, cURL response**

.. code::  

    HTTP/1.1 202 Accepted
    Content-Type: application/json

    {
        "id": "f7b10e9b-0cae-4a91-b162-562bc6096648",
        "created_at": "2015-06-18T19:59:44.000000",
        "updated_at": null,
        "ttl": 3600,
        "name": "example.org.",
        "zone_id": "a86dba58-0043-4cc6-a1bb-69d5e86f3ca3",
        "version": 1,
        "type": "A",
        "records": [ "10.1.0.2" ],
        "status": "PENDING",
        "action": "CREATE",
        "description": "This is an example record set.",
        "links": {
            "self": "https://global.dns.api.rackspacecloud.com/v2/123456/zones/a86dba58-0043-4cc6-a1bb-69d5e86f3ca3/recordsets/f7b10e9b-0cae-4a91-b162-562bc6096648"
        }
    }

This request is asynchronous, so the ``status`` is set to ``PENDING`` when the record set is 
initially created. When the record set is created completely, the ``status`` is set to 
``ACTIVE``. To get the status of the record set, you can query the ``self`` link returned in 
the create record set response.
