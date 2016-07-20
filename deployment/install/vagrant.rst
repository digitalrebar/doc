Vagrant and  Digital Rebar
==========================

Note: While workable, this is an inadviasble path for building an admin node!  It works very well adding local vm nodes to an existing admin node.  Unlike the ``kvm_slave`` approach, Vagrant bypasses the "bare metal" sledgehammer discovery process.
        
Vagrant File
------------

The `Vagrant file <https://raw.githubusercontent.com/rackn/digitalrebar-deploy/master/Vagrantfile>`_ is the only required file for these instructions, and the repo does not need to be cloned.  

Save the file and run Vagrant from that location.

Prereqs
-------

  * Vagrant installed (from `Vagrant Website <http://www.vagrantup.com/downloads.html>`_ not apt-get)
  * Vagrant requires several other items:
  
     * Virtualbox (or similar) (e.g.: `sudo apt-get install virtualbox`)

  * The Vagrant install uses the `rebar cli <../cli/README.rst>`_ for actions.  Therefore, it must be accessible from the Vagrant path.
    * The ``vagrant-trigger`` plugin is also required.

Admin Node
----------

The Docker tools can be used to directly bring up an Admin node!

``vagrant up base``

Review the output to see the assigned IP address.

Workload Nodes
--------------

Workload nodes can be used without the admin node! If there is already han Admin node, define REBAR_ENDPOINT and the script will use that instead of the default above.

``vagrant up node1``

Numbers up to 20 are supported.

When a system is no loger needed, it can be destroyed by using `vagrant destroy`.
