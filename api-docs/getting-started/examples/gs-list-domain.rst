.. _gs-list-domain:

List domain details
~~~~~~~~~~~~~~~~~~~

This operation provides detailed output for a specific domain configured
and associated with your account. This operation is not capable of
returning details for a domain that has been deleted.

This operation does not require a request body.

The examples list the details for the domain with **domain_id** that
you created in the previous section.

The following examples show the cURL requests for List domain details:

 
cURL List domain details: request
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

**XML request**

.. code::

    $ curl -s  \
    -H 'X-Auth-Token: your_auth_token'  \
    -H 'Accept: application/xml'  \
    'https://dns.api.rackspacecloud.com/v1.0/your_acct_id/domains/domain_id' | ppxml

**JSON request**

.. code::

    curl -s  \
    -H 'X-Auth-Token: your_auth_token'  \
    -H 'Accept: application/json'  \
    'https://dns.api.rackspacecloud.com/v1.0/your_acct_id/domains/domain_id' | python -m json.tool

Remember to replace the names in the examples above with their actual
respective values for all the cURL examples that follow:

-  **your\_auth\_token** — as returned in your authentication response
   (see the response examples in `Generate an authentication
   token <http://docs.rackspace.com/cdns/api/v1.0/cdns-getting-started/content/Generating_Auth_Token.html>`__)

-  **your\_acct\_id** — as returned in your authentication response
   (must be replaced in the request URL)

-  **domain\_id** — as returned in your create domain response (must be
   replaced in the request URL)

The following examples show the List domain details responses:

 
List domain details: response
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

**XML response**

.. code::

    HTTP/1.1 200 OK
    X-API-VERSION: 1.0.13
    Content-Type: application/xml
    Date: Thu, 15 Mar 2012 19:51:54 GMT
    Content-Length: 903
    Server: Jetty(7.3.1.v20110307)

    <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
    <domain xmlns="http://docs.rackspacecloud.com/dns/api/v1.0" xmlns:ns2="http://www.w3.org/2005/Atom"
      xmlns:ns3="http://docs.rackspacecloud.com/dns/api/management/v1.0" id="3191338" accountId="1234"
      name="example.com" ttl="3600" emailAddress="sample@rackspace.com" updated="2012-03-15T18:08:15Z"
      created="2012-03-15T18:08:15Z" comment="Optional domain comment...">
      <nameservers>
        <nameserver name="dns1.stabletransit.com"/>
        <nameserver name="dns2.stabletransit.com"/>
      </nameservers>
      <recordsList totalEntries="2">
        <record id="NS-7475194" type="NS" name="example.com" data="dns1.stabletransit.com" ttl="3600" updated="2012-03-15T18:08:15Z" created="2012-03-15T18:08:15Z"/>
        <record id="NS-7475195" type="NS" name="example.com" data="dns2.stabletransit.com" ttl="3600" updated="2012-03-15T18:08:15Z" created="2012-03-15T18:08:15Z"/>
      </recordsList>
    </domain>

**JSON response** 

