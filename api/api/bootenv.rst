.. index::
  pair: Bootenv; API

.. _api_provisioner_bootenv:

Bootenv API
===========

Bootenv APIs are used to manage boot environments for nodes.  Bootenvs reference
:ref:`api_provisioner_template` objects.

This API is only available through the reverse proxy feature.

API Actions
-----------

+----------+-------------------------------------------+-------------------------------------+
| Verb     | URL                                       | Comments                            |
+==========+===========================================+=====================================+
| GET      | provisioner/bootenvs                      | List                                |
+----------+-------------------------------------------+-------------------------------------+
| GET      | provisioner/bootens/:name                 | Specific Item                       |
+----------+-------------------------------------------+-------------------------------------+
| PUT      | provisioner/bootenvs/:name                | Update Item                         |
+----------+-------------------------------------------+-------------------------------------+
| POST     | provisioner/bootenvs                      | Create Item                         |
+----------+-------------------------------------------+-------------------------------------+
| DELETE   | provisioner/bootenvs/:name                | Delete Item                         |
+----------+-------------------------------------------+-------------------------------------+


Bootenv Object
--------------

The general bootenv object defines an execution environment for nodes.  A boot environment is a network
boot context that can lead to an installation, or discovery-like image (default sledgehammer environment),
or diskless-boot environment.  The boot environment defines the set of files needed for the node to PXE
boot into this environment.

To support the widest range of boot methods, the boot environment should provide at least three
template objects.  These are the file content needed to start the boot process based upon the PXE
boot loader in use.  These files must in the form:

::

      {
        "Name": "pxelinux",
        "Path": "pxelinux.cfg/{{.Machine.HexAddress}}",
        "UUID": "default-pxelinux.tmpl"
      },
      {
        "Name": "elilo",
        "Path": "{{.Machine.HexAddress}}.conf",
        "UUID": "default-elilo.tmpl"
      },
      {
        "Name": "ipxe",
        "Path": "{{.Machine.Address}}.ipxe",
        "UUID": "default-ipxe.tmpl"
      },

Notice the three bootloader types, *pxelinux*, *ipxe*, and *elilo*.  For most linux-based network installs,
the default three listed above is sufficient.  The BootParams, Kernel, and Initirds are properly injected
to launch the kernel with initrds.  The BootParams string should be used to reference other templated
files needed for installation.

For example:

::

  "BootParams": "ksdevice=bootif ks={{.Machine.Url}}/compute.ks method={{.Env.OS.InstallUrl}} inst.geoloc=0",

This example shows that the *compute.ks* file is served from the ``.Machine.Url`` variable.  The .MachineUrl
variable is helper that presents an HTTP path to the node's template expansion directory on the provisioner.
The template list should include a file that called *compute.ks*.  The ``.Env.OS.InstallURL`` is a helper
variable that references the ISO installation directory created in the provisioner.  This directory presents
the reference ISO exploded from its ISO file into a live filesystem image.  The provisioner serves that directory
from the ``.Env.OS.InstallURL`` path.

For the install process to work correctly, the bootenv used to install an OS must end in ``-install``.
The roles used to install OSes uses the the ``-install`` form to limit choices in the UI and to ensure
proper workflow progress during the bring-up process.


+--------------------+-----------------+------------+------------------------------------------------+
| Attribute          | Type            | Settable   | Note                                           |
+====================+=================+============+================================================+
| BootParams         | Template String | Yes        | String expanded and available as variable      |
|                    |                 |            | .BootParams in templates. Often used to        |
|                    |                 |            | represent the boot parameters passed to the    |
|                    |                 |            | initial boot kernel.                           |
+--------------------+-----------------+------------+------------------------------------------------+
| Initrds            | List of Strings | Yes        | A list of initrd images that are relative to   |
|                    | or              |            | CD expansion directory.  Often used with the   |
|                    | null            |            | template helper .Env.JoinInitrds.              |
+--------------------+-----------------+------------+------------------------------------------------+
| Kernel             | String          | Yes        | The path to the kernel to initially boot.      |
|                    |                 |            | Referenced by .Env.Kernel and used with        |
|                    |                 |            | template helper .Env.PathFor.                  |
+--------------------+-----------------+------------+------------------------------------------------+
| Name               | String          | Yes        | Unique name for this boot environment          |
+--------------------+-----------------+------------+------------------------------------------------+
| OS                 | OS Object       | Yes        | An OS Object defining information about the    |
|                    |                 |            | OS to install                                  |
+--------------------+-----------------+------------+------------------------------------------------+
| RequiredParams     | List of Strings | Yes        | A list of attributes that the bootenv requires |
|                    |                 |            | to fill in templates. The node object is       |
|                    |                 |            | for these values and provided to all the       |
|                    |                 |            | templates during expansion.                    |
+--------------------+-----------------+------------+------------------------------------------------+
| Templates          | List of         | Yes        | A list of template objects that define the     |
|                    | Template        |            | set of files to render for this boot           |
|                    | Objects         |            | environment for each node.                     |
+--------------------+-----------------+------------+------------------------------------------------+


OS Object
---------

