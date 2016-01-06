Digital Rebar Quick Start
=========================

For this quick start, we assume you'll ssh to the install server.  The goal is a temporary playground, not a long term install.  It is possible to install remote and fully automated, but we are keeping it very simple in this guide

Once you have the server, it should take about 10 minutes in AWS or Packet.net.

Installation Steps:
-------------------

1. AWS Path:
  #. Create AWS t2.medium (or larger) Ubuntu instance with your SSH key.  CRITICAL: You need access to Port 22, 443 and 3000!
  #. Connect to the server: ``ssh ubuntu@[ip address]``
  #. Figure out the system's CIDR address: ``ip a | grep -A 1 eth0``

2. Packet or B-Y-O-Server Path:
  #. Create Packet Type 1 Ubuntu Server with your SSH key
  #. Connect to the server: ``ssh root@[ip address]``
  #. Figure out the system's CIDR address: ``ip a | grep -A 1 bond0``

3. Save your system IP address: ``export IPA=[CIDR]``
#. Install Git: ``sudo apt-get install git ansible jq -y``  (may be apt-get install git)
#. Get the deployment code and test for pre-reqs
    
    ::
    
      cd ~
      mkdir digitalrebar
      cd digitalrebar
      git clone https://github.com/rackn/digitalrebar-deploy deploy
      cd deploy/compose
      ln -s ../../../digitalrebar digitalrebar
      cd ..
      echo "Checking prerequisites"
      ./run-in-system.sh --help
      echo "let's setup Digital Rebar!"

6. Install to local system: ``./run-in-system.sh --deploy-admin=local --con-node --access=HOST --admin-ip=$IPA``

This script ends with the Digital Rebar admin node fully operational but without any nodes.  

Let's Add Nodes!
----------------

* From your client, you can log on to the system using ``http://[external ip address]:3000``.  Reminders: 

  * Use the SSH address, not the internal IP address you used above
  * reminder: accept the self-signed SSL certificate.
* You can quickly test the system with docker based nodes using ``cd compose && docker-compose scale node=10``
* You can add nodes with the AWS or Packet provisioner from the "Utilities...Providers" menu.  `Instructions here <../provider.rst>`_.
