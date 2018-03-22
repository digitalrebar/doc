
.. note:: WARNING WARNING WARNING:  This is the Digital Rebar v2 product documentation.  The v2 version is EOL as of September 2017.  Please refer to the new Digital Rebar Provision v3 documentation:  http:\/\/provision.readthedocs.io\/en\/tip\/README.html

.. index::
  pair: Dev-Tools; Docker Admin

.. _docker_admin:

Developer Server (docker-admin)
===============================

Digital Rebar developers often run the system containers directly on their systems for development purposes.  In this mode, there is a convenience command that will start and stop the environment quickly.

To start the local admin, from an updated ``digitalrebar/core`` directory, use ``tools/docker-admin``.

This command will start a new shell session in the ``digitalrebar/deploy/compose`` directory with the correct containers running.  When exiting the command, it will remove and cleanup the environment.

There are several important command line flags to consider when using Docker Admin.

Compose Directives
~~~~~~~~~~~~~~~~~~

Add ``--no-pull`` to skip checking for updated containers.  This is very important when building containers.

Access Mode
~~~~~~~~~~~

By default, Docker Admin will start in forwarder mode.  Forwarder mode keeps all the services internal to Docker and makes it safer to run the full infrastructure.  ``tools/kvm-slave`` will still attach to the Docker network bridge and boot correctly.

Host mode is needed when attaching external services like Vagrant VMs to the Docker Admin or use the Reverse Proxy (this may be addressed by updates to the forwarder!).

**Note**: when using ``--access HOST`` the IP of the node must be supplied as an input for the command: ``EXTERNAL_IP=[CIDR] tools/docker-admin access HOST``.  This will set the correct information in the ``access.env`` file.

Omitting Containers
~~~~~~~~~~~~~~~~~~~

There are ``--no-$$$`` flags such as ``--no-dhcp`` can be added to omit containers from the start process.  This is handy when in HOST mode with a competing DHCP server or when trying to skip the time it takes to spin up a provisioner.
