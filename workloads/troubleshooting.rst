.. _workloads_troubleshooting:

Troubleshooting
---------------

There are several possible failures when running Workload scripts.

No Response From Server
~~~~~~~~~~~~~~~~~~~~~~~

Digital Rebar requires HTTPS and accepting the self-signed certificate.

SSH Key
~~~~~~~

If having trouble getting the SSH keys to work correctly, include the ``--clean-ids`` flag in the script.  
html Rebar creates a unique SSH key for each node created; consequently, Rebar SSH IDs may sometimes be orphaned with the provider.  These can be safely removed with the Provider UI or CLI.

Provider Failure
~~~~~~~~~~~~~~~~

Provider node allocation sometimes fails.  In these cases, the annealer will be stuck waiting for a node that never completes.  For worker nodes, simply``destroy`` the node and processing will continue.  If the node was a master node, the whole deployment might have to be destroyed and rebuilt.

See :ref:`troubleshoot_providers` for details about testing provider configuration.

Script Failure
~~~~~~~~~~~~~~

If the script fails to complete after it has created the Digital Rebar Admin node and before it completed Admin configuration, retry the script by providing the ``--device-id`` instead of ``--deploy-admin``.  This will tell the script retry the Rebar Admin setup.