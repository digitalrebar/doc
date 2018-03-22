
.. note:: WARNING WARNING WARNING:  This is the Digital Rebar v2 product documentation.  The v2 version is EOL as of September 2017.  Please refer to the new Digital Rebar Provision v3 documentation:  http:\/\/provision.readthedocs.io\/en\/tip\/README.html

=========================
raid-detected-controllers
=========================

Description
===========
The RAID controllers that were detected on this node.

Documentation
=============

The raid-detected-controllers attrib holds information on all of the
hardware raid controllers Rebar is able to manage on a node.  It consists
of a list of objects that describe the detected information for each controller.

A sample is below::

  [
    {
      "bus": 8,
      "device": 0,
      "device_id": "005b",
      "driver_name": "megacli",
      "firmware_package": "21.3.2-0005",
      "firmware_version": "3.131.05-4520",
      "function": 0,
      "id": "0",
      "native_jbod": false,
      "product_name": "PERC H710 Adapter",
      "raid_capable": true,
      "serial_number": "45D00BX",
      "sub_device_id": "1f35",
      "sub_vendor_id": "1028",
      "supported_raid_levels": [
        "raid0",
        "raid1",
        "raid5",
        "raid6",
        "raid10",
        "raid50",
        "raid60",
        "jbod"
      ],
      "vendor_id": "1000",
      "disks": [
        {
          "controller_id": "0",
          "disk_size": 4.99558383616e+11,
          "driver_name": "megacli",
          "enclosure": "",
          "media_type": "disk",
          "protocol": "sata",
          "sas_address": "0x4433221107000000",
          "slot": "0",
          "status": "Online, Spun Up"
        },
        {
          "controller_id": "0",
          "disk_size": 4.99558383616e+11,
          "driver_name": "megacli",
          "enclosure": "",
          "media_type": "disk",
          "protocol": "sata",
          "sas_address": "0x4433221106000000",
          "slot": "1",
          "status": "Online, Spun Up"
        },
        {
          "controller_id": "0",
          "disk_size": 4.99558383616e+11,
          "driver_name": "megacli",
          "enclosure": "",
          "media_type": "disk",
          "protocol": "sata",
          "sas_address": "0x4433221105000000",
          "slot": "2",
          "status": "Online, Spun Up"
        },
        {
          "controller_id": "0",
          "disk_size": 4.99558383616e+11,
          "driver_name": "megacli",
          "enclosure": "",
          "media_type": "disk",
          "protocol": "sata",
          "sas_address": "0x4433221104000000",
          "slot": "3",
          "status": "Online, Spun Up"
        }
      ],
      "volumes": [
        {
          "controller_id": "0",
          "driver_name": "megacli",
          "id": "0",
          "name": "os",
          "raid_level": "raid10",
          "span_length": 2,
          "spans": 2,
          "status": "Optimal",
          "stripe_size": 65536,
          "vol_size": 9.99116767232e+11
          "disks": [
            {
              "controller_id": "0",
              "disk_size": 4.99558383616e+11,
              "driver_name": "megacli",
              "enclosure": "",
              "media_type": "disk",
              "protocol": "sata",
              "sas_address": "0x4433221107000000",
              "slot": "0",
              "status": "Online, Spun Up"
            },
            {
              "controller_id": "0",
              "disk_size": 4.99558383616e+11,
              "driver_name": "megacli",
              "enclosure": "",
              "media_type": "disk",
              "protocol": "sata",
              "sas_address": "0x4433221106000000",
              "slot": "1",
              "status": "Online, Spun Up"
            },
            {
              "controller_id": "0",
              "disk_size": 4.99558383616e+11,
              "driver_name": "megacli",
              "enclosure": "",
              "media_type": "disk",
              "protocol": "sata",
              "sas_address": "0x4433221105000000",
              "slot": "2",
              "status": "Online, Spun Up"
            },
            {
              "controller_id": "0",
              "disk_size": 4.99558383616e+11,
              "driver_name": "megacli",
              "enclosure": "",
              "media_type": "disk",
              "protocol": "sata",
              "sas_address": "0x4433221104000000",
              "slot": "3",
              "status": "Online, Spun Up"
            }
          ]
        }
      ]
    }
  ]
