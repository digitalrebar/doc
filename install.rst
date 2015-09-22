Digital Rebar Install
=====================

*Approximate install time: 10-30 minutes depending on bandwidth.*  Once cached, reset takes *3-10 minutes* on most systems.

16 Gb of RAM (or better) is recommended.

.. contents:: The install steps are:
  :depth: 1

Rather than cover every operating system, we are assuming that you can translate between Ubuntu to other distributions.

*Need help?* Jump over to our `live chat <https://gitter.im/digitalrebar/core>`_  (Gitter.im)

**RECOMMENDATION:** Review the `RackN maintained deploy scripts <https://github.com/rackn/digitalrebar-deploy>`_ for updated step-by-step install examples.
  * Use `Vagrant <https://github.com/rackn/digitalrebar-deploy/blob/master/install_vagrant.md>`_? We've automated all these steps for that too.
  * Comfortable with `Ansible <https://github.com/rackn/digitalrebar-deploy/edit/master/install_ansible.md>`_? Deploy these steps automatically to Ubuntu and Centos.
  * Don't have hardware?  No problem, we've got a quick install in `Packet.net <https://github.com/rackn/digitalrebar-deploy/blob/master/install_packet.md>`_.

Provisioning from Containers
----------------------------

The goal for this document is getting a basic Digital Rebar Infastructure running quickly.  For that reason, many options and configuration choices have been omitted in the interest in brevity.

Digital Rebar operates all the infrastructure management functions in Docker containers; consequently, you need to be running in an environment that can run Docker.

    To improve support, the `Digital Rebar team <https://github.com/orgs/digitalrebar/teams>`_ is no longer creating or documenting install packages.

    For developers, we've collected some `additional guidance <development/advanced-install>`_ to review after you've got your first install working.

We are going to assume that you know how to use basic Docker and Docker Compose commands so that we can keep these instructions concise.  Please see the footnotes for command examples.

Step 1. Install Docker & Docker Compose
---------------------------------------

WARNING: freshness matters for Docker, do NOT use *apt-get* or *yum*!

Follow the `Docker install guide <http://docs.docker.io/en/latest/installation/>`_ 

- Install Docker. [11]_
- Get permission to run Docker without sudo. [12]_
- Turn off Apparmor [13]_ (`production deploy <deployment/>`_ could be configured to leave on)
- Map a local address (192.168.124.10/24) to the docker bridge [14]_ (required to boot VMs or metal)

Follow the `Compose install guide <https://docs.docker.com/compose/install/>`_ using VERSION = 1.4.0 (as of Sept 2015)

Want to see step by step? See `RackN Docker Install Ansible Playbook <https://github.com/rackn/digitalrebar-deploy/blob/master/tasks/docker.yml>`_

Step 2. Download Code & Prerequists
-----------------------------------

These steps are for **default** configuration.  Advanced configurations can adapt to more complex environments.

- Make sure you have *disabled* the following services locally:
   - bind: DNS server on :53 (e.g.: ``sudo killall dnsmasq``)
   - proxy: local proxy on :8123 (e.g.: ``sudo service squid3 stop``) 
   - ntp: Time server on :123 (e.g.: ``sudo service ntp stop``)
   - db: PostgreSQL on :5432 (e.g.: ``sudo service postgresql stop`` )
   - rails: local web apps on :3000
   - when starting Compose, you will be alerted of port conflicts with `assigned port conflicts <docker-compose-common.yml>`_ .
- Create an ssh key [21]_ for Digital Rebar to copy into your nodes.
- (optional) Download at least one ISO [23]_ from the list in `provisioner.yml <https://github.com/digitalrebar/core/blob/develop/barclamps/provisioner.yml#L135>`_ and copy to ``~/.cache/digitalrebar/tftpboot/isos``.  This step is required to provision bare metal or unimaged VMs using ``kvm-slave``.
- Install git.
- Clone the RackN Digital Rebar Deploy: ``git clone https://github.com/rackn/digitalrebar-deploy.git deploy``
- Run ``compose/setup.sh`` to clone the Digital Rebar code base from Github into the ``components/rebar/digitalrebar/core`` directory.
  - Add workloads to the base by passing them as parameters.  Examples are ``kubernetes``, ``ceph`` and ``hardware``.  This simply clones additional repos next to the core repo.
- (optional) Link the Digital Rebar code path [24]_ from the compose components directory to your home directory.

Step 3. Deploy infrastructure containers
----------------------------------------

FIRST INSTALL? The first install is slow because you have to pull the images, do this interactively using ``docker-compose pull``.  Once the images are local there is minimal network interaction.

From the ``compose`` directory, run ``docker-compose up -d`` to start the process.  If it does not come up the first time, try to reset the environement (steps below),

After a few minutes, the rebar-api-service will be available on http://127.0.0.1:3000

You can monitor the progress in several ways:

#. Use ``docker-compose logs rebar_api`` to send logs to the screen.  The command example shows how select one component to watch.
#. The Digital Rebar Consul service comes up quickly on http://127.0.0.1:8500.  There should be a list of approximately 10 services.  You can login once the "rebar-api-service" is passing.
#. A Kibana logstash service is running on http://127.0.0.1:5601.  Select a timestamp and then visit the Discover tab.
#. ``docker-compose ps`` will show you the status of the services and associated port mappings.
#. ``docker ps`` will show you the status of the containers

To reset the environment, you must stop and then remove [32]_ the containers.

