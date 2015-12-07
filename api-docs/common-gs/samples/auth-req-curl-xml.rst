.. auth-req-curl-xml

.. code::
   $ curl -s -d \
   '<?xml version="1.0" encoding="UTF-8"?>
   <auth>
      <apiKeyCredentials
          xmlns="http://docs.rackspace.com/identity/api/ext/RAX-KSKEY/v1.0"
          username="your_username"
          apiKey="your_api_key"/>
   </auth>' \
   -H 'Content-Type: application/xml' \
   -H 'Accept: application/xml' \
   'https://identity.api.rackspacecloud.com/v2.0/tokens' | ppxml