.. code::

    HTTP/1.1 200 OK
    X-API-VERSION: 1.0.13
    Content-Type: application/json
    Date: Thu, 15 Mar 2012 19: 54: 52 GMT
    Content-Length: 713
    Server: Jetty(7.3.1.v20110307)


    {
      "name": "example.com",
      "id": 3191338,
      "comment": "Optional domain comment...",
      "accountId": 1234,
      "updated": "2012-03-15T18:08:15.000+0000",
      "ttl": 3600,
      "recordsList": {
        "records": [
          {
            "name": "example.com",
            "id": "NS-7475194",
            "type": "NS",
            "data": "dns1.stabletransit.com",
            "updated": "2012-03-15T18:08:15.000+0000",
            "ttl": 3600,
            "created": "2012-03-15T18:08:15.000+0000"
          },
          {
            "name": "example.com",
            "id": "NS-7475195",
            "type": "NS",
            "data": "dns2.stabletransit.com",
            "updated": "2012-03-15T18:08:15.000+0000",
            "ttl": 3600,
            "created": "2012-03-15T18:08:15.000+0000"
          }
        ],
        "totalEntries": 2
      },
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

By default, the List domain details API call lists details of the
specified domain, with record information but *without* subdomains.

The following parameters are available to control the information
displayed by the List domain details responses:

-  ``showRecords`` — if this parameter is set to true, then information
   about records is returned; if this parameter is set to false, then
   information about records is not returned.

-  ``showSubdomains`` — if this parameter is set to true, then
   information about subdomains is returned; if this parameter is set to
   false, then information about subdomains is not returned.

For example, using the following version of the call, information about
subdomains will be displayed, but information about records will not be
displayed: ``'https://dns.api.rackspacecloud.com/v1.0/``
**your\_acct\_id** ``/domains/`` **domain\_id**
``?showRecords=false&showSubdomains=true``'

Displaying only the information needed will improve the performance of
the List domain details call.

The following examples show the cURL requests for List domain details
with subdomains, but no records:

 
cURL List domain details with subdomains, no records: request
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

**XML request**

.. code::

    $ curl -i  \
    -H 'X-Auth-Token: your_auth_token'  \
    -H 'Accept: application/xml'  \
    'https://dns.api.rackspacecloud.com/v1.0/your_acct_id/domains/domain_id?showRecords=false&showSubdomains=true'


**JSON request**

.. code::

    $ curl -i  \
    -H 'X-Auth-Token: your_auth_token'  \
    -H 'Accept: application/json'  \
    'https://dns.api.rackspacecloud.com/v1.0/your_acct_id/domains/domain_id?showRecords=false&showSubdomains=true'

Remember to replace the names in the examples above with their actual
respective values for all the cURL examples that follow:

-  **your\_auth\_token** — as returned in your authentication response
   (see the response examples in `Generate an authentication
   token <http://docs.rackspace.com/cdns/api/v1.0/cdns-getting-started/content/Generating_Auth_Token.html>`__)

-  **your\_acct\_id** — as returned in your authentication response;
   must be replaced in the request URL

-  **domain\_id** — as returned in your create domain final successful
   response (see the examples in `Create a
   domain <http://docs.rackspace.com/cdns/api/v1.0/cdns-getting-started/content/Create_Domain.html>`__);
   must be replaced in the request URL

The following examples show the List domain details with subdomains, no
records responses:

 
List domain details with subdomains, no records: response
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

**XML response**

.. code::

    HTTP/1.1 200 OK
    X-API-VERSION: 1.0.13
    Content-Type: application/xml
    Date: Thu, 15 Mar 2012 21:16:28 GMT
    Content-Length: 865
    Server: Jetty(7.3.1.v20110307)

    <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
    <domain xmlns="http://docs.rackspacecloud.com/dns/api/v1.0" xmlns:ns2="http://www.w3.org/2005/Atom"
      xmlns:ns3="http://docs.rackspacecloud.com/dns/api/management/v1.0" id="3191338" accountId="1234"
      name="example.com" ttl="3600" emailAddress="sample@rackspace.com" updated="2012-03-15T18:08:15Z"
      created="2012-03-15T18:08:15Z" comment="Optional domain comment...">
      <nameservers>
        <nameserver name="dns1.stabletransit.com"/>
        <nameserver name="dns2.stabletransit.com"/>
      </nameservers>
      <subdomains totalEntries="2">
        <domain id="3191339" name="sub1.example.com" updated="2012-03-15T18:08:16Z" created="2012-03-15T18:08:16Z" comment="1st sample subdomain"/>
        <domain id="3191340" name="sub2.example.com" updated="2012-03-15T18:08:17Z" created="2012-03-15T18:08:16Z" comment="1st sample subdomain"/>
      </subdomains>
    </domain>

**JSON response** 

.. code::

    HTTP/1.1 200 OK
    X-API-VERSION: 1.0.13
    Content-Type: application/json
    Date: Thu, 15 Mar 2012 19: 54: 52 GMT
    Content-Length: 713
    Server: Jetty(7.3.1.v20110307)

    {
       "id": "3191338",
       "accountId": "1234",
       "name": "example.com",
       "ttl": "3600",
       "emailAddress": "sample@rackspace.com",
       "updated": "2012-03-15T18:08:15Z",
       "created": "2012-03-15T18:08:15Z",
       "comment": "Optional domain comment...",
       "nameservers": {
          "nameserver": [
             {
                "name": "dns1.stabletransit.com"
             },
             {
                "name": "dns2.stabletransit.com"
             }
          ]
       },
       "subdomains": {
          "totalEntries": "2",
          "domain": [
             {
                "id": "3191339",
                "name": "sub1.example.com",
                "updated": "2012-03-15T18:08:16Z",
                "created": "2012-03-15T18:08:16Z",
                "comment": "1st sample subdomain"
             },
             {
                "id": "3191340",
                "name": "sub2.example.com",
                "updated": "2012-03-15T18:08:17Z",
                "created": "2012-03-15T18:08:16Z",
                "comment": "1st sample subdomain"
             }
          ]
       }
    }
