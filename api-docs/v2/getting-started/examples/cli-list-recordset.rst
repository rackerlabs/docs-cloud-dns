.. _cli-list-recordset:

Listing recordset with the CLI
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Use the **recordset show** CLI command to list a recordset.

``usage: openstack recordset show <zone_id> <recordset_id>``

Enter the following command:

.. code::  

    $ openstack recordset show b8500fe8-eff1-4523-90a4-0765cf39d273
          0536cf1c-e379-4617-a1b0-63cdd16fd671    

The response is similar to the following:

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
    | status      | ACTIVE                               |
    | ttl         | None                                 |
    | type        | A                                    |
    | updated_at  | None                                 |
    | version     | 1                                    |
    | zone_id     | b8500fe8-eff1-4523-90a4-0765cf39d273 |
    +-------------+--------------------------------------+

You can see from the response ``status`` that the recordset is
``ACTIVE``, indicating that the recordset is now created and active.

