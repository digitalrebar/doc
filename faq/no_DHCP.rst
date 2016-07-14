Digital Rebar did not start DHCP, Why?
======================================

The DHCP/PXE process is optional for Digital Rebar, it must be requested at system start to be functional. 

NOTE: At least one ISO must be provided for the provisioner to convert into install images.  The discovery images (aka Sledgehammer) is downloaded automatically by the provisioner.

How do We Use UEFI?
===================

To start DHCP and PXE,the Provisioner using the ``--con-provisioner`` flag must be included.  If the ``tools/docker-admin`` dev process is being used then that flag is set automatically.
