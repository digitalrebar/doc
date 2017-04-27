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
