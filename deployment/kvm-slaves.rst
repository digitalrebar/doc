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

There are some. Run the script and it will tell you! 

For reference, here are the current Ubuntu requirements:

- ``apt-get install qemu-kvm libvirt-bin ubuntu-vm-builder bridge-utils ruby1.9.1-dev make``
- ``gem install json net-http-digest_auth``

Start Up
^^^^^^^^

From the dev system, ``tools/kvm-slave``

This creates a KVM machine and attaches it to the Docker bridge.

Shutdown
~~~~~~~~

If you kill the pid of the kvm-slave, it will exit gracefully.

Common Usage
~~~~~~~~~~~~

Most of our kvm-slave usage looks like:

-  Create 3: ``for j in 1 2 3; do tools/kvm-slave & done``
-  Destroy 3: ``for j in 1 2 3; do kill %$j ; done``

