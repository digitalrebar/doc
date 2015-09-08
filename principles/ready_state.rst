Digital Rebar delivers "Ready State" infrastructure
===========================================

The following points focus on the unique aspects of the Digital Rebar Operations
Model. Unlike other Operating System Provisioning Tools (like Razor,
Foreman, Cobbler), Digital Rebar takes a systems perspective to physical
infrastracture management. Specifically, Rebar acknowledges that
successful deployment means connecting all the various operational
components together including NTP, DNS and (most critically) networking
from both the server and switch sides. We also believe there are no
"application islands" in production data centers: operators manage Ceph
and OpenStack as independent but connected applications. While a
coordinated system perspective is essential, we seek to complement and leverage
existing operational tools like Chef and Puppet.

This coordinated system perspective requires that actions take place in
controlled sequences both within and between data center components;
consequently, Rebar's heart is an orchestration platform designed for
physical hardware. Infrastructure has distinct challenges and needs that
are unique from other cloud focused orchestration and configuration
managment technologies. If we can solve these problems, then the general cloud focused
tools become even more effective in delivering their value to the operator. 

For this reason, we see Digital Rebar as complementary to application
provisioning tools like Fuel, Puppet, Chef, Juju, Salt or Ansible which
focus on application configuration post ready state. In these tools, the
community is working to capture the specific operational characteristics
of the applications. Rebar can be used to to simply provide ready state
or taken further to drive these tools at the system level. For example,
the OpenStack Chef Cookbooks lack the system orchestration that Rebar
provides but Juju includes. With that said, Juju lacks the ready-state capability and system-level awareness Digital Rebar posesses.

These are *not* OpenStack focused items. They are universal operations
concerns for any scale out application including OpenStack, Ceph, Docker
Hadoop, Cloud Foundry, Cloud Stack or others.

Key Points: \* configure RAID & BIOS systems (ideally, "late bound" so
target configuration is determined with application bring-up) \* in band
configuration using discovery images (as needed) \* out of band RAID &
BIOS - does not require systems to boot into discovery image for iDRAC
or iLO \* UEFI boot capable to handle > 2 TB drives \* IPv6 native \*
able to handle IPv6 communication \* setup IPv6 DNS records when nodes
are managed \* easier to change/reconfigure IPv4 \* Repeatable
server-side networking config \* able to use topology to setup bridges
and bonds \* able to correctly enumerate NICs over different hardware
types and configurations \* Operating System agnostic \* CMDB agnostic
(Chef & Chef Solo, Bash Scripts via SSH, Puppet, others possible) \*
DevOps configuration improves flexibly and reduces maintenance over
"golden" image based \* Rebar can deploy your golden images as you wish,
and even they can notify Rebar to change hardware configs, but they must
be part of the overall graph of attributes so that other workloads have
a say in hardware config.

Rebar’s key function ends up being orchestration, so it can plug in the
app provisioning tools to do their specific work. We tried to make Rebar
work as either "disolvable provisioning" or long term support.
Since Rebar uses SSH means there’s really no penalty for leaving Rebar
around and ready if you have to maintain the system; however, things
won’t crash if you stop using it. That was not true in v1 because we
relied on Chef Server to do everything.

Rebar is focused more on ready state because we’ve heard that is the
more universal problem. This time around, we really wanted to be able to use
community cookbooks – it was not productive to have Rebar only versions.
We do much better sharing operations knowledge in the
OpenStack/Ceph/Hadoop/etc communities and collaborating there. I think
Rebar brings a lot of operational value into those cookbooks but we
don’t want to force adoption in order to collaborate.
