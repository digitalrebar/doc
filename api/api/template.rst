.. index::
  pair: Template; API

.. _api_provisioner_template:

Template API
============

Template APIs are used to manage templates for boot environments.  Templates are referenced by
:ref:`api_provisioner_bootenv` objects.

This API is only available through the reverse proxy feature.

API Actions
-----------

API Actions

+----------+-------------------------------------------+-------------------------------------+
| Verb     | URL                                       | Comments                            |
+==========+===========================================+=====================================+
| GET      | provisioner/templates                     | List                                |
+----------+-------------------------------------------+-------------------------------------+
| GET      | provisioner/templates/:uuid               | Specific Item                       |
+----------+-------------------------------------------+-------------------------------------+
| PUT      | provisioner/templates/:uuid               | Update Item                         |
+----------+-------------------------------------------+-------------------------------------+
| POST     | provisioner/templates                     | Create Item                         |
+----------+-------------------------------------------+-------------------------------------+
| DELETE   | provisioner/templates/:uuid               | Delete Item                         |
+----------+-------------------------------------------+-------------------------------------+


Template Object
---------------

+--------------------+-----------------+------------+------------------------------------------------+
| Attribute          | Type            | Settable   | Note                                           |
+====================+=================+============+================================================+
| Content            | Template String | Yes        | String expanded using the template variables.  |
|                    |                 |            | The content is stored in a file on the file    |
|                    |                 |            | system based upon the referencing bootenv.     |
+--------------------+-----------------+------------+------------------------------------------------+
| UUID               | String          | Yes        | This is the identifier for this template.      |
|                    |                 |            | It must be unique.                             |
+--------------------+-----------------+------------+------------------------------------------------+

Example Template Object
-----------------------

Here is an example JSON object.

::

  {
    "Contents": "DEFAULT {{.Env.Name}}\nPROMPT 0\nTIMEOUT 10\nLABEL {{.Env.Name}}\n  KERNEL {{.Env.PathFor \"tftp\" .Env.Kernel}}\n  INITRD {{.Env.JoinInitrds \"tftp\"}}\n  APPEND {{.BootParams}}\n  IPAPPEND 2",
    "UUID": "default-pxelinux.tmpl"
  }


Template Expansion Variables
----------------------------

The following variables are used for expansion within templates and the Bootenv variables,
BootParams and Template Paths.  These variables are referenced within an escape sequence pair.
{{ }} is the mark for evaluation.  This is the golang template format.  More information about
the syntax can be found `here <https://golang.org/pkg/text/template/>`_.

+---------------------+------------------------------------------------------------------+
| Variable            | Comment and Usage                                                |
+=====================+==================================================================+
| .ProvisionerURL     | The URL of the provisioner that managed machines should use for  | 
|                     | installation and management.                                     |
+---------------------+------------------------------------------------------------------+
| .RebarURL           | The URL of the Rebar API endpoint that managed machines should   |
|                     | talk to.                                                         |
+---------------------+------------------------------------------------------------------+
| .BootParams         | Returns processed boot parameters for the boot environment.      |
+---------------------+------------------------------------------------------------------+
| .Env.Name           | The name of the boot environment.                                |
+---------------------+------------------------------------------------------------------+
| .Env.Kernel         | Raw partial path to the kernel for the boot environment. It      |
|                     | should  be processed into the full path appropriate to the       |
|                     | boot protocol with .Env.PathFor                                  |
+---------------------+------------------------------------------------------------------+
| .Env.Initrds        | The list of raw partial paths for the initrds for the boot env.  |
|                     | These should not be used directly, instead use the               |
|                     | .Env.JoinInitrds method.                                         |
+---------------------+------------------------------------------------------------------+
| .Env.BootParams     | The template for the boot parameters for this boot env. This     |
|                     | should not be used directly, instead use the                     |
|                     | .BootParams method.                                              |
+---------------------+------------------------------------------------------------------+
| .Env.OS.Name        | The name of the OS that this boot env boots into.                |
+---------------------+------------------------------------------------------------------+
| .Env.OS.Family      | The family of OS that this boot env boots into.                  |
+---------------------+------------------------------------------------------------------+
| .Env.OS.Codename    | The codename of this OS, if any.                                 |
+---------------------+------------------------------------------------------------------+
| .Env.OS.Version     | The version of the OS, if any.                                   |
+---------------------+------------------------------------------------------------------+
| .Env.OS.IsoFile     | The name of the downloaded ISO file.                             |
+---------------------+------------------------------------------------------------------+
| .Env.OS.IsoSha256   | The SHA256 of the ISO.                                           |
+---------------------+------------------------------------------------------------------+
| .Env.OS.IsoUrl      | The URL that the ISO can be downloaded from, if applicable.      |
+---------------------+------------------------------------------------------------------+
| .Machine.Name       | The FQDN of the machine.                                         |
+---------------------+------------------------------------------------------------------+
| .Machine.Address    | The IPv4 address we expect the machine to PXE boot from.         |
+---------------------+------------------------------------------------------------------+
| .Machine.HexAddress | The IPv4 address of the machine in hexadecimal form, suitable    |
|                     | for PXE.                                                         |
| .Machine.BootEnv    | The boot environment the machine will boot with.                 |
+---------------------+------------------------------------------------------------------+
| .Machine.Params     | The rest of the parameters that should be used by the templates. |
+---------------------+------------------------------------------------------------------+
| .Machine.Path       | The path to the directory for this specific node on expansion.   | 
+---------------------+------------------------------------------------------------------+

