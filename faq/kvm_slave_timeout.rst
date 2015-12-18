tools/kvm_slave timeout in TFTP
===============================

The tools/kvmslave script is very handy for local testing but may conflict with services running on your system.

The following commands may help resolve conflicts:

* ``sudo modprobe nf_nat_tftp``
