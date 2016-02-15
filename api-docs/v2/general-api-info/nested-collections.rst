.. _cdns-dg-nested-colls:

Nested Collections
~~~~~~~~~~~~~~~~~~

A nested collection is a collection without a URI of its own. The only current example of 
this is the ``records`` array underneath the ``recordsets`` resource.

By default, nested collections are included in the listing of its parent resource. For 
example, listing record sets will include the ``records`` collection for each of the 
``recordsets`` returned. For an example, see the List Record Sets operation.
