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
