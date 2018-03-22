
.. note:: WARNING WARNING WARNING:  This is the Digital Rebar v2 product documentation.  The v2 version is EOL as of September 2017.  Please refer to the new Digital Rebar Provision v3 documentation:  http:\/\/provision.readthedocs.io\/en\/tip\/README.html

.. _kvm_worker_nodes:

KVM Worker Nodes
----------------

Digital Rebar developers are *strongly* encouraged to always build and test
deployment code in multi-node situations.

Using kvm-slaves with *kvm-slaves* script
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Closing the KVM window will *not* stop the VM because the scripts
are designed to restart the VM if it halts.

Prereqs
^^^^^^^

There are some requirements; run the script and it will explain what is required! 

For reference, here are the current Ubuntu requirements:

- ``apt-get install qemu-kvm libvirt-bin ubuntu-vm-builder bridge-utils ruby-dev make``
- ``gem install json net-http-digest_auth``

You MUST be running the provisioner for this to work!

If you want to reach the VMs from your host, you should map the host IP to the docker bridge using ``sudo ip a add 192.168.124.4/24 dev docker0``

Start Up
^^^^^^^^

If you've already done this process, you need to cleanup PXE registration from the previous run using ``tools/kvm-slave``.

From the dev system and the core repo, ``tools/kvm-slave``

This creates a KVM machine and attaches it to the Docker bridge.

Shutdown
~~~~~~~~

If the pid of the kvm-slave is killed, it will exit gracefully.

Common Usage
~~~~~~~~~~~~

Most kvm-slave usage looks like:

-  Release PXE files: ``tools/kvm-release``
-  Create 3: ``for j in 1 2 3; do tools/kvm-slave & done``
-  Destroy 3: ``for j in 1 2 3; do kill %$j ; done``

