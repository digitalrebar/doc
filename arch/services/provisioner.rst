.. index::
  pair: Container; Provisioner
  pair: Services; Provisioner Web
  pair: Services; Provisioner TFTP
  pair: Services; Provisioner Management

.. _arch_service_provisioner:

Provisioner
-----------

The provisioner container provides a web server, TFTP server, and a management interface to control
the boot environments for the nodes.  The container is a wrapper for a single golang binary that manages
the system.

The provisioner has a volume mounted into its process space to store the various boot environments and
other files served to nodes.  The default location is the home directory of the process that runs
the docker-compose-up command.  In general, this is the root home directory of the :ref:`arch_other_systems`.
Its  default location is /root/.cache/digitalrebar/tftpboot

This directory allows for faster restarts and caching, so  downloaded and processed ISO do not have
to be generated every time the containers are restarted or rebuilt.
