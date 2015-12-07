.. _gs-create-server:

Create a new cloud server 
~~~~~~~~~~~~~~~~~~~~~~~~~

This guide requires two cloud servers for setting up DNS using the Cloud
DNS API. If you will be using two *existing* cloud servers on your
account for this purpose, skip Steps 1-5 and go directly to Step 6
below. Otherwise, follow the steps below:

Create a cloud server using the cloud servers section of the `Cloud
Control Panel <http://mycloud.rackspace.com/>`__.

..  note::
    You can also create a cloud server using the Cloud Servers API. Refer to
    the *`Cloud Servers API Developer Guide <https://developer.rackspace.com/docs/cloud-servers/v2/developer-guide/>`__*
    for details.

 
**To create a cloud server using the Cloud Control
Panel:**

1.  Click **Servers** to view the Cloud Servers page.

2.  Click **Create Server**.

3.  Specify the **Server Name** and select a **Size** for your cloud
    server, then click **Create Server**.

4.  Using the **Region** drop-down menu, select the appropriate region.

5.  Select an image from a list of different operating systems,
    including Linux Distributions and Windows Images. For the purposes
    of this exercise, you can select any image listed and the two
    servers do not need to use the same image.

6.  Select the desired\ **Flavor**. 1 GB General Purpose v1 is suggested
    for this exercise.

7.  Click **Create Server** to create your server.

8.  Record the IP address listed for your cloud server below:

    -  FIRST cloud server IP address = ___________________________________


    Also make a note of the root admin password, since you will need it
    to perform administrative tasks on the server.

9.  Repeat steps 2-8 to create a second cloud server.

10. Record the IP address listed for your cloud server below:

    -  SECOND cloud server IP address = ________________________________

    Also make a note of the root admin password, since you will need it
    to perform administrative tasks on the server.
