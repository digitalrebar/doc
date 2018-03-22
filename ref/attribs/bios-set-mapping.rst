
.. note:: WARNING WARNING WARNING:  This is the Digital Rebar v2 product documentation.  That product line is EOL as of September 2017.  Please refer to the new Digital Rebar Provision v3 documentation:  http:\/\/provision.readthedocs.io\/en\/tip\/README.html

================
bios-set-mapping
================

Description
===========
Mapping of chassis manufacturers and product names to config sets

Documentation
=============

The bios-set-mapping attrib is responsible for providing all the information needed
to determine what low-level BIOS config system must be used for any given system,
as well as providing a reasonable set of default settings for the system.
It consists of an array of test objects with the following format::

  {
    "match": {
      "a-system-attrib": "value or regex to match"
      ...
      }
    "role": "low-level-bios-config-role-for-this-system"
    "configs": [
      {
        "name": "config-name"
        "parent": "config-this-inherits-settings-from"
        "settings": {
          "bios-setting": "desired-value"
          ...
        }
      }
    ]
  }

The stanzas of the test object have the following meanings:

* "match" in the test object contains an object whose keys
  are the name of Rebar attribs to test, and whose values are
  either regular expressions (if the value is /between slashes/)
  or the actual value the attrib must have.  If all the values
  in the match object match with the corresponding values for the
  attribs specified by the keys of the the match stanza,
  then the role and BIOS configs will be used for this system and no
  other tests will be looked at.
* "role" in the test object contains the low-level BIOS configuration
  role that will be bound to the node of the match stanza.
* "configs" contains an array of driver-specific BIOS configuration
  sets that should be used for this system.  This array must contain at least
  one entry named "default", which will serve as a basic configuration
  and upon which more task-specific configuration sets can be inherited from.

The stanzas of each specific BIOS config have the following meanings:

* "name" is the name of the configuration.  At least one of the
  configurations must be named "default"
* "parent" (if present) is the name of the BIOS configuration that this one
  will inherit settings from.  Any settings defined in this configuration
  will override settings from the parent.
* "settings" is an object whose keys are the names of discrete BIOS settings
  and whose values are what the settings should be set to.  The interpretation
  of the names and values is handled by the low-level BIOS configuration role, and
  is highly model and driver specific.

For Dell PowerEdge R series gear, you can use
``digitalrebar/tools/get-dell-poweredge-sample.rb`` to get the current BIOS
config settings we support from a running system.  For details on what those settings
mean, you should consult the support documentation for that system along with the
WSMAN documentation specific to the system from
http://en.community.dell.com/techcenter/systems-management/w/wiki/1906.dcim-library-profile

For SuperMicro gear, you can use
``digitalrebar/tools/get-supermicro-defaults.rb`` to get the BIOS default settings
from a running SuperMicro system.  For details on what those settings mean, you should
consult the documentation available for the system from SuperMicro along with the
SuperMicro Update Manager manual.
