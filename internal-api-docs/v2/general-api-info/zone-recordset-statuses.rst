.. _zone-recordset-statuses:

============================
Zone and record set statuses
============================

The |product name| service returns one of the following statuses during and
after asynchronous operations for resources and tasks:

- **ACTIVE**: The resource is active in the system and is either available or
  in the process of propagating to the name servers.
- **PENDING**: The request was accepted and the system is still processing.
- **DELETED**: The resource or task was deleted from the system.
- **ERROR**: An issue occurred while processing the resource or task.
- **COMPLETE**: Processing for the task has completed.