Vagrant and  Digital Rebar
==========================

Note: While workable, this is not our suggested path for building an admin node!  It works very well adding local vm nodes to an existing admin node.  Unlike the ``kvm_slave`` approach, Vagrant bypasses the "bare metal" sledgehammer discovery process.

Prereqs
-------

The Vagrant install uses the `rebar cli <../cli/README.rst>`_ for actions.  It must be accessible from your Vagrant path.

You also need the ``vagrant-trigger`` plugin.

Admin Node
----------

We recommend using the Docker tools directly to bring up an Admin node!

``vagrant up base``

Workload Nodes
--------------

``vagrant up node1``

Numbers up to 20 are supported.

