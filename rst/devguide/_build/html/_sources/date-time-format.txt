================
Date/Time format
================

The DNS service uses an ISO-8601 compliant date format for the display
and consumption of date/time values.

**Example: DNS Service Date/Time Format**

.. code::

    yyyy-MM-dd'T'HH:mm:ssZ

See the table below for a description of the date/time format codes.

May 19th, 2011 at 8:07:08 AM, GMT-5 would have the following format:

.. code::

    2011-05-19T08:07:08-0500

**Explanation of Date/Time Format Codes**

yyyy
   Four digit year

MM
   Two digit month

dd
   Two digit day of month

T
   Separator for date/time

HH
   Two digit hour of day (00-23)

mm
   Two digit minutes of hour

ss
   Two digit seconds of the minute

Z
   RFC-822 timezone (offset from GMT)

