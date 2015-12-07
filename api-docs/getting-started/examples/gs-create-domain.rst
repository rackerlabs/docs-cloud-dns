.. _gs-create-domain:

Create a domain
~~~~~~~~~~~~~~~

The Create domain API call provisions one or more new DNS domains under
the account specified, based on the configuration defined in the request
object. If the corresponding request cannot be fulfilled due to
insufficient or invalid data, an ``HTTP`` 400 (Bad Request) error
response will be returned with information regarding the nature of the
failure in the body of the response. Failures in the validation process
are non-recoverable and require the caller to correct the cause of the
failure and **POST** the request again.

This call returns an *asynchronous* response. In fact, **PUT**,
**POST**, and **DELETE** DNS API calls are all *asynchronous*, since
they may take some time to process. Therefore they return 202 ACCEPTED
responses containing information with a callback URL, which allows the
progress, status, and/or response information of the call to be
retrieved at a later point in time.

You need to use the Create domain API call (POST ``/domains``) to create
a domain with the configuration that you specify.

In this case, assume that you want to create a domain with the following
configuration:

-  Domain name=example.com

      style="margin-left: 0.5in; margin-right: 0.5in;">

   ..  note::
       The DNS specification reserves "example.com" for documentation
       purposes. Therefore you will need to substitute your own domain name
       in order for the examples to work with the Cloud DNS API. To name
       your domain, you can use any letter, numbers between 0 and 9, and the
       character "-". For example, you might use your first name and last
       initial at the beginning of the name, as follows: "bobmexample.com."

-  ttl=3600

-  emailAddress="sample@rackspace.com"

-  comment="Optional domain comment..."

-  With subdomains as follows:

   -  Domain name = sub1.example.com

         style="margin-left: 0.5in; margin-right: 0.5in;">

      ..  note::
          Remember to modify the domain name "sub1.example.com" listed above
          to conform to the name you have chosen for your domain, for
          example: "sub1.<**your\_domain\_name**>".

   -  emailAddress="sample@rackspace.com"

   -  comment="1st sample subdomain"

   -  Domain name = sub2.example.com

         style="margin-left: 0.5in; margin-right: 0.5in;">

      ..  note::
          Remember to modify the domain name "sub2.example.com" listed above
          to conform to the name you have chosen for your domain, for
          example: "sub2.<**your\_domain\_name**>".

   -  emailAddress="sample@rackspace.com"

   -  comment="2nd sample subdomain"

..  note::
    Although you could add records for your domain in this Create domain
    call, to keep things simple, you will add the records using the separate
    Add records call in :ref:`Add records <gs-add-records>` instead.

The following examples show the cURL requests for Create domain:

cURL Create domain: request
^^^^^^^^^^^^^^^^^^^^^^^^^^^

**XML request**

.. code::

    $ curl -s -d \
    '<domains xmlns:ns2="http://docs.rackspacecloud.com/dns/api/management/v1.0"
    xmlns="http://docs.rackspacecloud.com/dns/api/v1.0" xmlns:ns3="http://www.w3.
    org/2005/Atom">
        <domain name="your_domain_name" ttl="3600" emailAddress="sample@rackspace.com"
    comment="Optional domain comment...">
            <subdomains>
                <domain name="sub1.your_domain_name" emailAddress="sample@rackspace.
    com" comment="1st sample subdomain"/>
                <domain name="sub2.your_domain_name" emailAddress="sample@rackspace.
    com" comment="1st sample subdomain"/>
            </subdomains>
        </domain>
    </domains>' \
    -H 'X-Auth-Token: your_auth_token' \
    -H 'Content-Type: application/xml' \
    -H 'Accept: application/xml' \
    'https://dns.api.rackspacecloud.com/v1.0/your_acct_id/domains' | ppxml

**JSON request**

.. code::

    $ curl -s -d \
    '{
        "domains" : [ {
            "name" : "your_domain_name",
            "comment" : "Optional domain comment...",
            "subdomains" : {
                "domains" : [ {
                    "name" : "sub1.your_domain_name",
                    "comment" : "1st sample subdomain",
                    "emailAddress" : "sample@rackspace.com"
                }, {
                    "name" : "sub2.your_domain_name",
                    "comment" : "1st sample subdomain",
                    "emailAddress" : "sample@rackspace.com"

                } ]
            },
            "ttl" : 3600,
            "emailAddress" : "sample@rackspace.com"
    } ]
    }' \
    -H 'X-Auth-Token: your_auth_token' \
    -H 'Content-Type: application/json' \
    'https://dns.api.rackspacecloud.com/v1.0/your_acct_id/domains' | python -m json.tool

