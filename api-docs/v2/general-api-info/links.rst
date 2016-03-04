.. _cdns-dg-links:

Links
~~~~~

A ``links`` object will exist at the root of all collection responses. At the minimum, it 
will contain a ``self`` link. If the collection resultset is not complete, a ``next`` or 
``previous`` link will be included for pagination to point to the respective items in the 
collection.

 
**Example of ``links`` in the response for a collection**

.. code::  

    HTTP/1.1 200 OK
    Vary: Accept
    Content-Type: application/json  

.. code::  

     {
       "examples": [{
         "id": "a86dba58-0043-4cc6-a1bb-69d5e86f3ca3",
         "....": "...."
       }, {
         "id": "fdd7b0dc-52a3-491e-829f-41d18e1d3ada",
         "....": "...."
       }],
       "links": {
         "self": "<URL for This Page>",
         "next": "<URL for Next Page>",
         "previous": "<URL for Previous Page>"
       }
     }   
