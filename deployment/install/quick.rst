.. _quick_start:

Digital Rebar Quick Start
=========================

This TL;DR only! See :ref:`install` for more options.

For this quick start, we assume ssh access to the install server.  The goal is a temporary playground, not a long term install.  It is possible to install different operating systems and work by remote or fully automated, but we are keeping it very simple in this guide.

Once the server is avalible, it should take about 20 minutes in AWS or Packet.net to complete all steps.

Base Installation (10 mins)
---------------------------

#. Choose the Required Path

-AWS Path:

   #. Create AWS m4.large (or larger!) Ubuntu instance. This can be done with the SSH key or by following the following steps:
      
      #. Login to AWS and click on EC2 under Compute.
      #. Click on Launch Instance. This will begin the instance set up.
      #. Select Ubuntu Server for the AMI, then select `m4.large` or larger. 
      #. Next, navigate to the Configure Security Group tab.  The "default" Security Group for this server needs Port 22 (ssh), 443 & 3000 (rebar), 2375 & 2475 (docker), 4646 (chef), 8300 & 8301 (consul), 8888 (certificate signing service) and ICMP!  This is just our recommended base. Depending on the application, additional ports might be required or Docker, Chef and Consul may be omitted.
      #. Launch the instance and save the ``.pem`` key as ``[key_name].pem`` to the home directory. This can be done by using the ``gedit`` command in the terminal, then copying and pasting the key to the new file.
   
   #. Connect to the server: ``ssh -i "[key_name].pem" ubuntu@[public_DNS]``.

-Packet Path:

   #. Create a Packet Account
   #. Use ``ssh-keygen -t rsa ``,``cd ~/.ssh ``,``cat id_rsa.pub `` to generate a required key.
   #. Use the key to create a server.
   #. Now go to ``Manage>[the project::servers]>[the server::overview]>Console `` and use the command there to ssh to the server.

-B-Y-O-Server Path:

   #. Create A Type 1 Ubuntu Server with the SSH key (8 Gb RAM minimum)
   #. Make sure ports 22, 443, 3000, 2375, 2475, 4646, 8300, 8301, 8888, and ICMP are avlible through the enacted policy.
   #. Connect to the server: ``ssh root@[ip address]``

#. Save the used system's EXTERNAL IP address: ``export IPA=[CIDR]`` (`CIDR <https://en.wikipedia.org/wiki/Classless_Inter-Domain_Routing>`_ is the IP address with the /## subnet included)

   Note: For local installs use ``ip -4 addr`` to find the CIDR, or use the external IP given by the server provider. 

#. Clone Digital Rerbar and Install Prereqs
    
    ::
    
      curl -fsSL https://raw.githubusercontent.com/digitalrebar/digitalrebar/master/deploy/quickstart.sh | bash


#. Ansible Install Digital Rebar (using deploy ./run-in-system command)
    
    ::
    
      curl -fsSL https://raw.githubusercontent.com/digitalrebar/digitalrebar/master/deploy/quickstart.sh | bash

#. Using node's the _public ip_, open Digital Rebar on your Server via the Digital Rebar UI on https://[public ip] (default user/pass is ``rebar/rebar1``).

Troubleshooting Tip:  "Monitor...Annealer" provides a view of exactly what is going on.  If there is an error, that view provides a ``Retry`` button that often resolves simple timing issues.

#. After you've connected for the first time, switch to the new UX ("new UX") on the menu or visit https://[public ip]/ux

Let's add a Provider and Nodes!
-------------------------------

In order to maintain simplicity for new users, use cloud servers, not local vms or physical servers.  These are supported in a more complex setup. This guide covers adding nodes using the UI. 

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

For more on the UI, see :ref:`web_user_guide`. For instructions on how to add nodes with the UX, see :ref:`ux_nodes`.

Use the Workload Wizard to Build Cluster (using RackN UX)
---------------------------------------------------------

We are using a very basic Kubernetes as a reference app for this quick install.

#. Select Workloads...Kubernetes from the left hand navigation and follow the steps.  
  
   #. Name your deployment.  If you want to review it before starting, uncheck the auto-commit.
   #. Select different node(s) as ``docker-swarm-member`` using the checkboxes
   #. Your OS is set when you create your provider (you may only have one).  System nodes are for physical deployments and will provision the OS.
   #. Configure select options.  There may be additional options, these are the ones exposed for the Wizard.
   #. Select your nodes and set their roles in the deployment.  Defaults are safe here.
   #. Review the JSON that will be submitted to direct the install.  You can edit this by clicking the "pencil" button.
#. Watch Digital Rebar build the cluster from the Deployment...Matrix tab or Annealer button (top right corner).
#. Login to the cluster from the Master Node using ``https://[ip of master]/ui`` (admin/changeme) 

   #. Get the IP of the manager from Nodes and looking for the address of the node that is assigned as the cluster-master
