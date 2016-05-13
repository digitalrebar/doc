.. _install:

Digital Rebar Install
=====================

`TL;DR Quick Start <https://github.com/digitalrebar/doc/blob/master/deployment/install/quick.rst>`_ if you've got easy access to a Ubuntu system (AWS is perfect).

General Installation
--------------------

First, you need ``git`` to pull the deploy repo.  Usually something like:

* Ubuntu/Debian: `apt-get install git`
* CentOS/RedHat: `yum install git`.
* OS X already has it, but: https://git-scm.com/ just in case

By following the directory structure below, you are set for either production or development deployment.

::

  cd ~
  mkdir digitalrebar
  git clone https://github.com/rackn/digitalrebar-deploy digitalrebar/deploy
  ln -s digitalrebar/ digitalrebar/deploy/compose/digitalrebar
  cd digitalrebar/deploy
  echo "Checking prerequisites"
  ./run-in-system.sh --help
  echo "let's setup Digital Rebar!"

In human words, 

* Change to your home directory
* Make the digitalrebar directory
* Clone the digitalrebar-deploy tree from RackN as deploy in the digitalrebar directory  
* Create a symbolic link from the compose directory to the Digital Rebar top-level directory
* Change to the deploy directory
* Make sure other prerequisites are installed by showing the help for one of the scripts
* Cheerleading!

At this point, you are ready to use the deploy tools and scripts to build your admin node.

Specific Environments
---------------------

.. toctree::
  :maxdepth: 1
  :glob:

  *