After the install has progressed (the ``rebar-api-service`` is up in `Consul <http://127.0.0.1:8500>`_ ), you should be able to monitor the progress of the Admin container at http://localhost:3000.

You can connect to any container using ``docker exec -it [name] bash``; however, we recommend using `Kibana <http://127.0.0.1:5601>`_ to check centralized logs first.

Housekeeping Notes
~~~~~~~~~~~~~~~~~~

To remove Docker image cruft, we suggest running ``docker ps -q -a | xargs docker rm`` on a regular basis.

Step 4. Provision Nodes!
------------------------

And now, the real fun begins!  

#. Log in to Digital Rebar on http://127.0.0.1:3000 using default user ``rebar`` and password ``rebar1``
#. Wait for the first annealing pass to complete (all marks are green).  Please be patient on the first run because Digital Rebar is building and caching provisioning images (during ``provisioner-base-images`` role) from the downloaded ISOs

If this is your first install, the Docker and KVM nodes approach will allow you to play with Digital Rebar with minimal network configuration.

Docker Nodes (fast testing)
~~~~~~~~~~~~~~~~~~~~~~~~~~~

From the deploy/compse directory:

#. ``docker-compose scale node=5``

You can turn the number of nodes up and down by changing the number.

KVM Nodes (high fidelity test)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Works on Linux environments that can run KVM.  It is **not compatable** with simultaneous VirtualBox / Vagrant testing.

These instructions assume that you've linked [24]_ the Digital Rebar code to ~/rebar.

#. Install prereqs: 

   #. ``apt-get install qemu-kvm libvirt-bin ubuntu-vm-builder bridge-utils ruby1.9.1-dev make``
   #. ``gem install json net-http-digest_auth``

#. Under ~/rebar/core, use ``tools/kvm-slave &`` to spawn a KVM virtual machine that will boot from the freshly-deployed admin node.

More details? See `virtual nodes <development/advanced-install/kvm-slaves.rst>`_ for testing using KVM.

Real Hardware
~~~~~~~~~~~~~

To boot Real Hardware, bind a physical interface to docker0 with brctl,
make sure that interface is up and does not have an address, and plug it
in to a switch that has the physical boxes you want to boot.

Example Commands: 

  #. Install prereqs: ``sudo apt-get install bridge-utils``
  #. (optional) To configure RAID or BIOS, you need the RackN Hardware workload.
     #. Clone the RackN Hardware workload: ``compose/workload.sh rackn hardware``
     #. Download the required tools.  See `RackN Hardware Docs <https://github.com/rackn/hardware/blob/master/doc/README.md>`_
  #. slave the eth2 to the docker bridge, ``sudo brctl addif docker0 eth2`` 
  #. turn on eth2 for the bridge, ``sudo ip link set eth2 up`` 
  #. boot the physical nodes from a switch connected to eth2

Virtual Box (generally for Mac or Windows users)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

    This approach simulates the same steps as metal, so it expects that you've created a VM to host the
    Admin container.  If so, make sure you added an ethernet device (not
    up'd) to your VM that will be the admin network for slave VMs. Also,
    if using vmware, you'll need to use E1000 Nics and make sure your
    network settings are set to "Allow" promiscuous mode.

If your development environment is running in VMs then:

#. make sure that your Admin VM has an extra eth port connected to a
   dedicated host only bridge (let's assume eth2)
#. slave the eth2 to the docker bridge,
   ``sudo brctl addif docker0 eth2``
#. turn on eth2 for the bridge, ``sudo ip link set eth2 up``
#. create a VM with eth0

   #. attached to the dedicated host only bridge
   #. make sure it is able to network boot

#. boot the VM

   #. it should PXE boot
   #. the VM should register and automatically progress in the system
      deployment
   #. if you have issues, review the ``/var/log/install.log`` for
      details

Step 5. Install Workloads
-------------------------

From the Digital Rebar UI, you can use one of the Deployment...Wizards to select roles to install on available nodes.  Once you have selected roles for nodes, you must "commit" the deployment.

Command Reference
-----------------

**WARNING**: These suggestions may become out of date.  We strongly recommend reviewing the actively maintained `deploy scripts <https://github.com/rackn/digitalrebar-deploy>`_.

Step 1 Items:

.. [11] ``curl -sSL https://get.docker.com/ -o /tmp/docker.sh | sh``
.. [12] ``sudo usermod -a -G docker <your-user>``
   plus, if you don't want to reboot right away, run ``sudo chmod 666 /var/run/docker.sock`` to temporarily allow everyone access.
.. [13] ``sudo service apparmor teardown`` and ``sudo update-rc.d -f apparmor remove``
.. [14] ``sudo ip a add 192.168.124.10/24 dev docker0``

Step 2 Items:

.. [21] ``ssh-keygen -t rsa``
.. [23] ISO download steps:

        #. ``mkdir -p .cache/digitalrebar/tftpboot/isos``
        #. ``cd .cache/digitalrebar/tftpboot/isos``
        #. Choose one or both:

           #. ``wget http://mirrors.kernel.org/centos/7.1.1503/isos/x86_64/CentOS-7-x86_64-Minimal-1503-01.iso -nc``
           #. ``wget http://mirrors.kernel.org/ubuntu-releases/trusty/ubuntu-14.04.3-server-amd64.iso -nc``
.. [24] ``-s ~/deploy/compose/components/rebar_api/digitalrebar/ rebar``

Step 3 Items:

.. [32] ``docker-compose stop && docker-compose rm``

