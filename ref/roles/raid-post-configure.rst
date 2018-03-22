
.. note:: WARNING WARNING WARNING:  This is the Digital Rebar v2 product documentation.  That product line is EOL as of September 2017.  Please refer to the new Digital Rebar Provision v3 documentation:  http:\/\/provision.readthedocs.io\/en\/tip\/README.html

===================
raid-post-configure
===================

Description
===========
Update ohai data after the RAID volumes are configured.

Documentation
=============

After the RAID volumes have been created by the raid-configure role,
the ohai data stored for the OS visible disks will be out of date.
raid-post-conifgure is responsible for rerunning chef-client in order
to gather updated ohai data representing the current disk configuration
as seen by the OS.
