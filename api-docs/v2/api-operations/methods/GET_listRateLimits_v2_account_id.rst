.. _GET_listRateLimits_v2_account_id:

List rate limits
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code::

    GET /v2/{TENANT_ID}/ratelimits

This operation provides a list of the user's current rate limits, updated in real time.
If a user with a rate limit of 60/minute for a operation X performs that operation
twice and then executes this rate limits operation, the remaining limit for the operation 
X would show as 58.


This table shows the possible response codes for this operation:

+---------+-----------------------+---------------------------------------------+
| Response| Name                  | Description                                 |
| code    |                       |                                             |
+=========+=======================+=============================================+
| 200     | Success               | The request succeeded.                      |
+---------+-----------------------+---------------------------------------------+
| 400     | Bad Request           | The request is missing one or more          |
|         |                       | elements, or the values of some elements    |
|         |                       | are invalid.                                |
+---------+-----------------------+---------------------------------------------+
| 401     | Unauthorized          | You are not authorized to complete this     |
|         |                       | operation. This error can occur if the      |
|         |                       | request is submitted with an invalid        |
|         |                       | authentication token.                       |
+---------+-----------------------+---------------------------------------------+
| 403     | Forbidden             | The server did not find anything matching   |
|         |                       | the request URI.                            |
+---------+-----------------------+---------------------------------------------+
| 404     | Not Found             | The requested item was not found.           |
+---------+-----------------------+---------------------------------------------+
| 405     | Method Not Allowed    | The method specified in the request is      |
|         |                       | not allowed for the resource identified by  |
|         |                       | the request URI.                            |
+---------+-----------------------+---------------------------------------------+
| 413     | Over Limit            | The request exceeds the rate limit or quota.|
+---------+-----------------------+---------------------------------------------+
| 415     | Unsupported Media     | The server won't service the                |
|         | Type                  | request because the entity of the request   |
|         |                       | is in a format not supported by the         |
|         |                       | requested resource for the requested        |
|         |                       | method.                                     |
+---------+-----------------------+---------------------------------------------+
| 503     | Service Unavailable   | The service is not available.               |
+---------+-----------------------+---------------------------------------------+

Request
""""""""""""""""

This table shows the URI parameters for the request:

+-----------------------+---------+---------------------------------------------+
| Name                  | Type    | Description                                 |
+=======================+=========+=============================================+
| ``{TENANT_ID}``       | ​String | The account ID of the account owner.        |
+-----------------------+---------+---------------------------------------------+

**Example:  List rate limits, request**

.. code::  

    GET /v2/123456/ratelimits HTTP/1.1
    Host: global.dns.rackspacecloud.com
    Accept: application/json
    Content-Type: application/json

This operation does not accept a request body.

Response
""""""""""""""""

This table shows the body parameters for the response:

+--------------------------------+----------------------+----------------------+
|Name                            |Type                  |Description           |
+================================+======================+======================+
|**limits**                      |Object                |A container of limits.|
+--------------------------------+----------------------+----------------------+
|limits.\ **rate**               |Array                 |An array of rate      |
|                                |                      |limits objects.       |
+--------------------------------+----------------------+----------------------+
|limits.rate. \ **limit**        |Array                 |An array of limits for|
|                                |                      |a URI.                |
+--------------------------------+----------------------+----------------------+
|limits.rate.limit. \            |Date                  |The next available    |
|**next-available**              |                      |time an API call can  |
|                                |                      |be made to this URI   |
|                                |                      |without being rate    |
|                                |                      |limited.              |
+--------------------------------+----------------------+----------------------+
|limits.rate.limit. \ **unit**   |String                |The type of unit for  |
|                                |                      |the rate limit.  For  |
|                                |                      |example, ``MINUTE``   |
|                                |                      |or ``DAY``.           |
+--------------------------------+----------------------+----------------------+
|limits.rate.limit. \            |Integer               |The time remaining    |
|**remaining**                   |                      |for the limit in      |
|                                |                      |units.                |
+--------------------------------+----------------------+----------------------+
|limits.rate.limit. \ **value**  |Integer               |The maximum allowed   |
|                                |                      |time in units.        |
+--------------------------------+----------------------+----------------------+
|limits.rate.limit. \ **verb**   |String                |The HTTP operation.   |
+--------------------------------+----------------------+----------------------+
|limits.rate. \ **regex**        |Regular Expression    |The regular expression|
|                                |                      |that defines the      |
|                                |                      |actual endpoints that |
|                                |                      |are encompassed in the|
|                                |                      |rate limit.           |
+--------------------------------+----------------------+----------------------+
|limits.rate. \ **uri**          |URL                   |The endpoint being    |
|                                |                      |limited.              |
+--------------------------------+----------------------+----------------------+

**Example: List rate limits, response**

.. code::  

    HTTP/1.1 200 OK
    Vary: Accept
    Content-Type: application/json

   {
     "limits": {
       "rate": [
         {
           "limit": [
             {
               "next-available": "2016-05-26T14:59:13.119Z",
               "unit": "MINUTE",
               "remaining": 4,
               "value": 4,
               "verb": "GET"
             }
           ],
           "regex": ".*/v2/(\\d+)/recordsets.*",
           "uri": "/recordsets"
         },
         {
           "limit": [
             {
               "next-available": "2016-05-26T14:59:13.119Z",
               "unit": "MINUTE",
               "remaining": 20,
               "value": 20,
               "verb": "DELETE"
             }
           ],
           "regex": ".*/v2/(\\d+/zones)/[0-9a-f]{8}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{12}/recordsets.*",
           "uri": "/zones/id/recordsets/id"
         },
         {
           "limit": [
             {
               "next-available": "2016-05-26T14:59:13.119Z",
               "unit": "MINUTE",
               "remaining": 10,
               "value": 10,
               "verb": "POST"
             }
           ],
           "regex": ".*/v2/(\\d+/zones/?(?:tasks/imports/?)?)",
           "uri": "/zones"
         }
         {
           "limit": [
             {
               "next-available": "2016-05-26T14:59:13.119Z",
               "unit": "MINUTE",
               "remaining": 20,
               "value": 20,
               "verb": "PATCH"
             }
           ],
           "regex": ".*/v2/(\\d+/zones)/[0-9a-f]{8}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{12}/?",
           "uri": "/zones/id"
         }
       ]
     }
   }
