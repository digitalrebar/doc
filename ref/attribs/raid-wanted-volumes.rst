
.. note:: WARNING WARNING WARNING:  This is the Digital Rebar v2 product documentation.  The v2 version is EOL as of September 2017.  Please refer to the new Digital Rebar Provision v3 documentation:  http:\/\/provision.readthedocs.io\/en\/tip\/README.html

===================
raid-wanted-volumes
===================

Description
===========
How RAID shold be configured on this node.

Documentation
=============

Describing RAID Volumes to Create
=================================

To have Digital Rebar create RAID volumes other than the default (a
single JBOD for the OS volume), you need to ensure that the
``raid-wanted-volumes`` attrib is configured for the system (either
directly on the system or via a profile that is bound to the system).

raid-wanted-volumes contains a list of desired RAID arrays for a given
system.  This list contains a series of JSON objects in the following
format:

::

  {
    "name": "name of the volume",
    "raid_level": "target raid level",
    "size": "min" or "max" or available size in bytes of the volume,
    "disks": number of physical disks to use in the array,
    "exclusive": true or false,
    "disk_type": nil or "ssd" or "disk",
    "protocol": nil or "sas" or "sata",
    "force_good": true or false,
    "controller_id": "The ID of the controller from the raid-detected-controllers attrib"
  }

To actually build the RAID volume, the underlying physical disks
are bucketized according to the following rules:

  1. If the ``exclusive`` flag is set, then physical disks that
     already have a volume on them are ignored by the rest of the
     bucketization rules.
  2. Sort the physical disks into 4 top level buckets based on their
     disk_type and protocol
  3. In each bucket created above, subdivide the disks it has into
     size-buckets based on the amount of free space each has in 32
     gigabyte increments.

If the size is neither "min" nor "max", calculate the per-disk size
requirement based on the raid_level and the requested final size of
the array.

Walk over the top-level buckets in the following order:

  1. disk/sas
  2. disk/sata
  3. ssd/sas
  4. ssd/sata

* If the desired RAID array has disk_type or protocol set, then top
  level buckets that do not match the set values are ignored.

* If the size is "min", look at the size-buckets in ascending order, and pick the
  first one that can satisfy the volume creation request.

* If the size is "max", look at the size-buckets in descending order,
  and pick the first one that can satisfy the volume creation request.

* Otherwise, look at the size-buckets in ascending order starting with
  the smallest one that satisfies the per-disk dize requirements, and
  pick the first one that can satisfy the volume creation request.

* If a size-bucket was found that can satisfy the volume creation
  request, grab the number of required disks (sorted by the underlying
  RAID controllers notion of the disk ID in ascending order) from the
  bucket and create volume, forcing the individual disks to be "good"
  if force_good is set.  Otherwise move on to the next applicable
  top-level bucket and try again.
