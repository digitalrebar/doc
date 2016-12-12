.. index::
  pair: Deploy Tools; Install

.. _initial_install_setup:

Get Digital Rebar Deploy Tools
==============================

First, git is required to pull the deploy repository.  To install git, use one of the following:

* Ubuntu/Debian: ``sudo apt-get install git``.
* CentOS/RedHat: ``yum install git``.
* OS X should already have git.
* Otherwise, see https://git-scm.com/ to download the proper version.

Next, by following the directory structure below, either production or development deployment will be ready for use.  These
steps are necessary to either bring up an admin node directly or use ansible and ssh to bring up a remote admin node.
The choice of deployment tool options will determine where the admin node is brought up.

::

  cd ~
  git clone https://github.com/digitalrebar/digitalrebar
  cd digitalrebar/deploy
  echo "Checking prerequisites"
  ./run-in-system.sh --help
  echo "let's setup Digital Rebar!"

The directory completes the following steps:

* Change to the home directory
* Make the digitalrebar directory
* Clone the digitalrebar-deploy tree from RackN as deploy in the digitalrebar directory
* Create a symbolic link from the compose directory to the Digital Rebar top-level directory
* Change to the deploy directory
* Make sure other prerequisites are installed by showing the help for one of the scripts

  * This will make sure that ``curl``, ``jq``, and ``ansible`` are avaialbe.
  * This will make sure that a ssh public/private key pair is available for this user.
  * Future invocations may add aws or google tools and unzip.

* Cheerleading!

At this point, the initial configuration of the admin node can be modified, or
the deploy tools and scripts can build an admin node.