Remember to replace the names in the examples above with their actual
respective values for all the cURL examples that follow:

-  **your\_domain\_name** — to name your domain, you can use any letter,
   numbers between 0 and 9, and the character "-".

-  **your\_auth\_token** — as returned in your authentication response
   (see the response examples in `Generate an authentication
   token <http://docs.rackspace.com/cdns/api/v1.0/cdns-getting-started/content/Generating_Auth_Token.html>`__)

-  **your\_acct\_id** — as returned in your authentication response
   (must be replaced in the request URL)

The following examples show the initial asynchronous responses for
Create domain:

 
Create domain: initial asynchronous response
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

**XML Response**

.. code::

    HTTP/1.1 202 Accepted
    X-API-VERSION: 1.0.13
    Content-Type: application/xml
    Date: Thu, 15 Mar 2012 16:21:49 GMT
    Content-Length: 1309
    Server: Jetty(7.3.1.v20110307)

    <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
    <asyncResponse xmlns="http://docs.rackspacecloud.com/dns/api/v1.0"
        xmlns:ns2="http://www.w3.org/2005/Atom"
        xmlns:ns3="http://docs.rackspacecloud.com/dns/api/management/v1.0">
        <jobId>c1b06e08-d7bd-4708-982e-30da5e64ce28</jobId>
        <callbackUrl>https://dns.api.rackspacecloud.com/v1.0/1234/status/c1b06e08-d7bd-4708-982e-30da5e64ce28</callbackUrl>
        <status>RUNNING</status>
        <requestUrl>http://dns.api.rackspacecloud.com/v1.0/1234/domains</requestUrl>
        <verb>POST</verb>
        <request> <;domains xmlns:ns2=";http://docs.rackspacecloud.com/dns/api/management/v1.0";
        xmlns=";http://docs.rackspacecloud.com/dns/api/v1.0"; xmlns:ns3=";http://www.w3.
        org/2005/Atom";>;
        <;domain name=";example.com"; ttl=";3600"; emailAddress=";sample@rackspace.com";
        comment=";Optional domain comment...";>;
        <;subdomains>;
        <;domain name=";sub1.example.com"; emailAddress=";sample@rackspace.com"; comment=";1st sample subdomain";/>;
        <;domain name=";sub2.example.com"; emailAddress=";sample@rackspace.com"; comment=";1st sample subdomain";/>;
        <;/subdomains>;
        <;/domain>;
        <;/domains>;
        </request>
    </asyncResponse>

