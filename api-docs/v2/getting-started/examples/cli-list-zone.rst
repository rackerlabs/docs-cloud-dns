.. _cli-list-zone:

Listing zone with the CLI
~~~~~~~~~~~~~~~~~~~~~~~~~~

Use the **zone show** CLI command to list a zone.

``usage: openstack zone show <zone_name>``

Enter the following command:

.. code::  

     $ openstack zone show example.org.  

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
    | status         | ACTIVE                               |
    | transferred_at | None                                 |
    | ttl            | 7200                                 |
    | type           | PRIMARY                              |
    | updated_at     | 2015-10-29T21:54:39.000000           |
    | version        | 3                                    |
    +----------------+--------------------------------------+

You can see from the response that the zone has been created and is ``ACTIVE``.
