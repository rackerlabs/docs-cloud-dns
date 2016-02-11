.. _cdns-dg-date-time:

================
Date/Time format
================

<<<<<<< HEAD
The DNS service uses an ISO-8601 compliant date format for the display
and consumption of date/time values.
=======
The |product name| service uses an ISO-8601 compliant date format for the display
and consumption of date/time values. The system time is expressed as UTC.
>>>>>>> 67e2a107191eb8bef87aa0a08dd3c73120a05f0c

**Example: DNS Service Date/Time Format**

.. code::

    yyyy-MM-dd'T'HH:mm:ssZ

<<<<<<< HEAD
See the table below for a description of the date/time format codes.

May 19th, 2011 at 8:07:08 AM, GMT-5 would have the following format:
=======
For example, May 19th, 2011 at 8:07:08 AM, GMT-5 would have the following UCT-5 format:
>>>>>>> 67e2a107191eb8bef87aa0a08dd3c73120a05f0c

.. code::

    2011-05-19T08:07:08-0500
<<<<<<< HEAD

**Table. Explanation of Date/Time Format Codes**

+------+------------------------------------+
| Code | Description                        |
+======+====================================+
| yyyy | Four digit year                    |
+------+------------------------------------+
| MM   | Two digit month                    |
+------+------------------------------------+
| dd   | Two digit day of month             |
+------+------------------------------------+
| T    | Separator for date/time            |
+------+------------------------------------+
| HH   | Two digit hour of day (00-23)      |
+------+------------------------------------+
| mm   | Two digit minutes of hour          |
+------+------------------------------------+
| ss   | Two digit seconds of the minute    |
+------+------------------------------------+
| Z    | RFC-822 timezone (offset from GMT) |
+------+------------------------------------+
=======
    
See the following table for a description of the date/time format codes.

**Table. Explanation of Date/Time Format Codes**

+------+---------------------------------------+
| Code | Description                           |
+======+=======================================+
| yyyy | Four digit year                       |
+------+---------------------------------------+
| MM   | Two digit month                       |
+------+---------------------------------------+
| dd   | Two digit day                         |
+------+---------------------------------------+
| T    | Separator for date/time               |
+------+---------------------------------------+
| HH   | Two digit hour of day (00-23)         |
+------+---------------------------------------+
| mm   | Two digit minute                      |
+------+---------------------------------------+
| ss   | Two digit second                      |
+------+---------------------------------------+
| Z    | ISO 8601 timezone (offset from GMT).  | 
|      | If Z is not replaced with the offset  | 
|      | from GMT, it indicates a 00:00 offset.|
+------+---------------------------------------+
>>>>>>> 67e2a107191eb8bef87aa0a08dd3c73120a05f0c

