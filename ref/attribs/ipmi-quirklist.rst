==============
ipmi-quirklist
==============

Description
===========
List of interesting quirks to use when talking to IPMI controllers

Documentation
=============

IPMI controllers tend to have interesting and widely-spread bugs in their implementation.
ipmi-quirklist is a compilation of ones we have encountered in the wild.  Each
quirk represents a special-case that the ipmi-configure code must take into account
when configuring the IPMI controller to ensure that we wind up with an operational
and properly configured IPMI controller.  The quirks we have cataloged are as follows:

* "ipmi-nodelay" indicates that you do not have to sleep for a certain amount of
  time in between ipmitool invocations.  That this is a quirk instead of the default
  says volumes in and of itself about BMC firmware quality in general.
* "ipmi-dell-dedicated-nic" indicates that a Dell-specific ipmitool command should
  be used to flip the IPMI controller between using its own dedicated nic and piggybacking
  on the internal nics.
* "ipmi-crossed-access-channels" indicates that the channels used to configure the LAN
  controller are miswired, and that certian channel-control settings should be modified
  accrodingly.
* "ipmi-hard-reset-after-config" indicates that the IPMI controller must be hard
  reset after issuing configuration settings before the new settings are actually
  applied.
* "ipmi-immutable-rootname" indicates that the preconfigured admin user in slot 2
  cannot have its name changed.
* "ipmi-immutable-root" indicates that the preconifgured admin user in slot 2 cannot
  be changed at all, and we must create the user that Rebar will access the controller
  remotely with in slot 3 instead.
