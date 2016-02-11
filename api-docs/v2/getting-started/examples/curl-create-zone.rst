.. _curl-create-zone:

Creating a zone with the cURL 
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Use the **Create zone** API call (``POST /zones``) to create a zone with the configuration 
that you specify.

The following example shows the cURL request for Create zone:

**Example Create zone request**

.. code::  

    curl -s -d \
    '{
        "name" : "your_zone_name",
        "email" : "joe@example.org",
        "ttl" : 7200,
        "description" : "This is an example zone."
    }' \
    -H "X-Auth-Token: $token" \
    -H "Content-Type: application/json" \
    https://dns.api.rackspacecloud.com/v2/$account/zones | python -m json.tool

Remember to replace the names in the examples above with their actual respective values 
for all the cURL examples that follow:

-  **your_zone_name** — to name your zone, you can use any letter,
   numbers between 0 and 9, and the character "-".

The following example shows the initial asynchronous responses for **Create zone**:

 
**Example Create zone: initial asynchronous response**

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
          "self": "https://dns.api.rackspacecloud.com/v2/zones/a86dba58-0043-4cc6-a1bb-69d5e86f3ca3"
        }
    }

This request is asynchronous. So the ``status`` is set to ``PENDING`` when the zone is 
initially created. When the zone is created completely, the status is set to ``ACTIVE``. 
To get the status of the zone, you can query the ``self`` link returned in the create 
response. You will see the ``ACTIVE`` status in the next section when you call the **List 
zone** operation.

..  note:: 

    Refer to  :ref:`Synchronous and asynchronous responses<cdns-dg-synch-asynch>` for more 
    information about how the asynchronous call works.  

In the previous example, you can see that the zone ``example.org.`` was created. You will 
need the zone ``id`` returned in the response for making the List zone call in the next 
section, and you should supply this value wherever you see the field **zone\_id** in the 
examples in this guide.
