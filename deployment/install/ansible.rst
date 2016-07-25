Using the `Ansible <http://ansible.com>`_ Playbook
##################################################

.. contents:: Table of Contents
  :depth: 6

The Digital Rebar playbook starts in `digitalrebar.yml <https://github.com/rackn/digitalrebar-deploy/digitalrebar.yml>`_ and uses the `tasks <https://github.com/rackn/digitalrebar-deploy/tasks>`_ and `group vars <https://github.com/rackn/digitalrebar-deploy/group_vars>`_ to drive configuration.

The playbook is driven by a set of scripts handle accessing the system be it linux-based (remote or local), Mac OSX, or in a metal provider (Packet).

Check the `scripts <https://github.com/rackn/digitalrebar-deploy>`_ to see how to run the playbook.  *run-in-xxx.sh*

What's installed?
"""""""""""""""""

The following is done by default:

* all prerequisites including latest Docker with correct permissions
* latest Digital Rebar code from develop branch
* Node target operating systems:
    * Ubuntu 14.04 and Centos 7 ISO
* Default IP maps for Digital Rebar:
    * internal address of 192.168.124.11
    * port mapping of UI (:3000) and Consul (:8500)

All of these can be altered by the group_vars/all.yml.

Step 1. Install Docker & Docker Compose
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

WARNING: Freshness matters for Docker, do NOT use *apt-get* or *yum*!

Follow the `Docker install guide <http://docs.docker.io/en/latest/installation/>`_:

- Install Docker. [11]_
- Get permission to run Docker without sudo. [12]_
- Turn off Apparmor [13]_ (`production deploy <deployment/>`_ could be configured to leave on)
- Map a local address (192.168.124.10/24) to the docker bridge [14]_ (required to boot VMs or metal)

Follow the `Compose install guide <https://docs.docker.com/compose/install/>`_ using VERSION = 1.4.0 (as of Sept 2015)

For step by step instructions see: `RackN Docker Install Ansible Playbook <https://github.com/rackn/digitalrebar-deploy/blob/master/tasks/docker.yml>`_

Step 2. Download Code & Prerequists
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

These steps are for **default** configuration.  Advanced configurations can adapt to more complex environments.

 - When starting Compose, there will be an alert of `assigned port conflicts <docker-compose-common.yml>`_ .
 - Make sure the following services are *disabled* locally:
   - rails: local web apps on :3000
   - consul: UI on :8500
- Create an ssh key [21]_ for Digital Rebar to copy into the nodes.
- (optional) Download at least one ISO [22]_ from the list in `provisioner.yml <https://github.com/digitalrebar/core/blob/develop/barclamps/provisioner.yml#L135>`_ and copy to ``~/.cache/digitalrebar/tftpboot/isos``.  This step is required to provision bare metal or unimaged VMs using ``kvm-slave``.
- Install git.
- Clone the RackN Digital Rebar Deploy: ``git clone https://github.com/rackn/digitalrebar-deploy.git deploy``
- Run ``compose/setup.sh`` to clone the Digital Rebar code base from Github into the ``components/rebar/digitalrebar/core`` directory.
   - Copy desired ssh keys into the compose digitalrebar core configuration ssh_keys directory [23]_
   - Add workloads to the base by passing them as parameters.  Examples are ``kubernetes``, ``ceph`` and ``hardware``.  This simply clones additional repos next to the core repo.
- (optional) Link the Digital Rebar code path [24]_ from the compose components directory to the home directory.

Step 3. Deploy infrastructure containers
----------------------------------------

#. From the ``compose`` directory, run ``./init_files.sh --access FORWARDER --provisioner``.  This will create the required .yml files for docker-compose.  To see what other options are available for ``init_files.sh``, run ``./init_files.sh --help``.
#. The first install is slow because the images have to be pulled, do this interactively using ``docker-compose pull``.  Once the images are local there is minimal network interaction.  Make certan to re-pull the containers (and the deploy git repository) on a regular basis to keep up to date with the changes to the containers.
#. From the ``compose`` directory, run ``docker-compose up -d`` to start the process.  If it does not come up the first time, try to reset the environement (steps below),

After a few minutes, the rebar-api-service will be available on http://127.0.0.1:3000

The progress can be monitored in several ways:

#. Use ``docker-compose logs rebar_api`` to send logs to the screen.  The command example shows how to select one component to watch.
#. The Digital Rebar Consul service comes up quickly on http://127.0.0.1:8500.  There should be a list of approximately 10 services. Once the "rebar-api-service" is passing login will be avalible. #. A Kibana logstash service is running on http://127.0.0.1:5601.  Select a timestamp and then visit the Discover tab.
#. ``docker-compose ps`` will show the status of the services and associated
#. ``docker ps`` will show the status of the containers

To reset the environment, stop and then remove [32]_ the containers.

After the install has progressed (the ``rebar-api-service`` is up in `Consul <http://127.0.0.1:8500>`_ ), the progress of the Admin container should be visible at http://localhost:3000.

Any container can be contacted using ``docker exec -it [name] bash``; however, we recommend using `Kibana <http://127.0.0.1:5601>`_ to check centralized logs first.

Housekeeping Notes
------------------

To remove Docker image cruft, we suggest running ``docker ps -q -a | xargs docker rm`` on a regular basis.

Step 4. Provision Nodes!
~~~~~~~~~~~~~~~~~~~~~~~~

And now, the real fun begins!

#. Log in to Digital Rebar on http://127.0.0.1:3000 using default user ``rebar`` and password ``rebar1``
#. Wait for the first annealing pass to complete (all marks are green).  Please be patient on the first run because Digital Rebar is building and caching provisioning images (during ``provisioner-base-images`` role) from the downloaded ISOs

If this is the first install, the Docker and KVM nodes approach will allow for some experimentation with Digital Rebar with minimal network configuration.


KVM Nodes (high fidelity test)
------------------------------

Works on Linux environments that can run KVM.  It is **not compatable** with simultaneous VirtualBox / Vagrant testing.

These instructions assume that the Digital Rebar code has been linked [24]_  to ~/rebar.

#. Install prereqs:

   #. ``apt-get install qemu-kvm libvirt-bin ubuntu-vm-builder bridge-utils ruby1.9.1-dev make``
   #. ``gem install json net-http-digest_auth``

#. Under ~/rebar/core, use ``tools/kvm-slave &`` to spawn a KVM virtual machine that will boot from the freshly-deployed admin node.

More details? See `virtual nodes <development/advanced-install/kvm-slaves.rst>`_ for testing using KVM.

Real Hardware
-------------

To boot Real Hardware, bind a physical interface to docker0 with brctl,
make sure that interface is up and does not have an address, and plug it
in to a switch that has the physical boxes that are to be booted.

Example Commands:

  #. Install prereqs: ``sudo apt-get install bridge-utils``
  #. (optional) To configure RAID or BIOS, the RackN Hardware workload is required.
     #. Clone the RackN Hardware workload: ``compose/workload.sh rackn hardware``
     #. Download the required tools.  See `RackN Hardware Docs <https://github.com/rackn/hardware/blob/master/doc/README.md>`_
  #. slave the eth2 to the docker bridge, ``sudo brctl addif docker0 eth2``
  #. turn on eth2 for the bridge, ``sudo ip link set eth2 up``
  #. boot the physical nodes from a switch connected to eth2

Virtual Box (generally for Mac or Windows users)
------------------------------------------------

    This approach simulates the same steps as metal, so it expects that a VM has been
    created to host the Admin container.  If so, make sure an ethernet device has been
    added (not up'd) to the VM that will be the admin network for slave VMs. Also,
    if using vmware, E1000 Nics will be required and make sure the
    network settings are set to "Allow" promiscuous mode.

If the development environment is running in VMs then:

#. Make sure that the Admin VM has an extra eth port connected to a
   dedicated host only bridge (let's assume eth2)
#. Slave the eth2 to the docker bridge,
   ``sudo brctl addif docker0 eth2``
#. Turn on eth2 for the bridge, ``sudo ip link set eth2 up``
#. Create a VM with eth0

   #. Attached to the dedicated host only bridge
   #. Make sure it is able to network boot

#. Boot the VM

   #. It should PXE boot
   #. The VM should register and automatically progress in the system
      deployment
   #. If there are issues, review the ``/var/log/install.log`` for
      details

Step 5. Install Workloads
~~~~~~~~~~~~~~~~~~~~~~~~~

From the Digital Rebar UI, use one of the Deployment...Wizards to select roles to install on available nodes.  Once roles have been selected for nodes, the deployment must be "commited."

Command Reference
-----------------

**WARNING**: These suggestions may become out of date.  We strongly recommend reviewing the actively maintained `deploy scripts <https://github.com/rackn/digitalrebar-deploy>`_.

Step 1 Items:

.. [11] ``curl -sSL https://get.docker.com/ -o /tmp/docker.sh | sh``
.. [12] ``sudo usermod -a -G docker <your-user>``
run ``sudo chmod 666 /var/run/docker.sock`` to temporarily allow everyone access and avoid an immediate reboot.
.. [13] ``sudo service apparmor teardown`` and ``sudo update-rc.d -f apparmor remove``
.. [14] ``sudo ip a add 192.168.124.10/24 dev docker0``

Step 2 Items:

.. [21] ``ssh-keygen -t rsa``
.. [22] ISO download steps:

        #. ``mkdir -p .cache/digitalrebar/tftpboot/isos``
        #. ``cd .cache/digitalrebar/tftpboot/isos``
        #. Choose one or both:

           #. ``wget http://mirrors.kernel.org/centos/7.1.1503/isos/x86_64/CentOS-7-x86_64-Minimal-1503-01.iso -nc``
           #. ``wget http://mirrors.kernel.org/ubuntu-releases/trusty/ubuntu-14.04.3-server-amd64.iso -nc``
.. [23] ``cp ~/.ssh/id_rsa.pub deploy/compose/digitalrebar/core/config/ssh_keys/setup-0.key``
.. [24] ``-s ~/deploy/compose/components/rebar_api/digitalrebar/ rebar``

Step 3 Items:

.. [32] ``docker-compose stop && docker-compose rm``


Configuration Options
"""""""""""""""""""""

The following options are available to be modified in the `group_vars/all.yml <https://github.com/rackn/digitalrebar-deploy/group_vars/all.yml>`_ file.  The file contains documentation for each var, but additional detail is specified in the table below.

+---------------+----------+-----------+---------+
| *Key*         | *Values* | *Default* | *Notes* |
+---------------+----------+-----------+---------+
| dr_services   |          |           |         |
|               |          | jj        | jj      |
+---------------+----------+-----------+---------+
| dr_workload   | jj       | jj        |         |
+---------------+----------+-----------+---------+


.. code-block:: shell

  <h1>code block example</h1>
