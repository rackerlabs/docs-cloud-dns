
.. THIS OUTPUT IS GENERATED FROM THE WADL. DO NOT EDIT.

=============================================================================
Clone Domain -  Rackspace Cloud DNS Developer Guide
=============================================================================

Clone Domain
~~~~~~~~~~~~~~~~~~~~~~~~~

`Request <post-clone-domain-v1.0-account-domains-domainid-clone.html#request>`__
`Response <post-clone-domain-v1.0-account-domains-domainid-clone.html#response>`__

.. code::

    POST /v1.0/{account}/domains/{domainId}/clone

Clones a domain.

Creates a specified domain ( ``example2.com`` ) by cloning a domain with id domainId. All options except cloneName assume a default value of ``true``.

.. note::
   This call returns an asynchronous response, as described in `Synchronous and Asynchronous Responses <http://docs.rackspace.com/cdns/api/v1.0/cdns-devguide/content/sync_asynch_responses.html>`__. The AsyncResponse returned will be similar to that returned for Create domain but with the request element absent because the clone request has no body.
   
   

This call duplicates a single existing domain configuration with a new domain name for a specified Cloud account. By default, all records and, optionally, subdomain(s) are duplicated as well. Both the existing domain (referred to as the reference domain) and the new cloned domain must exist under the same Cloud account.

See the query parameters table for the parameters and options available to specify how the cloning affects subdomains, comments, email addresses, and record data.

.. note::
   Notes 
   
   *  If the corresponding request cannot be fulfilled due to insufficient or invalid data, or if the reference domain does not exist, an HTTP 400 (Bad Request) error response will be returned in the body of the response with information regarding the nature of the failure.
   *  Clone domain is an atomic operation. If there is a failure in the duplication of a single record or subdomain, the entire process will fail. Failures are non-recoverable and require the caller to correct the cause of the failure and ``POST`` the request again.
   *  The Clone domain operation is currently supported for domains under a given Cloud account. The cloned domain must belong to the same account as the reference domain.
   *  The Clone domain operation will return an exception if the operation would result in creating a domain that already exists. The exception would indicate that the domain already exists.
   *  The Clone domain operation may take slightly longer to complete than a comparable Create domain request.
   *  PTR records (for Reverse DNS) are not represented when a domain is created and, therefore, are not included when a domain is cloned.
   *  If your reference domain already has both default Rackspace Nameserver (NS) records, the cloned domain will be created with no additional default Rackspace NS records. If your reference domain lacks one or both of the default Rackspace NS records, the cloned domain will be created with additional Rackspace default NS records to make a total of two default Rackspace NS records. If the presence of default Rackspace NS records is not your preference, they can be deleted from the cloned domain as long as at least one NS record remains (Rackspace or non-Rackspace).
   *  Any non-default (non-Rackspace) NS records in the reference domain are cloned and modified in a way that is consistent with all other record types.
   
   
   

According to the cloneName specified, the domain name and record name(s) will automatically be modified and replaced in the new cloned domain as part of the cloning process and cannot be influenced by any request options. See the table below for the parameters and options available to specify how the cloning affects subdomains, comments, email addresses, and record data.

The following examples show the Clone domain requests.

.. note::
   The following examples show the initial 202 Accepted response for the asynchronous call and indicate that the task has been accepted for processing. Refer to `Synchronous and Asynchronous Responses <http://docs.rackspace.com/cdns/api/v1.0/cdns-devguide/content/sync_asynch_responses.html>`__ for a description of how the asynchronous call works.
   
   



This table shows the possible response codes for this operation:


+--------------------------+-------------------------+-------------------------+
|Response Code             |Name                     |Description              |
+==========================+=========================+=========================+
|202                       |Accepted                 |Request is accepted.     |
+--------------------------+-------------------------+-------------------------+
|400 500                   |dnsFault                 |The DNS service has      |
|                          |                         |experienced a fault.     |
+--------------------------+-------------------------+-------------------------+
|409                       |Already Exists           |The item already exists. |
+--------------------------+-------------------------+-------------------------+
|503                       |Service Unavailable      |The service is not       |
|                          |                         |available.               |
+--------------------------+-------------------------+-------------------------+
|401                       |Unauthorized             |You are not authorized   |
|                          |                         |to complete this         |
|                          |                         |operation. This error    |
|                          |                         |can occur if the request |
|                          |                         |is submitted with an     |
|                          |                         |invalid authentication   |
|                          |                         |token.                   |
+--------------------------+-------------------------+-------------------------+
|400                       |Bad Request              |The request is missing   |
|                          |                         |one or more elements, or |
|                          |                         |the values of some       |
|                          |                         |elements are invalid.    |
+--------------------------+-------------------------+-------------------------+
|404                       |Not Found                |The requested item was   |
|                          |                         |not found.               |
+--------------------------+-------------------------+-------------------------+
|413                       |Over Limit               |The number of items      |
|                          |                         |returned is above the    |
|                          |                         |allowed limit.           |
+--------------------------+-------------------------+-------------------------+


