.. _op_principles:

Operational Principles
======================

The operational model behind Digital Rebar is entering its third generation and
its important to understand the principles behind that model.  The model
is critical because it shapes how Rebar approaches the infrastructure at
a fundamental level.  The experience makes it easier to interact with the platform
as it influences our approach to operations.  Rebar’s goal is to create
emergent services.

The topics in this guide help explain Digital Rebar's core architectural
principles.


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
:ref:`simulated_annealing` and networking model. These
backgrounds heavily influenced how we approached Rebar.

First, we started with best of field DevOps infrastructure: Opscode
Chef. There was already a remarkable open source community around this
tool and an enthusiastic following for cloud and scale operators . Using
Chef to do the majority of the installation left the Rebar team to focus
on infrastructure provisioning.

Key Features of Digital Rebar
-----------------------------

-  *Heterogeneous Operating Systems*: Rebar has the ability to adapt to whatever operating system is desired.
-  *CMDB Flexibility*: Using Rebar does not require being locked into a DevOps toolset.
-  *Attribute injection*: Rebar allows for clean abstraction boundaries, thus the use of multiple tools (think Chef and Puppet playing together) is possible.
-  *Ops Annealer*: The orchestration at Rebar’s heart combines the best
   of directed graphs with late binding and parallel execution. We
   believe annealing is the key ingredient for repeatable and OpenOps
   shared code upgrades.
-  *Upstream Friendly*: Infrastructure as code works best as a
   community practice, and Rebar uses upstream code without injecting the “rebarisms” that were previously required. Therefore,
   knowledge can be shared to the broader DevOps community, even if they do not use Rebar.
-  *Node Discovery (or not)*: Rebar maintains the same proven discovery
   image based approach that we used before, but we have streamlined and
   expanded our approach. Rebar’s APIs can be used outside of the PXE discovery
   system to accommodate Docker containers, existing systems, and VMs.
-  *Hardware Configuration*: Rebar maintains the same optional hardware
   neutral approach to RAID and BIOS configuration. Configuring hardware
   with repeatability is difficult and requires much iterative testing.
   While our approach is open and generic, the team works hard
   to validate on a specific set of gear. It is impossible to make
   statements beyond that test matrix.
-  *Network Abstraction*: Rebar has dramatically extended our DevOps
   network abstraction. We have learned that networking is the key to
   success for deployment and upgrade, so we have made Rebar networking
   flexible and concise. Rebar networking works with attribute injection
   so that hardwiring networking into DevOps scripts can be avoided.
-  *Out of band control*: When the Annealer hands off work, Rebar gives
   the worker implementation flexibility to do it on the node (using
   SSH) or remotely (using an API). Making agents optional means that
   operators and developers are allowed to make the best choices for the actions that
   they need to take.
-  *Technical Debt Paydown*: We have also updated the Rebar
   infrastructure to use the latest libraries like Ruby 2, Rails 4, and Chef
   11. Even more importantly, we have dramatically simplified the code
   structure, including in repo documentation and a Docker based
   developer environment that makes building a working Rebar environment
   fast and repeatable.

Digital Rebar vs Crowbar/OpenCrowbar
------------------------------------

Back before Rebar, we founded the Crowbar Project while working for Dell. Since Crowbar was an "MVP" and is still being actively developed by SUSE and focuses solely on installing OpenStack, splitting the repositories allow both versions to progress with less confusion. This new generation is structurally and philosophically different from Crowbar, and we have invested substantially in expanding the extensibility of the architecture, refactoring the tooling, paying down the technical debt, and cleaning up the documentation.

Digital Rebar Concepts
----------------------

.. toctree::
   :maxdepth: 1
   :glob:

   concepts/*
