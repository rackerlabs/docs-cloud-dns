.. _curl-list-zone:

Listing zone with cURL
~~~~~~~~~~~~~~~~~~~~~~~~~~

This operation does not require a request body.

The following example shows the cURL request for List zone:

**Example List zone request**

.. code::  

    curl -s  \
    -H "X-Auth-Token: $AUTH_TOKEN" \
    -H "Accept: application/json"  \
    https://global.dns.api.rackspacecloud.com/v2/$TENANT_ID/zones/{zone_id} | python -m json.tool

Remember to replace the names in the examples above with their actual respective values 
for all the cURL examples that follow:

Header:

-  **AUTH_TOKEN** - the token you received during authentication.  For automatic 
   replacement, set your environment variables 
   (see :ref:`Configure environment variables <configure-environment-variables>`).

URL:

-  **TENANT_ID** - your Rackspace Cloud account ID.  For automatic  replacement, set your 
   environment variables (see :ref:`Configure environment variables <configure-environment-variables>`).
   
-  **zone_id** — as returned in your create zone response.

The following example shows the List zone response:

**Example List zone response**

.. code::  

    HTTP/1.1 200 OK
    Vary: Accept
    Content-Type: application/json

    {
        "id": "a86dba58-0043-4cc6-a1bb-69d5e86f3ca3",
        "pool_id": "572ba08c-d929-4c70-8e42-03824bb24ca2",
        "project_id": "123456",
        "name": "example.org.",
        "email": "joe@example.org.",
        "ttl": 7200,
        "serial": 1404757531,
        "status": "ACTIVE",
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

You can see from the response that the zone has been created and is ``ACTIVE``.

..  note:: 

    If you have multiple zones or records and want to get a subset of them, you could 
    paginate, sort or filter the results. See :ref:`Pagination<cdns-paginated-collections>` 
    or :ref:`Filtering<cdns-dg-filtering>` for more information.
    
