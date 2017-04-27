========================
firmware-selection-tests
========================

Description
===========
The list of selection tests that Rebar knows about to pick firmware to flash

Documentation
=============

Firmware Selection Tests
------------------------

The ``firmware-selection-tests`` attrib is used by the ``firmware-flash`` role to
determine what firmware update packages (as defined by the ``firmware-packages`` attrib)
should be applied to a given system.  It consists of a lists of tests with the
following structure:

A map of firmware type: version.
If an entry for a type is missing, the flasher will assume you want the latest version.
::
  {
    "test": "The name of the test."
    "current-version-script": "A shell script that gets the current version of the firmware in question."
    "packages" [
      {
        "package": "The name of the package in the firmware-packages attrib",
        "version": "The version of the package",
        "downgrade-fence": true or false,
        "upgrade-fence": true or false
      }
    ],
    "match": {
      "dmi_attrib": "value that must match",
      "other_dmi_attrib": "value that must match"
    }
  }

The packages section of the test structure can contain any number of packages that
can be flashed for the specific test.  The packages list must be ordered in ascending version
order with the earliest version at the top.

The keys of each individual entry in the packages list:

* "package" is the name of the package in the firmware-packages attrib.
  If there is no matching entry in the firmware-packages attrib and this
  package was chosen to be run, the update will fail.
* "version" is the version of the firmware update package.  The version string
  should be vaguely semver-ish.
* "downgrade-fence" indicates that the formware in question cannot be downgraded
  past this version.
* "upgrade-fence" indicates that this package must be flashed when upgrading to
  a later version.

The match section consists of an object whose keys are the names of node attribs, and
the values are the exact values that the attrib in question must match exactly.  These
are what determines if a given test is applicable to a given system.  The attrib names
must be in the following list:

* bios-vendor
* bios-version
* bios-revision
* system_manufacturer
* system_product
* baseboard_manufacturer
* baseboard_product_name
* ipmi-enable
* ipmi-firmware-rev
* ipmi-device-id
* ipmi-device-rev
* ipmi-mfgr-id
* ipmi-product-id
* raid-detected-controllers