Request
^^^^^^^^^^^^^^^^^

This table shows the URI parameters for the request:

+--------------------------+-------------------------+-------------------------+
|Name                      |Type                     |Description              |
+==========================+=========================+=========================+
|X-Auth-Token              |xs:string *(Required)*   |Arbitrary character      |
|                          |                         |string generated by the  |
|                          |                         |authentication service   |
|                          |                         |in response to valid     |
|                          |                         |credentials.             |
+--------------------------+-------------------------+-------------------------+
|{account}                 |*(Required)*             |The tenant ID.           |
+--------------------------+-------------------------+-------------------------+
|{domainId}                |xs:string *(Required)*   |ID for the domain.       |
+--------------------------+-------------------------+-------------------------+



This table shows the query parameters for the request:

+--------------------------+-------------------------+-------------------------+
|Name                      |Type                     |Description              |
+==========================+=========================+=========================+
|cloneName                 |xs:string *(Required)*   |The name of the new      |
|                          |                         |(cloned) domain.         |
+--------------------------+-------------------------+-------------------------+
|cloneSubdomains           |xs:string *(Required)*   |Recursively clone        |
|                          |                         |subdomains. Defaults to  |
|                          |                         |``true``. If set to      |
|                          |                         |``false``, then only the |
|                          |                         |top level domain and its |
|                          |                         |records are cloned.      |
|                          |                         |Cloned subdomain         |
|                          |                         |configurations are       |
|                          |                         |modified the same way    |
|                          |                         |that cloned top level    |
|                          |                         |domain configurations    |
|                          |                         |are modified.            |
+--------------------------+-------------------------+-------------------------+
|modifyRecordData          |xs:string *(Required)*   |Replaces occurrences of  |
|                          |                         |the reference domain     |
|                          |                         |name with the new domain |
|                          |                         |name in data fields (of  |
|                          |                         |records) on the cloned   |
|                          |                         |(new) domain. Does not   |
|                          |                         |affect NS records.       |
|                          |                         |Defaults to ``true``.    |
+--------------------------+-------------------------+-------------------------+
|modifyEmailAddress        |xs:string *(Required)*   |Replaces occurrences of  |
|                          |                         |the reference domain     |
|                          |                         |name with the new domain |
|                          |                         |name in email addresses  |
|                          |                         |on the cloned (new)      |
|                          |                         |domain. Defaults to      |
|                          |                         |``true``.                |
+--------------------------+-------------------------+-------------------------+
|modifyComment             |xs:string *(Required)*   |Replaces occurrences of  |
|                          |                         |the reference domain     |
|                          |                         |name with the new domain |
|                          |                         |name in comments on the  |
|                          |                         |cloned (new) domain.     |
|                          |                         |Defaults to ``true``.    |
+--------------------------+-------------------------+-------------------------+







**Example Clone domain: XML request**


.. code::

    POST https://dns.api.rackspacecloud.com/v1.0/1234/domains/3586209/clone?cloneName=clone1.com
    Accept: application/xml
    X-Auth-Token: ea85e6ac-baff-4a6c-bf43-848020ea3812
    Content-Type: application/xml
    Content-Length: 0
    


**Example Clone domain: JSON request**


.. code::

    POST https://dns.api.rackspacecloud.com/v1.0/1234/domains/3586209/clone?cloneName=clone1.com
    Accept: application/json
    X-Auth-Token: ea85e6ac-baff-4a6c-bf43-848020ea3812
    Content-Type: application/json
    Content-Length: 0
    


Response
^^^^^^^^^^^^^^^^^^





**Example Initial (202) Clone domain: XML response**


