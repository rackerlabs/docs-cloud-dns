.. _cdns-dg-propagation:

===============
DNS propagation
===============

After a DNS change (add, delete, or update) is made to a customer's records, it might take 
up to a minute for the change to propagate to Rackspace name servers.  Many changes made 
simultaneously might take two to three minutes to propagate. If a new domain is added or 
an existing domain is deleted, this change can take up to a few minutes to propagate. Under 
extremely high load, propagation times may exceed five minutes when creating or deleting 
domains. When name servers for a domain are changed, complete propagation will take about 
two days for most domains; this is enforced by the registries.

