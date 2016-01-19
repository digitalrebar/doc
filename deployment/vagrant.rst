Vagrant and  Digital Rebar
==========================

Note: While workable, this is not our suggested path for building an admin node!  It works very well adding local vm nodes to an existing admin node.  Unlike the ``kvm_slave`` approach, Vagrant bypasses the "bare metal" sledgehammer discovery process.

Vagrant File
------------

You only need the `Vagrant file <https://raw.githubusercontent.com/rackn/digitalrebar-deploy/master/Vagrantfile>`_ for these instructions.  You do not need to clone the repo.

Save the file and run Vagrant from that location.

Prereqs
-------

  * Vagrant installed (from [Vagrant website](http://www.vagrantup.com/downloads.html) not apt-get)
  * Vagrant requires several other items:
  
     * Virtualbox (or similar) (e.g.: `sudo apt-get install virtualbox`)
  * The Vagrant install uses the `rebar cli <../cli/README.rst>`_ for actions.  It must be accessible from your Vagrant path.
   * You also need the ``vagrant-trigger`` plugin.

Admin Node
----------

We recommend using the Docker tools directly to bring up an Admin node!

``vagrant up base``

Review the output to see the assigned IP address.

Workload Nodes
--------------

You can use this type without the admin node! If you already have an Admin node, define REBAR_ENDPOINT and the script will use that instead of the default above.

``vagrant up node1``

Numbers up to 20 are supported.

### Cleanup 

When finished, you can destroy the system using `vagrant destroy`

