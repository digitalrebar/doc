
.. note:: WARNING WARNING WARNING:  This is the Digital Rebar v2 product documentation.  The v2 version is EOL as of September 2017.  Please refer to the new Digital Rebar Provision v3 documentation:  http:\/\/provision.readthedocs.io\/en\/tip\/README.html

=================
firmware-packages
=================

Description
===========
The map of packages that Rebar knows how to flash

Documentation
=============

Firmware Package Information
----------------------------

The firmware-packages attrib contains all of the firmware packages that
Digital Rebar knows how to flash, regardless of system type.  It consists
of a JSON object that maps the full filename of the firmware update package
to metadata about that package.  The metadata is defined as follows:

::

  {
    "source": "The full URL the firmware update package should be downloaded from",
    "sha256sum": "The SHA256 checksum of the firmware update package",
    "script": "The script that will be invoked by the firmware-flash role to apply the firmware update"
  }

The firmware-flash role expects to be able to download the firmware
update package from the provisioner (at $provisioner/files/firmware/$package_name).
In order to make the update package available, you need to download the update
package from its source, and then upload it to the provisioner with:

* ``rebar provisioner files upload $downloaded_file as firmware/$package_name``

The script that applies the firmware update package should take care to reboot the system
if that is required to complete the firmware update.
