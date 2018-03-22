
.. note:: WARNING WARNING WARNING:  This is the Digital Rebar v2 product documentation.  That product line is EOL as of September 2017.  Please refer to the new Digital Rebar Provision v3 documentation:  http:\/\/provision.readthedocs.io\/en\/tip\/README.html

.. index::
	UEFI; Usage

.. _faq_using_uefi:

How do We Use UEFI?
===================

To start DHCP and PXE, the :ref:`arch_service_provisioner` using the ``--con-provisioner`` flag must be included.  If the ``tools/docker-admin`` dev process is being used, that flag is set automatically.