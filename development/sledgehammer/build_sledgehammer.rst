.. _sledge_build:

Build Sledgehammer (Advanced Dev Only)
======================================

Sledgehammer is the component of Digital Rebar that is used as a
bootstrapping tool to perform initial node discovery and register its
discovered state within the Digital Rebar node provisioning framework.
After it has been discovered, Sledehammer can be controlled to prepare
the hardware, lay down the operating system, and assure correct
node configuration.  It consists of a slightly modified Centos 7 live
environment.

By default, setup will now download golden sledgehammers and this step
is not needed.

Only do this step if changes are required for Sledgehammer! We
recommend using the golden sledgehammer.

#. prep for sledgehammer requirements:

   #. ubuntu: ``sudo apt-get install curl rpm rpm2cpio``

#. from core, ``tools/build_sledgehammer.sh``

   #. warning: this may take multiple attempts to complete to downloads.
      Keep trying.
   #. warning: might need a better literal mirror in
      sledgehammer/sledgehammer.ks - see below.

WARNING: Option step! Usually requires multiple retries.


Failures
~~~~~~~~

If it fails to find some packages, change the mirror kickstart is using
in ``sledgehammer\sledgehammer.ks``

List of mirrors `here <http://isoredirect.centos.org/centos/7/isos/x86_64/>`_

