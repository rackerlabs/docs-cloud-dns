.. _gs-add-records:

Add records
~~~~~~~~~~~

This section shows you how to add records for your new domain:

-  Two A records to map the IPV4 addresses of your two cloud servers
   that you recorded in `Create a new cloud
   server <gs-create-server>`.
   to the new domain that you created in `Create a
   domain <gs-create-domain>`.

-  One CNAME record to create an alias (www.example.com) for your domain
   with a TTL of 5400 and a comment of “This is a comment on the CNAME
   record.”

-  Make the first cloud server the ftp server (ftp.example.com) for your
   domain with a TTL of 5571.

-  Make the second cloud server the domain server with a TTL of 86400.

..  note::
    If you had IPV6 addresses to map, you would need to create AAAA records
    in addition to any A records for IPv4 addresses.

The following examples show the cURL requests for Add records:

 
cURL Add records: request
^^^^^^^^^^^^^^^^^^^^^^^^^^

**XML Request**

.. code::

    curl -s -d \
    '<?xml version="1.0" ?>
    <recordsList xmlns:ns2="http://docs.rackspacecloud.com/dns/api/management/v1.
    0" xmlns="http://docs.rackspacecloud.com/dns/api/v1.0" xmlns:ns3="http://www.
    w3.org/2005/Atom">
        <record type="A" name="ftp.example.com"
        data="your_FIRST_Cloud_Server_IP_address" ttl="5771"/>
        <record type="A" name="example.com"
        data="your_SECOND_Cloud_Server_IP_address" ttl="86400"/>
        <record type="CNAME" name="www.example.com" data="example.com" ttl="5400"
        comment="This is a comment on the CNAME record"/>
    </recordsList>' \
    -H 'X-Auth-Token: your_auth_token' \
    -H 'Content-Type: application/xml' \
    -H 'Accept: application/xml' \
    'https://dns.api.rackspacecloud.com/v1.0/your_acct_id/domains/domain_id/records' | ppxml

 
**JSON request**

.. code::

    curl -s -d \
    '{
        "records": [
            {
                "name" : "ftp.example.com",
                "type" : "A",
                "data" : "your_FIRST_Cloud_Server_IP_address",
                "ttl" : 5771
            },
            {
                "name" : "example.com",
                "type" : "A",
                "data" : "your_SECOND_Cloud_Server_IP_address",
                "ttl" : 86400
            },
            {
                "name" : "www.example.com",
                "type" : "CNAME",
                "comment" : "This is a comment on the CNAME record",
                "data" : "example.com",
                "ttl" : 5400
            }
        ]
    }' \
    -H 'X-Auth-Token: your_auth_token' \
    -H 'Content-Type: application/json' \
    'https://dns.api.rackspacecloud.com/v1.0/your_acct_id/domains/domain_id/records' | python -m json.tool

Remember to replace the names in the examples above with their actual
respective values:

-  **your\_auth\_token** — as returned in your authentication response
   (see the examples in `Generate an authentication
   token <http://docs.rackspace.com/cdns/api/v1.0/cdns-getting-started/content/Generating_Auth_Token.html>`__)

-  **your\_acct\_id** — as returned in your authentication response (see
   the examples in `Generate an authentication
   token <http://docs.rackspace.com/cdns/api/v1.0/cdns-getting-started/content/Generating_Auth_Token.html>`__);
   must be replaced in the request URL

-  **domain\_id** — as returned in your create domain final successful
   response (see the examples in `Create a
   domain <http://docs.rackspace.com/cdns/api/v1.0/cdns-getting-started/content/Create_Domain.html>`__);
   must be replaced in the request URL

The following examples show the initial asynchronous responses for Add
records:

 
Initial asynchronous response
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

**XML Response**

