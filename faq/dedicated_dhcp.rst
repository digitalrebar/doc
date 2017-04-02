.. index::
	DHCP; Live Environment
	Live Environment; Dedicated DHCP

.. _faq_dedicated_dhcp:

Would a Live Environment Require a Dedicated DHCP?
==================================================

We provide an API driven DHCP service to handle our internal DHCP needs (`located here <https://github.com/rackn/rebar-dhcp>`_); however, it is NOT required Digital Rebar to manage bare metal.

To use an external DHCP server, you will need to configure that server to next boot to the Digital Rebar Provisioner infrastructure.  Digital Rebar DHCP will not "lead" UDP unless you've configured it to answer requests.

The DHCP service is packaged in a Docker container that we automatically pull in if needed.
