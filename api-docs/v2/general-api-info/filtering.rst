.. _cdns-dg-filtering:

Filtering
~~~~~~~~~

Filtering is available on all collections and is controlled using query parameters, which 
match the name of the attribute being filtered. All attributes need not be available as 
filter targets, but the majority will be. Filters are an exact match. Use of wildcard or 
substring matching is not supported.

Currently, the following attributes support filtering:

-  **Record sets**: name, type, ttl, data, description, status

-  **Zones**: name, email, ttl, description, status

Filters can be an exact match search or a wildcard search. Currently, wildcard search is 
supported using the '\*' character.

The following example takes a collection of zones and filters it by the “name” parameter.

 
**Example Request with a collection of zones**

.. code::  

     GET /v2/zones?name=example.com. HTTP/1.1 
     Host: dns.provider.com
     Accept: application/json
     X-Auth-Token: *************  

 
**Example Response for a collection of zones**

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
        "project_id": "noauth-project",
        "email": "hostmaster@example.com",
        "links": {
          "self": "http://dns.provider.com/v2/zones/a4e29ed3-d7a4-4e4d-945d-ce64678d3b94"
        }
      }],
      "links": {
        "self": "https://dns.provider.com/v2/zones?name=example.com."
      }
    } 

Wildcards can be placed anywhere within the query. The following example demonstrates the 
use of wildcards on the right side of a query:

 
**Example 3.13. Request with a wildcard**

.. code::  

    GET /v2/zones?name=example* HTTP/1.1
    Host: dns.provider.com
    Accept: application/json
    X-Auth-Token: ************* 

 
**Example Response example for a wildcard**

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
        "project_id": "noauth-project",
        "email": "hostmaster@example.com",
        "links": {
          "self": "http://dns.provider.com/v2/zones/a4e29ed3-d7a4-4e4d-945d-ce64678d3b94"
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
        "project_id": "noauth-project",
        "email": "hostmaster@example.org",
        "links": {
          "self": "http://dns.provider.com/v2/zones/38dbf635-45cb-4873-8300-6c273f0283c7"
        }
      }],
      "links": {
        "self": "https://dns.provider.com/v2/zones?name=example*"
      }
    } 

This example demonstrates the use of multiple wildcards:

 
**Example Request with multiple wildcards**

.. code::  

    GET /v2/zones?name=*example* HTTP/1.1
    Host: dns.provider.com
    Accept: application/json
    X-Auth-Token: ************* 

 
**Example Response for multiple wildcards**

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
        "project_id": "noauth-project",
        "email": "hostmaster@example.com",
        "links": {
          "self": "http://dns.provider.com/v2/zones/a4e29ed3-d7a4-4e4d-945d-ce64678d3b94"
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
        "project_id": "noauth-project",
        "email": "hostmaster@example.com",
        "links": {
          "self": "http://dns.provider.com/v2/zones/13db810b-917d-4898-bc28-4d4ee370d20d"
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
        "project_id": "noauth-project",
        "email": "hostmaster@example.org",
        "links": {
          "self": "http://dns.provider.com/v2/zones/38dbf635-45cb-4873-8300-6c273f0283c7"
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
        "project_id": "noauth-project",
        "email": "hostmaster@example.net",
        "links": {
          "self": "http://dns.provider.com/v2/zones/c316def0-8599-4030-9dcd-2ce566348115"
        }
      }],
      "links": {
        "self": "https://dns.provider.com/v2/zones?name=*example*"
      }
    }
