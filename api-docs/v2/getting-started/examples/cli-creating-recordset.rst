.. _cli-creating-recordset:

Creating a record set with the CLI
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Use the ``recordset create`` CLI command to create a record set.

``Syntax: openstack recordset create <zoneId> <recordSetName> --records <records> --type <type>``

Enter the following command:

.. code::  

      $ openstack recordset create b8500fe8-eff1-4523-90a4-0765cf39d273 example.org. 
         --records 10.1.0.5 --type "A"   

The response is similar to the following example:

.. code::  

    +-------------+--------------------------------------+
    | Field       | Value                                |
    +-------------+--------------------------------------+
    | action      | CREATE                               |
    | created_at  | 2015-10-29T22:38:58.000000           |
    | description | None                                 |
    | id          | 0536cf1c-e379-4617-a1b0-63cdd16fd671 |
    | name        | example.org.                         |
    | records     | 10.1.0.5                             |
    | status      | PENDING                              |
    | ttl         | None                                 |
    | type        | A                                    |
    | updated_at  | None                                 |
    | version     | 1                                    |
    | zone_id     | b8500fe8-eff1-4523-90a4-0765cf39d273 |
    +-------------+--------------------------------------+

The ``status`` is set to ``PENDING`` when the record set is initially created. When the 
record set is created completely, the status is set to ``ACTIVE``. To get the status of 
the record set, you can use the ``recordset show`` CLI command, as described in the next 
section.