.. code::

    Status: 202 Accepted
    Date: Thu, 28 Jul 2011 21:54:21 GMT
    X-API-VERSION: 1.0.17
    Content-Type: application/xml
    Content-Length: 592
    
    <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
    <asyncresponse xmlns:ns2="http://www.w3.org/2005/Atom" xmlns="http://docs.rackspacecloud.com/dns/api/v1.0" xmlns:ns3="http://docs.rackspacecloud.com/dns/api/management/v1.0">
        <jobId>52179628-6df6-46a0-bdb3-078769cd0e9d</jobId>
        <callbackUrl>https://dns.api.rackspacecloud.com/v1.0/1234/status/52179628-6df6-46a0-bdb3-078769cd0e9d</callbackUrl>
        <status>RUNNING</status>
        <requestUrl>https://dns.api.rackspacecloud.com/v1.0/1234/domains/3586209/clone?cloneName=clone1.com</requestUrl>
        <verb>POST</verb>
    </asyncresponse>
    


**Example Initial (202) Clone domain: JSON response**


.. code::

    Status: 202 Accepted
    Date: Thu, 28 Jul 2011 21:54:21 GMT
    X-API-VERSION: 1.0.17
    Content-Type: application/json
    Content-Length: 315
    
    {
      "status" : "RUNNING",
      "verb" : "POST",
      "jobId" : "52179628-6df6-46a0-bdb3-078769cd0e9d",
      "callbackUrl" : "https://dns.api.rackspacecloud.com/v1.0/1234/status/52179628-6df6-46a0-bdb3-078769cd0e9d",
      "requestUrl" : "https://dns.api.rackspacecloud.com/v1.0/1234/domains/3586209/clone?cloneName=clone1.com"
    }


**Example Reference (Existing) domain cloner.com: XML**


.. code::

    Status: 200 OK
    Date: Thu, 28 Jul 2011 21:54:21 GMT
    X-API-VERSION: 1.0.17
    Content-Type: application/xml
    Content-Length: 2804
    
    <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
    <domain id="3586209" accountId="1234" name="cloner.com" ttl="7788" emailAddress="owner@cloner.com" updated="2013-05-06T12:10:55-05:00" created="2013-05-06T12:10:51-05:00" comment="cloner.com is a template domain for cloning others. cloner.com has subdomains - sub1.cloner.com, sub2.cloner.com, sub3.cloner.com" xmlns:ns2="http://www.w3.org/2005/Atom" xmlns="http://docs.rackspacecloud.com/dns/api/v1.0" xmlns:ns3="http://docs.rackspacecloud.com/dns/api/management/v1.0">
        <nameservers>
            <nameserver name="dns1.stabletransit.com"/>
            <nameserver name="dns2.stabletransit.com"/>
        </nameservers>
        <recordsList totalEntries="7">
            <record id="A-9516802" type="A" name="ftp.cloner.com" data="192.0.2.8" ttl="5771" updated="2013-05-06T12:10:52-05:00" created="2013-05-06T12:10:52-05:00"/>
            <record id="A-9516803" type="A" name="cloner.com" data="192.0.2.17" ttl="86400" updated="2013-05-06T12:10:52-05:00" created="2013-05-06T12:10:52-05:00"/>
            <record id="NS-8504404" type="NS" name="cloner.com" data="dns1.stabletransit.com" ttl="7788" updated="2013-05-06T12:10:51-05:00" created="2013-05-06T12:10:51-05:00"/>
            <record id="NS-8504405" type="NS" name="cloner.com" data="dns2.stabletransit.com" ttl="7788" updated="2013-05-06T12:10:51-05:00" created="2013-05-06T12:10:51-05:00"/>
            <record id="NS-8504406" type="NS" name="cloner.com" data="server1.cloner.com" ttl="3600" updated="2013-05-06T12:10:53-05:00" created="2013-05-06T12:10:53-05:00"/>
            <record id="MX-4220031" type="MX" name="cloner.com" data="mail.cloner.com" ttl="3600" priority="5" updated="2013-05-06T12:10:54-05:00" created="2013-05-06T12:10:54-05:00"/>
            <record id="CNAME-11336151" type="CNAME" name="www.cloner.com" data="cloner.com" ttl="5400" updated="2013-05-06T12:10:55-05:00" created="2013-05-06T12:10:55-05:00" comment="This is a comment on the CNAME record"/>
        </recordsList>
        <subdomains totalEntries="3">
            <domain id="3586210" name="sub1.cloner.com" emailAddress="administrator@rackspace.com" updated="2013-05-06T12:10:56-05:00" created="2013-05-06T12:10:55-05:00" comment="sub1.cloner.com uses rackspace.com for email domain name. Sister subdomains are sub2.cloner.com, sub3.cloner.com"/>
            <domain id="3586211" name="sub2.cloner.com" emailAddress="admin@cloner.com" updated="2013-05-06T12:10:56-05:00" created="2013-05-06T12:10:56-05:00" comment="sub1.cloner.com uses parent domain name, cloner.com, for email domain name"/>
            <domain id="3586212" name="sub3.cloner.com" emailAddress="adm@sub3.cloner.com" updated="2013-05-06T12:10:57-05:00" created="2013-05-06T12:10:57-05:00" comment="sub3.cloner.com uses it's own domain name for email domain name"/>
        </subdomains>
    </domain>
    


