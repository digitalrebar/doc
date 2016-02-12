Dedicated DHCP?
===============

Q: would a live environment, given that it handles DHCP itself require a dedicated instance for DHCP?

We provide an API driven DHCP service to handle our internal DHCP needs (at https://github.com/rackn/rebar-dhcp, if you are interested), and in order for Digital Rebar to manage bare metal it is currently required.  Getting rid of that requirement is doable with some coding and testing.  The DHCP service is packaged in a Docker container that we automatically pull in if needed.
