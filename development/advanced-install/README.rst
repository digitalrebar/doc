Dev System Configuration
========================

Installation and Configuration Overview - What you'll be doing:
---------------------------------------------------------------

1. Install the base OS
2. Configure base OS for running Rebar
3. git clone https://github.com/digitalrebar/core
4. Start rebar in a Docker container
5. Deploy slave nodes and Hack away!

Prereqs
-------

Before we begin, let's review what you'll need (or end up with after
following these docs):

-  A Linux development environment (running on bare metal or VirtualBox)
-  Internet Access
-  Your own user (NOT ROOT)
-  Several Networks:
-  Digital Rebar relies on a few private networks - they can all be on the same
   NIC, bridges, or whatever.
-  Recommended: a local caching proxy server - we download a lot.

OK, let's get started setting up the development environment:
=============================================================

Step 1: What's your platform?
-----------------------------

Virtual Machine Platform Configs
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

-  `VirtualBox <virtualbox.md>`__ based installations - network configs
   and basic install info
-  `KVM on Ubuntu <kvm-ubuntu.md>`__
-  `KVM on Fedora Core 19 <kvm-fedora.md>`__

Bare Metal Platform Configs (must be Linux)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

-  Just start with the O/S configs below for your favorite flavor.

Step 2: Now Let's Configure Your Development OS
-----------------------------------------------

Get the docker stuff all configured properly:

-  `Ubuntu 12.04.03 <dev-ubuntu-12.04.03.md>`__
-  [CentOS 6.5]
-  [Fedora Core 19]
-  `SUSE <dev-vm-SUSE.md>`__
-  `OpenSUSE Images <dev-openSUSE-images.md>`__

Step 3: Big important step - Setup Docker Admin Node
----------------------------------------------------

1. follow steps in `docker-admin.md <docker-admin.md>`__

Step 4: Deploy Nodes!
---------------------

Now that you've got Digital Rebar installed, it's time to look in the
`Deployment Guide <../../deployment-guide/README.md>`__ for instructions
about provisioning nodes.

Important - once you're in the Docker container, you need to change to
Digital Rebar user 1. ``su - rebar`` to gain ruby-2.0 and control Rebar via the
CLI! 1. we've provided a handle ``tools/rails-console`` command if you
want to reach deep into the bowels of the bunny.
