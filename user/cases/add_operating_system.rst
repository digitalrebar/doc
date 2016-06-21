.. _ug_uc_os_bootenv:

OS Install Boot Environments
----------------------------

The following describes some actions that can be taken on provisioner boot environments.  While these 
section talk about operating system install boot environments, a boot environment can be any execution
context for the node.  Installation can be a by-product of a boot environment, but it doesn't have to.

.. _ug_uc_base_os_bootenv:

Supported Base Boot Environments
================================

The default set of ISOs can be found in :ref:`dg_add_os`.  Adding a default ISO can be accomplished by:

.. index::
  Boot Environment; Base
  OS Install; Base

#. Add iso to tftpboot/isos directory, usually on the admin node in */root/.cache/digitalrebar/tftpboot/isos*.
#. Restart the provisioner container

  On the admin node as root, run:

  ::

    cd /root/digitalrebar/deploy/compose
    DR_TAG=latest docker-compose restart provisioner


.. _ug_uc_add_os_bootenv:

Adding OS Install Environment
=============================

.. index::
  Boot Environment; Add
  OS Install; Add

Adding an operating system to Digital Rebar requires creating a boot environment.
The boot environment lives in the provisioner.  The node's can be configured to target
the boot environment to install the OS or whatever function the boot environment provides.
The boot environment must provide a network boot that installs the OS or other tooling and 
then sets the next boot environment to localboot upon completion. 
See :ref:`api_provisioner_bootenv` and :ref:`api_provisioner_template`.

#. Add iso to tftpboot/isos directory, usually on the admin node in */root/.cache/digitalrebar/tftpboot/isos*.
#. Create install templates for new OS (or reuse)
#. Create install bootenv for new OS
#. Upload templates to provisioner
#. Upload bootenv to provisioner

The main requirement for an OS install environment is that a post-install step needs to set the next
bootenv environment on the node to ``local``.  An example post-install can be found in the
`CentOS 7 Kickstart Template <https://github.com/rackn/digitalrebar-deploy/blob/master/containers/provisioner/update-nodes/templates/centos-7.ks.tmpl>`__.  Once all steps are complete, the node should reboot to the next
environment.

Once the boot environment is available, add the ``rebar-installed-node`` role to the node.
This will add the ``provisioner-os-install`` node role to the node.  The attrib ``provisioner-target-os``
will have been added to the node.  This attrib can be changed to the newly added environment.  
Once the deployment or node is committed, the node will progress through that boot environment.
The :ref:`ug_uc_edit_bootenv` section will describe how to iterate to a successful install.


.. _ug_uc_edit_bootenv:

Editing OS Install Boot Environment
===================================

.. index::
  Boot Environment; Edit
  OS Install; Edit

TODO: Describe how to edit ks and preseed for file system environments.

This describes making a copy of the existing bootenv for custom needs.

#. Get templates and bootenv to update.
#. Edit templates for need - changing names.
#. Edit bootenv to change name and template refs.
#. Add templates
#. Add bootenv
#. Use new env
#. If errors, edit templates and bootenv.
#. Update templates and bootenv.
#. Retry - if errors iterate.


