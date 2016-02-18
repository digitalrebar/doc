Digital Rebar did not start DHCP
--------------------------------

The DHCP/PXE process is optional for Digital Rebar, you must as the system to start the Provisioner to get this functionality.

NOTE: You must also include at least one ISO for the provisioner to convert into install images.  The discovery images (aka Sledgehammer) is downloaded automatically by the provisioner.

How To Use UEFI:
----------------

To start DHCP and PXE, you need to include the Provisioner using the ``--con-provisioner`` flag.  If you are using the ``tools/docker-admin`` dev process then that flag is set automatically.
