
.. note:: WARNING WARNING WARNING:  This is the Digital Rebar v2 product documentation.  The v2 version is EOL as of September 2017.  Please refer to the new Digital Rebar Provision v3 documentation:  http:\/\/provision.readthedocs.io\/en\/tip\/README.html

=============
bios-discover
=============

Description
===========
Discover information about the BIOS

Documentation
=============

bios-discover is responsible for figuring out what low-level configuration
method (if any) should be used to manipulate BIOS settings on a node, and select
a reasonable default configuration for the system BIOS.

The BIOS subsystem knows how to configure BIOS settings for two system types:

* Dell PowerEdge R gear (12th gen and up) via direct interaction with WSMAN on the iDRAC.
  Systems using this method will have the bios-dell-rseries-configure role bound
  to them by the bios-discover role.
* SuperMicro gear via SuperMicro Update Manager via the IPMI controller.  Systems
  using this method will have the bios-supermicro-configure role bound to them
  by the bios-discover role.

The bios-discover role works by scanning the default BIOS configurations
provided by the bios-set-mapping attrib to find out if a matching BIOS config set is defined.
If one is, the appropriate low-level bios conifg role is bound to the node, and the
bios-config-sets attrib is set to the matched BIOS config set.

If no matching BIOS config sets are found, then the bios-discover role succeeds without
doing anything.