The OS Object define Operating System information used to populate the served install directory.

+--------------------+-----------------+------------+------------------------------------------------+
| Attribute          | Type            | Settable   | Note                                           |
+====================+=================+============+================================================+
| Name               | String          | Yes        | Name of OS - Usually BootEnv Name minus the    |
|                    |                 |            | *-install*.                                    |
+--------------------+-----------------+------------+------------------------------------------------+
| Family             | String          | Yes        | OS Family name - e.g, RedHat, Ubuntu           |
+--------------------+-----------------+------------+------------------------------------------------+
| Codename           | String          | Yes        | OS Codename - distro codename, e.g. trusty     |
+--------------------+-----------------+------------+------------------------------------------------+
| Version            | String          | Yes        | OS Version - distro version, e.g. 14.04        |
+--------------------+-----------------+------------+------------------------------------------------+
| IsoFile            | String          | Yes        | The name of the ISO in the isos directory.     |
+--------------------+-----------------+------------+------------------------------------------------+
| IsoSha256          | String          | Yes        | The SHA256 sum of the ISO to ensure viability  |
+--------------------+-----------------+------------+------------------------------------------------+
| IsoUrl             | String          | Yes        | The URL the ISO can be downloaded from         |
+--------------------+-----------------+------------+------------------------------------------------+
| Files              | null or list of | Yes        | A list of file objects to place in the install |
|                    | File Objects    |            | directory.  Used for static install files.     |
+--------------------+-----------------+------------+------------------------------------------------+


File Object
-----------

File objects define static files that be used to populate the install directory.  These are often
used when the isos are not complete or the install method is not ISO-based.  For example, CoreOS.

+--------------------+-----------------+------------+----------------------------------------------------+
| Attribute          | Type            | Settable   | Note                                               |
+====================+=================+============+====================================================+
| URL                | String          | Yes        | URL where to find the file                         |
+--------------------+-----------------+------------+----------------------------------------------------+
| Name               | String          | Yes        | Name of the file to place in the install directory |
+--------------------+-----------------+------------+----------------------------------------------------+
| ValidationURL      | String          | Yes        | Can be null. Location of checksum or signature     |
+--------------------+-----------------+------------+----------------------------------------------------+
| ValidationMethod   | String          | Yes        | Can be null, Method to use for validation.         |
+--------------------+-----------------+------------+----------------------------------------------------+

NOTE: Validation is not currently implemented in the provisioner.


Template Object
---------------

This object defines a reference to the template objects.  UUID is the template object id.

+--------------------+-----------------+------------+------------------------------------------------------+
| Attribute          | Type            | Settable   | Note                                                 |
+====================+=================+============+======================================================+
| UUID               | String          | Yes        | UUID of the :ref:`api_provisioner_template` Object   |
+--------------------+-----------------+------------+------------------------------------------------------+
| Path               | Template String | Yes        | String expanded and available as variable            |
+--------------------+-----------------+------------+------------------------------------------------------+
| Name               | String          | Yes        | Name of template inside this bootenv.                |
+--------------------+-----------------+------------+------------------------------------------------------+



Example Bootenv Object
----------------------

Here is an example JSON object.

::

  {
    "BootParams": "ksdevice=bootif ks={{.Machine.Url}}/compute.ks method={{.Env.OS.InstallUrl}} inst.geoloc=0",
    "Initrds": [
      "images/pxeboot/initrd.img"
    ],
    "Kernel": "images/pxeboot/vmlinuz",
    "Name": "centos-7.2.1511-install",
    "OS": {
      "Codename": "",
      "Family": "",
      "Files": null,
      "IsoFile": "CentOS-7-x86_64-Minimal-1511.iso",
      "IsoSha256": "f90e4d28fa377669b2db16cbcb451fcb9a89d2460e3645993e30e137ac37d284",
      "IsoUrl": "http://mirrors.kernel.org/centos/7.2.1511/isos/x86_64/CentOS-7-x86_64-Minimal-1511.iso",
      "Name": "centos-7.2.1511",
      "Version": ""
    },
    "RequiredParams": [
      "logging_servers",
      "ntp_servers",
      "operating-system-disk",
      "provisioner-default-password-hash",
      "proxy-servers",
      "rebar-access_keys",
      "rebar-machine_key"
    ],
    "Templates": [
      {
        "Name": "pxelinux",
        "Path": "pxelinux.cfg/{{.Machine.HexAddress}}",
        "UUID": "default-pxelinux.tmpl"
      },
      {
        "Name": "elilo",
        "Path": "{{.Machine.HexAddress}}.conf",
        "UUID": "default-elilo.tmpl"
      },
      {
        "Name": "ipxe",
        "Path": "{{.Machine.Address}}.ipxe",
        "UUID": "default-ipxe.tmpl"
      },
      {
        "Name": "compute.ks",
        "Path": "{{.Machine.Path}}/compute.ks",
        "UUID": "centos-7.ks.tmpl"
      },
      {
        "Name": "rebar_join.sh",
        "Path": "{{.Machine.Path}}/rebar_join.sh",
        "UUID": "rebar-join.sh.tmpl"
      }
    ]
  }



