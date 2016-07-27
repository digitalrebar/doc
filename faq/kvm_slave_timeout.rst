Tools/kvm_slave Causes a Timeout in TFTP?
=========================================

The tools/kvmslave script is very handy for local testing but may conflict with services running on the system.

For this to work, tell Digital Rebar to start the the provisioner container (``--provisioner``).

The following commands may help resolve conflicts:

* ``sudo modprobe nf_nat_tftp``
