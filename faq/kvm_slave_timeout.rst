
.. note:: WARNING WARNING WARNING:  This is the Digital Rebar v2 product documentation.  The v2 version is EOL as of September 2017.  Please refer to the new Digital Rebar Provision v3 documentation:  http:\/\/provision.readthedocs.io\/en\/tip\/README.html

.. index::
	Tools; TFTP Timeout
	KMV Slave; TFTP Timeout
	TFTP; Timeout

.. _faq_tftp_timeout:

Tools/kvm_slave Causes a Timeout in TFTP?
=========================================

The tools/kvmslave script is very handy for local testing but may conflict with services running on the system.

For this to work, tell Digital Rebar to start the the provisioner container (``--provisioner``).

The following commands may help resolve conflicts:

* ``sudo modprobe nf_nat_tftp``
