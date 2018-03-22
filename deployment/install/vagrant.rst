
.. note:: WARNING WARNING WARNING:  This is the Digital Rebar v2 product documentation.  The v2 version is EOL as of September 2017.  Please refer to the new Digital Rebar Provision v3 documentation:  http:\/\/provision.readthedocs.io\/en\/tip\/README.html

.. index::
  Vagrant

.. _vagrant:

Vagrant and  Digital Rebar
==========================

**Note**: While workable, this is not an advisable path for building an admin node!  It works very well adding local vm nodes to an existing admin node.  Unlike the ``kvm_slave`` approach, Vagrant bypasses the "bare metal" sledgehammer discovery process.

Vagrant File
------------

The `Vagrantfile <https://raw.githubusercontent.com/digitalrebar/digitalrebar/master/deploy/Vagrantfile>`_ is the only required file for these instructions, and the repo does not need to be cloned.

Save the file and run Vagrant from that location.

Prereqs
-------

* Vagrant installed (from `Vagrant Website <http://www.vagrantup.com/downloads.html>`_ not apt-get)
* Vagrant requires several other items:

  * Virtualbox (or similar) (e.g.: `sudo apt-get install virtualbox`)

  * The Vagrant install uses the :ref:`rebar_cli` for actions.  Therefore, it must be accessible from the Vagrant path.

  * The `vagrant-triggers <https://github.com/emyl/vagrant-triggers>`_ plugin is also required. (e.g. `vagrant plugin install vagrant-triggers`)

Admin Node
----------

The Docker tools can be used to directly bring up an :ref:`arch_other_systems`!

``vagrant up base``

Review the output to see the assigned IP address.

Workload Nodes
--------------

Workload nodes can be used without the admin node! If there is already han Admin node, define REBAR_ENDPOINT and the script will use that instead of the default above.

``vagrant up node1``

Numbers up to 20 are supported.

When a system is no longer needed, it can be destroyed by using `vagrant destroy`.
