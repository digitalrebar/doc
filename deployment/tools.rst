.. _initial_install_setup:

Get Digital Rebar Deploy Tools
==============================

First,``git`` is required to pull the deploy repo.  Usually something like:

* Ubuntu/Debian: `apt-get install git`
* CentOS/RedHat: `yum install git`.
* OS X already has it, but: https://git-scm.com/ just in case

By following the directory structure below, either production or development deployment will be ready for use.  These
steps are needed for either bringing up an admin node directly or using ansible and ssh to bring up a remote admin node.
The choice of deploy tool options will determine where the admin node is brought up.

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

