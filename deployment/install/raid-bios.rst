.. index::
  pair: RAID; BIOS
  
 .. _raid:
 .. _bios:
 
 Providing RAID and BIOS Utilities
 =================================
 
 This step is _required_ to use the provisioner even if the utliities are not needed for the system in question.
 
 The locations and names in this document were updated December 2016.  Please check the RAID barclamp configuration file for the latest information: https://github.com/digitalrebar/digitalrebar/blob/master/core/barclamps/raid.yml
 
 Download the files as directed below, then copy the files to your host system under ``~/.cache/digitalrebar/tftpboot/file/raid``.  This will allow the files to managed by Digital Rebar.
 
 NOTE: This can be done AFTER installation.  Simply re-run the raid-tools-install role.
 
 Downloading the BIOS Utility
 -----------------------------
 
 Visit Broadcom looking for the SAS2IRCU_P20 utility at https://www.broadcom.com
 
 This link will search for it directly: https://www.broadcom.com/broadcom-search?q=8.07.14_megacli.zip
 
 You must accept the EULA to download this file (that is why it cannot be packaged into the install for you).
 
 
 Downloading the RAID Utility
 ----------------------------
 
 Visit Broadcom looking for the SAS2IRCU_P20 utility at https://www.broadcom.com
 
 This link will search for it directly: https://www.broadcom.com/broadcom-search?q=sas2ircu_p20.zip
 
 You must accept the EULA to download this file (that is why it cannot be packaged into the install for you).
 
