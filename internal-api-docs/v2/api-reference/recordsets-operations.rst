.. _recordsets-operations:

Record set operations
~~~~~~~~~~~~~~~~~~~~~


There are record set operations to view information about the record sets for a
specified zone or across all zones.

If you wish to manage recordsets within a specific zone, uses the following
operations:

	- :ref:`Create a record set <POST_createRecordset_v2__account_id__zones__zone_id__recordsets_recordsets>`
	- :ref:`List all record sets for a zone <GET_listRecordsets_v2__account_id__zones__zone_id__recordsets_recordsets>`
	- :ref:`List a record set for a zone <GET_listRecordset_v2__account_id__zones__zone_id__recordsets__recordset_id__recordsets>`
	- :ref:`Update a record set <PUT_updateRecordset_v2__account_id__zones__zone_id__recordsets__recordset_id__recordsets>`
	- :ref:`Delete a record set <DELETE_deleteRecordset_v2__account_id__zones__zone_id__recordsets__recordset_id__recordsets>`

If you prefer to work across all zones, use the following operations:

	- :ref:`List all record sets <GET_listRecordsets_v2__account_id__recordsets_recordsets>`
	- :ref:`List a record set <GET_listRecordset_v2__account_id__recordsets__recordset_id__recordsets>`


.. include:: methods/POST_createRecordset_v2__account_id__zones__zone_id__recordsets_recordsets.rst
.. include:: methods/GET_listRecordsets_v2__account_id__zones__zone_id__recordsets_recordsets.rst
.. include:: methods/GET_listRecordset_v2__account_id__zones__zone_id__recordsets__recordset_id__recordsets.rst
.. include:: methods/PUT_updateRecordset_v2__account_id__zones__zone_id__recordsets__recordset_id__recordsets.rst
.. include:: methods/DELETE_deleteRecordset_v2__account_id__zones__zone_id__recordsets__recordset_id__recordsets.rst

.. include:: methods/GET_listRecordsets_v2__account_id__recordsets_recordsets.rst
.. include:: methods/GET_listRecordset_v2__account_id__recordsets__recordset_id__recordsets.rst
