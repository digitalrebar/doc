Digital Rebar Directory Structure
=================================

A complete Digital Rebar installation consists of a **core** component,
and optional workloads (such as **kubernetes**, **ceph**, **hardware**). 

The workloads each have their own GIT repository. The Digital
Rebar **core** repository is the essential engine that drives Digital
Rebar and can operate alone from any of the workload components. The
workload components of Digital Rebar have built-in dependencies on the
**core**.  Workloads are not required to be part of the Digital Rebar project to run on the framework.

Digital Rebar core directory layout
-----------------------------------

The directory structure of the **core** consists of these parts under
the */opt/digitalrebar/core* directory:

+-----------------+-----------------------------------------------------------------------------+
| Sub-Directory   | Description of Contents                                                     |
+=================+=============================================================================+
| BDD             | Business Driven Development Testing Infrastructre                           |
+-----------------+-----------------------------------------------------------------------------+
| barclamps       | Metadata that for barclamps which drive workload deployment                 |
+-----------------+-----------------------------------------------------------------------------+
| bin             | Digital Rebar executables and helper files                                  |
+-----------------+-----------------------------------------------------------------------------+
| bootstrap       | Utility files used to ready the **core** for operation                      |
+-----------------+-----------------------------------------------------------------------------+
| clients         | API clients applications                                                    |
+-----------------+-----------------------------------------------------------------------------+
| etc             | Target deployment platform Digital Rebar stop/start scripts                 |
+-----------------+-----------------------------------------------------------------------------+
| jig - chef      | The **core** cookbook recipes for Digital Rebar node-role drivers           |
+-----------------+-----------------------------------------------------------------------------+
| jig - noop      | Support infrastructure for the **no-op** jig                                |
+-----------------+-----------------------------------------------------------------------------+
| jig - script    | Support for the **script** jig                                              |
+-----------------+-----------------------------------------------------------------------------+
| rails           | core only ruby-on-rails infrastructure support tools and utilities          |
+-----------------+-----------------------------------------------------------------------------+
| rails-engines   | ruby-on-rails support for workload deployment                               |
+-----------------+-----------------------------------------------------------------------------+
| setup           | Tools and utilities to help get Digital Rebar bootstrapped                  |
+-----------------+-----------------------------------------------------------------------------+
| sledgehammer    | Contains the utilities used to generate the PXE boot image                  |
+-----------------+-----------------------------------------------------------------------------+
| smoketest       | Automated self-test validation drivers                                      |
+-----------------+-----------------------------------------------------------------------------+
| test            | Additional role test facilities                                             |
+-----------------+-----------------------------------------------------------------------------+
| tools           | Tools used to enable the *admin* node to manage OS installed slaves         |
+-----------------+-----------------------------------------------------------------------------+
| updates         | Merge tools                                                                 |
+-----------------+-----------------------------------------------------------------------------+

Role configuration information is located within the jig infrastructure.
