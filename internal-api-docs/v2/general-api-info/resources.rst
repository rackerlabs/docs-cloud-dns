.. _resources:

=========
Resources
=========

A resource is an item that you access in an API operation, such as a zone or
record set.

A ``links`` object exists inside the resource object. At a minimum, it contains
a ``self`` link that points to the given resource.


**Example: Response with ``links`` for a resource**

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