.. code::

    HTTP/1.1 202 Accepted
    X-API-VERSION: 1.0.13
    Content-Type: application/xml
    Date: Fri, 16 Mar 2012 15:17:52 GMT
    Content-Length: 1283
    Server: Jetty(7.3.1.v20110307)

    <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
    <asyncResponse xmlns="http://docs.rackspacecloud.com/dns/api/v1.0" xmlns:ns2="http://www.w3.org/2005/Atom" xmlns:ns3="http://docs.rackspacecloud.com/dns/api/management/v1.0">
      <jobId>1912f480-4636-498e-bba4-609661d19083</jobId>
      <callbackUrl>https://dns.api.rackspacecloud.com/v1.0/1234/status/1912f480-4636-498e-bba4-609661d19083</callbackUrl>
      <status>RUNNING</status>
      <requestUrl>http://dns.api.rackspacecloud.com/v1.0/1234/domains/3191338/records</requestUrl>
      <verb>POST</verb>
      <request><;?xml version=";1.0"; ?>;
    <;recordsList xmlns:ns2=";http://docs.rackspacecloud.com/dns/api/management/v1.
    0"; xmlns=";http://docs.rackspacecloud.com/dns/api/v1.0"; xmlns:ns3=";http://www.
    w3.org/2005/Atom";>;
    <;record type=";A"; name=";ftp.example.com";
      data=";50.56.207.146"; ttl=";5771";/>;
    <;record type=";A"; name=";example.com";
      data=";108.166.67.215"; ttl=";86400";/>;
    <;record type=";CNAME"; name=";www.example.com"; data=";example.com"; ttl=";5400";
      comment=";This is a comment on the CNAME record";/>;
    <;/recordsList>;</request>
    </asyncResponse>

 
**JSON response**

.. code::

    HTTP/1.1 202 Accepted
    X-API-VERSION: 1.0.13
    Content-Type: application/json
    Date: Fri, 16 Mar 2012 17:16:16 GMT
    Content-Length: 700
    Server: Jetty(7.3.1.v20110307)

    {
      "request": "{\n\"records\": [\n{\n\"name\" : \"ftp.example.com\",\n\"type\" : \"A\",\n\"data\" : \"50.56.207.146\",\n\"ttl\" : 5771\n},\n{\n\"name\" : \"example.com\",\n\"type\" : \"A\",\n\"data\" : \"108.166.67.215\",\n\"ttl\" : 86400\n},\n{\n\"name\" : \"www.example.com\",\n\"type\" : \"CNAME\",\n\"comment\" : \"This is a comment on the CNAME record\",\n\"data\" : \"example.com\",\n\"ttl\" : 5400\n}\n]\n}",
      "status": "RUNNING",
      "verb": "POST",
      "jobId": "e6b78833-2b5e-4c4c-88c6-6aabb55a706b",
      "callbackUrl": "https://dns.api.rackspacecloud.com/v1.0/1234/status/e6b78833-2b5e-4c4c-88c6-6aabb55a706b",
      "requestUrl": "http://dns.api.rackspacecloud.com/v1.0/1234/domains/3191338/records"
    }

The following examples show the cURL asynchronous status requests for
Add records:

 
cURL asynchronous status for Add records: request
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

**XML request**

.. code::

    curl -i  \
    -H 'X-Auth-Token: your_auth_token' \
    -H 'Content-Type: application/xml' \
    -H 'Accept: application/xml' \
    'https://dns.api.rackspacecloud.com/v1.0/your_acct_id/status/job_id?showDetails=true'

**JSON request**

.. code::

    curl -i  \
    -H 'X-Auth-Token: your_auth_token' \
    -H 'Content-Type: application/json' \
    'https://dns.api.rackspacecloud.com/v1.0/your_acct_id/status/job_id?showDetails=true'

Adding the parameter ``?showDetails=true`` at the end of the end of the
URL after the **job\_id** causes the response to display all details for
the aynch request, including the results, if they are available.
Omitting this parameter causes just basic details to be displayed
(jobId, callbackUrl, and status attributes).

Remember to replace the names in the examples above with their actual
respective values for all the cURL examples that follow:

-  **your\_auth\_token** — as returned in your authentication response
   (see the response examples in `Generate an authentication
   token <http://docs.rackspace.com/cdns/api/v1.0/cdns-getting-started/content/Generating_Auth_Token.html>`__)

-  **your\_acct\_id** — as returned in your authentication response
   (must be replaced in the request URL)

-  **job\_id** — as returned in your Create domain response (must be
   replaced in the request URL)

The following examples show the *final* successful response for the
asynchronous Add records call. Refer to
http://docs.rackspace.com/cdns/api/v1.0/cdns-devguide/content/sync_asynch_responses.html
for more information about how the asynchronous call works.

 
**cURL Add records: final successful response
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

**XML response**