**Example Resulting (Cloned) domain clone1.com: XML**


.. code::

    Status: 200 OK
    Date: Thu, 28 Jul 2011 21:54:21 GMT
    X-API-VERSION: 1.0.17
    Content-Type: application/xml
    Content-Length: 2804
    
    <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
    <domain id="3586213" accountId="1234" name="clone1.com" ttl="7788" emailAddress="owner@clone1.com" updated="2013-05-06T12:17:35-05:00" created="2013-05-06T12:17:31-05:00" comment="clone1.com is a template domain for cloning others. clone1.com has subdomains - sub1.clone1.com, sub2.clone1.com, sub3.clone1.com" xmlns:ns2="http://www.w3.org/2005/Atom" xmlns="http://docs.rackspacecloud.com/dns/api/v1.0" xmlns:ns3="http://docs.rackspacecloud.com/dns/api/management/v1.0">
        <nameservers>
            <nameserver name="dns1.stabletransit.com"/>
            <nameserver name="dns2.stabletransit.com"/>
        </nameservers>
        <recordsList totalEntries="7">
            <record id="A-9516805" type="A" name="ftp.clone1.com" data="192.0.2.8" ttl="5771" updated="2013-05-06T12:17:32-05:00" created="2013-05-06T12:17:32-05:00"/>
            <record id="A-9516806" type="A" name="clone1.com" data="192.0.2.17" ttl="86400" updated="2013-05-06T12:17:33-05:00" created="2013-05-06T12:17:33-05:00"/>
            <record id="NS-8504413" type="NS" name="clone1.com" data="dns1.stabletransit.com" ttl="7788" updated="2013-05-06T12:17:31-05:00" created="2013-05-06T12:17:31-05:00"/>
            <record id="NS-8504414" type="NS" name="clone1.com" data="dns2.stabletransit.com" ttl="7788" updated="2013-05-06T12:17:31-05:00" created="2013-05-06T12:17:31-05:00"/>
            <record id="NS-8504415" type="NS" name="clone1.com" data="server1.clone1.com" ttl="3600" updated="2013-05-06T12:17:34-05:00" created="2013-05-06T12:17:34-05:00"/>
            <record id="MX-4220032" type="MX" name="clone1.com" data="mail.clone1.com" ttl="3600" priority="5" updated="2013-05-06T12:17:35-05:00" created="2013-05-06T12:17:35-05:00"/>
            <record id="CNAME-11336152" type="CNAME" name="www.clone1.com" data="clone1.com" ttl="5400" updated="2013-05-06T12:17:35-05:00" created="2013-05-06T12:17:35-05:00" comment="This is a comment on the CNAME record"/>
        </recordsList>
        <subdomains totalEntries="3">
            <domain id="3586214" name="sub1.clone1.com" emailAddress="administrator@rackspace.com" updated="2013-05-06T12:17:36-05:00" created="2013-05-06T12:17:36-05:00" comment="sub1.clone1.com uses rackspace.com for email domain name. Sister subdomains are sub2.clone1.com, sub3.clone1.com"/>
            <domain id="3586215" name="sub2.clone1.com" emailAddress="admin@clone1.com" updated="2013-05-06T12:17:37-05:00" created="2013-05-06T12:17:37-05:00" comment="sub1.clone1.com uses parent domain name, clone1.com, for email domain name"/>
            <domain id="3586216" name="sub3.clone1.com" emailAddress="adm@sub3.clone1.com" updated="2013-05-06T12:17:37-05:00" created="2013-05-06T12:17:37-05:00" comment="sub3.clone1.com uses it's own domain name for email domain name"/>
        </subdomains>
    </domain>
    


