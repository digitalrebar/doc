.. _quick_start:

Digital Rebar Quick Start
=========================

This TL;DR only! See :ref:`install` for more options.

For this quick start, we assume ssh access to the install server.  The goal is a temporary playground, not a long term install.  It is possible to install different operating systems and work by remote or fully automated, but we are keeping it very simple in this guide.

Once the server is avalible, it should take about 20 minutes in AWS or Packet.net to complete all steps.

Base Installation (10 mins)
---------------------------

#. AWS Path:

   #. Create AWS m4.large (or larger!) Ubuntu instance with the SSH key.  
   #. The "default" Security Group needs Port 22 (ssh), 443 & 3000 (rebar), 2375 & 2475 (docker), 4646 (chef), 8300 & 8301 (consul), 8888 (certificate signing service) and ICMP!  This our recommended base; depending on the application, additional ports might be required or Docker, Chef and Consul may be omitted.
   #. Connect to the server: ``ssh ubuntu@[ip address]``

#. Packet or B-Y-O-Server Path:

   #. Create Packet Type 1 Ubuntu Server with the SSH key (8 Gb RAM minimum)
   #. Make sure ports 22, 443, 3000, 2375, 2475, 4646, 8300, 8301, 8888, and ICMP are avlible through the enacted policy.
   #. Connect to the server: ``ssh root@[ip address]``

#. Save the used system's EXTERNAL IP address: ``export IPA=[CIDR]`` (`CIDR <https://en.wikipedia.org/wiki/Classless_Inter-Domain_Routing>`_ is the IP address with the /## subnet included)

   Note: For local installs use ``ip -4 addr`` to find the CIDR, or use the external IP given by the server provider. 

#. Install Prereqs: ``sudo apt-get update && sudo apt-get install git python python-pymongo python-pycurl -y``
#. Get the deployment code and test for pre-reqs
    
    ::
    
      cd ~
      mkdir digitalrebar
      git clone https://github.com/rackn/digitalrebar-deploy digitalrebar/deploy
      ln -s ~/digitalrebar/ digitalrebar/deploy/compose/digitalrebar
      cd digitalrebar/deploy
      echo "Checking prerequisites"
      ./run-in-system.sh --help
      echo "let's set up Digital Rebar!"

#. Install to local system: ``./run-in-system.sh --deploy-admin=local --access=HOST --wl-docker-swarm --admin-ip=$IPA``  (notes: it's OK to retry this script and IP must include /## for CIDR)

Add ``--wl-kubernetes`` or  other ``--wl-[workload]`` (see list from --help) if other choices are intended for examination.
This script ends with the Digital Rebar admin node fully operational but without any nodes.  For the next step, login to the Digital Rebar UI (default user/pass is ``rebar/rebar1``).

Troubleshooting Tip:  "Monitor...Annealer" provides a view of exactly what is going on.  If there is an error, that view provides a ``Retry`` button that often resolves simple timing issues.

Let's Add Nodes!
----------------

In order to maintain simplicity, we use cloud servers, not local vms or physical servers.  These are supported in a more complex setup.

#. From the client, it is possible to log on to the system using ``https://[external ip address]:3000``.  Reminders: 

   #. Use External IP (same as the SSH address) with port 3000
   #. It's HTTPS, so accepting the self-signed SSL certificate is required.
#. Add a AWS Provider from the "Nodes...Providers" menu:

   #. Add a provider using tye AWS Credentials.  Choose the same region as the admin is using.
#. Add 2+ nodes from the "Nodes" menu:

   #. Add nodes from form at the top of the Nodes page.  The API has additional options.
   #. Recommended: For Swarm in AWS, the "default_os" should be sufficient.  It loads Ubuntu 14.014 and is `mapped in many AWS regions. <https://github.com/rackn/digitalrebar-deploy/blob/master/containers/cloudwrap/cloudwrap/api.rb#L110>`_
   
   #.  Use of the single specific Centos7 is avalible in Google with ``projects/centos-cloud/global/images/centos-7-v20151104``.
   #. Other clouds or images, it is possible to override default_os based on `provider o/s map <https://github.com/rackn/digitalrebar-deploy/blob/master/workloads/os.map>`_  For example: Centos 7 AMI UUID for us-west-2 is ami-d440a6e7.
   #. Detailed `Instructions here <../provider.rst>`_.
#. Allow the system to complete annealing (progress in top right corner)

Remember to delete used nodes from the Nodes page before taking the system down!  There is no automatic cleanup.

Build a Docker Swarm Cluster
----------------------------

We are using a very basic Docker Swarm as a reference app for this quick install.

#. Select 2+ nodes for Docker Swarm using the "Deployments...Docker Swarm Wizard":
  
   #. Select one node as ``docker-swarm-manager`` using the checkboxes. This node is the manager for step 4 below.
   #. Select different node(s) as ``docker-swarm-member`` using the checkboxes
   #. "Create" the proposal for the cluster from the Wizard
#. "Commit" the porposal created by the Docker Swarm Wizard (Deployments...Docker Swarm page)
#. Watch Digital Rebar build the cluster!
#. Test using ``docker -H tcp://[ip of manager]:2475 info`` when it's done: 

   #. Get the IP of the manager from Nodes...Nodes and looking for the address of the node that is assigned as the docker-swarm-manager in step 1i.
   #. Advanced users may try ``docker -H tcp://[ip of manager]:2475 run -it ubuntu:latest bash`` to start a container
