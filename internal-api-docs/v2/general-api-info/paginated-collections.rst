.. _paginated-collections:

======================
Pagination and sorting
======================

Collection responses include a ``links`` object that contains absolute URLs for
the next and previous pages. These links may be omitted, or null, at the edges
of a paginated collection.

Pagination and sorting is available on all collections and is controlled using
a combination of four query parameters:

- **marker**: ID of the last item in the previous list
- **limit**: Sets the page size.
- **sort_key**: Attribute used for sorting
- **sort_dir**: Direction (``asc`` for ascending and ``desc`` for descending)

For example:
``marker=<uuid>&limit=<integer>&sort_key=<string>&sort_dir<string>``.

To navigate the collection, the parameters ``limit`` and ``marker`` can be set
in the URI (for example: ``?limit=100&marker=<uuid>``). Both parameters are
optional.

Items are sorted by create time in descending order. When a create time is not
available, they are sorted by ID. To sort results, set the ``sort_key`` query
parameter to a valid attribute (for example, ``name``or ``email``). To sort in
descending order, specify add the ``sort_dir=desc`` query parameter.

**Example: Request for a paginated collection of zones**

.. code::

    GET /v2/zones?marker=c74af170-0673-11e3-8ffd-0800200c9a66&limit=2 HTTP/1.1
     Host: global.dns.api.rackspacecloud.com
     Accept: application/json
     X-Auth-Token: ************


**Example: Response for a paginated collection of zones**

.. code::

    HTTP/1.1 200 OK
    Content-Type: application/json

    {
      "zones": [
        {
          "status": "ACTIVE",
          "masters": [],
          "name": "joe1.com.",
          "links": {
            "self": "https://global.dns.api.rackspacecloud.com/v2/123456/zones/bb069ab4-85e7-47ab-b949-0587c84f4ac1"
          },
          "transferred_at": null,
          "created_at": "2016-02-23T15:46:21.000000",
          "pool_id": "794ccc2c-d751-44fe-b57f-8894c9f5c842",
          "updated_at": "2016-02-23T15:46:29.000000",
          "version": 3,
          "id": "bb069ab4-85e7-47ab-b949-0587c84f4ac1",
          "ttl": 300,
          "action": "NONE",
          "serial": 1456242381,
          "project_id": "123456",
          "type": "PRIMARY",
          "email": "user1@user1.com",
          "description": "poo poo"
        },
        {
          "status": "ACTIVE",
          "masters": [],
          "name": "joe2.com.",
          "links": {
            "self": "https://global.dns.api.rackspacecloud.com/v2/123456/zones/43400f29-815f-4357-8474-336ea6a40d0a"
          },
          "transferred_at": null,
          "created_at": "2016-02-23T15:46:41.000000",
          "pool_id": "794ccc2c-d751-44fe-b57f-8894c9f5c842",
          "updated_at": "2016-02-23T15:47:01.000000",
          "version": 3,
          "id": "43400f29-815f-4357-8474-336ea6a40d0a",
          "ttl": 300,
          "action": "CREATE",
          "serial": 1456242401,
          "project_id": "123456",
          "type": "PRIMARY",
          "email": "user1@user1.com",
          "description": "poo poo"
        }
      ],
      "links": {
        "self": "https://global.dns.api.rackspacecloud.com/v2/123456/zones?marker=8bbad290-dc58-42b9-a190-464e21b6497c&limit=2",
        "next": "https://global.dns.api.rackspacecloud.com/v2/123456/zones?limit=2&marker=43400f29-815f-4357-8474-336ea6a40d0a"
      },
      "metadata": {
        "total_count": 7
      }
    }
