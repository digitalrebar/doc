==============
ipmi-configure
==============

Description
===========
Allow Rebar to control the node via IPMI

Documentation
=============

ipmi-configure is responsible granting admin rights to the user that Rebar will
use to access the node.  It will reset the user in siot 2 (or 3 if the IPMI controller
has the ipmi-immutable-root quirk) to have the username and password specified
by the ipmi-username and ipmi-password attribs and give that user admin rights
when accessed over the lan.  It will also configure the LAN interface for the IPMI
controller if desired.
