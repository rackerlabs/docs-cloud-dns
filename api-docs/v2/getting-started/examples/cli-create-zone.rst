.. _cli-create-zone:

Creating a zone with the CLI 
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Use the **zone create** CLI call to create a zone with the configuration that you specify.

``usage: openstack zone create zone_name --email <EMAIL> --ttl <TTL>``

Enter the following command:

.. code::  

     $ openstack zone create example.org. --email "joe@example.org" --ttl 7200 

..  note:: 

    If you decide to change the zone name, make sure to use a valid name. You can use any 
    letter, numbers between 0 and 9, and the character "-".

The response is similar to the following:

.. code::  

    +----------------+--------------------------------------+
    | Field          | Value                                |
    +----------------+--------------------------------------+
    | action         | CREATE                               |
    | created_at     | 2015-10-29T21:54:09.000000           |
    | description    | None                                 |
    | email          | joe@example.org                      |
    | id             | b8500fe8-eff1-4523-90a4-0765cf39d273 |
    | masters        |                                      |
    | name           | example.org.                         |
    | pool_id        | 794ccc2c-d751-44fe-b57f-8894c9f5c842 |
    | project_id     | 938611                               |
    | serial         | 1446155649                           |
    | status         | PENDING                              |
    | transferred_at | None                                 |
    | ttl            | 7200                                 |
    | type           | PRIMARY                              |
    | updated_at     | None                                 |
    | version        | 1                                    |
    +----------------+--------------------------------------+

..  note:: 

    Please disregard the following warning from keystone:

    .. parsed-literal::  

       Failed to contact the endpoint at  \ |apiserviceendpoint|\ 938611 
       for discovery. Fallback to  using that endpoint as the base url. 

This request is asynchronous. So the ``status`` is set to ``PENDING`` when the zone is 
initially created. When the zone is created completely, the status is set to ``ACTIVE``. 
You will be able to see the ``ACTIVE`` status when you run the **zone show** command in 
the next section.

..  note:: 

    Refer to :ref:`Synchronous and asynchronous responses<cdns-dg-synch-asynch>` for more 
    information about how the asynchronous call works.

In the previous example, you can see that the zone ``example.org.`` was created. You will 
need the zone ``id`` returned in the response for making the Get zone call in the next 
section, and you should supply this value wherever you see the field ``zone_id`` in the 
examples in this guide.
