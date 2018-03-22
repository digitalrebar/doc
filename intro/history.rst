
.. note:: WARNING WARNING WARNING:  This is the Digital Rebar v2 product documentation.  The v2 version is EOL as of September 2017.  Please refer to the new Digital Rebar Provision v3 documentation:  http:\/\/provision.readthedocs.io\/en\/tip\/README.html

.. _history:

History
=======

While it has been completely rebuilt by DevOps artisans, Digital Rebar history includes years of battle-tested ops learnings by the `Crowbar Project <http://github.com/crowbar>`_ founders.

.. index::
  History; Crowbar
  History; OpenCrowbar
  Crowbar; History
  OpenCrowbar; History

Lessons from Crowbar v1
-----------------------

It was 2011, the dawn of the OpenStack Era, and the Digital Rebar founders, at Dell, were already battle weary from trying to make repeatable installs around Azure, Eucalyptus, Joyent, and Hadoop.  The simple reality is that there was no success pattern that we could follow deploying any one of those platforms and certainly none cross-platform.  Even though all used basically the same compute and network infrastructure, they each had custom deployment code and configuration approaches.  We jumped on being an OpenStack founding partner as a way to try to break the failure pattern.

What was failing? Each platform had deeply embedded environmental assumptions that were not repeatable or portable.

For example, one of those platforms required thirty (30!) full racks of gear and tethering back to the master deployer because their management and topology was hard wired into their infrastructure.  Others were not much better: installation was often “ssh apt-get install platform” then “scp pre-built configuration files.” Even worse, those steps were always proceeded with 30 pages of prescriptive manual system prep steps that were updated daily.

Incorrectly, we believed that the solution was to create a better installer for OpenStack.

The Crowbar project, which is still used by SUSE, created a fully integrated install sequence from PXE boot and discovery to testing the final OpenStack installation.  We could build a cloud on a complete rack of gear from boxes in minutes.  The open source project even used open tools like Chef and hardware agnostic options to increase its community appeal.  As the first installer (it even pre-dates DevStack), the project was widely used in early OpenStack evaluations.

Despite that success, as a v1 technology Crowbar’s major shortcoming was that it tightly coupled components and services together.  That made the installation and management process very rigid and non-conforming to disparate operational models and environments.

Our install scars showed us the real battle lines that prevented portability.  Even minor infrastructure variations resulted in broken or site-specific configuration.  A major part of the challenge is that variation is not neatly contained; instead, it is spread throughout the environment.  We needed to create automation that could both cope with heterogeneity across the community and be change tolerant after installation to enable upgrades.

We came to accept that there is no single installer.  Instead, scalable installers must assume that they will interoperate with other parts of the system in a coordinated way because the diversity of options makes it impossible for them to control everything.  In fact, we've seen that smaller composable install steps are much easier to automate consistently.  Even more importantly, smaller steps make it possible to manage system-wide upgrades in a controllable way.

Asking for an “easy button” installer is the wrong question.  Instead, let’s ask “can we create sharable components that can be automated in multiple ways?”

There's no universal installation script to create cloud rainbows; however, there are strategies that we can use to make individual projects installable over a wide range of options.  These approaches include composability, consistent configuration and use of standard tools and patterns for operation.  These items help projects focus on their own concerns and allow operators to apply best practice techniques.

From OpenCrowbar to Digital Rebar
---------------------------------

The original 2014 fork of Crowbar v2 was called OpenCrowbar.  This was done to allow SUSE to continue working in the original Crowbar repositories.  They have continued to maintain Crowbar as their OpenStack installer.  As OpenCrowbar features and methodogy diverged significantly from Crowbar, there was naming confusion for the community.

In 2015, we made the decision to both rename the project and make a substantial refactoring effort towards containers and microservices.  Combining both efforts created a very clean break between the original Crowbar code base and Digital Rebar.

Where OpenCrowbar had significant installation similarities with Crowbar, Digital Rebar is a very different application architecture.
