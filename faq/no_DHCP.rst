
.. note:: WARNING WARNING WARNING:  This is the Digital Rebar v2 product documentation.  The v2 version is EOL as of September 2017.  Please refer to the new Digital Rebar Provision v3 documentation:  http:\/\/provision.readthedocs.io\/en\/tip\/README.html

.. index::
	DHCP; Failed start

.. _faq_no_DHCP:

Why did Digital Rebar not start DHCP?
=====================================

The DHCP/PXE process is optional for Digital Rebar, thus it must be requested at system start to be functional. 

**Note**: At least one ISO must be provided for the provisioner to convert into install images.  The discovery images (aka Sledgehammer) is downloaded automatically by the provisioner.


