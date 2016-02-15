.. _cdns-dg-resources:

Resources
~~~~~~~~~

A resource is an item you access in an API operation, such as a zone or record set.

A ``links`` object will exist inside the resource object. At the minimum, it will contain 
a ``self`` link that points to the given resource.

 
**Example Response with ``links`` in the response for a resource**

.. code::  

    HTTP/1.1 200 OK
    Vary: Accept
    Content-Type: application/json  

.. code::  

      {
       "example": {
         "id": "a86dba58-0043-4cc6-a1bb-69d5e86f3ca3",
         "....": "....",
         "links": {
           "self": "https://global.dns.api.rackspacecloud.com/v2/examples/a86dba58-0043-4cc6-a1bb-69d5e86f3ca3",
         }
       }
     } 
