.. _dg_add_os:

Seeding Provisionable Operating Systems
=======================================

.. index::
  Boot Environment; Default List
  OS Install; Default List

When deploying an admin node in production mode, you will want to be
able to install operating systems on slave nodes. By default, the
``provisioner`` container will look for OS install ISO images in
``/root/.cache/digitalrebar/tftpboot/isos``.

As of June 2016, the provisioner knows how to install the following
operating systems from the following ISO images:

-  ``ubuntu-12.04``: ``ubuntu-12.04.5-server-amd64.iso``
-  ``ubuntu-14.04``: ``ubuntu-14.04.3-server-amd64.iso``
-  ``ubuntu-15.04``: ``ubuntu-15.04-server-amd64.iso``
-  ``ubuntu-16.04``: ``ubuntu-16.04-server-amd64.iso``
-  ``centos-6.6``: ``CentOS-6.6-x86_64-bin-DVD1.iso``
-  ``centos-7.1.1503``: ``CentOS-7-x86_64-Minimal-1503-01.iso``
-  ``centos-7.2.1511``: ``CentOS-7-x86_64-Minimal-1511.iso``
-  ``redhat-6.5``: ``RHEL6.5-20131111.0-Server-x86_64-DVD1.iso``
-  ``redhat-7.0``: ``rhel-server-7.0-x86_64-dvd.iso``
-  ``debian-7``: ``debian-7-mini-amd64.iso``
-  *NOTE* This is really the netboot mini.iso renamed. This can be found
   `here <http://ftp.nl.debian.org/debian/dists/wheezy/main/installer-amd64/current/images/netboot/mini.iso>`__
-  ``debian-8`` : ``debian-8-mini-amd64.iso``
-  *NOTE* This is really the netboot mini.iso renamed. This can be found
   `here <http://ftp.nl.debian.org/debian/dists/jessie/main/installer-amd64/current/images/netboot/mini.iso>`__
-  ``ESXi 6.0``:
   ``VMware-VMvisor-Installer-6.0.0.update02-3620759.x86_64.iso``

    This list is subject to change! For the latest list, consult
    `Provisioner Default Boot Environments
    <https://github.com/rackn/digitalrebar-deploy/tree/master/containers/provisioner/update-nodes/bootenvs>`__

To make these environments available after installation, see :ref:`ug_uc_base_os_bootenv`.

The boot environments and their required templates can also be updated programatically.
See :ref:`api_provisioner_bootenv` and :ref:`api_provisioner_template`.

