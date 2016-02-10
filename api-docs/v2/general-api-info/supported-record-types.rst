.. _cdns-dg-supported-record-types:

======================
Supported Record Types
======================

The |product name| service supports the following *record* types:

Record Type: **A**  (Maps an IPV4 address to a zone)
     	
	.. code::  
	
	   {  "name" : "example.com", 
	      "description" : "This is an example A record set.", 
	      "type" : "A", 
	      "ttl" : 3600, 
	      "records" : [ "123.456.78.9" ] }
     	 
    	
Record Type: **AAAA** (Maps an IPV6 address to a zone)
	
	.. code:: 
	
	   {  “name” : “example.com”, 
	      “description” : “This is an example AAAA record set.”, 
	      “type” : “AAAA”, 
	      “ttl” : 3600, 
	      “records” : [ "4321:0:1:2:3:4:567:89ab" ] }
    	 
Record Type: **CNAME** (Creates an alias for a zone)

	.. code::
	
	   {  "name" : “www.example.com.",
	      "description" : "This is an example CNAME record set.",
	      "type" : “CNAME",
	      "ttl" : 3600,
	      "records" : [ “example.com." ] }
    	
  	.. note::
  	
  	   A CNAME record label (name) can have underscores anywhere in any subzone labels, 
  	   but not in the main zone name of the zone to which the record belongs. For example, 
  	   for the zone *example.com*, a CNAME record belonging to that zone can have the label 
  	   ``_ab_b_.cd_e.example.com``.

Record Type: **MX** (Designates a zone's mail server)

	.. code::
	   
	   {  "name" : "mail.example.com.",
	      "description": “This is an example MX record set.",
	      "type" : “MX",
	      "ttl" : 3600,
	      "records" : [ “10 mail.example.com." ] }

  	.. note::
  	
  	   The MX record set data format is “<priority> <host>”, so in the preceding recordset 
  	   example, the priority = ``10`` and host = ``mail.example.com``.
  	   
Record Type: **NS** (Designates a zone's authoritative name server)

   .. code::
   
      {  "name" : "example.com.",
         "description" : "This is an example NS record set.",
         "type" : "NS",
         "ttl" : 3600,
         "records" : [ "ns1.com" ] }

Record Type: **PTR** (Designates a reverse DNS record)

   .. code::
   
      {  "name" : "7.0.2.192.in-addr.arpa.",
         "description”: “This is an example PTR record set.",
         "type" : "PTR",
         "ttl" : 3600,
         "records" : [ "example.com." ] }
   
   .. note::

      PTR records are not supported during Early Access and will only be supported during 
      the upcoming Unlimited Availability phase.

Record Type: **SRV** (General service locator record for a zone)

   .. code::
   
      {  "name" : "_sip.tcp.example.com.",
         "description": "This is an example SRV record set.",
         "type" : "SRV",
         "ttl" : 3600,
         "records" : [ "10 0 5060 server.example.com." ] }

   .. note::

      The SRV record set data format is “<priority> <weight> <port> <target-hostname>” 
      (for example: ``10 0 5060 server.example.org``, as shown in the preceding example.). 
      The ``name`` attribute should contain the service name, protocol, and zone name 
      (for example: ``_sip.tcp.example.org``.).

      The DNS API flags two SRV records as duplicates if their service name, protocol, 
      zone name, priority, and weight all match, **and** both records are targeted to the 
      same server (host and port combination). So, for the zone example.com, the DNS API 
      will accept the following SRV records for the zone and will not flag them as 
      duplicates (in the format “<name><ttl> IN <type><priority><weight><port><target-hostname>”):

		.. code::
		
		   _sip._tcp.example.com. 86400 IN SRV 20 0 5060 backupbox1.example.com.
		   _sip._tcp.example.com. 86400 IN SRV 20 0 5061 backupbox1.example.com.	
		   _ftp._tcp.example.com. 86400 IN SRV 20 0 5062 backupbox2.example.com.
		   _sip._tcp.example.com. 86400 IN SRV 20 0 5061 backupbox2.example.com.

   .. note::
   
      The data attribute of an SRV record specifies the *weight*, *port*, and *target* of 
      the service represented by the record. These values are space delimited. The 
      |apiservice| makes the following assumptions when parsing the data attribute of an 
      ``SRV`` record:
   	
   	-  The values for the *weight*, *port* and *target* are specified in that order.

   	-  If only one field is provided in the data attribute, it is assumed to be the 
   	   *target*.

   	-  If two fields are provided in the data attribute, it is assumed they are the 
   	   *port* and *target* (in that order).

   	-  If all three fields are provided, it is assumed they are the *weight*, *port*, 
   	   and *target* (in that order).

   	-  If more than three fields are provided, it is assumed that the first three are the 
   	   *weight*, *port*, and *target* (in that order), and the rest are ignored.
      
Record Type: **TXT** (Arbitrary text)

   .. code::

      {  "name" : "example.com.",
         "description" : "This is an example TXT record set.",
         "type" : "TXT",
         "ttl" : 3600,
         "records" : [	"Some example text" ] }

   ..  note:: 
   
      ``DKIM`` records are supported using ``TXT`` records with appropriately formatted 
      data fields.