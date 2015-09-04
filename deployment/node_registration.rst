Node Registration Process
-------------------------

Digital Rebar uses its API to creates nodes and bind their initial NodeRoles
(generally No-Op roles).

Use the following steps to register a new node in the system and add
under Digital Rebar management. These steps are automatically used by the PXE
discovery image (Sledgehammer) when Nodes are detected during their
initial boot.

1. POST to ``/api/v2/nodes`` to create a basic Node object. This will
   not have any roles bound to it nor will it have any addresses from
   the admin network assigned to it. The node will neither be alive nor
   available.
2. in the CLI, use ``rebar nodes create ...``

3. (Optional) PUT any node-specific hints that may be needed for the
   bootstrap process, including node MAC addresses or your suggested IP
   address.

4. POST to ``/api/v2/node_roles`` to bind default roles to the node.
   Binding rebar-admin-node will result in the node having all the roles
   needed for it to act as an admin node and a rebar-managed-node will
   bind all the roles needed for the Sledgehammer discovery process to
   work.
   
5. in the CLI, use ``rebar nodes [node] bind [role]``

6. (Optional) PUT any node-specific attrib updates to the node.

7. PUT to ``/api/v2/nodes/[node-key]/commit`` to move all the node's
   NodeRoles from PROPOSED to TODO, and mark the node as available (but
   still not alive).

8. PUT to ``/api/v2/nodes/[node-key]/alive`` to make the node as alive
   so processing can start.

    An example of this process is implemented in the ``production.sh``
    script in the root of the Digital Rebar repo.
