.. _quick_start:

Digital Rebar Quick Start
=========================

This is a TL;DR only! See :ref:`install` for more options.

Don't like to read?  Try our :ref:`videos`.

For this quick start, we assume ssh access to the install server.  The goal is a temporary playground, not a long term install.  It is possible to install different operating systems and work by remote or fully automated.  We are keeping it very simple in this quick start.

Once the server is available and you've run the single install step, it should take about 20 minutes in AWS or Packet.net for the system to be ready.

SSH to an Ubuntu Server 16.04 with 8 GB RAM
-------------------------------------------

Note: This quick start focuses on a minimal fast path with Ubuntu 16.04.  However, Digital Rebar can run on Centos, RHEL and other distros.

#. AWS Path:

   #. Create AWS m4.large (or larger!) Ubuntu instance. This can be done with the SSH key or by following these steps:

      #. Login to AWS and click on EC2 under Compute.
      #. Our AWS provider default is US West (Oregon) so that region is recommended for this quick start.
      #. Click on Launch Instance. This will begin the instance set up.
      #. Select 16.04 Ubuntu Server (not 14.04!) for the AMI, then select `m4.large` or larger. A minimum of 8 Gb of RAM is required.
      #. Next, navigate to the Configure Security Group tab.  The "default" Security Group for this server needs Port 22 (ssh), 443 & 3000 (rebar), 2375 & 2475 (docker swarm), 4646 (chef), 8300 & 8301 (consul), 8888 (certificate signing service) and ICMP to be available!  This is just our recommended base. Depending on the application, additional ports might be required, or Docker, Chef and Consul may be omitted.
      #. Launch the instance and save the ``.pem`` key as ``[key_name].pem`` to the home directory. This can be done by using the ``gedit`` command in the terminal, then copying and pasting the key to the new file.

   #. Connect to the server: ``ssh -i "[key_name].pem" ubuntu@[public_DNS]``.

#. Packet.net Path:

   #. Create a Packet Account
   #. Use ``ssh-keygen -t rsa`` , ``cd ~/.ssh`` , ``cat id_rsa.pub`` to generate a required key.
   #. Use the key to create a server.
   #. Now go to Manage>[the project::servers]>[the server::overview]>Console and use the command there to ssh to the server.
   #. Provision at Type 1 Ubuntu Server then follow the B-Y-O-Server steps below.

#. B-Y-O-Server Path:

   #. Create an Ubuntu Server with the SSH key (16.04 preferred, 8 Gb RAM minimum)
   #. Make sure ports 22, 443, 3000, 2375, 2475, 4646, 8300, 8301, 8888, and ICMP are available through the enacted policy.
   #. Connect to the server: ``ssh root@[ip address]``

Install Digital Rebar
---------------------

In this section only, you need to SSH to the target install server.  This step adds pre-reqs and then deploys via the ``deploy/run-in-system`` command.

#. Run the Quick Start script

    ::

      curl -fsSL https://raw.githubusercontent.com/digitalrebar/digitalrebar/master/deploy/quickstart.sh | bash

   Note: Since the provisioner is not installed in this case, some steps are skipped in order to save time.

   #. Troubleshooting ``Ansible Install "Prereqs"`` fail: You may have to upgrade Ansible to v 2.1+ yourself
   #. Troubleshooting ``wait for admin convergence`` fail: This is just a timeout.  The system is generally running but slower than expected.
   #. If you save the file locally and ``chmod +x [file]`` then you can run it with parameters like ``--con-provisioner`` for local booting.

#. Using the node's public IP, open Digital Rebar on your Server via the Digital Rebar UI on https://[public_ip]

   #. The default username and password are ``rebar`` and ``rebar1`` respectively.
   #. "Monitor...Annealer" provides a view of exactly what is going on.  If there is an error, this view provides a ``Retry`` button that often resolves simple timing issues.

#. After connecting for the first time, switch to the new user interface ("New UX") on the menu or visit https://[public_ip]/ux.

Add a Provider and Node
-----------------------

In order to maintain simplicity for new users, use cloud servers instead of local VMs or physical servers.  The latter two are supported in a more complex setup. This quick start guide covers adding nodes using the New UX.

#. From the client, it is possible to log on to the system using ``https://[external ip address]/ux``.  Reminders:

   #. Use External IP. This is the same as the SSH address.
   #. Since it is HTTPS, it is required to accept the self-signed SSL certificate.
#. Add a AWS Provider from the "Providers" page by clicking the add (+) button, located in the bottom right corner:

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

For more on the UI, see :ref:`web_user_guide`. For instructions on how to add nodes with the UX, see :ref:`ux_nodes`.

Workload Wizard to Build Cluster (using RackN UX)
-------------------------------------------------

We are using a very basic Kubernetes as a reference app for this quick install.

#. Select Workloads...Kubernetes from the left hand navigation and follow the steps.

   #. The defaults are safe, you do not need to make any changes.
      #. Name your deployment.  Leaving auto-commit on skips the deployment review and is recommended for quick start.
      #. Your OS is set when you create your provider (you may only have one).  Do not try System (Physical) Nodes for quick start.
      #. Configure select options.  There may be additional options, just key ones exposed for the Wizard.
      #. Select your nodes and set their roles in the deployment.  Defaults are safe here.
   #. Review the JSON that will be submitted to direct the install.  You can edit this by clicking the "pencil" button.
#. Watch Digital Rebar build the cluster from the Deployment...Matrix tab or Annealer button (top right corner).
#. Login to the cluster from the Master Node using ``https://[ip of master]/ui`` (admin/changeme)

   #. Get the IP of the manager from Nodes and looking for the address of the node that is assigned as the cluster-master
