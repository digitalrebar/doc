.. _quick_start:

Digital Rebar Quick Start
=========================

This is a TL;DR only! See :ref:`install` for more options.

Don't like to read?  Try our :ref:`videos`.  Training videos `001a <https://www.youtube.com/watch?v=uYG9nstYpD4&index=1&list=PLXPBeIrpXjfgurJuwVjZkcfmatCoXYM_v>`_, `001b <https://www.youtube.com/watch?v=dHSCwifAlK8&index=2&list=PLXPBeIrpXjfgurJuwVjZkcfmatCoXYM_v>`_ and `001c <https://www.youtube.com/watch?v=3xawxPiSeJ4&index=3&list=PLXPBeIrpXjfgurJuwVjZkcfmatCoXYM_v>`_ cover all the information found in this guide in depth.

For this quick start, we will assume SSH access to the install server.  The goal is a temporary playground, not a long term install.  It is possible to install different operating systems and work by remote or fully automated.  We are keeping it very simple in this quick start.

For more on the Web UX that is used extensively throughout this quick start, see :ref:`web_ux_guide`.

Once the server is available and the install step is executed, it should take about 20 minutes in AWS or Packet.net for the system to be ready.

SSH to an Ubuntu Server 16.04 with 8 GB RAM
-------------------------------------------

Note: This quick start focuses on a minimal fast path with Ubuntu 16.04.  However, Digital Rebar will run on Centos, RHEL and other distros.

#. AWS Path:

   #. Create AWS `m4.large` (or larger!) Ubuntu instance. This can be done with the SSH key or by following these steps:

      #. Login to AWS and click on EC2 under Compute.
      #. Our AWS provider default is US West (Oregon) so that region is recommended for this quick start.
      #. Click on Launch Instance. This will begin the instance set up.
      #. Select 16.04 Ubuntu Server (not 14.04!) for the AMI, then select `m4.large` or larger. A minimum of 8 Gb of RAM is required.
      #. A minimum of 20 Gb of Disk is recommended.  8 Gb is required.
      #. Next, navigate to the Configure Security Group tab.  The "default" Security Group for this server needs Port 22 (ssh), 443 (rebar/HTTPS) and ICMP to be available!  This is just our recommended base. Depending on the application, additional ports might be required such as Docker, Chef and Consul.
      #. Launch the instance and save the ``.pem`` key as ``[key_name].pem`` to the home directory. This can be done by using the ``gedit`` command in the terminal, then copying and pasting the key to the new file.
      #. Modify key permissions using ``chmod 600 [key_name].pem``.

   #. Connect to the server: ``ssh -i "[key_name].pem" ubuntu@[public_DNS]``.

#. Packet.net Path:

   #. Create a Packet Account
   #. Use ``ssh-keygen -t rsa`` , ``cd ~/.ssh`` , ``cat id_rsa.pub`` to generate a required key.
   #. Use the key to create a server.
   #. Now go to Manage>[the project::servers]>[the server::overview]>Console and use the command there to SSH to the server.
   #. Provision at Type 1 Ubuntu Server then follow the B-Y-O-Server steps below.

#. B-Y-O-Server Path:

   #. Create an Ubuntu Server with the SSH key (16.04 preferred, 8 Gb RAM minimum)
   #. Make sure ports 443, 22 and ICMP are available through the enacted policy.
   #. Connect to the server: ``ssh root@[ip address]``

Install Digital Rebar
---------------------

In this section only, using SSH is necessary to the target install server.  This step adds pre-reqs and then deploys via the ``deploy/run-in-system`` command.

#. Run the Quick Start script

    ::

      curl -fsSL https://raw.githubusercontent.com/digitalrebar/digitalrebar/master/deploy/quickstart.sh | bash

   #. Troubleshooting ``Ansible Install "Prereqs"`` fail: You may have to upgrade Ansible to v 2.1+ yourself
   #. Troubleshooting ``wait for admin convergence`` fail: This is just a timeout.  The system is generally running but slower than expected.

#. Using the node's public IP, open Digital Rebar on your Server via the Digital Rebar UI on https://[public_ip]

   #. The default username and password are ``rebar`` and ``rebar1`` respectively.

Add a Provider and Node
-----------------------

In order to maintain simplicity for new users, use cloud servers instead of local VMs or physical servers.  The latter two are supported in a more complex setup. This quick start guide covers adding nodes using the New UX.

#. From the client, log on to the system using ``https://[external ip address]``.  Reminders:

   #. Use External IP. This is the same as the SSH address.
   #. Since it is HTTPS, it is required to accept the self-signed SSL certificate.
#. Add a AWS Provider from the "Providers" page by clicking the add (+) button, located in the bottom right corner:

   #. To Automatically Add AWS credentials, you must have used the AWS CLI on your local system to populate the ``.aws`` configuration files.

      ::

         curl -fsSL https://raw.githubusercontent.com/digitalrebar/digitalrebar/master/deploy/aws-add-provider.sh | bash -s -- --provider=aws --admin-ip=[external ip address]

      #. REMEMBER to set the external IP in the command
      #. You must have AWS credentials stored locally for this script to work
   #. To Manually Add AWS Key (similar steps for Packet or Google)

      #. Add a provider using AWS type and your Credentials.
      #. Choose the same region as the admin is using. Note that the default AMI targets us-west-2. Thus, if a different region is selected, the AMI must also be changed to match (for demo use Centos 7.2+).
      #. Consult :ref:`configure_providers` for detailed instructions and troubleshooting including live log review.
#. Add a node from the "Nodes" and the add (+) button (lower right side)

   #. Pick a name for your node and the provider added above.
   #. You can use the system deployment for now.
   #. Additional instructions can be found at :ref:`configure_providers`.
   #. After adding, you can also watch the node being created in your AWS Cloud console.
#. Allow the system to complete annealing (progress in top right corner).
#. For troubleshooting help, see :ref:`troubleshoot_providers`.

Remember to delete used nodes from the Nodes page before taking the system down!  There is no automatic cleanup.

For instructions on how to add nodes with the UX, see :ref:`ux_nodes`.

Workload Wizard to Build a Cluster with RackN UX
-------------------------------------------------

We are using a basic Kubernetes as a reference app for this quick install.

#. Select App Catalog...Kubernetes from the left hand navigation and follow these steps:

   #. Name the deployment.  (These names are case sensitive!) If auto-commit is left on, deployment review is skipped.  This is recommended for quick start.
   #. The OS is set when the provider is created. (Note: There may only be one.)  Do not try System (Physical) Nodes for quick start.
   #. Configure select options.  There may be additional options, but only the key ones are exposed in the Wizard.  The defaults here are safe.
   #. Select desired nodes and set their roles in the deployment.  The defaults are safe here.
   #. Review the JSON that will be submitted to direct the install.  The JSON can be edited by clicking the pencil icon in the top right corner.

#. Watch Digital Rebar build the cluster from the Deployment page or from the Annealer button in the top right corner.  For more on the Deployment page and the Annealer, see :ref:`ux_deployment` and :ref:`ux_annealer` respectively.
#. Login to the cluster from the Master Node using ``https://[ip of master]/ui`` (admin/changeme)

   #. Get the IP of the manager from Nodes and look for the address of the node that is assigned as the cluster-master.
