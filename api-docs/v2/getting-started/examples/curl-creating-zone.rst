.. _curl-creating-zone:

Creating a zone with cURL 
~~~~~~~~~~~~~~~~~~~~~~~~~~

Use the ``create zone`` API operation (``POST /zones``) to create a zone with the 
configuration that you specify.

The following example shows the cURL request for the create zone operation.

**Example: Create zone, cURL request**

.. code::  

    curl -s -d \
    '{
        "name" : "your_zone_name",
        "email" : "joe@example.org",
        "ttl" : 7200,
        "description" : "This is an example zone."
    }' \
    -H "X-Auth-Token: $AUTH_TOKEN" \
    -H "Content-Type: application/json" \
    https://global.dns.api.rackspacecloud.com/v2/$TENANT_ID/zones | python -m json.tool

Remember to replace the values in the example with their actual values.

-  **AUTH_TOKEN** 

	The token that you received during authentication.  For automatic replacement, set your 
	environment variables (see 
	:ref:`Configure environment variables <configure-environment-variables>`).

-  **TENANT_ID** 

	Your Rackspace Cloud account ID.  For automatic  replacement, set your environment 
	variables (see :ref:`Configure environment variables <configure-environment-variables>`).
   
-  **name**
	
	To name your zone, you can use any letter, numbers from 0 to 9, and the hyphen.

The following example shows the initial asynchronous responses for the operation.
 
**Example: Create zone, initial asynchronous response**

.. code::  

    HTTP/1.1 202 Accepted
    Content-Type: application/json

    {
        "id": "a86dba58-0043-4cc6-a1bb-69d5e86f3ca3",
        "pool_id": "572ba08c-d929-4c70-8e42-03824bb24ca2",
        "project_id": "123456",
        "name": "example.org.",
        "email": "joe@example.org.",
        "ttl": 7200,
        "serial": 1404757531,
        "status": "PENDING",
        "description": "This is an example zone.",
        "masters": [],
        "type": "PRIMARY",
        "transferred_at": null,
        "version": 1,
        "created_at": "2015-06-18T18:25:31.275934",
        "updated_at": null,
        "links": {
          "self": "https://global.dns.api.rackspacecloud.com/v2/123456/zones/a86dba58-0043-4cc6-a1bb-69d5e86f3ca3"
        }
    }

Because this request is asynchronous, the ``status`` is set to ``PENDING`` when the zone is 
initially created. When the zone is created completely, the status is set to ``ACTIVE``. 
To get the status of the zone, you can query the ``self`` link returned in the create 
response. You will see the ``ACTIVE`` status when you use the ``list zone`` operation.

..  note:: 

    For more information about how the asynchronous call works, see 
    :ref:`Synchronous and asynchronous responses<cdns-dg-synch-asynch>` .  

In the preceding example, the zone was created. You need the zone ``id`` that is returned 
in the response to get details about the zone, and you should supply this value wherever 
you see the **zone_id** field in the examples in this guide.
