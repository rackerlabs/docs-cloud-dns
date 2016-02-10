.. _cdns-dg-descriptions:

Descriptions
~~~~~~~~~~~~~~

Descriptions are supported for requests and responses of zones and recordsets using the 
``description`` attribute, as demonstrated in the following example:
 
**Example 3.7. Example Response with description**

.. code::  

    Status: 200 OK
    Date: Thu, 28 Jul 2011 21:54:21 GMT
    X-API-VERSION: 1.0.17
    Content-Type: application/json
    Content-Length: 3020

    {
      "status": "ACTIVE",
      "masters": null,
      "name": "example.com.",
      "links": {
        "self": "http://127.0.0.1:9001/v2/zones/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxxx"
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
      "project_id": "noauth-project",
      "type": "PRIMARY",
      "email": "user@example.org",
      "description": "Optional zone description"
    }

Notes for descriptions:
-	Are limited to 160 characters each

-	Can be any text characters

-	Are optional

-	To remove a description, set it to the empty string, for example: description=""

-	Are returned on **GET** calls for both zones and recordsets regardless of whether the 
	call is a single or multiple call, and regardless of whether it is a detail or 
	non-detail call
