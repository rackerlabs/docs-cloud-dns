.. _cdns-dg-synch-asynch:

======================================
Synchronous and asynchronous responses
======================================

All successful **GET** requests are *synchronous* calls, since they are
always retrieving (reading) existing information. With these requests,
the caller waits until the call returns with the specified code and
response body.

**PUT**, **POST**, and **DELETE** calls are *asynchronous*, however,
since they may take some time to process. Therefore they return 202
ACCEPTED responses containing information with a callback URL, which
allows the progress, status, and/or response information of the call to
be retrieved at a later point in time.

When the status of a request is queried (via a ``callbackUrl`` supplied
by the API), only basic information regarding the status of the job is
returned by default. If more detail is desired, any status URL may
include an optional ``showDetails`` query parameter that will display
more information regarding the original request:

**GET** /status/*jobId*\ ?\ ``showDetails``\ =\ ``[true|false]``

- List status of the specified asynchronous request. Display details, as
  specified by the ``showDetails`` parameter.
   
- Representations: XML, JSON
   
Normal Response Code(s): 200

Error Response Code(s): dnsFault (400, 500), serviceUnavailable (503),
unauthorized (401), badRequest (400), itemNotFound (404), overLimit (413)

The results of asynchronous calls are retained for up to 24 hours.

If a request body does not pass initial validation or an error
condition arises, you may receive an immediate error response from the
request.

The following list shows the complete set of attributes for
asynchronous responses:

**Table. Attributes for asynchronous responses**

+-------------+--------------------------------------------------------------------------------+------------------+
| Attribute   | Description                                                                    | Inclusion        |
+=============+================================================================================+==================+
| jobid       | An identifier for the specific request.                                        | Basic and Detail |
+-------------+--------------------------------------------------------------------------------+------------------+
| callbackUrl | Resource locator for querying the status of the request.                       | Basic and Detail |
+-------------+--------------------------------------------------------------------------------+------------------+
| status      | An indicator of the request status: INITIALIZED, RUNNING, COMPLETED, or ERROR. | Basic and Detail |
|             |                                                                                |                  |
|             | **Note**: INITIALIZED is the status that immediately precedes RUNNING and      |                  |
|             | is the first possible status of a job. It indicates acceptance of the job.     |                  |
+-------------+--------------------------------------------------------------------------------+------------------+
| requestUrl  | The URL of the original request.                                               | Detail only      |
+-------------+--------------------------------------------------------------------------------+------------------+
| verb        | The type of the original request: PUT, POST, or DELETE.                        | Detail only      |
+-------------+--------------------------------------------------------------------------------+------------------+
| request     | The original request data, if any.                                             | Detail only      |
+-------------+--------------------------------------------------------------------------------+------------------+
| response    | The results of a COMPLETE operation, if any.                                   | Detail only      |
+-------------+--------------------------------------------------------------------------------+------------------+
| error       | The results of an ERROR operation.                                             | Detail only      |
+-------------+--------------------------------------------------------------------------------+------------------+

The asynchronous response body will look similar to the following
examples, depending on whether basic or detailed information is
requested.

If you use the callback URL *without* specifying the query parameter
``showDetails=true``, only *basic* information is returned (jobId,
callbackUrl, and status attributes):

**Example: Basic success asynchronous request: XML**

.. code::

    GET https://dns.api.rackspacecloud.com/v1.0/1234/status/3593a5e9-83af-4eb8-ae1a-25f07b747d80
    Accept: application/xml
    X-Auth-Token: ea85e6ac-baff-4a6c-bf43-848020ea3812
    Content-Type: application/xml
    Content-Length: 0


**Example: Basic success asynchronous request: JSON**

.. code::

    GET https://dns.api.rackspacecloud.com/v1.0/1234/status/3593a5e9-83af-4eb8-ae1a-25f07b747d80
    Accept: application/json
    X-Auth-Token: ea85e6ac-baff-4a6c-bf43-848020ea3812
    Content-Type: application/json
    Content-Length: 0

When a request is made to the callback URL provided and the job is still
running, another 202 ACCEPTED response is returned with the same
information as the previous one.

If the request is successful, the ``status`` is ``COMPLETED``:

**Example: Basic success asynchronous response: XML**

.. code::

    Status: 200 OK
    Date: Thu, 28 Jul 2011 21:54:21 GMT
    X-API-VERSION: 1.0.17
    Content-Type: application/xml
    Content-Length: 455

    <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
    <asyncresponse xmlns:ns2="http://www.w3.org/2005/Atom" xmlns="http://docs.rackspacecloud.com/dns/api/v1.0" xmlns:ns3="http://docs.rackspacecloud.com/dns/api/management/v1.0">
        <jobId>3593a5e9-83af-4eb8-ae1a-25f07b747d80</jobId>
        <callbackUrl>https://dns.api.rackspacecloud.com/v1.0/1234/status/3593a5e9-83af-4eb8-ae1a-25f07b747d80</callbackUrl>
        <status>COMPLETED</status>
    </asyncresponse>


**Example: Basic success asynchronous response: JSON**

.. code::

    Status: 200 OK
    Date: Thu, 28 Jul 2011 21:54:21 GMT
    X-API-VERSION: 1.0.17
    Content-Type: application/json
    Content-Length: 190

    {
      "status" : "COMPLETED",
      "jobId" : "3593a5e9-83af-4eb8-ae1a-25f07b747d80",
      "callbackUrl" : "https://dns.api.rackspacecloud.com/v1.0/1234/status/3593a5e9-83af-4eb8-ae1a-25f07b747d80"
    }

If you specify the query parameter ``showDetails=true`` for the callback
URL, *detailed* information is returned (all attributes) :

**Example: Detail success asynchronous request: XML**

.. code::

    GET https://dns.api.rackspacecloud.com/v1.0/1234/status/3593a5e9-83af-4eb8-ae1a-25f07b747d80?showDetails=true
    Accept: application/xml
    X-Auth-Token: ea85e6ac-baff-4a6c-bf43-848020ea3812
    Content-Type: application/xml
    Content-Length: 0

**Example: Detail success asynchronous request: JSON**

.. code::

    GET https://dns.api.rackspacecloud.com/v1.0/1234/status/3593a5e9-83af-4eb8-ae1a-25f07b747d80?showDetails=true
    Accept: application/json
    X-Auth-Token: ea85e6ac-baff-4a6c-bf43-848020ea3812
    Content-Type: application/json
    Content-Length: 0

If the request is successful, this includes the ``response``, which
contains the results of the operation:

**Example: Detail success asynchronous response: XML**

.. code::

    Status: 200 OK
    Date: Thu, 28 Jul 2011 21:54:21 GMT
    X-API-VERSION: 1.0.17
    Content-Type: application/xml
    Content-Length: 1187

    <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
    <asyncresponse xmlns:ns2="http://www.w3.org/2005/Atom" xmlns="http://docs.rackspacecloud.com/dns/api/v1.0" xmlns:ns3="http://docs.rackspacecloud.com/dns/api/management/v1.0">
        <jobId>3593a5e9-83af-4eb8-ae1a-25f07b747d80</jobId>
        <callbackUrl>https://dns.api.rackspacecloud.com/v1.0/1234/status/3593a5e9-83af-4eb8-ae1a-25f07b747d80</callbackUrl>
        <status>COMPLETED</status>
        <requestUrl>https://dns.api.rackspacecloud.com/v1.0/1234/domains</requestUrl>
        <verb>POST</verb>
        <request>{
            "domains" : [ {
            "name" : "example.com",
            "emailAddress" : "admin@example.com"
            } ]
            }
        </request>
        <response xsi:type="domains" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
            <domain id="12345" accountId="1234" name="example.com" ttl="3600" emailAddress="admin@example.com" updated="2011-08-23T14:02:54-05:00" created="2011-08-23T14:02:54-05:00">
                <nameservers>
                    <nameserver name="dns1.stabletransit.com"/>
                    <nameserver name="dns2.stabletransit.com"/>
                </nameservers>
            </domain>
        </response>
    </asyncresponse>



**Example: Detail success asynchronous response: JSON**

.. code::

    Status: 200 OK
    Date: Thu, 28 Jul 2011 21:54:21 GMT
    X-API-VERSION: 1.0.17
    Content-Type: application/json
    Content-Length: 866

    {
      "status" : "COMPLETED",
      "request" : "{\n        \"domains\" : [ {\n        \"name\" : \"example.com\",\n        \"emailAddress\" : \"admin@example.com\"\n        } ]\n        }\n    ",
      "verb" : "POST",
      "jobId" : "3593a5e9-83af-4eb8-ae1a-25f07b747d80",
      "callbackUrl" : "https://dns.api.rackspacecloud.com/v1.0/1234/status/3593a5e9-83af-4eb8-ae1a-25f07b747d80",
      "requestUrl" : "https://dns.api.rackspacecloud.com/v1.0/1234/domains",
      "response" : {
        "domains" : [ {
          "name" : "example.com",
          "id" : 12345,
          "updated" : "2011-08-23T19:02:54.000+0000",
          "nameservers" : [ {
            "name" : "dns1.stabletransit.com"
          }, {
            "name" : "dns2.stabletransit.com"
          } ],
          "accountId" : 1234,
          "ttl" : 3600,
          "emailAddress" : "admin@example.com",
          "created" : "2011-08-23T19:02:54.000+0000"
        } ]
      }
    }


.. note::
   Examples of successful responses in the rest of this guide only
   demonstrate the *contents* of the asynchronous ``response`` attribute.
   Additional attributes and elements have been omitted for clarity.

If an error occurs as a result of processing the original request,
querying the callback URL will return the information about the error.
If you use the callback URL without specifying the query parameter
``showDetails=true``, only basic information is provided:

**Example: Basic error asynchronous response: XML**

.. code::

    Status: 200 OK
    Date: Thu, 28 Jul 2011 21:54:21 GMT
    X-API-VERSION: 1.0.17
    Content-Type: application/xml
    Content-Length: 451

    <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
    <asyncresponse xmlns:ns2="http://www.w3.org/2005/Atom" xmlns="http://docs.rackspacecloud.com/dns/api/v1.0" xmlns:ns3="http://docs.rackspacecloud.com/dns/api/management/v1.0">
        <jobId>e63886c9-acf0-4e5d-8023-09a0fae37446</jobId>
        <callbackUrl>https://dns.api.rackspacecloud.com/v1.0/1234/status/e63886c9-acf0-4e5d-8023-09a0fae37446</callbackUrl>
        <status>ERROR</status>
    </asyncresponse>

**Example: Basic error asynchronous response: JSON**

.. code::

    Status: 200 OK
    Date: Thu, 28 Jul 2011 21:54:21 GMT
    X-API-VERSION: 1.0.17
    Content-Type: application/json
    Content-Length: 186

    {
      "status" : "ERROR",
      "jobId" : "e63886c9-acf0-4e5d-8023-09a0fae37446",
      "callbackUrl" : "https://dns.api.rackspacecloud.com/v1.0/1234/status/e63886c9-acf0-4e5d-8023-09a0fae37446"
    }

If you use the callback URL with the query parameter
``showDetails=true``, then detailed information is provided:

**Example: Detail error asynchronous response: XML**

.. code::

    Status: 200 OK
    Date: Thu, 28 Jul 2011 21:54:21 GMT
    X-API-VERSION: 1.0.17
    Content-Type: application/xml
    Content-Length: 847

    <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
    <asyncresponse xmlns:ns2="http://www.w3.org/2005/Atom" xmlns="http://docs.rackspacecloud.com/dns/api/v1.0" xmlns:ns3="http://docs.rackspacecloud.com/dns/api/management/v1.0">
        <jobId>e63886c9-acf0-4e5d-8023-09a0fae37446</jobId>
        <callbackUrl>https://dns.api.rackspacecloud.com/v1.0/1234/status/e63886c9-acf0-4e5d-8023-09a0fae37446</callbackUrl>
        <status>ERROR</status>
        <requestUrl>https://dns.api.rackspacecloud.com/v1.0/1234/domains</requestUrl>
        <verb>POST</verb>
        <request>{
            "domains" : [ {
            "name" : "example.com",
            "emailAddress" : "admin@example.com"
            } ]
            }
        </request>
        <error code="409">
            <message>The object already exists.</message>
            <details>Domain already exists</details>
        </error>
    </asyncresponse>



**Example: Detail error asynchronous response: JSON**

.. code::

    Status: 200 OK
    Date: Thu, 28 Jul 2011 21:54:21 GMT
    X-API-VERSION: 1.0.17
    Content-Type: application/json
    Content-Length: 564

    {
      "status" : "ERROR",
      "error" : {
        "message" : "The object already exists.",
        "code" : 409,
        "details" : "Domain already exists"
      },
      "request" : "{\n        \"domains\" : [ {\n        \"name\" : \"example.com\",\n        \"emailAddress\" : \"admin@example.com\"\n        } ]\n        }\n    ",
      "verb" : "POST",
      "jobId" : "e63886c9-acf0-4e5d-8023-09a0fae37446",
      "callbackUrl" : "https://dns.api.rackspacecloud.com/v1.0/1234/status/e63886c9-acf0-4e5d-8023-09a0fae37446",
      "requestUrl" : "https://dns.api.rackspacecloud.com/v1.0/1234/domains"
    }

.. note::
   Examples of error responses in the rest of this guide only show the
   *contents* of the asynchronous ``error`` attribute. Additional
   attributes and elements have been omitted for clarity.

Viewing status of all asynchronous job requests
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

As well as viewing status for a *particular job ID*, as described in the
previous section, you can also view status information for *all*
asynchronous job requests for an account. You can also filter the
information requested by using the following optional boolean request
parameters:

*  ``showErrors`` – if ``true``, specifies that errors are shown

*  ``showRunning`` – if ``true``, specifies that jobs still running are
   shown

*  ``showCompleted`` – if ``true``, specifies that completed jobs are
   shown

*  ``showDetails``– if ``true``, specifies that job details are shown

In addition, paging request parameters ``limit`` and ``offset`` can also
be supplied for the request. 
See :ref:`Pagination <paginated-collections>` for details.

The default values for these request parameters (if they are not
specified) are:

*  ``showErrors=true``

*  ``showRunning=true``

*  ``showCompleted=true``

*  ``showDetails=false``

*  ``limit=100``

*  ``offset=0``

+------+-----------------------------------+----------------------------------------+-----------------+
| Verb | URI                               | Description                            | Representations |
+======+===================================+========================================+=================+
| GET  | /status?showDetails=[true|false]  | List status of all asynchronous job    | XML, JSON       |
|      | &showErrors=[true|false]          | requests for an account and filter the |                 |
|      | &showRunning=[true|false]         | information requested by using the     |                 |
|      | &showCompleted=[true|false]       | optional boolean request parameters.   |                 |
|      | &limit=int1 &offset=int2          |                                        |                 |
+------+-----------------------------------+----------------------------------------+-----------------+

List status of all asynchronous job requests for an account and filter
the information requested by using the optional boolean request
parameters.

Representations: XML, JSON

Normal Response Code(s): 200

Error Response Code(s): dnsFault (400, 500), serviceUnavailable (503),
unauthorized (401), badRequest (400), itemNotFound (404), overLimit
(413)

By omitting the ``showDetails`` parameter from the request (or
explicitly setting it to ``false``), you can request basic information
for all errors, running jobs, and completed jobs for the account. By
default (with no query parameters specified) only *basic* information is
requested:

**Example: Get basic status for all jobs request: XML**

.. code::

    GET https://dns.api.rackspacecloud.com/v1.0/1234/status
    Accept: application/xml
    X-Auth-Token: ea85e6ac-baff-4a6c-bf43-848020ea3812
    Content-Type: application/xml
    Content-Length: 0

**Example: Get basic status for all jobs request: JSON**

.. code::

    GET https://dns.api.rackspacecloud.com/v1.0/1234/status
    Accept: application/json
    X-Auth-Token: ea85e6ac-baff-4a6c-bf43-848020ea3812
    Content-Type: application/json
    Content-Length: 0



The response lists all the user's jobs that have had errors, followed by
those still running, and then those that have completed:

**Example: Get basic status for all jobs response: XML**

.. code::

    Status: 202 Accepted
    Date: Thu, 28 Jul 2011 21:54:21 GMT
    X-API-VERSION: 1.0.17
    Content-Type: application/xml
    Content-Length: 822

    <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
    <asyncjobsstatus totalEntries="12" xmlns:ns2="http://www.w3.org/2005/Atom" xmlns="http://docs.rackspacecloud.com/dns/api/v1.0" xmlns:ns3="http://docs.rackspacecloud.com/dns/api/management/v1.0">
        <asyncResponse>
            <jobId>1ada58ab-f413-4d7e-a139-19c96eaea8b2</jobId>
            <callbackUrl>http://dns.api.rackspacecloud.com/v1.0/1234/status/1ada58ab-f413-4d7e-a139-19c96eaea8b2?showDetails=true</callbackUrl>
            <status>COMPLETED</status>
        </asyncResponse>
        <asyncResponse>
            <jobId>34c0160a-6109-4b61-9ea4-1f0513df031b</jobId>
            <callbackUrl>http://dns.api.rackspacecloud.com/v1.0/1234/status/34c0160a-6109-4b61-9ea4-1f0513df031b?showDetails=true</callbackUrl>
            <status>COMPLETED</status>
        </asyncResponse>
    </asyncjobsstatus>



**Example: Get basic status for all jobs response: JSON**

.. code::

    Status: 202 Accepted
    Date: Thu, 28 Jul 2011 21:54:21 GMT
    X-API-VERSION: 1.0.17
    Content-Type: application/json
    Content-Length: 482

    {
      "totalEntries" : 12,
      "asyncResponses" : [ {
        "status" : "COMPLETED",
        "jobId" : "1ada58ab-f413-4d7e-a139-19c96eaea8b2",
        "callbackUrl" : "http://dns.api.rackspacecloud.com/v1.0/1234/status/1ada58ab-f413-4d7e-a139-19c96eaea8b2?showDetails=true"
      }, {
        "status" : "COMPLETED",
        "jobId" : "34c0160a-6109-4b61-9ea4-1f0513df031b",
        "callbackUrl" : "http://dns.api.rackspacecloud.com/v1.0/1234/status/34c0160a-6109-4b61-9ea4-1f0513df031b?showDetails=true"
      } ]
    }



To get *detailed* status information for all jobs, set the
``showDetails`` parameter to true (``showDetails=true``):

**Example: Get detailed status for all jobs request: XML**

.. code::

    GET https://dns.api.rackspacecloud.com/v1.0/1234/status?showDetails=true
    Accept: application/xml
    X-Auth-Token: ea85e6ac-baff-4a6c-bf43-848020ea3812
    Content-Type: application/xml
    Content-Length: 0



**Example: Get detailed status for all jobs request: JSON**

.. code::

    GET https://dns.api.rackspacecloud.com/v1.0/1234/status?showDetails=true
    Accept: application/json
    X-Auth-Token: ea85e6ac-baff-4a6c-bf43-848020ea3812
    Content-Type: application/json
    Content-Length: 0



The response lists all the user's jobs that have had errors, followed by
those still running, and then those that have completed:

**Example: Get detailed status for all jobs response: XML**

.. code::

    Status: 202 Accepted
    Date: Thu, 28 Jul 2011 21:54:21 GMT
    X-API-VERSION: 1.0.17
    Content-Type: application/xml
    Content-Length: 1601

    <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
    <asyncjobsstatus totalEntries="12" xmlns:ns2="http://www.w3.org/2005/Atom" xmlns="http://docs.rackspacecloud.com/dns/api/v1.0" xmlns:ns3="http://docs.rackspacecloud.com/dns/api/management/v1.0">
        <asyncResponse>
            <jobId>1ada58ab-f413-4d7e-a139-19c96eaea8b2</jobId>
            <callbackUrl>http://dns.api.rackspacecloud.com/v1.0/1234/status/1ada58ab-f413-4d7e-a139-19c96eaea8b2?showDetails=true</callbackUrl>
            <status>COMPLETED</status>
            <requestUrl>http://dns.api.rackspacecloud.com/v1.0/1234/domains/2764176</requestUrl>
            <verb>DELETE</verb>
        </asyncResponse>
        <asyncResponse>
            <jobId>34c0160a-6109-4b61-9ea4-1f0513df031b</jobId>
            <callbackUrl>http://dns.api.rackspacecloud.com/v1.0/1234/status/34c0160a-6109-4b61-9ea4-1f0513df031b?showDetails=true</callbackUrl>
            <status>COMPLETED</status>
            <requestUrl>http://dns.api.rackspacecloud.com/v1.0/1234/domains</requestUrl>
            <verb>POST</verb>
            <request>
            </request>
            <response xsi:type="domains" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
                <domain id="2764458" accountId="440369" name="example.com" ttl="3642" emailAddress="hostmaster@example.com" updated="2011-08-29T15:49:53-05:00" created="2011-08-29T15:49:53-05:00">
                    <nameservers>
                        <nameserver name="dns1.stabletransit.com"/>
                        <nameserver name="dns2.stabletransit.com"/>
                    </nameservers>
                </domain>
            </response>
        </asyncResponse>
    </asyncjobsstatus>



**Example: Get detailed status for all jobs response: JSON**

.. code::

    Status: 202 Accepted
    Date: Thu, 28 Jul 2011 21:54:21 GMT
    X-API-VERSION: 1.0.17
    Content-Type: application/json
    Content-Length: 1170

    {
      "totalEntries" : 12,
      "asyncResponses" : [ {
        "status" : "COMPLETED",
        "verb" : "DELETE",
        "jobId" : "1ada58ab-f413-4d7e-a139-19c96eaea8b2",
        "callbackUrl" : "http://dns.api.rackspacecloud.com/v1.0/1234/status/1ada58ab-f413-4d7e-a139-19c96eaea8b2?showDetails=true",
        "requestUrl" : "http://dns.api.rackspacecloud.com/v1.0/1234/domains/2764176"
      }, {
        "status" : "COMPLETED",
        "request" : "\n\t\t",
        "verb" : "POST",
        "jobId" : "34c0160a-6109-4b61-9ea4-1f0513df031b",
        "callbackUrl" : "http://dns.api.rackspacecloud.com/v1.0/1234/status/34c0160a-6109-4b61-9ea4-1f0513df031b?showDetails=true",
        "requestUrl" : "http://dns.api.rackspacecloud.com/v1.0/1234/domains",
        "response" : {
          "domains" : [ {
            "name" : "example.com",
            "id" : 2764458,
            "updated" : "2011-08-29T20:49:53.000+0000",
            "nameservers" : [ {
              "name" : "dns1.stabletransit.com"
            }, {
              "name" : "dns2.stabletransit.com"
            } ],
            "accountId" : 440369,
            "ttl" : 3642,
            "emailAddress" : "hostmaster@example.com",
            "created" : "2011-08-29T20:49:53.000+0000"
          } ]
        }
      } ]
    }



