
.. note:: WARNING WARNING WARNING:  This is the Digital Rebar v2 product documentation.  That product line is EOL as of September 2017.  Please refer to the new Digital Rebar Provision v3 documentation:  http:\/\/provision.readthedocs.io\/en\/tip\/README.html

.. index::
  Provisioning; Provisioning Process
  TODO; describe_provisioning_process

.. _provisioning_process:

Provisioning Process
====================

TODO: Update for provisioning process

Overview
--------

The :ref:`arch_service_provisioner` provides the roles and recipes needed to set up the
provisioning server and a base environment for all provisioned nodes.
The Provisioner also provides the transition entry point for nodes that
require DHCP transitions completed.  The Provisioner assumes that
addressing will be handled outside of this barclamp.

Roles
-----

The following node roles are defined:

-  *Provisioner-server*: Configures the system to run the provisioning services (TFTP, Web server with apt packages, APT repository).

-  *Provisioner-service*: Allows for the injection of the provisioner information into other components.

-  *DHCP-server*: Provides a DHCP server for doing initial device discovery and points to the provisioner-service.

-  *DHCP-database*: Updates the DHCP information based upon the boot.env properties.

-  *Provisioner-database*: Updates the provisioner boot information based upon the bootenv properties. (See :ref:`api_provisioner_bootenv`.)

-  *Provisioner-repos*: Makes sure that the apt/yum repository is configured and a root ssh key is deployed.

-  *Provisioner-setup-base*: Prepares boot environments from ISOs.

Workflow
--------

The provisioner provides the Sledgehammer discovery image.  It is
expected that there is a DHCP server (provided by Digital Rebar or external
to Digital Rebar) that will allocate an address and point to the
provisioner.

The Sledgehammer discovery image will register the node in Digital Rebar
and allocate an admin address.  Once the node is created, the database
roles will update the provisioner and DHCP server to enable future
control for operating system installation, local booting, or other boot
environments as needed.

New operating systems can be seen `Adding Operating
Systems <../deployment-guide/adding-operating-systems.md>`__.

After an operating system is installed, the system injects code to
update Digital Rebar and informs it that the node has completed installation.  The
database roles will update the provisioner and DHCP servers to automatically boot from
local drives.
