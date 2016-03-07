Operational Principles
======================

The operational model behind Digital Rebar is entering its third generation and
its important to understand the principles behind that model. The model
is critical because it shapes how Rebar approaches the infrastructure at
a fundamental level so it makes it easier to interact with the platform
if you see how we are approaching operations. Rebar’s goal is to create
emergent services.

The topics in this guide help explain Digital Rebar's core architectural
principles.


.. toctree::
   :maxdepth: 1
   :glob:
   
   *

Design Objective
----------------

Digital Rebar delivers repeatable best practice deployments. Rebar is not just
about installation: we define success as a sustainable operations model
where we continuously improve how people use their infrastructure. The
complexity and pace of technology change is accelerating so we must have
an approach that embraces continuous delivery in the data center.

Rebar’s objective is to help operators and technology become more efficient, stable and
resilient over time.

Background
----------

When Greg Althaus (github @GAlthaus) and Rob "zehicle" Hirschfeld
(github @Zehicle) started the project, we had some very specific
targets in mind. We’d been working towards using organic emergent
swarming (think ants) to model continuous application deployment. We had
also been struggling with the most routine foundational tasks (bios,
raid, o/s install, networking, ops infrastructure) when bringing up
early scale cloud & data applications. Another key contributor, Victor
Lowther (github @VictorLowther) has critical experience in Linux
operations, networking and dependency resolution that lead to made
significant contributions around the
`Annealing <simulated_annealing.md>`__ and networking model. These
backgrounds heavily influenced how we approached Rebar.

First, we started with best of field DevOps infrastructure: Opscode
Chef. There was already a remarkable open source community around this
tool and an enthusiastic following for cloud and scale operators . Using
Chef to do the majority of the installation left the Rebar team to focus
on infrastructure provisioning. 

Key Features of Digital Rebar
-----------------------------

-  *Heterogeneous Operating Systems* – chose which operating system you
   want to install on the target servers.
-  *CMDB Flexibility* – don’t be locked in to a devops toolset.
-  *Attribute injection* - allows clean abstraction boundaries so you can
   use multiple tools (Chef and Puppet, playing together).
-  *Ops Annealer* –the orchestration at Rebar’s heart combines the best
   of directed graphs with late binding and parallel execution. We
   believe annealing is the key ingredient for repeatable and OpenOps
   shared code upgrades
-  *Upstream Friendly* – infrastructure as code works best as a
   community practice and Rebar use upstream code without injecting “rebarisms” that were previously required. So you
   can share your learning with the broader DevOps community even if
   they don’t use Rebar.
-  *Node Discovery (or not)* – Rebar maintains the same proven discovery
   image based approach that we used before, but we’ve streamlined and
   expanded it. You can use Rebar’s API outside of the PXE discovery
   system to accommodate Docker containers, existing systems and VMs.
-  *Hardware Configuration* – Rebar maintains the same optional hardware
   neutral approach to RAID and BIOS configuration. Configuring hardware
   with repeatability is difficult and requires much iterative testing.
   While our approach is open and generic, the team works hard
   to validate a on specific set of gear: it’s impossible to make
   statements beyond that test matrix.
-  *Network Abstraction* – Rebar dramatically extended our DevOps
   network abstraction. We’ve learned that a networking is the key to
   success for deployment and upgrade so we’ve made Rebar networking
   flexible and concise. Rebar networking works with attribute injection
   so that you can avoid hardwiring networking into DevOps scripts.
-  *Out of band control* – when the Annealer hands off work, Rebar gives
   the worker implementation flexibility to do it on the node (using
   SSH) or remotely (using an API). Making agents optional means allows
   operators and developers make the best choices for the actions that
   they need to take.
-  *Technical Debt Paydown* - We’ve also updated the Rebar
   infrastructure to use the latest libraries like Ruby 2, Rails 4, Chef
   11. Even more importantly, we’re dramatically simplified the code
   structure including in repo documentation and a Docker based
   developer environment that makes building a working Rebar environment
   fast and repeatable.

Digital Rebar vs Crowbar/OpenCrowbar
------------------------------------

Some of you may remember us from our Dell days (we've all since left and founded, RackN) when we founded the Crowbar Project. Since Crowbar was an "MVP" and is still being actively developed by SUSE and focuses solely on installing OpenStack, splitting the repositories allow both versions to progress with less confusion. This new generation is structurally and philosphically different from Crowbar and we’ve investing substantially in expanding the extensibility of the architecture, refactoring the tooling, paying down technical debt and cleanup up documentation. 
