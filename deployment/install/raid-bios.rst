
.. note:: WARNING WARNING WARNING:  This is the Digital Rebar v2 product documentation.  The v2 version is EOL as of September 2017.  Please refer to the new Digital Rebar Provision v3 documentation:  http:\/\/provision.readthedocs.io\/en\/tip\/README.html

.. index::
  RAID; BIOS
  
.. _raid_bios:
 
Providing RAID and BIOS Utilities
---------------------------------

This step is *required* to use the provisioner even if the utliities are not needed for the system in question.

The locations and names in this document were updated December 2016.  Please check the RAID barclamp configuration file for the latest information: https://github.com/digitalrebar/digitalrebar/blob/master/core/barclamps/raid.yml

Download the files as directed below, then copy the files to your host system under ``~/.cache/digitalrebar/tftpboot/files/raid``.  This will allow the files to managed by Digital Rebar.

**Note**: This can be done AFTER installation.  Simply re-run the raid-tools-install role.

Downloading the MegaCLI RAID Utility
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Visit Broadcom looking for the 8.07.14_MegaCLI.zip utility at https://www.broadcom.com

This link will search for it directly: https://www.broadcom.com//site-search?q=8.07.14_megacli.zip

Should resolve to this link: https://docs.broadcom.com/docs/12351587

**Note**: This file may be downloaded as ``8-07-14_MegaCLI.zip`` (note the dashes) and *must* be renamed as ``8.07.14_MegaCLI.zip``

You must accept the EULA to download this file (that is why it cannot be packaged into the install for you).


Downloading the SAS2IRCU RAID Utility
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Visit Broadcom looking for the SAS2IRCU_P20 utility at https://www.broadcom.com

This link will search for it directly: https://www.broadcom.com//site-search?q=sas2ircu_p20.zip

Should resolve to this link: https://docs.broadcom.com/docs/SAS2IRCU_P20.zip

You must accept the EULA to download this file (that is why it cannot be packaged into the install for you).

