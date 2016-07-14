.. _emergent_services:

Emergent Services
-----------------

We see data center operations as a duel between conflicting priorities.
On one hand, the environment is constantly changing, and systems must
adapt quickly to these changes. On the other hand, users of the
infrastructure expect it to provide stable and consistent services for
consumption. We have described that as “always ready, never finished.”

To address this duality, the infrastructure that Digital Rebar
builds is decomposed into well-defined service layers that can then be
(re)assembled dynamically. Rather than require any component of the
system to be in a ready state, Digital Rebar design principles assume that we
can automate the construction of every level of the infrastructure from
BIOS to network and application. Consequently, we can hold off
(re)making decisions at the bottom levels until we have figured out what
we are doing at the top.

Effectively, we allow the overall infrastructure services configuration
to evolve or emerge based on the desired end use. These concepts are
built on computer science principles that we have appropriated for Ops
use. Since we also subscribe to Chef's “Infrastructure-As-Code”, we
believe that these terms fit well in a DevOps environment. In the
next few pages, we will explore the principles behind this approach, including
the concepts surrounding simulated annealing, late binding, attribute injection,
and emergent design.

Emergent (aka iterative or evolutionary) design challenges the
traditional assumption that all factors must be known before starting.***

-  Dependency graph – multidimensional relationship
-  High degree of reuse via abstraction and isolation of service
   boundaries.
-  Increasing complexity of deployments means more dependencies
-  Increasing revision rates of dependencies but with higher stability
   of APIs
