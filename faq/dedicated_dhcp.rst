.. index::
	DHCP; Live Environment
	Live Environment; Dedicated DHCP

.. _faq_dedicated_dhcp:

Would a Live Environment Require a Dedicated DHCP?
==================================================

We provide an API driven DHCP service to handle our internal DHCP needs (`located here <https://github.com/rackn/rebar-dhcp>`_), and in order for Digital Rebar to manage bare metal, it is currently required.  Getting rid of that requirement is doable with some coding and testing.  The DHCP service is packaged in a Docker container that we automatically pull in if needed.
