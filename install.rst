Digital Rebar Install
=====================

The fast-path install steps are:

1. Install Docker
#. Download Code & Prerequists (operating systems to install)
#. Deploy Admin container
#. Provision Nodes! (just testing? use fast virtual nodes)

Rather than cover every operating system, we are assuming that you can translate between differences in major distributions.

**RECOMMENDATION:** Review the `RackN maintained deploy scripts <https://github.com/rackn/digitalrebar-deploy>`_ for updated step-by-step install examples.

Admin In a Container!
---------------------

The goal for this document is getting a basic Digital Rebar admin running quickly.  For that reason, many options and configuration choices have been omitted in the interest in brevity.

Digital Rebar operates the administrative functions in Docker containers; consequently, you need to be running in an environment that can run Docker.

    To improve support, the `Digital Rebar team <https://github.com/orgs/digitalrebar/teams>`_ is no longer creating or documenting install packages.

    For developers, we've collected some `additional guidance <development/advanced-install>`_ to review after you've got your first install working.

We are going to assume that you know how to use basic Docker commands to keep these instructions concise.

Step 1. Install Docker
----------------------

Follow the `community instructions for installing Docker <http://docs.docker.io/en/latest/installation/>`_ on the most common Linux
distributions.

- Get permission to run Docker without sudo. [1]_
- Turn off Apparmor [2]_ (`production deploy <deployment/>`_ could be configured to leave on)
- Map a local address (192.168.124.4/24) to the docker bridge. [7]_

Step 2. Download Code & Prerequists
-----------------------------------

- Configure your no_proxy environment variable [3]_ (really, add it to .bashrc)
- Make sure you have an ssh key [4]_
- Enable passwordless sudo [5]_
- Download at least one ISO from the list in `provisioner.yml <https://github.com/digitalrebar/core/blob/develop/barclamps/provisioner.yml#L135>`_ and copy to ``~/.cache/opencrowbar/tftpboot/isos``
- Install git.
- If you plan to run VMs as test nodes, then you'll also need "qemu-kvm libvirt-bin ubuntu-vm-builder bridge-utils ruby1.9.1-dev make"
- Clone Digital Rebar core
  - You *must* "git clone https://github.com/digitalrebar/core.git"
- If you add workloads, they need to be in sibling directories to the core.  For example, "../workload1" or "../company/workload2"
   - `Kubernetes <https://github.com/rackn/kubernetes>`_
   - `Ceph <https://github.com/rackn/ceph>`_
   - `Hardware <https://github.com/rackn/hardware>`_
   - By request: StackEngine, DockerEngine, CloudFoundry BOSH Metal CPI


Step 3. Deploy Admin container
-------------------------------

From the Digital Rebar core directory, run the ``tools/docker-admin`` command. [6]_ 

The ``docker-admin`` flags are:

1. ``--daemon``   (optional, omit this flag to keep your terminal in the container)
#. ``centos``     (required, the container O/S)
#. ``./production.sh`` (required, the script to start in the container)
#. ``pick.valid.fqdn`` (required, name of admin server for production.sh script)

After the install has progressed, you should be able to monitor the progress of the admin node deployment at http://localhost:3000. Once the admin node is finished deploying (or
if anything goes wrong), you will be left at a running shell inside the
container unless you used the --daemon flag.

You can ssh into the container from the host by finding its IP address
through Docker or 192.168.124.10 if you've mapped a host address to docker0.

Step 4. Provision Nodes!
------------------------

KVM Nodes (fast test)
~~~~~~~~~~~~~~~~~~~~~

If your environment is running on bare metal (as opposed to
running inside a VM), you can spawn `virtual nodes <development/advanced-install/kvm-slaves.rst>`_ for testing using.  Use ``tools/kvm-slave &`` to spawn a KVM
virtual machine that will boot from the freshly-deployed admin node.

Real Hardware
~~~~~~~~~~~~~

To boot Real Hardware, bind a physical interface to docker0 with brctl,
make sure that interface is up and does not have an address, and plug it
in to a switch that has the physical boxes you want to boot.

Example Commands: 1. slave the eth2 to the docker bridge,
``sudo brctl addif docker0 eth2`` 1. turn on eth2 for the bridge,
``sudo ip link set eth2 up`` 1. boot the physical nodes from a switch
connected to eth2

Virtual Box (generally for Windows users)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

    This approach expects that you've created a VM to host the
    Admin container.  If so, make sure you added an ethernet device (not
    up'd) to your VM that will be the admin network for slave VMs. Also,
    if using vmware, you'll need to use E1000 Nics and make sure your
    network settings are set to "Allow" promiscuous mode.

If your development environment is running in VMs then:

1. make sure that your Admin VM has an extra eth port connected to a
   dedicated host only bridge (let's assume eth2)
2. slave the eth2 to the docker bridge,
   ``sudo brctl addif docker0 eth2``
3. turn on eth2 for the bridge, ``sudo ip link set eth2 up``
4. create a VM with eth0

   1. attached to the dedicated host only bridge
   2. make sure it is able to network boot

5. boot the VM

   1. it should PXE boot
   2. the VM should register and automatically progress in the system
      deployment
   3. if you have issues, review the ``/var/log/install.log`` for
      details

Additional References
---------------------

**WARNING**: These suggestions may become out of date.  We strongly recommend reviewing the actively maintained `deploy scripts <https://github.com/rackn/digitalrebar-deploy>`_.

.. [1] ``sudo usermod -a -G docker <your-user>``
   plus, if you don't want to reboot, run ``sudo chmod 666 /var/run/docker.sock``
.. [2] ``sudo service apparmor teardown`` and ``sudo update-rc.d -f apparmor remove``
.. [3] ``export no_proxy="127.0.0.1,[::1],localhost,192.168.124.0/24,172.16.0.0/12"``
.. [4] ``ssh-keygen -t rsa``
.. [5] ``sudo sed -ie "s/%sudo\tALL=(ALL:ALL) ALL/%sudo ALL=(ALL) NOPASSWD:ALL/g" /etc/sudoers``
.. [6] ``tools/docker-admin --daemon centos ./production.sh admin.rebar.digital``
.. [7] ``sudo ip a add 192.168.124.4/24 dev docker0``