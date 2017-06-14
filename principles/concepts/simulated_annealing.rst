.. index::
	Concepts; Annealing
	Annealer; Concepts

.. _simulated_annealing:

Simulated Annealing
-------------------

See also: :ref:`ux_annealer`

Simulated Annealing is a modeling strategy from computer science that
seeks optimal or stable outcomes through iterative analysis.  A
physical analogy for this is the process of strengthening steel by repeatedly
heating, quenching and hammering.  In both computer science and
metallurgy, the process involves evaluating state, taking action,
factoring in new data, and then repeating.  Each annealing cycle improves
the system, even though we may not know the final target state.

Annealing is well suited for problems where there is no mathematical
solution, there’s an irregular feedback loop, or the datasets change over
time.  We have all three challenges in continuous data center operations
environments.  While it is clear that a deployment can be modeled as a directed
graph (a mathematical solution) at a specific point in time, the reality
is that there are too many unknowns to have a reliable graph.  The
problem is compounded because of unpredictable variance in hardware (NIC
enumeration, drive sizes, BIOS revisions, network topology, etc) that prove more challenging if we factor in adapting to failures.  Essentially, an operating
infrastructure is a moving target that is hard to model predictively.

Digital Rebar implements the simulated annealing algorithm by decomposing the
operations infrastructure into atomic units, known as node-roles (see :ref:`api_node_role`), that perform the smallest unit of work definable.  Some or all of these node-roles
are changed whenever the infrastructure changes.  Digital Rebar anneals the
environment by exercising the node-roles in a consistent way until
system re-stabilizes.

One way to visualize Digital Rebar annealing is to imagine children who have to
cross a field but do not have a teacher to coordinate them.  One student takes
a step forward and looks around.  Another then sees the first and takes
two steps.  Each child advances based on what their classmates are doing.  None of them
want to get too far ahead or to be left behind.  The line progresses
irregularly but consistently based on the natural relationships within
the group.

To understand the Digital Rebar Annealer, we have to break it down into three
distinct components: deployment timeline, annealing, and node-role state.
The deployment timeline represents externally (user, hardware, etc)
initiated changes that propose a new target state.  Once that new target
is committed, Digital Rebar anneals by iterating through all the node-roles in a
reasonable order.  As the Annealer runs the node-roles, they update their
own state.  The aggregate state of all the node-roles determines the
state of the deployment.

In Digital Rebar, a deployment is a combination of user and system defined state.  Digital Rebar’s
job is to stabilize the deployments and then maintain the desired configuration over time.

