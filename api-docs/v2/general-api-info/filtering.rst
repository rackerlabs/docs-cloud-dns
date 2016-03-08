.. _cdns-dg-filtering:

Filtering
~~~~~~~~~

Filtering is available on all collections and is controlled by using query parameters that  
match the name of the attribute being filtered.

The following attributes support filtering:

-  **Record sets**: ``name``, ``type``, ``ttl``, ``data``, ``description``, ``status``

-  **Zones**: ``name``, ``email``, ``ttl``, ``description``, ``status``

Filters can be an exact match search or a wildcard search. Wildcard search is 
supported by using the asterisk (*) character.

The following example filters a collection of zones by the ``name`` parameter.

 
**Example: Request to filter a collection of zones**

.. code::  

     GET /v2/zones?name=example.com. HTTP/1.1 
     Host: global.dns.api.rackspacecloud.com
     Accept: application/json
     X-Auth-Token: *************  

 
**Example: Response to filter a collection of zones**

.. code::  

    HTTP/1.1 200 OK
    Content-Type: application/json

    {
      "zones": [{
        "status": "ACTIVE",
        "description": null,
        "updated_at": "2014-07-08T20:28:31.000000",
        "ttl": 86400,
        "serial": 1404851315,
        "id": "a4e29ed3-d7a4-4e4d-945d-ce64678d3b94",
        "name": "example.com.",
        "created_at": "2014-07-08T20:28:19.000000",
        "pool_id": "572ba08c-d929-4c70-8e42-03824bb24ca2",
        "version": 1,
        "project_id": "123456",
        "email": "hostmaster@example.com",
        "links": {
          "self": "https://global.dns.api.rackspacecloud.com/v2/123456/zones/a4e29ed3-d7a4-4e4d-945d-ce64678d3b94"
        }
      }],
      "links": {
        "self": "https://global.dns.api.rackspacecloud.com/v2/123456/zones?name=example.com."
      },
      "metadata": {
        "total_count": 1
      }
    } 

Wildcards can be placed anywhere within the query. The following example demonstrates the 
use of wildcards on the right side of a query:

 
**Example: Request to filter with a wildcard**

.. code::  

    GET /v2/zones?name=example* HTTP/1.1
    Host: global.dns.api.rackspacecloud.com
    Accept: application/json
    X-Auth-Token: ************* 

 
**Example: Response to filter with a wildcard**

.. code::  

    HTTP/1.1 200 OK
    Content-Type: application/json

    {
      "zones": [{
        "status": "ACTIVE",
        "description": null,
        "updated_at": "2014-07-08T20:28:31.000000",
        "ttl": 86400,
        "serial": 1404851315,
        "id": "a4e29ed3-d7a4-4e4d-945d-ce64678d3b94",
        "name": "example.com.",
        "created_at": "2014-07-08T20:28:19.000000",
        "pool_id": "572ba08c-d929-4c70-8e42-03824bb24ca2",
        "version": 1,
        "project_id": "123456",
        "email": "hostmaster@example.com",
        "links": {
          "self": "https://global.dns.api.rackspacecloud.com/v2/123456/zones/a4e29ed3-d7a4-4e4d-945d-ce64678d3b94"
        }
      },
      {
        "status": "ACTIVE",
        "description": null,
        "updated_at": null,
        "ttl": 3600,
        "serial": 1405435142,
        "id": "38dbf635-45cb-4873-8300-6c273f0283c7",
        "name": "example.org.",
        "created_at": "2014-07-15T14:39:02.000000",
        "pool_id": "572ba08c-d929-4c70-8e42-03824bb24ca2",
        "version": 1,
        "project_id": "123456",
        "email": "hostmaster@example.org",
        "links": {
          "self": "https://global.dns.api.rackspacecloud.com/v2/123456/zones/38dbf635-45cb-4873-8300-6c273f0283c7"
        }
      }],
      "links": {
        "self": "https://global.dns.api.rackspacecloud.com/v2/123456/zones?name=example*"
      },
      "metadata": {
        "total_count": 2
      }
    } 

The following example demonstrates the use of multiple wildcards.

 
**Example: Request to filter with multiple wildcards**

.. code::  

    GET /v2/zones?name=*example* HTTP/1.1
    Host: global.dns.api.rackspacecloud.com
    Accept: application/json
    X-Auth-Token: ************* 

 
**Example: Response to filter with multiple wildcards**

.. code::  

    HTTP/1.1 200 OK
    Content-Type: application/json

    {
      "zones": [{
        "status": "ACTIVE",
        "description": null,
        "updated_at": "2014-07-08T20:28:31.000000",
        "ttl": 86400,
        "serial": 1404851315,
        "id": "a4e29ed3-d7a4-4e4d-945d-ce64678d3b94",
        "name": "example.com.",
        "created_at": "2014-07-08T20:28:19.000000",
        "pool_id": "572ba08c-d929-4c70-8e42-03824bb24ca2",
        "version": 1,
        "project_id": "123456",
        "email": "hostmaster@example.com",
        "links": {
          "self": "https://global.dns.api.rackspacecloud.com/v2/123456/zones/a4e29ed3-d7a4-4e4d-945d-ce64678d3b94"
        }
      },
      {
        "status": "ACTIVE",
        "description": null,
        "updated_at": null,
        "ttl": 3600,
        "serial": 1405435099,
        "id": "13db810b-917d-4898-bc28-4d4ee370d20d",
        "name": "abc.example.com.",
        "created_at": "2014-07-15T14:38:19.000000",
        "pool_id": "572ba08c-d929-4c70-8e42-03824bb24ca2",
        "version": 1,
        "project_id": "123456",
        "email": "hostmaster@example.com",
        "links": {
          "self": "https://global.dns.api.rackspacecloud.com/v2/123456/zones/13db810b-917d-4898-bc28-4d4ee370d20d"
        }
      },
      {
        "status": "ACTIVE",
        "description": null,
        "updated_at": null,
        "ttl": 3600,
        "serial": 1405435142,
        "id": "38dbf635-45cb-4873-8300-6c273f0283c7",
        "name": "example.org.",
        "created_at": "2014-07-15T14:39:02.000000",
        "pool_id": "572ba08c-d929-4c70-8e42-03824bb24ca2",
        "version": 1,
        "project_id": "123456",
        "email": "hostmaster@example.org",
        "links": {
          "self": "https://global.dns.api.rackspacecloud.com/v2/123456/zones/38dbf635-45cb-4873-8300-6c273f0283c7"
        }
      },
      {
        "status": "ACTIVE",
        "description": null,
        "updated_at": null,
        "ttl": 3600,
        "serial": 1405435156,
        "id": "c316def0-8599-4030-9dcd-2ce566348115",
        "name": "abc.example.net.",
        "created_at": "2014-07-15T14:39:16.000000",
        "pool_id": "572ba08c-d929-4c70-8e42-03824bb24ca2",
        "version": 1,
        "project_id": "123456",
        "email": "hostmaster@example.net",
        "links": {
          "self": "https://global.dns.api.rackspacecloud.com/v2/123456/zones/c316def0-8599-4030-9dcd-2ce566348115"
        }
      }],
      "links": {
        "self": "https://global.dns.api.rackspacecloud.com/v2/123456/zones?name=*example*"
      },
      "metadata": {
        "total_count": 4
      }
    }