.. code::

    HTTP/1.1 200 OK
    X-API-VERSION: 1.0.13
    Content-Type: application/xml
    Date: Fri, 16 Mar 2012 15:53:22 GMT
    Content-Length: 1906
    Server: Jetty(7.3.1.v20110307)

    <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
    <asyncResponse xmlns="http://docs.rackspacecloud.com/dns/api/v1.0" xmlns:ns2="http://www.w3.org/2005/Atom" xmlns:ns3="http://docs.rackspacecloud.com/dns/api/management/v1.0">
      <jobId>1912f480-4636-498e-bba4-609661d19083</jobId>
      <callbackUrl>https://dns.api.rackspacecloud.com/v1.0/1234/status/1912f480-4636-498e-bba4-609661d19083</callbackUrl>
      <status>COMPLETED</status>
      <requestUrl>http://dns.api.rackspacecloud.com/v1.0/1234/domains/3191338/records</requestUrl>
      <verb>POST</verb>
      <request><;?xml version=";1.0"; ?>;
    <;recordsList xmlns:ns2=";http://docs.rackspacecloud.com/dns/api/management/v1.
    0"; xmlns=";http://docs.rackspacecloud.com/dns/api/v1.0"; xmlns:ns3=";http://www.
    w3.org/2005/Atom";>;
    <;record type=";A"; name=";ftp.example.com";
      data=";50.56.207.146"; ttl=";5771";/>;
    <;record type=";A"; name=";example.com";
      data=";108.166.67.215"; ttl=";86400";/>;
    <;record type=";CNAME"; name=";www.example.com"; data=";example.com"; ttl=";5400";
      comment=";This is a comment on the CNAME record";/>;
    <;/recordsList>;</request>
      <response xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="recordsList">
        <record id="A-8135987" type="A" name="ftp.example.com" data="50.56.207.146" ttl="5771" updated="2012-03-16T15:17:53Z" created="2012-03-16T15:17:53Z"/>
        <record id="A-8135988" type="A" name="example.com" data="108.166.67.215" ttl="86400" updated="2012-03-16T15:17:53Z" created="2012-03-16T15:17:53Z"/>
        <record id="CNAME-10713155" type="CNAME" name="www.example.com" data="example.com" ttl="5400" updated="2012-03-16T15:17:54Z" created="2012-03-16T15:17:54Z" comment="This is a comment on the CNAME record"/>
      </response>
    </asyncResponse>

**JSON response**

.. code::

    HTTP/1.1 200 OK
    X-API-VERSION: 1.0.13
    Content-Type: application/json
    Date: Fri, 16 Mar 2012 16:16:23 GMT
    Content-Length: 1455
    Server: Jetty(7.3.1.v20110307)

    {
    "request": "{\n\"records\": [\n{\n\"name\" : \"ftp.example.com\",\n\"type\" : \"A\",\n\"data\" : \"50.56.207.146\",\n\"ttl\" : 5771\n},\n{\n\"name\" : \"example.com\",\n\"type\" : \"A\",\n\"data\" : \"108.166.67.215\",\n\"ttl\" : 86400\n},\n{\n\"name\" : \"www.example.com\",\n\"type\" : \"CNAME\",\n\"comment\" : \"This is a comment on the CNAME record\",\n\"data\" : \"example.com\",\n\"ttl\" : 5400\n}\n]\n}",
      "response": {
        "records": [
          {
            "name": "ftp.example.com",
            "id": "A-8135987",
            "type": "A",
            "data": "50.56.207.146",
            "updated": "2012-03-16T15:17:53.000+0000",
            "ttl": 5771,
            "created": "2012-03-16T15:17:53.000+0000"
          },
          {
            "name": "example.com",
            "id": "A-8135988",
            "type": "A",
            "data": "108.166.67.215",
            "updated": "2012-03-16T15:17:53.000+0000",
            "ttl": 86400,
            "created": "2012-03-16T15:17:53.000+0000"
          },
          {
            "name": "www.example.com",
            "id": "CNAME-10713155",
            "type": "CNAME",
            "comment": "This is a comment on the CNAME record",
            "data": "example.com",
            "updated": "2012-03-16T15:17:54.000+0000",
            "ttl": 5400,
            "created": "2012-03-16T15:17:54.000+0000"
          }
        ]
      },
      "status": "COMPLETED",
      "verb": "POST",
      "jobId": "1912f480-4636-498e-bba4-609661d19083",
      "callbackUrl": "https://dns.api.rackspacecloud.com/v1.0/1234/status/1912f480-4636-498e-bba4-609661d19083",
      "requestUrl": "http://dns.api.rackspacecloud.com/v1.0/1234/domains/3191338/records"
    }

You can now call List domain details again to confirm that the records
are added to your domain. See `List domain
details <gs-list-domain>`
for instructions.
