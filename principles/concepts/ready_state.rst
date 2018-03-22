
.. note:: WARNING WARNING WARNING:  This is the Digital Rebar v2 product documentation.  That product line is EOL as of September 2017.  Please refer to the new Digital Rebar Provision v3 documentation:  http:\/\/provision.readthedocs.io\/en\/tip\/README.html

.. _ready_state:

Digital Rebar delivers "Ready State" infrastructure
===================================================

The following points focus on the unique aspects of the Digital Rebar Operations
Model.  Unlike other Operating System Provisioning Tools (such as Razor,
Foreman, and Cobbler), Digital Rebar takes a systems perspective to physical
infrastructure management.  Specifically, Rebar acknowledges that
successful deployment means connecting all the various operational
components together including NTP, DNS and (most critically) networking
from both the server and switch sides.  We also believe there are no
"application islands" in production data centers, thus the operators manage Ceph
and OpenStack as independent but connected applications.  While a
coordinated system perspective is essential, we seek to complement and leverage
existing operational tools like Chef and Puppet.

This coordinated system perspective requires that actions take place in
controlled sequences both within and between data center components.
Consequently, at Rebar's heart is an orchestration platform designed for
physical hardware.  Infrastructure has distinct challenges and needs that
are unique from other cloud focused orchestration and configuration
management technologies.  If we can solve these problems, then the general cloud focused
tools become even more effective in delivering their value to the operator.

For this reason, we see Digital Rebar as complementary to application
provisioning tools such as Fuel, Puppet, Chef, Juju, Salt or Ansible, which
focus on application configuration post ready state.  In these tools, the
community is working to capture the specific operational characteristics
of the applications.  Rebar can be used to simply provide ready state, or it can be taken further to drive these tools at the system level.  For example,
the OpenStack Chef Cookbooks lack the system orchestration that Rebar
provides but Juju includes.  However, Juju lacks the ready-state capability and system-level awareness that Digital Rebar possesses.

These concerns are not OpenStack focused items.  Rather, they are universal operations
concerns for any scale out application, including OpenStack, Ceph, Docker
Hadoop, Cloud Foundry, Cloud Stack and others.

Key points of the model:

- *Configuration of RAID & BIOS systems*: Ideally, they will be "late bound," so that target configuration is determined with application bring-up.
- In band configuration using discovery images (as needed)
- *Out of band RAID & BIOS*: It does not require systems to boot into discovery image for iDRAC or iLO.
- UEFI boot capable of handling > 2 TB drives
- IPv6 native
- Able to handle IPv6 communication
- Setup IPv6 DNS records when nodes are managed
- Easier to change/reconfigure IPv4
- Repeatable server-side networking configuration
- Able to use topology to setup bridges and bonds
- Able to correctly enumerate NICs over different hardware types and configurations
- *Operating System and CMDB agnostic*: It is possible to use Chef & Chef Solo, Bash Scripts via SSH, Puppet, and others.
- DevOps configuration improves flexibly and reduces maintenance over "golden" image based.
- Rebar can deploy the golden images as is wished, and the images can notify Rebar to change hardware configurations.  However, they must be part of the overall graph of attributes so that other workloads have a say in hardware configurations.

Rebar’s key function ends up being orchestration, so it can plug in the
app provisioning tools to do their specific work.  We tried to make Rebar
work as either "dissolvable provisioning" or long term support.
Since Rebar uses SSH, there is minimal penalty for leaving Rebar
around and ready in the event of system maintenance.  However, things
will not crash if Rebar is not in use.  This was not true in v1 because we
relied on Chef Server to do everything.

Since we have heard that one of the most universal of problems is the ready state, Rebar focuses on this.  With this version, we wanted to be able to use community cookbooks because it was unproductive to have Rebar only versions.
We do much better sharing operations knowledge in the
OpenStack/Ceph/Hadoop/etc communities and collaborating there.  We believe that
Rebar brings a lot of operational value into those cookbooks, but we
do not want to force adoption in order to collaborate.
