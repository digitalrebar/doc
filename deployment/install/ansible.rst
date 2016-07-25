Using the `Ansible <http://ansible.com>`_ Playbook
##################################################

.. contents:: Table of Contents
  :depth: 6

The Digital Rebar playbook starts in `digitalrebar.yml <https://github.com/rackn/digitalrebar-deploy/digitalrebar.yml>`_ and uses the `tasks <https://github.com/rackn/digitalrebar-deploy/tasks>`_ and `group vars <https://github.com/rackn/digitalrebar-deploy/group_vars>`_ to drive configuration.

The playbook is driven by a set of scripts handle accessing the system be it Linux-based (remote or local), Mac OSX, or in a metal provider (Packet).

Check the `scripts <https://github.com/rackn/digitalrebar-deploy>`_ to see how to run the playbook.  *run-in-xxx.sh*

What's installed?
"""""""""""""""""
Installation requires several steps. To begin with, the following is done by default:

* All prerequisites including the latest Docker with correct permissions (instructions for some of these are included, just in case)
* Latest Digital Rebar code from develop branch
* Node target operating systems:
    * Ubuntu 14.04 and Centos 7 ISO
* Default IP maps for Digital Rebar:
    * internal address of 192.168.124.11
    * port mapping of UI (:3000) and Consul (:8500)

All of these can be altered by the group_vars/all.yml.

**Note:** While sample code is provided below, the code may be out of date. Therefore, it is strongly recommended to review the actively maintained scripts at `deploy scripts <https://github.com/rackn/digitalrebar-deploy>`_.

Part 1: Install Docker & Docker Compose
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

WARNING: Freshness matters for Docker, do NOT use *apt-get* or *yum*!

Steps for setting up Docker:

#. Install Docker, using the `Docker install guide <http://docs.docker.io/en/latest/installation/>`_: for reference.
#. Get permission to run Docker without sudo.
#. Turn off Apparmor. (If desired, production deployment can be configured to allow Apparmor to remain on.)
#. Map a local address (192.168.124.10/24) to the Docker bridge. This is required to boot VMs or metal.

Sample code to execute these steps::

  curl -SSL https://get.docker.com/ -o /tmp/docker.sh | sh
  sudo usermod -a -G docker <your-user>
  sudo update-rc.d -f apparmor remove
  sudo ip a add 192.168.124.10/24 dev docker0

After Docker is set up, follow the `Compose install guide <https://docs.docker.com/compose/install/>`_ using VERSION = 1.4.0 (as of Sept 2015).

*Note:* When executing the command to run Docker without sudo, running ``sudo chmod 666 /var/run/docker.sock`` will temporarily allow everyone access and prevent an immediate reboot.

Part 2: Download Code & Prerequisites
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
These steps are for **default** configuration.  Advanced configurations are able to adapt to more complex environments.

Note that upon starting Compose, there will be an alert of `assigned port conflicts <docker-compose-common.yml>`_ . To fix this, ensure that the following services are *disabled* locally:
   * rails: local web apps on :3000
   * consul: UI on :8500

**Steps to satisfy the installation prerequisites:**

#. Create an ssh key for Digital Rebar to copy into the nodes.
#. (optional) Download at least one ISO from the list in `provisioner.yml <https://github.com/digitalrebar/core/blob/develop/barclamps/provisioner.yml#L135>`_ and copy to ``~/.cache/digitalrebar/tftpboot/isos``.  This step is required to provision bare metal or unimaged VMs using ``kvm-slave``.
#. Download `git <https://git-scm.com/>`_ and install it. (See :ref:`initial_install_setup` for install commands.)

Sample code for prerequisites::

  ssh-keygen -t rsa
  mkdir -p .cache/digitalrebar/tftpboot/isos
  cd .cache/digitalrebar/tftpboot/isos
  wget http://mirrors.kernel.org/centos/7.1.1503/isos/x86_64/CentOS-7-x86_64-Minimal-1503-01.iso -nc
  wget http://mirrors.kernel.org/ubuntu-releases/trusty/ubuntu-14.04.3-server-amd64.iso -nc

If omitting the optional step, only the first line of code is necessary.

**Steps to download the code:**

#. Clone the RackN Digital Rebar Deploy.
#. Clone the Digital Rebar code base from Github into the ``components/rebar/digitalrebar/core`` directory by running ``compose/setup.sh``.
   #. Copy desired ssh keys into the compose digitalrebar core configuration ssh_keys directory.
   #. Add workloads to the base by passing them as parameters.  Examples are ``kubernetes``, ``ceph`` and ``hardware``.  This simply clones additional repos next to the core repo.
#. (optional) Link the Digital Rebar code path from the compose components directory to the home directory.

Sample code for downloading::

  git clone https://github.com/rackn/digitalrebar-deploy.git deploy
  cp ~/.ssh/id_rsa.pub deploy/compose/digitalrebar/core/config/ssh_keys/setup-0.key
  -s ~/deploy/compose/components/rebar_api/digitalrebar/ rebar

If omitting the optional step, leave out the last line.

Part 3: Deploy infrastructure containers
----------------------------------------
To start up the rebar-api-service:

#. From the ``compose`` directory, run ``./init_files.sh --access FORWARDER --provisioner``.  This will create the required .yml files for docker-compose.  To see what other options are available for ``init_files.sh``, run ``./init_files.sh --help``.
#. The first install is slow because the images have to be pulled, do this interactively using ``docker-compose pull``.  Once the images are local there is minimal network interaction.  Make certan to re-pull the containers (and the deploy git repository) on a regular basis to keep up to date with the changes to the containers.
#. From the ``compose`` directory, run ``docker-compose up -d`` to start the process.  If it does not come up the first time, try to reset the environment (steps below).

Sample code for this::

  ./init_files.sh --access FORWARDER --provisioner
  docker-compose pull
  docker-compose up -d

After a few minutes, the rebar-api-service will be available on http://127.0.0.1:3000

The progress can be monitored in several ways:

#. Use ``docker-compose logs rebar_api`` to send logs to the screen.  The command example shows how to select one component to watch.
#. The Digital Rebar Consul service comes up quickly on http://127.0.0.1:8500.  There should be a list of approximately 10 services. Once the "rebar-api-service" is passing login will be available.
#. A Kibana logstash service is running on http://127.0.0.1:5601.  Select a timestamp and then visit the Discover tab.
#. ``docker-compose ps`` will show the status of the services and associated
#. ``docker ps`` will show the status of the containers

To reset the environment, stop and then remove the containers. A command for this is::

  docker-compose stop && docker-compose rm

After the install has progressed and the ``rebar-api-service`` is up in `Consul <http://127.0.0.1:8500>`_, the progress of the Admin container should be visible at http://localhost:3000.

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

Works on Linux environments that can run KVM.  It is **not compatible** with simultaneous VirtualBox / Vagrant testing.

These instructions assume that the Digital Rebar code has been linked to ~/rebar. To do this, run `-s ~/deploy/compose/components/rebar_api/digitalrebar/ rebar`

#. Install the prerequisites::

     apt-get install qemu-kvm libvirt-bin ubuntu-vm-builder bridge-utils ruby1.9.1-dev make
     gem install json net-http-digest_auth

#. Under ~/rebar/core, use ``tools/kvm-slave &`` to spawn a KVM virtual machine that will boot from the freshly-deployed admin node.

More details? See `virtual nodes <development/advanced-install/kvm-slaves.rst>`_ for testing using KVM.
..virtual nodes page no longer exists

Real Hardware
-------------

To boot Real Hardware, bind a physical interface to docker0 with brctl,
make sure that interface is up and does not have an address, and plug it
in to a switch that has the physical boxes that are to be booted.

Steps for booting:

  #. Install the prerequisites.
  #. (optional) To configure RAID or BIOS, the RackN Hardware workload is required.
     #. Clone the RackN Hardware workload.
     #. Download the required tools.  See `RackN Hardware Docs <https://github.com/rackn/hardware/blob/master/doc/README.md>`_ for instructions.
  #. Slave the eth2 to the Docker bridge.
  #. Turn on eth2 for the bridge.
  #. Boot the physical nodes from a switch connected to eth2

Sample code (includes optional step)::

  sudo apt-get install bridge-utils
  compose/workload.sh rackn hardware
  sudo brctl addif docker0 eth2
  sudo ip link set eth2 up

If omitting the optional step, leave out line 2.

Virtual Box (generally for Mac or Windows users)
------------------------------------------------

This approach simulates the same steps as metal, so it expects that a VM has been
created to host the Admin container.  If so, make sure an ethernet device has been
added (not up'd) to the VM that will be the admin network for slave VMs. Also,
if using vmware, E1000 Nics will be required and make sure the
network settings are set to "Allow" promiscuous mode.

If the development environment is running in VMs, the steps for this are as follows:

#. Make sure that the Admin VM has an extra eth port connected to a dedicated host only bridge (let's assume eth2)
#. Slave the eth2 to the Docker bridge.
#. Turn on eth2 for the bridge.
#. Create a VM with eth0
   #. It should be attached to the dedicated host only bridge
   #. Make sure it is able to network boot
#. Boot the VM.
   #. It should PXE boot.
   #. The VM should register and automatically progress in the system deployment.
   #. If there are issues, review the ``/var/log/install.log`` for details.

Sample code for this::

  sudo brctl addif docker0 eth2
  sudo ip link set eth2 up

Step 5. Install Workloads
~~~~~~~~~~~~~~~~~~~~~~~~~

From the Digital Rebar UI, use one of the Deployment Wizards to select roles to install on available nodes.  Once roles have been selected for nodes, the deployment must be "committed."


Configuration Options
"""""""""""""""""""""

The following options are available to be modified in the `group_vars/all.yml <https://github.com/rackn/digitalrebar-deploy/group_vars/all.yml>`_ file.  The file contains documentation for each variable, but additional detail is specified in the table below.

+---------------+----------+-----------+---------+
| *Key*         | *Values* | *Default* | *Notes* |
+---------------+----------+-----------+---------+
| dr_services   |          |           |         |
|               |          | jj        | jj      |
+---------------+----------+-----------+---------+
| dr_workload   | jj       | jj        |         |
+---------------+----------+-----------+---------+
