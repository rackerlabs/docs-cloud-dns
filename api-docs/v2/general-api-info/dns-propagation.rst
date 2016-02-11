.. _cdns-dg-propagation:

===============
DNS propagation
===============

<<<<<<< HEAD
Typical DNS propagation to Rackspace name servers (globally) may take up
to one minute. This refers to the amount of time it takes after a change
(add/delete/update) is made to a customer's records via API, DNS
Manager, MyRackspace Customer Portal, Cloud Control, and so forth before
the change is live on our name servers.

A large amount of changes made simultaneously may take 2-3 minutes. If a
new domain is added or an existing domain is deleted, this may take up
to a few minutes to propagate to our Rackspace name servers. When
changing name servers for a domain, complete propagation will take about
2 days for most domains; this is enforced by the registries.
=======
After a DNS change (add, delete, or update) is made to a customer's records, it might take 
up to a minute for the change to propagate to Rackspace name servers.  Many changes made 
simultaneously might take two to three minutes to propagate. If a new domain is added or 
an existing domain is deleted, this change can take up to a few minutes to propagate. Under 
extremely high load, propagation times may exceed five minutes when creating or deleting 
domains. When name servers for a domain are changed, complete propagation will take about 
two days for most domains; this is enforced by the registries.

>>>>>>> 67e2a107191eb8bef87aa0a08dd3c73120a05f0c