**Example Reference (Existing) domain cloner.com: JSON**


.. code::

    Status: 200 OK
    Date: Thu, 28 Jul 2011 21:54:21 GMT
    X-API-VERSION: 1.0.17
    Content-Type: application/json
    Content-Length: 3325
    
    {
      "name" : "cloner.com",
      "id" : 3586209,
      "comment" : "cloner.com is a template domain for cloning others. cloner.com has subdomains - sub1.cloner.com, sub2.cloner.com, sub3.cloner.com",
      "updated" : "2013-05-06T17:10:55.000+0000",
      "nameservers" : [ {
        "name" : "dns1.stabletransit.com"
      }, {
        "name" : "dns2.stabletransit.com"
      } ],
      "accountId" : 1234,
      "recordsList" : {
        "totalEntries" : 7,
        "records" : [ {
          "name" : "ftp.cloner.com",
          "id" : "A-9516802",
          "type" : "A",
          "data" : "192.0.2.8",
          "updated" : "2013-05-06T17:10:52.000+0000",
          "ttl" : 5771,
          "created" : "2013-05-06T17:10:52.000+0000"
        }, {
          "name" : "cloner.com",
          "id" : "A-9516803",
          "type" : "A",
          "data" : "192.0.2.17",
          "updated" : "2013-05-06T17:10:52.000+0000",
          "ttl" : 86400,
          "created" : "2013-05-06T17:10:52.000+0000"
        }, {
          "name" : "cloner.com",
          "id" : "NS-8504404",
          "type" : "NS",
          "data" : "dns1.stabletransit.com",
          "updated" : "2013-05-06T17:10:51.000+0000",
          "ttl" : 7788,
          "created" : "2013-05-06T17:10:51.000+0000"
        }, {
          "name" : "cloner.com",
          "id" : "NS-8504405",
          "type" : "NS",
          "data" : "dns2.stabletransit.com",
          "updated" : "2013-05-06T17:10:51.000+0000",
          "ttl" : 7788,
          "created" : "2013-05-06T17:10:51.000+0000"
        }, {
          "name" : "cloner.com",
          "id" : "NS-8504406",
          "type" : "NS",
          "data" : "server1.cloner.com",
          "updated" : "2013-05-06T17:10:53.000+0000",
          "ttl" : 3600,
          "created" : "2013-05-06T17:10:53.000+0000"
        }, {
          "name" : "cloner.com",
          "priority" : 5,
          "id" : "MX-4220031",
          "type" : "MX",
          "data" : "mail.cloner.com",
          "updated" : "2013-05-06T17:10:54.000+0000",
          "ttl" : 3600,
          "created" : "2013-05-06T17:10:54.000+0000"
        }, {
          "name" : "www.cloner.com",
          "id" : "CNAME-11336151",
          "type" : "CNAME",
          "comment" : "This is a comment on the CNAME record",
          "data" : "cloner.com",
          "updated" : "2013-05-06T17:10:55.000+0000",
          "ttl" : 5400,
          "created" : "2013-05-06T17:10:55.000+0000"
        } ]
      },
      "subdomains" : {
        "domains" : [ {
          "name" : "sub1.cloner.com",
          "id" : 3586210,
          "comment" : "sub1.cloner.com uses rackspace.com for email domain name. Sister subdomains are sub2.cloner.com, sub3.cloner.com",
          "updated" : "2013-05-06T17:10:56.000+0000",
          "emailAddress" : "administrator@rackspace.com",
          "created" : "2013-05-06T17:10:55.000+0000"
        }, {
          "name" : "sub2.cloner.com",
          "id" : 3586211,
          "comment" : "sub1.cloner.com uses parent domain name, cloner.com, for email domain name",
          "updated" : "2013-05-06T17:10:56.000+0000",
          "emailAddress" : "admin@cloner.com",
          "created" : "2013-05-06T17:10:56.000+0000"
        }, {
          "name" : "sub3.cloner.com",
          "id" : 3586212,
          "comment" : "sub3.cloner.com uses it's own domain name for email domain name",
          "updated" : "2013-05-06T17:10:57.000+0000",
          "emailAddress" : "adm@sub3.cloner.com",
          "created" : "2013-05-06T17:10:57.000+0000"
        } ],
        "totalEntries" : 3
      },
      "ttl" : 7788,
      "emailAddress" : "owner@cloner.com",
      "created" : "2013-05-06T17:10:51.000+0000"
    }


