.. index::
  pair: Machine; API

.. _api_provisioner_machine:

Machine API
===========

Machine APIs are used to manage the boot environments of machines in the provisioner.

This API is only available through the reverse proxy feature.

This API is really only meant to be viewed or driven by the Digital Rebar core.  Use carefully.

API Actions
-----------

+----------+-------------------------------------------+-------------------------------------+
| Verb     | URL                                       | Comments                            |
+==========+===========================================+=====================================+
| GET      | provisioner/machines                      | List                                |
+----------+-------------------------------------------+-------------------------------------+
| GET      | provisioner/machines/:uuid                | Specific Item                       |
+----------+-------------------------------------------+-------------------------------------+
| PUT      | provisioner/machines/:uuid                | Update Item                         |
+----------+-------------------------------------------+-------------------------------------+
| POST     | provisioner/machines                      | Create Item                         |
+----------+-------------------------------------------+-------------------------------------+
| DELETE   | provisioner/machines/:uuid                | Delete Item                         |
+----------+-------------------------------------------+-------------------------------------+


Machine Object
--------------

+--------------------+-----------------+------------+------------------------------------------------+
| Attribute          | Type            | Settable   | Note                                           |
+====================+=================+============+================================================+
| UUID               |  String         | Yes        | UUID of node this entry references in Digital  |
|                    |                 |            | Rebar                                          |
+--------------------+-----------------+------------+------------------------------------------------+
| Name               | String          | Yes        | Name of node when this bootenv was set for     |
|                    |                 |            | node.                                          |
+--------------------+-----------------+------------+------------------------------------------------+
| Adderss            | String          | Yes        | Admin address of this node.                    |
+--------------------+-----------------+------------+------------------------------------------------+
| BootEnv            | String          | Yes        | Name of :ref:`api_provisioner_bootenv` object  |
|                    |                 |            | to apply to this node.                         |
+--------------------+-----------------+------------+------------------------------------------------+
| Params             | Map of Strings  | Yes        | The expanded required parameters from the      |
|                    |                 |            | :ref:`api_provisioner_bootenv` object at the   |
|                    |                 |            | time the bootenv was set for this node.        |
|                    |                 |            | The keys for the map are the                   |
|                    |                 |            | RequiredParameters from the bootenv.           |
+--------------------+-----------------+------------+------------------------------------------------+


Example Machine Object
----------------------

Here is an example JSON object.

::

  {
    "Address": "10.13.241.128",
    "BootEnv": "sledgehammer",
    "Name": "d78-e7-d1-24-08-8d.rackn.hpe.com",
    "Params": {
      "ntp_servers": [
        "10.13.241.2"
      ],
      "provisioner-online": true,
      "rebar-access_keys": {
        "admin-0": "ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDPDTneyYdj7yr12NF02W657DHbueI1YxKgxFQVdVwCCpM36/TojbRKV30HYBjzJEnRtWkQokUX69tUPE3piAOxM3VRMSBFRm3c5DfnkETMEvu2KF/NyzxtLl2pVggMah1GKre0+qjZsbiWie2TsIwRyF1mFF+T3Q/KlVrX0dnXpX/bi8IjyGYWt/GjTsxM/GL0MGHfN6y34/XpsDfpYOiL1Z/UDZ0kiWzBKUOFlgKiOfSCuQEgijpQqJZbLqmnVULN8EbPSbhCHQa9lkh58yFL2YFT9Tu8yBLlkSj2ebIgPYXXG8pOM/ZnMM0jaL0o4kzQ+YhnaVx8CUBnBeTXFhQT rebar@7955382b54b7\n",
        "greg": "ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDvqrpVfs9MXwjleLNPICcjAMviF3FJq85sMAe/4ejNDLMOcjDIFz4aQxrZx6sPlaqWADdy9XADaKgaYZwNssE9s6GNGJVORXl+vacLslwcrWo7aThzfKSlkn6wul3PcVjvIINQGiH/sUznLT8zUGR0hWX2Pds80iSxaQhIoFC8+DEVPSr5CIlliaCiYmwBB2FjBvR6ryltqxx3PIjJ4RwiP77DV6kdkG2khdY2XB7WLJptlgrg2U20TKG/9LrBqPFcM/m0BEmp01xN60A/O5Iw+vTXQoR3CX0mlNIzQIeAbtqau+uPkzd2TPzNOZebEvOnw1MxJPLjLqvxXRw54Bt9 galthaus@Gregs-MacBook-Pro.local\n",
        "setup-0": "ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQC8soZtPzTX0s6uR/57OJVnkYqPpTwOuRAjPnebGM0B7SEDeM+JbsmK27Ot76JhoIQrEOOUw3c3voMmyxk8WMmTU3Qp6JC6Mk61NKFx8MhzY0XCTsHtYcaupuCy77pNbioSiMK2q1s8spHSB/gHSbqBrOpNqJBBE6pqmsgJyYsk+dYPCGOvlElEVLYLptzUH1fbRoOqnTS4LI26prbhLrehlVHJVkqm4Qb/p3H+vodr1M6xt57ZTQt55xYyH122hdFUF5LlGkH3shZgyKVtNLrmC/IGZwhqSM3Y1Tx6rvLQIZM2oOyrSOQNsKwntTgItxj8tojFeN3Hofm0a2AFntGJ root@admin\n",
        "victor": "ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAII+xjdFlumg04ekNkjBO6h9FGYLKPc1tJHPtSyb/DKmN victor@m4700\n"
      },
      "rebar-machine_key": "machine-install:f86bff8f5e88fcf79bd4f3061013d67210426e83729e01df7cf9d5e8570b8c4e3f44d7c2fb87508c5b83eae5d8bd57fb5c07bda0cd6a6adc873a633f2ea3cad7"
    },
    "Uuid": "07104204-7d93-41d3-86e5-b14a5b8d2e37"
  }

