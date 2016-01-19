Digital Rebar Quick Start
=========================

For this quick start, we assume you'll ssh to the install server.  The goal is a temporary playground, not a long term install.  It is possible to install different operating systems and work by remote or fully automated, but we are keeping it very simple in this guide.

Once you have the server, it should take about 20 minutes in AWS or Packet.net to complete all steps.

Installation Steps:
-------------------

#. AWS Path:

   #. Create AWS t2.medium (or larger) Ubuntu instance with your SSH key.  
   #. Security Group access needs Port 22, 443, 3000 (rebar), 4646 (chef), 8301 (consul) and ICMP!  This our recommended base, depending on your application, you'll need additional ports open or may be able to Chef and Consul.
   #. Connect to the server: ``ssh ubuntu@[ip address]``

#. Packet or B-Y-O-Server Path:

   #. Create Packet Type 1 Ubuntu Server with your SSH key
   #. Make sure your policy gives access to ports 22, 443, 3000, 4646, 8301 and ICMP.
   #. Connect to the server: ``ssh root@[ip address]``

#. Save your system EXTERNAL IP address: ``export IPA=[CIDR]`` (`CIDR <https://en.wikipedia.org/wiki/Classless_Inter-Domain_Routing>`_ is the IP address with the /## subnet included)
#. Install Prereqs: ``sudo apt-get install git ansible jq -y``
#. Get the deployment code and test for pre-reqs
    
    ::
    
      cd ~
      mkdir digitalrebar
      git clone https://github.com/rackn/digitalrebar-deploy digitalrebar/deploy
      ln -s digitalrebar/ digitalrebar/deploy/compose/digitalrebar
      cd digitalrebar/deploy
      echo "Checking prerequisites"
      ./run-in-system.sh --help
      echo "let's setup Digital Rebar!"

#. Install to local system: ``./run-in-system.sh --deploy-admin=local --access=HOST --wl-docker-swarm --admin-ip=$IPA``

Add ``--wl-kubernetes`` or  other ``--wl-[workload]`` (see list from --help) if you'd like to play with other choices later.

This script ends with the Digital Rebar admin node fully operational but without any nodes.  You need to login to the Digital Rebar UI (default user/pass is ``rebar/rebar1``) for the next step.

Troubleshooting Tip:  You can see exactly what's going on using "Monitor...Annealer."  If there is an error, that view provides a ``Retry`` button that often resolves simple timing issues.

Let's Add Nodes!
----------------

To keep it simple, we're using cloud servers, not local vms or physical servers.  These are supported in a more complex setup.

#. From your client, you can log on to the system using ``https://[external ip address]:3000``.  Reminders: 

   #. Use External IP (same as the SSH address) with port 3000
   #. It's HTTPS, so you must accept the self-signed SSL certificate.
#. Add a AWS Provider from the "Nodes...Providers" menu:

   #. Add a provider using your AWS Credentials.
   #. optionally, you can also add GCE and Packet.net API Credentials
#. Add 2+ nodes from the "Nodes" menu:

   #. Add nodes from form at the top of the Nodes page.  The API has additional options.
   #. Detailed `Instructions here <../provider.rst>`_.

Remember to delete your nodes from the Nodes page before you take the system down!  There is no automatic cleanup.

Build a Docker Swarm Cluster
---------------------------

We are using a very basic Docker Swarm as a reference app for this quick install.

#. Select 2+ nodes for Docker Swarm using the "Deployments...Docker Swarm Wizard":
  
   #. Select one node as ``docker-swarm-manager`` using the checkboxes
   #. Select different node(s) as ``docker-swarm-member`` using the checkboxes
   #. "Create" the proposal for the cluster from the Wizard
#. "Commit" the porposal created by the Docker Swarm Wizard (Deployments...Docker Swarm page)
#. Watch Digital Rebar build your cluster!
#. Test using ``docker -H tcp://[ip of manager]:2475 info`` when it's done
