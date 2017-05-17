.. _cdns-dg-comments:

========
Comments
========

Comments are supported for domains and records and their requests and
responses using the ``comment`` attribute. See the examples that follow.

**Example: Response with comments: XML**

.. code::

    Status: 200 OK
    Date: Thu, 28 Jul 2011 21:54:21 GMT
    X-API-VERSION: 1.0.17
    Content-Type: application/xml
    Content-Length: 2421

    <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
    <domain id="2725233" accountId="1234" name="example.com" ttl="3600" emailAddress="sample@rackspace.com" updated="2011-06-24T01:23:15Z" created="2011-06-24T01:12:51Z" comment="Optional domain comment..." xmlns:ns2="http://www.w3.org/2005/Atom" xmlns="http://docs.rackspacecloud.com/dns/api/v1.0" xmlns:ns3="http://docs.rackspacecloud.com/dns/api/management/v1.0">
        <nameservers>
            <nameserver name="ns.rackspace.com"/>
            <nameserver name="ns2.rackspace.com"/>
        </nameservers>
        <recordsList totalEntries="6">
            <record id="A-6817754" type="A" name="ftp.example.com" data="192.0.2.8" ttl="5771" updated="2011-05-19T08:07:08-05:00" created="2011-05-18T14:53:09-05:00"/>
            <record id="A-6822994" type="A" name="example.com" data="192.0.2.17" ttl="86400" updated="2011-06-24T01:12:52Z" created="2011-06-24T01:12:52Z"/>
            <record id="NS-6251982" type="NS" name="example.com" data="ns.rackspace.com" ttl="3600" updated="2011-06-24T01:12:51Z" created="2011-06-24T01:12:51Z"/>
            <record id="NS-6251983" type="NS" name="example.com" data="ns2.rackspace.com" ttl="3600" updated="2011-06-24T01:12:51Z" created="2011-06-24T01:12:51Z"/>
            <record id="MX-3151218" type="MX" name="example.com" data="mail.example.com" ttl="3600" priority="5" updated="2011-06-24T01:12:53Z" created="2011-06-24T01:12:53Z"/>
            <record id="CNAME-9778009" type="CNAME" name="www.example.com" data="example.com" ttl="5400" updated="2011-06-24T01:12:54Z" created="2011-06-24T01:12:54Z" comment="This is a comment on the CNAME record"/>
        </recordsList>
        <subdomains totalEntries="4">
            <domain id="2725257" name="sub1.example.com" emailAddress="sample@rackspace.com" updated="2011-06-23T03:09:34Z" created="2011-06-23T03:09:33Z" comment="1st sample subdomain"/>
            <domain id="2725258" name="sub2.example.com" emailAddress="sample@rackspace.com" updated="2011-06-23T03:52:55Z" created="2011-06-23T03:52:55Z" comment="1st sample subdomain"/>
            <domain id="2725260" name="north.example.com" emailAddress="sample@rackspace.com" updated="2011-06-23T03:53:10Z" created="2011-06-23T03:53:09Z"/>
            <domain id="2725261" name="south.example.com" emailAddress="sample@rackspace.com" updated="2011-06-23T03:53:14Z" created="2011-06-23T03:53:14Z" comment="Final sample subdomain"/>
        </subdomains>
    </domain>

**Example: Response with comments: JSON**

.. code::

    Status: 200 OK
    Date: Thu, 28 Jul 2011 21:54:21 GMT
    X-API-VERSION: 1.0.17
    Content-Type: application/json
    Content-Length: 3020

    {
      "name" : "example.com",
      "id" : 2725233,
      "comment" : "Optional domain comment...",
      "updated" : "2011-06-24T01:23:15.000+0000",
      "nameservers" : [ {
        "name" : "ns.rackspace.com"
      }, {
        "name" : "ns2.rackspace.com"
      } ],
      "accountId" : 1234,
      "recordsList" : {
        "totalEntries" : 6,
        "records" : [ {
          "name" : "ftp.example.com",
          "id" : "A-6817754",
          "type" : "A",
          "data" : "192.0.2.8",
          "updated" : "2011-05-19T13:07:08.000+0000",
          "ttl" : 5771,
          "created" : "2011-05-18T19:53:09.000+0000"
        }, {
          "name" : "example.com",
          "id" : "A-6822994",
          "type" : "A",
          "data" : "192.0.2.17",
          "updated" : "2011-06-24T01:12:52.000+0000",
          "ttl" : 86400,
          "created" : "2011-06-24T01:12:52.000+0000"
        }, {
          "name" : "example.com",
          "id" : "NS-6251982",
          "type" : "NS",
          "data" : "ns.rackspace.com",
          "updated" : "2011-06-24T01:12:51.000+0000",
          "ttl" : 3600,
          "created" : "2011-06-24T01:12:51.000+0000"
        }, {
          "name" : "example.com",
          "id" : "NS-6251983",
          "type" : "NS",
          "data" : "ns2.rackspace.com",
          "updated" : "2011-06-24T01:12:51.000+0000",
          "ttl" : 3600,
          "created" : "2011-06-24T01:12:51.000+0000"
        }, {
          "name" : "example.com",
          "priority" : 5,
          "id" : "MX-3151218",
          "type" : "MX",
          "data" : "mail.example.com",
          "updated" : "2011-06-24T01:12:53.000+0000",
          "ttl" : 3600,
          "created" : "2011-06-24T01:12:53.000+0000"
        }, {
          "name" : "www.example.com",
          "id" : "CNAME-9778009",
          "type" : "CNAME",
          "comment" : "This is a comment on the CNAME record",
          "data" : "example.com",
          "updated" : "2011-06-24T01:12:54.000+0000",
          "ttl" : 5400,
          "created" : "2011-06-24T01:12:54.000+0000"
        } ]
      },
      "subdomains" : {
        "domains" : [ {
          "name" : "sub1.example.com",
          "id" : 2725257,
          "comment" : "1st sample subdomain",
          "updated" : "2011-06-23T03:09:34.000+0000",
          "emailAddress" : "sample@rackspace.com",
          "created" : "2011-06-23T03:09:33.000+0000"
        }, {
          "name" : "sub2.example.com",
          "id" : 2725258,
          "comment" : "1st sample subdomain",
          "updated" : "2011-06-23T03:52:55.000+0000",
          "emailAddress" : "sample@rackspace.com",
          "created" : "2011-06-23T03:52:55.000+0000"
        }, {
          "name" : "north.example.com",
          "id" : 2725260,
          "updated" : "2011-06-23T03:53:10.000+0000",
          "emailAddress" : "sample@rackspace.com",
          "created" : "2011-06-23T03:53:09.000+0000"
        }, {
          "name" : "south.example.com",
          "id" : 2725261,
          "comment" : "Final sample subdomain",
          "updated" : "2011-06-23T03:53:14.000+0000",
          "emailAddress" : "sample@rackspace.com",
          "created" : "2011-06-23T03:53:14.000+0000"
        } ],
        "totalEntries" : 4
      },
      "ttl" : 3600,
      "emailAddress" : "sample@rackspace.com",
      "created" : "2011-06-24T01:12:51.000+0000"
    }



Notes for comments:

*  Are limited to 160 characters each

*  Can be any text characters

*  Are optional

*  To remove a comment, set it to the empty string, for example:
   comment=""

*  Are returned on **GET** calls for both domain and records regardless
   of whether the call is a single or multiple call, and regardless of
   whether it is a detail or non-detail call

In summary, all Create Domain and Create Record(s) and all Modify Domain
and Modify Record(s) calls can take an optional comment
(``comment="value of comment"``). In other words,
all these request calls can have an optional comment attribute.

