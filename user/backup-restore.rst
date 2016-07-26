.. index::
  pair: System; Backup and Restore

.. _backup_restore:

Backup and Restore
------------------

Digital Rebar functions as a group of services wrapped in containers.  The state for those containers is stored external to those containers.  That allows operators to stop, remove, and restart the containers without losing data.

To provide a more durable and portable backup, the RackN team has written a `backup.sh` script that exports that database, consul and other key components.  This script must be run while system is running (Rebar_API).

To make a backup, simply run the `./backup.sh` script from the ./deploy directory.

To restore the backup, use the matching `./restore.sh` script in the same directory.

The output of the backup should be stored on a different system than the Digital Rebar admin.
