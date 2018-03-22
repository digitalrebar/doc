
.. note:: WARNING WARNING WARNING:  This is the Digital Rebar v2 product documentation.  That product line is EOL as of September 2017.  Please refer to the new Digital Rebar Provision v3 documentation:  http:\/\/provision.readthedocs.io\/en\/tip\/README.html

================
bios-sum-archive
================

Description
===========
The name of the SuperMicro Update Manager utility

Documentation
=============

In order for bios-supermicro-configure to function, Rebar needs to have an available
copy of SuperMicro Update Manager present.  We currently support running with
sum 1.6.0, which should be placed at ``digitalrebar/deploy/compose/config-dir/tools``
before starting the Rebar API container.
