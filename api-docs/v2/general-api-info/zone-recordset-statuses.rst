.. _cdns-dg-zone-recordset-statuses:

============================
Zone and Record Set Statuses
============================

The |product name| service will return one of the following statuses during and after
asynchronous operations for resources and tasks:

- **ACTIVE**: The resource is active in the system and is either available or in the process of propagating to the name servers.
- **PENDING**: The request was accepted and the system is still processing.
- **DELETED**: The resource or task was deleted from the system.
- **ERROR**: An issue occurred processing the resource or task.
- **COMPLETE**: Processing for the task has completed.