======
Faults
======

When an error occurs, the DNS Service returns a fault object containing
an HTTP error response code that denotes the type of error. In the body
of the response, the system will return additional information about the
fault.

The following table lists possible fault types with their associated
error codes and descriptions.


``dnsFault``
   500, as well as other 5xx-level:

   Generic catch-all. Should not be seen as often as the specific faults
   below. See the ``details`` element for more specifics.

``serviceUnavailable``
   503
   The request could not be processed because back-end services were
   temporarily unavailable. This condition should be temporary; contact
   support if the error persists.

``unauthorized``
   401

   The user is not authorized to access the API functionality in question.
   The user may not have authenticated to the API. If the user should have
   access to the API functionality, contact support.

``badRequest``
   400

   The request is missing one or more elements, or the values of some
   elements are invalid. See the ``details`` element or
   ``validationErrors`` element for specifics.

``itemNotFound``
   404

   The back-end services did not find anything matching the Request-URI.

``overLimit``
   413

   Either the number of entities in the request is larger than allowed
   limits, or the user has exceeded allowable request rate limits. See the
   ``details`` element for more specifics. Contact support if you think you
   need higher request rate limits.

``itemAlreadyExists``
   409

   The back-end services could not complete the request due to a conflict
   with the current state of the resource. Possibly, the user is trying to
   create an entity that already exists. See the ``details`` element for
   specifics.

``deleteFault``
   500 and nested other fault codes

   The back-end services could not successfully delete some of a number of
   entities requested to be deleted. See the ``failedItems`` element for
   specifics.

``internalServerError``
   500

   The back-end services encountered an unexpected condition that prevented
   it from fulfilling the request. See the ``details`` element for
   specifics.

   The base of all fault types is ``dnsFault``. From an XML schema
   perspective, all API faults are extensions of the base fault type
   ``dnsFault``. When working with a system such as JAXB that binds XML to
   actual classes, ``dnsFault`` can be used as a catch-all if there is no
   interest in distinguishing between individual fault types.

   ``dnsFault`` has the structure and elements shown below. All other fault
   types extend ``dnsFault``. Currently only fault types ``badRequest`` and
   ``deleteFault`` actually add additional elements to their structure as
   compared to the parent ``dnsFault``. These two fault types are described
   later.

**Example: Fault Response: XML**

.. code::

    <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
    <dnsFault xmlns="http://docs.rackspacecloud.com/dns/api/v1.0" code="500">
         <message>Main fault</message>
         <details>Error Details</details>
    </dnsFault>


**Example: Fault Response: JSON**

.. code::

    {
      "message" : "Main fault",
      "code" : 500,
      "details" : "Error Details"
    }


The error code (``code``) is returned in the body of the response for
convenience. The ``message`` element returns a human-readable message
that is appropriate for display to the end user. The ``details`` element
is optional and may contain information that is useful for tracking down
an error, such as a stack trace. The ``details`` element may or may not
be appropriate for display to an end user, depending on the role and
experience of the end user.

The fault's root element (for example, ``dnsFault``) may change
depending on the type of error. ``badRequest`` fault adds a
``validationErrors`` element that contains a list of error messages for
invalid requests. The first two ``badRequest`` examples show errors when
the request structure is wrong:

**Example: badRequest Fault on Request Structure Errors: XML**

.. code::

    <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
    <badRequest xmlns="http://docs.rackspacecloud.com/dns/api/v1.0" code="400">
         <message>The request could not be processed.</message>
         <details> Unexpected close tag &lt;/domains&gt; expected &lt;/domain&gt;.
         </details>
    </badRequest>


**Example: badRequest Fault on Request Structure Errors:
JSON**

.. code::

    {
      "message":"The request could not be processed.",
      "code":400,
      "details":"Unexpected close tag </domains>; expected </domain>."
    }


The next two ``badRequest`` examples show validation errors:

**Example: badRequest fault on validation errors: XML response**

.. code::

    <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
    <badRequest xmlns="http://docs.rackspacecloud.com/dns/api/v1.0" code="400">
         <validationErrors>
              <messages>Must provide a name for each domain.</messages>
              <messages>null is not a valid domain name.</messages>
         </validationErrors>
    </badRequest>


**Example: badRequest fault on validation errors: JSON response**

.. code::

    {
      "validationErrors":
      {
        "messages":
        [
          "Must provide a name for each domain.",
          "null is not a valid domain name."
        ]
      },
      "code":400
    }


``deleteFault`` adds a ``failedItems`` element that contains details on
entities that could not be deleted:

**Example: Example deleteFault: XML**

.. code::

    <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
    <deleteFault xmlns="http://docs.rackspacecloud.com/dns/api/v1.0" code="500">
         <message>One or more items could not be deleted.</message>
         <details>See errors list for details.</details>
         <failedItems>
              <fault code="503">
                   <message>The DNS API is currently not available.</message>
                   <details>Domain ID: 123</details>
              </fault>
         </failedItems>
    </deleteFault>


**Example: deleteFault: JSON**

.. code::

    {
        "failedItems":
         {
            "faults":
             [
              {
                "message":"The DNS API is currently not available.",
                "code":503,
                "details":"Domain ID: 123"
              }
             ]
         },
         "message":"One or more items could not be deleted.",
         "code":500,
         "details":"See errors list for details."
    }

