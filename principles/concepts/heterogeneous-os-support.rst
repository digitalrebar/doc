.. _heterogeneous_os_support:

Heterogeneous Operating System Support
=====================================

This section documents how to deploy multiple different operating systems
in Digital Rebar.

Deploying a heterogeneous OS cluster in Digital Rebar relies on
a few prerequisites:

-  *Online mode*: The provisioner must be configured to operate in online mode to deploy multiple different operating systems. This is needed to allow the operating systems to pick up all the packages they well need for a node installation.

-  *online\_mirror stanzas in the deployed provisioner proposal for all
   operating systems that are to be deployed*: These are needed so that the provisioner find the proper location to copy all the information needed to kick off a network-based installation of an operating system. The default proposal includes stanzas for the Ubuntu and CentOS operating system releases Digital Rebar supports.

-  *Proper recipe supoprt for the OS in the provisioner*: Right now we
   only include support for Ubuntu and CentOS. Adding Redhat support is
   trivial, and adding SuSE support is slightly less so.

Once the above prerequisites are met, the Digital Rebar ``provisioner``
command is able to query the list of available operating systems a node can install. It is also able to view and change the OS that the provisioner will deploy onto a node. The new
commands are:

-  rebar provisioner oses
-  rebar provisioner current\_os
-  rebar provisioner set\_os

These commands can be executed at any time, and the next time a node
transitions through the installing or reinstall states, it will have the
appropriate operating system installed.
