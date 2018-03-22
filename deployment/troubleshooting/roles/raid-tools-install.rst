
.. note:: WARNING WARNING WARNING:  This is the Digital Rebar v2 product documentation.  The v2 version is EOL as of September 2017.  Please refer to the new Digital Rebar Provision v3 documentation:  http:\/\/provision.readthedocs.io\/en\/tip\/README.html

raid-tools-install
==================

Cannot Find RAID/BIOS Utilities
-------------------------------

:typical log message: ``Cannot download 8.07.14_MegaCLI.zip`` or ``Cannot download SAS2IRCU_P20.zip``
:cause: Require utilities for RAID/BIOS configuration are missing.  These utilities are required even if they are not used for the specific node type.
:solution: Please follow directions on :ref:`raid_bios`
:note: Restart NOT required.  Simply add the missing files and retry the role.
