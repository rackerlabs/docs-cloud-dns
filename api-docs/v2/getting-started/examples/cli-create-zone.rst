.. _cli-create-zone:

Create a zone with the CLI 
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Use the ``zone create`` CLI command to create a zone (domain) with the configuration that 
you specify.

``Syntax: openstack zone create <zoneName> --email <email> --ttl <ttl>``

Enter the following command:

.. code::  

     $ openstack zone create example.org. --email "joe@example.org" --ttl 7200 

..  note:: 

    If you decide to change the zone name, be sure to use a valid name. You can use any 
    letter, numbers from 0 to 9, and the hyphen.

The response is similar to the following example:

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
    | project_id     | 123456                               |
    | serial         | 1446155649                           |
    | status         | PENDING                              |
    | transferred_at | None                                 |
    | ttl            | 7200                                 |
    | type           | PRIMARY                              |
    | updated_at     | None                                 |
    | version        | 1                                    |
    +----------------+--------------------------------------+

..  note:: 

    You can disregard the following warning from keystone:

    .. code::  

       Failed to contact the endpoint at https://global.dns.api.rackspacecloud.com/v2/123456 
       for discovery. Fallback to using that endpoint as the base url. 

This request is asynchronous, so the ``status`` is set to ``PENDING`` when the zone is 
initially created. When the zone is created completely, the status is set to ``ACTIVE``. 
To get the status of the zone, you can use the ``zone show`` command, as described in 
the next section.

..  note:: 

    For more information about how the asynchronous operations work, see 
    :ref:`Synchronous and asynchronous responses<cdns-dg-synch-asynch>` 

In the preceding example, the ``example.org.`` zone was created. You need the zone ``id`` 
that is returned in the response to get the details about the zone, and you should supply 
this value wherever you see the ``zone_id`` field in the examples in this guide.