..  note::
    The ``<request>`` in the XML response comes back with the request you
    sent, with the HTML entities encoded (<; >; ";).

**JSON Response**

.. code::

    HTTP/1.1 202 Accepted
    X-API-VERSION: 1.0.13
    Content-Type: application/json
    Date: Thu, 15 Mar 2012 18:08:15 GMT
    Content-Length: 931
    Server: Jetty(7.3.1.v20110307)

    {
    "callbackUrl": "https://dns.api.rackspacecloud.com/v1.0/1234/status/ec180c96-5488-4b29-8d25-ce3e2985afd4",
      "jobId": "ec180c96-5488-4b29-8d25-ce3e2985afd4",
      "request": "{\n    \"domains\" : [ {\n        \"name\" : \"example.com\",   \n        \"comment\" : \"Optional domain comment...\",   \n        \"subdomains\" : {\n            \"domains\" : [ {\n                \"name\" : \"sub1.example.com\",\n                \"comment\" : \"1st sample subdomain\",\n                \"emailAddress\" : \"sample@rackspace.com\"\n            }, {\n                \"name\" : \"sub2.example.com\",\n                \"comment\" : \"1st sample subdomain\",\n                \"emailAddress\" : \"sample@rackspace.com\"\n\n            } ]\n        },\n        \"ttl\" : 3600,\n        \"emailAddress\" : \"sample@rackspace.com\"\n} ]\n}",
      "requestUrl": "http://dns.api.rackspacecloud.com/v1.0/1234/domains",
      "status": "RUNNING",
      "verb": "POST"
    }

Notice that you can see the 202 ACCEPTED responses containing
information with a callback URL (``callbackUrl``), which allows the
progress, status, and/or response information of the call to be
retrieved at a later point in time. When a request is made to the
callback URL provided and the job is still running, another 202 ACCEPTED
response is returned with the same information as the previous one. If
the request is successful, the status is COMPLETED.

The following examples show the requests to get the status for the job
using the ``jobID`` and ``callbackUrl`` provided (which you can see in
the previous example). Note that the **job\_id** is automatically
inserted for you at the end of the callbackUrl, so you can just copy the
entire callbackUrl and place it within the single quotes at the end of
the cURL command. Then follow it with the ``?showDetails=true``
parameter.

The following examples show the cURL status requests for Create domain:

 
cURL Create domain asynchronous status: request
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

**XML Request**

.. code::

    $ curl -i  \
    -H 'X-Auth-Token: your_auth_token' \
    -H 'Content-Type: application/xml' \
    -H 'Accept: application/xml' \
    'https://dns.api.rackspacecloud.com/v1.0/your_acct_id/status/job_id?showDetails=true'

**JSON Request**

.. code::

    $ curl -i  \
    -H 'X-Auth-Token: your_auth_token' \
    -H 'Content-Type: application/json' \
    'https://dns.api.rackspacecloud.com/v1.0/your_acct_id/status/job_id?showDetails=true'

Adding the parameter ``?showDetails=true`` at the end of the end of the
URL after the **job\_id** causes the response to display all details for
the asynchronous request, including the results, if they are available.
Omitting this parameter causes just basic details to be displayed
(jobId, callbackUrl, and status attributes).

Remember to replace the names in the examples above with their actual
respective values for all the cURL examples that follow:

-  **your\_auth\_token** — as returned in your authentication response
   (see the response examples in `Generate an authentication
   token <http://docs.rackspace.com/cdns/api/v1.0/cdns-getting-started/content/Generating_Auth_Token.html>`__)

-  **your\_acct\_id** — as returned in your authentication response
   (must be replaced in the request URL)

-  **job\_id** — as returned in your Create Domain response (must be
   replaced in the request URL)

..  note::
    The following examples show the *final* successful response for the
    asynchronous call. You can find more information about how asynchronous
    calls work in the
    `Cloud DNS developer guide <https://developer.rackspace.com/docs/cloud-dns/v1/developer-guide/#document-general-api-info/synchronous-and-asynchronous-responses>`__.

The following examples show the final successful responses for Create
domain:

 
Create domain: final successful response
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

**XML Response**

.. code::

    HTTP/1.1 200 OK
    X-API-VERSION: 1.0.13
    Content-Type: application/xml
    Date: Thu, 15 Mar 2012 17:56:10 GMT
    Content-Length: 2400
    Server: Jetty(7.3.1.v20110307)

    <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
    <asyncResponse xmlns="http://docs.rackspacecloud.com/dns/api/v1.0"
        xmlns:ns2="http://www.w3.org/2005/Atom"
        xmlns:ns3="http://docs.rackspacecloud.com/dns/api/management/v1.0">
        <jobId>b32efdff-e217-4a97-9851-aac406811a38</jobId>
        <callbackUrl>https://dns.api.rackspacecloud.com/v1.0/1234/status/b32efdff-e217-4a97-9851-aac406811a38</callbackUrl>
        <status>COMPLETED</status>
        <requestUrl>http://dns.api.rackspacecloud.com/v1.0/1234/domains</requestUrl>
        <verb>POST</verb>
        <request> <;domains xmlns:ns2=";http://docs.rackspacecloud.com/dns/api/management/v1.0";
        xmlns=";http://docs.rackspacecloud.com/dns/api/v1.0"; xmlns:ns3=";http://www.w3.
        org/2005/Atom";>;
        <;domain name=";example.com"; ttl=";3600"; emailAddress=";sample@rackspace.com";
        comment=";Optional domain comment...";>;
        <;subdomains>;
        <;domain name=";sub1.example.com"; emailAddress=";sample@rackspace.com"; comment=";1st sample subdomain";/>;
        <;domain name=";sub2.example.com"; emailAddress=";sample@rackspace.com"; comment=";1st sample subdomain";/>;
        <;/subdomains>;
        <;/domain>;
        <;/domains>;
        </request>
        <response xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="domains">
            <domain id="3191305" accountId="1234" name="example.com" ttl="3600"
                emailAddress="sample@rackspace.com" updated="2012-03-15T17:53:05Z"
                created="2012-03-15T17:53:05Z" comment="Optional domain comment...">
                <nameservers>
                    <nameserver name="dns1.stabletransit.com"/>
                    <nameserver name="dns2.stabletransit.com"/>
                </nameservers>
                <subdomains>
                    <domain id="3191307" accountId="1234" name="sub1.example.com" ttl="3600"
                        emailAddress="sample@rackspace.com" updated="2012-03-15T17:53:05Z"
                        created="2012-03-15T17:53:05Z" comment="1st sample subdomain">
                        <nameservers>
                            <nameserver name="dns1.stabletransit.com"/>
                            <nameserver name="dns2.stabletransit.com"/>
                        </nameservers>
                    </domain>
                    <domain id="3191308" accountId="1234" name="sub2.example.com" ttl="3600"
                        emailAddress="sample@rackspace.com" updated="2012-03-15T17:53:05Z"
                        created="2012-03-15T17:53:05Z" comment="1st sample subdomain">
                        <nameservers>
                            <nameserver name="dns1.stabletransit.com"/>
                            <nameserver name="dns2.stabletransit.com"/>
                        </nameservers>
                    </domain>
                </subdomains>
            </domain>
        </response>
    </asyncResponse>

**JSON Response**

.. code::

    HTTP/1.1 200 OK
    X-API-VERSION: 1.0.13
    Content-Type: application/json
    Date: Thu, 15 Mar 2012 18:46:01 GMT
    Content-Length: 1892
    Server: Jetty(7.3.1.v20110307)

    {
    "request": "{\n    \"domains\" : [ {\n        \"name\" : \"example.com\",\n        \"comment\" : \"Optional domain comment...\",\n        \"subdomains\" : {\n            \"domains\" : [
    {\n                \"name\" : \"sub1.example.com\",\n                \"comment\" : \"1st sample subdomain\",\n                \"emailAddress\" : \"sample@rackspace.com\"\n            }, {
    \n                \"name\" : \"sub2.example.com\",\n                \"comment\" : \"1st sample subdomain\",\n                \"emailAddress\" : \"sample@rackspace.com\"\n\n            } ]\n
    },\n        \"ttl\" : 3600,\n        \"emailAddress\" : \"sample@rackspace.com\"\n} ]\n}",
    "response": {
      "domains": [
        {
          "name": "example.com",
          "id": 3191338,
          "comment": "Optional domain comment...",
          "accountId": 1234,
          "subdomains": {
            "domains": [
              {
                "name": "sub1.example.com",
                "id": 3191339,
                "comment": "1st sample subdomain",
                "accountId": 1234,
                "updated": "2012-03-15T18:08:16.000+0000",
                "ttl": 3600,
                "emailAddress": "sample@rackspace.com",
                "nameservers": [
                  {
                    "name": "dns1.stabletransit.com"
                  },
                  {
                    "name": "dns2.stabletransit.com"
                  }
                ],
                "created": "2012-03-15T18:08:16.000+0000"
              },
              {
                "name": "sub2.example.com",
                "id": 3191340,
                "comment": "1st sample subdomain",
                "accountId": 1234,
                "updated": "2012-03-15T18:08:16.000+0000",
                "ttl": 3600,
                "emailAddress": "sample@rackspace.com",
                "nameservers": [
                  {
                    "name": "dns1.stabletransit.com"
                  },
                  {
                    "name": "dns2.stabletransit.com"
                  }
                ],
                "created": "2012-03-15T18:08:16.000+0000"
              }
            ]
          },
          "updated": "2012-03-15T18:08:15.000+0000",
          "ttl": 3600,
          "emailAddress": "sample@rackspace.com",
          "nameservers": [
            {
              "name": "dns1.stabletransit.com"
            },
            {
              "name": "dns2.stabletransit.com"
            }
          ],
          "created": "2012-03-15T18:08:15.000+0000"
        }
      ]
    },
    "status": "COMPLETED",
    "verb": "POST",
    "jobId": "ec180c96-5488-4b29-8d25-ce3e2985afd4",
    "callbackUrl": "https://dns.api.rackspacecloud.com/v1.0/1234/status/ec180c96-5488-4b29-8d25-ce3e2985afd4",
    "requestUrl": "http://dns.api.rackspacecloud.com/v1.0/1234/domains"
    }

Notice that you can see the 200 OK responses containing information
about the domain/subdomains with status COMPLETED. This indicates that
the call was successfully completed.

..  note::
    The following examples show the *final* successful response for the
    asynchronous call. You can find more information about how asynchronous
    calls work in the
    `Cloud DNS developer guide <https://developer.rackspace.com/docs/cloud-dns/v1/developer-guide/#document-general-api-info/synchronous-and-asynchronous-responses>`__.

In the previous examples, you can see that the domain example.com was
created along with its subdomains sub1.example.com and sub2.example.com.
You will need the domain ``id`` for making the List domain details call
in the next section, and you should supply this value wherever you see
the field **domain\_id** in the examples in this guide.
