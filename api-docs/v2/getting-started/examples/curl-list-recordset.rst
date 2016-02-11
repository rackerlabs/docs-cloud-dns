.. _curl-list-recordset:

Listing recordset with cURL
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The following example shows the cURL request for List recordset:

 
**Example cURL List recordset request**

.. parsed-literal::  

    curl -s \
    -H "X-Auth-Token: $token" \
    -H "Content-Type: application/json" \
    \ |apiserviceendpoint|\ $account/zones/zone_id/recordsets/recordset_id | python -m json.tool

Remember to replace the names in the examples above with their actual respective values:

-  **zone_id** — as returned in your **Create zone** response (see the examples in the 
   previous section **Creating a zone**) must be replaced in the request URL.

-  **recordset_id** — as returned in your **Creating a recordset** (see the examples in 
   the previous section **Creating a recordset**) must be replaced in the request URL.

The following example shows the response for List recordset:

**Example List recordset response**

.. parsed-literal::  

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
            "self": "\ |apiserviceendpoint|\ $account/zones/2150b1bf-dee2-4221-9d85-11f7886fb15f/recordsets/f7b10e9b-0cae-4a91-b162-562bc6096648"
        },
    }

Note that ``status`` is set to ``ACTIVE``, indicating that the recordset is now created and 
active.
