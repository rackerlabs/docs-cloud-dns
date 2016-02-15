.. _install-CLI-client:

Install the CLI clients
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

If you want to run the cURL examples instead of CLI, skip this step and proceed to the 
next section "Send Requests to the API".

Run the following commands on a Mac or Linux distribution to install the OpenStack and 
Designate clients:

.. code::  

    $ sudo pip install -U python-openstackclient 
    $ sudo pip install -U python-designateclient 

Create a CLI config file with the content as shown below, and name the file **clouds.yaml** 
underneath your current directory.

.. code::  

    clouds:
      prod:
        auth:
          auth_url: https://identity.api.rackspacecloud.com/v2.0/
          project_id: 123456
          username: <RACKSPACE_CLOUD_USERNAME>
          password: <RACKSPACE_CLOUD_PASSWORD>

See the following for more CLI configuration options: 
:os-docs:`Configuring Openstack CLI <developer/python-openstackclient/configuration.html>`

Export the necessary environment variables:

.. code::  

     $ export OS_CLOUD=prod 

Run the following command to see if OpenStack/Designate CLI works:

.. code::  

    $ openstack --help 

If you get an error such as ``Exception: Versioning for this project requires either an 
sdist tarball, or access to an upstream git repository. Are you sure that git is installed?``, 
run the following command:

.. code::  

    $ sudo pip install -U distribute

Now that your command line tool is ready, jump to :ref:`Creating a zone with the CLI<cli-create-zone>`.