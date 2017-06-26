.. index::
  Attribute; Injection

.. _attribute_injections:

Attribute Injection
-------------------

Attribute Injection is an essential aspect of the "FuncOps" story that helps clean the boundaries needed to implement consistent
scripting behavior between divergent sites.

It also allows Digital Rebar to abstract and isolate provisioning layers.  This
operational approach means that deployments are composed of layered
services (see :ref:`emergent_services`) instead of locked "golden" images.  The
layers can be maintained independently and allow users to compose
specific configurations *a la carte*.  This approach works if the layers
have clean functional boundaries (FuncOps) that can be scoped and
managed atomically.

To explain how Attribute Injection accomplishes this, we need to explore
why search became an anti-pattern in Crowbar v1.  Originally, being able to
use server based search functions in operational scripting was a
critical feature.  It allowed individual nodes to act as part of a system
by searching for global information needed to make local decisions.  This
greatly added to Crowbar's mission of system level configuration; however, it
also created significant hidden interdependencies between scripts.  As
Crowbar v1 grew in complexity, searches became more and more difficult to
maintain because they were difficult to correctly scope, hard to
centrally manage, and prone to timing issues.

Digital Rebar is not unique in dealing with this problem.  The Attribute
Injection pattern has become a preferred alternative to search in
integrated community cookbooks.

Attribute Injection in Digital Rebar works by establishing specific
inputs and outputs for all state actions (NodeRole runs).  By declaring
the exact inputs needed and the outputs provided, Digital Rebar can better manage
each annealing operation.  This control includes deployment scoping
boundaries, time sequences of information, and the override or substitution of inputs based on the execution paths.

This concept is not unique to Digital Rebar.  It has become the best practice for
operational scripts.  Digital Rebar simply extends the paradigm to both the system and orchestration levels.

Attribute Injection enabled operations to be:

-  *Atomic*: Only the information needed for the operation is provided, so
   risk of "bleed over" between scripts is minimized.  This is also a
   functional programming preference.

-  *Isolated Idempotent*: The risk of accidentally picking up changed
   information from previous runs is reduced by controlling the inputs.
   This makes it more likely that scripts can be idempotent.

-  *Cleanly Scoped*: System deployment boundaries can be used in place of search parameters to limit information passed into operations.  This allows the orchestration to manage when and how information is added into configurations.

-  *Easy to troubleshoot*: Since the information is limited and
   controlled, recreating runs for troubleshooting is easier.  This
   has substantial value for diagnostics.
