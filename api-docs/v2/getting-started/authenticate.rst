.. _authenticate-to-cloud:

.. COMMENT - source common-gs authenticate.rst

Authenticate to the Rackspace Cloud
-------------------------------------

Whether you use cURL, a REST client, or a command line client (CLI) to interact with the
|apiservice|, you need an authentication token that you include in the ``X-Auth-Token``
header in each API request. You also need your account number, also known as your tenant ID. 

With a valid token, you can submit API requests to any of the API service endpoints included 
in the service catalog. A token is valid for only 24 hours, which means that you must 
generate a new token each day.


.. note::

   These instructions show how to authenticate by using username and API key credentials, 
   which is a more secure way to communicate with API services. For information about other 
   types of credentials you can use to authenticate, see 
   :rax-devdocs:`Authentication requests <cloud-identity/v2/developer-guide/#document-api-operations/token-operations>` 
   in the Rackspace Cloud Identity service developer guide. For more information about 
   authentication tokens, see the following topics in the Rackspace Cloud Identity developer 
   documentation.

.. include:: ../common-gs/auth-using-curl.rst
