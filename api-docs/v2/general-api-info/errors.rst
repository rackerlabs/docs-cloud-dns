.. _cdns-dg-errors:

======
Errors
======

When an error occurs, the |product name| service returns a an object containing an HTTP 
error response code that denotes the type of error. In the body of the response, the system 
will return additional information about the error.

The following table lists possible error types with their associated error codes and 
descriptions.

+----------------------+------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Error Type           |Error | Description                                                                                                                                                                                                                                       |
|                      |Code  |                                                                                                                                                                                                                                                   |
+----------------------+------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Service Unavailable  | 503  | The request could not be processed because back-end services were temporarily unavailable. This condition should be temporary; contact support if the error persists.                                                                             |
+----------------------+------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| unauthorized         | 401  | The user is not authorized to access the API functionality in question. The user may not have authenticated to the API. If the user should have access to the API functionality, contact support.                                                 |
+----------------------+------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| bad_request          | 400  | The request is missing one or more elements, or the values of some elements are invalid. See errors or type item for specifics.                                                                                                                   |
+----------------------+------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| forbidden            | 403  | The endpoint is not defined in the service catalog, or the user is not permitted to perform the API action in question.                                                                                                                           |
+----------------------+------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| resource_not_found   | 404  | The back-end services did not find anything matching the request UUID.                                                                                                                                                                            |
+----------------------+------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| method_not_allowed   | 405  | The method is not allowed for the URL.                                                                                                                                                                                                            |
+----------------------+------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| over_quota           | 413  | The user has exceeded allowable request rate limits or the absolute limits for the resource. Contact support if you think you need higher limits.                                                                                                 |
+----------------------+------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| duplicate_resource   | 409  | The back-end services could not complete the request due to a conflict with the current state of the resource. Possibly, the user is trying to create an entity that already exists. See the message element for specifics.                       |
+----------------------+------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| timeout              | 504  | The back-end services encountered an unexpected condition that prevented it from fulfilling the request in the allotted time.                                                                                                                     |
+----------------------+------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Internal Server Error| 500  | The back-end services encountered an unexpected condition that prevented it from fulfilling the request. See the details element for specifics.                                                                                                   |
+----------------------+------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Global Rate Limit    | 513  | The system is under peak load and new requests are being rate limited. Please try again.                                                                                                                                                          |
+----------------------+------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

All errors will look similar. A ``code`` element will show the HTTP error code for convenience.
The ``type`` element will show the type of error. The ``request_id`` will help API operators
debug the request in a support ticket, if necessary. The ``message`` field, when present, 
will inform the user of the exact problem the API detected.

**Example: Fault response**

.. code::

    {
      "code" : 500,
      "type" : "error",
      "request_id": "req-6d896f1e-9686-454e-af6f-412a802f9451"
    }


The ``bad_request`` example shows validation errors:

**Example: bad_request fault on validation errors**

.. code::

    {
      "code":400,
      "type": "invalid_object",
      "errors": {
         "errors": [
            {
               "path": [ "name" ],
               "message": "u'example.com' is not a 'domainname'",
               "validator": "format",
               "validator_value": "domainname"
            }
         ]
      },
      "request_id": "req-9ebcb6a5-5673-4696-bbfc-61524e986f31"
    }