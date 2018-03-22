
.. note:: WARNING WARNING WARNING:  This is the Digital Rebar v2 product documentation.  The v2 version is EOL as of September 2017.  Please refer to the new Digital Rebar Provision v3 documentation:  http:\/\/provision.readthedocs.io\/en\/tip\/README.html

========================
firmware-target-versions
========================

Description
===========
A map of firmware test:version

Documentation
=============

Firmware Target Versions
------------------------

firmware-target-versions is a per-machine attrib that contains
a map of firmware-test -> version overrides, where firmware-test is the
name of a test field in the list of tests in the firmware-selection-tests
attrib.

This attrib allows you to pin firmware versions for a specific machine -- in the
absence of an entry for a firmware test in this attrib, the firmware-flash role
will try to flash up to the latest firmware update package available for a matching test.