**Example Resulting (Cloned) domain clone1.com: JSON**


.. code::

    Status: 200 OK
    Date: Thu, 28 Jul 2011 21:54:21 GMT
    X-API-VERSION: 1.0.17
    Content-Type: application/json
    Content-Length: 3325
    
    {
      "name" : "clone1.com",
      "id" : 3586213,
      "comment" : "clone1.com is a template domain for cloning others. clone1.com has subdomains - sub1.clone1.com, sub2.clone1.com, sub3.clone1.com",
      "updated" : "2013-05-06T17:17:35.000+0000",
      "nameservers" : [ {
        "name" : "dns1.stabletransit.com"
      }, {
        "name" : "dns2.stabletransit.com"
      } ],
      "accountId" : 1234,
      "recordsList" : {
        "totalEntries" : 7,
        "records" : [ {
          "name" : "ftp.clone1.com",
          "id" : "A-9516805",
          "type" : "A",
          "data" : "192.0.2.8",
          "updated" : "2013-05-06T17:17:32.000+0000",
          "ttl" : 5771,
          "created" : "2013-05-06T17:17:32.000+0000"
        }, {
          "name" : "clone1.com",
          "id" : "A-9516806",
          "type" : "A",
          "data" : "192.0.2.17",
          "updated" : "2013-05-06T17:17:33.000+0000",
          "ttl" : 86400,
          "created" : "2013-05-06T17:17:33.000+0000"
        }, {
          "name" : "clone1.com",
          "id" : "NS-8504413",
          "type" : "NS",
          "data" : "dns1.stabletransit.com",
          "updated" : "2013-05-06T17:17:31.000+0000",
          "ttl" : 7788,
          "created" : "2013-05-06T17:17:31.000+0000"
        }, {
          "name" : "clone1.com",
          "id" : "NS-8504414",
          "type" : "NS",
          "data" : "dns2.stabletransit.com",
          "updated" : "2013-05-06T17:17:31.000+0000",
          "ttl" : 7788,
          "created" : "2013-05-06T17:17:31.000+0000"
        }, {
          "name" : "clone1.com",
          "id" : "NS-8504415",
          "type" : "NS",
          "data" : "server1.clone1.com",
          "updated" : "2013-05-06T17:17:34.000+0000",
          "ttl" : 3600,
          "created" : "2013-05-06T17:17:34.000+0000"
        }, {
          "name" : "clone1.com",
          "priority" : 5,
          "id" : "MX-4220032",
          "type" : "MX",
          "data" : "mail.clone1.com",
          "updated" : "2013-05-06T17:17:35.000+0000",
          "ttl" : 3600,
          "created" : "2013-05-06T17:17:35.000+0000"
        }, {
          "name" : "www.clone1.com",
          "id" : "CNAME-11336152",
          "type" : "CNAME",
          "comment" : "This is a comment on the CNAME record",
          "data" : "clone1.com",
          "updated" : "2013-05-06T17:17:35.000+0000",
          "ttl" : 5400,
          "created" : "2013-05-06T17:17:35.000+0000"
        } ]
      },
      "subdomains" : {
        "domains" : [ {
          "name" : "sub1.clone1.com",
          "id" : 3586214,
          "comment" : "sub1.clone1.com uses rackspace.com for email domain name. Sister subdomains are sub2.clone1.com, sub3.clone1.com",
          "updated" : "2013-05-06T17:17:36.000+0000",
          "emailAddress" : "administrator@rackspace.com",
          "created" : "2013-05-06T17:17:36.000+0000"
        }, {
          "name" : "sub2.clone1.com",
          "id" : 3586215,
          "comment" : "sub1.clone1.com uses parent domain name, clone1.com, for email domain name",
          "updated" : "2013-05-06T17:17:37.000+0000",
          "emailAddress" : "admin@clone1.com",
          "created" : "2013-05-06T17:17:37.000+0000"
        }, {
          "name" : "sub3.clone1.com",
          "id" : 3586216,
          "comment" : "sub3.clone1.com uses it's own domain name for email domain name",
          "updated" : "2013-05-06T17:17:37.000+0000",
          "emailAddress" : "adm@sub3.clone1.com",
          "created" : "2013-05-06T17:17:37.000+0000"
        } ],
        "totalEntries" : 3
      },
      "ttl" : 7788,
      "emailAddress" : "owner@clone1.com",
      "created" : "2013-05-06T17:17:31.000+0000"
    }

