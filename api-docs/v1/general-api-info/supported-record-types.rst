.. _cdns-dg-supported-record-types:

======================
Supported Record Types
======================

The Rackspace Cloud DNS Service supports the *record* types listed below.

**Rackspace Cloud DNS Supported Record Types**

Record Type: **A**

- Maps an IPV4 address to a domain

  Example A Record: XML:

    .. code::

        <record id="A-123" type="A" name="example.foo.com" data="123.456.78.9" ttl="86400"/>

  Example A Record : JSON:

    .. code::

       { "id" : "A-123", "type" : "A", "name" : "example.foo.com", "data" : "123.456.78.9", "ttl" : 86400 }

Record Type: **AAAA**

- Maps an IPV6 address to a domain

  Example AAAA Record : XML:

    .. code::

        <record id="AAAA-123" type="AAAA" name="example.foo.com" data="4321:0:1:2:3:4:567:89ab" ttl="86400"/>

  Example AAAA Record : JSON:

    .. code::

        { "id" : "AAAA-123", "type" : "AAAA", "name" : "example.foo.com", "data" : "4321:0:1:2:3:4:567:89ab", "ttl" : 86400 }

Record Type: **CNAME**

- Creates an alias for a domain

  Example CNAME Record : XML:

    .. code::

        <record id="CNAME-123" type="CNAME" name="www.example.foo.com" data="example.foo.com" ttl="86400"/>

  Example CNAME Record : JSON:

    .. code::

       { "id" : "CNAME-123", "type" : "CNAME", "name" : "www.example.foo.com", "data" : "example.foo.com", "ttl" : 86400 }

  .. note::

        A CNAME record label (name) can have underscores anywhere in any subdomain labels, but not in the main domain name of the domain to which the record belongs. For example, for the domain example.com, a CNAME record belonging to that domain can have the label ``_ab_b_.cd_e.example.com``

Record Type: **MX**

- Designates a domain's mail server

  Example MX Record : XML:

    .. code::

       <record id="MX-123" priority="10" type="MX" name="example.foo.com" data="mail.example.foo.com" ttl="3600"/>

  Example MX Record : JSON:

    .. code::

       { "id" : "MX-123", "priority" : 10, "type" : "MX", "name" : "example.foo.com", "data" : "mail.example.foo.com", "ttl" : 3600 }

Record Type: **NS**

- Designates a domain's authoritative name server

  Example NS Record : XML:

    .. code::

        <record id="NS-123" type="NS" name="example.foo.com" data="ns1.foo.com" ttl="54000"/>

  Example NS Record : JSON:

    .. code::

        { "id" : "NS-123", "type" : "NS", "name" : "example.foo.com", "data" : "ns1.foo.com", "ttl" : 54000 }

Record Type: **PTR**

- Designates a reverse DNS record

  Example PTR Record : XML:

   .. code::

        <record id="PTR-000002" type="PTR" name="example.com" data="192.0.2.7" ttl="56000" updated="2011-09-24T01:12:51Z" created="2011-09-24T01:12:51Z"/>

  Example PTR Record : JSON:

    .. code::

        { "name" : "example.com", "id" : "PTR-000002", "type" : "PTR", "data" : "192.0.2.7", "ttl" : 56000, "updated" : "2011-09-24T01:12:51.000+0000", "created" : "2011-09-24T01:12:51.000+0000" }

    .. note::

       PTR records can only be managed using the /rdns URIs.

Record Type: **SRV**

- General service locator record for a domain

  Example SRV Record : XML:

    .. code::

       <record id="SRV-123" type="SRV" name="_sip._tcp.example.foo.com" priority="30" data="1 3443 sip.foo.com" ttl="86400"/>

  Example SRV Record : JSON:

    .. code::

       { "id" : "SRV-123", "type" : "SRV", "name" : "_sip._tcp.example.foo.com", "priority" : 30, "data" : "1 3443 sip.foo.com", "ttl" : 86400 }

Notes
~~~~~

*  The standard format of an SRV record is: \_service.\_proto.name TTL
   class SRV priority weight port target, for example:
   \_sip.\_tcp.example.com. 86400 IN SRV 10 60 5060 bigbox.example.com.

*  The DNS API flags two SRV records as duplicates if their \_service,
   \_proto, name, priority, and weight match, **and** both records are
   targeted to the same server (host and port combination) as well. So,
   for the domain example.com, the DNS API will accept the following SRV
   records for the domain and will not flag them as duplicates:

   *  \_sip.\_tcp.example.com. 86400 IN SRV 20 0 5060
      backupbox1.example.com.

   *  \_sip.\_tcp.example.com. 86400 IN SRV 20 0 5061
      backupbox1.example.com.

   *  \_ftp.\_tcp.example.com. 86400 IN SRV 20 0 5062
      backupbox2.example.com.

   *  \_sip.\_tcp.example.com. 86400 IN SRV 20 0 5061
      backupbox2.example.com.

*  The data attribute of an SRV record specifies the *weight*, *port*,
   and *target* of the service represented by the record. These values
   are space delimited. The DNS API makes the following assumptions when
   parsing the data attribute of an SRV record:

   *  The values for the *weight*, *port* and *target* are specified in
      that order.

   *  If only one field is provided in the data attribute, it is assumed
      to be the *target*.

   *  If two fields are provided in the data attribute, it is assumed
      they are the *port* and *target* (in that order).

   *  If all three fields are provided, it is assumed they are the
      *weight*, *port*, and *target* (in that order).

   *  If more than three fields are provided, it is assumed that the
      first three are the *weight*, *port*, and *target* (in that
      order), and the rest are ignored.

Record Type: **TXT**

- Arbitrary text for a domain record

  Example TXT Record : XML:

   .. code::

    <record id="TXT-123" type="TXT" name="example.foo.com" data="Some example text" ttl="3600"/>

  Example TXT Record : JSON:

   .. code::

    { "id" : "TXT-123", "type" : "TXT", "name" : "example.foo.com", "data" : "Some example text", "ttl" : 3600 }

Notes
~~~~~

*  ``DKIM`` and ``SPF`` records are supported using ``TXT`` records with
   appropriately formatted data fields.

*  Invalid quote and slash characters are automatically removed from ``TXT``
   records by the |product name| Service.



