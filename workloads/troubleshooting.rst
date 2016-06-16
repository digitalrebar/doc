.. _workloads_troubleshooting:

Troubleshooting
---------------

There are several possible failures when running Workload scripts.

No Response From Server
~~~~~~~~~~~~~~~~~~~~~~~

Digital Rebar requires HTTPS and accepting the self-signed certificate.

SSH Key
~~~~~~~

If you are having trouble getting your SSH keys to work correctly, you may need to include the ``--clean-ids`` flag in the script.  
html
Rebar creates a unique SSH key for each node created; consequently, you may also have orphaned Rebar SSH IDs with your provider.  These can be safely removed with the Provider UI or CLI.

Provider Failure
~~~~~~~~~~~~~~~~

Provider node allocation sometimes fails.  In these cases, the annealer will be stuck waiting for a node that never completes.  For worker nodes, you can simply ``destroy`` the node and processing will continue.  If the node was a master node, you may need to destroy the whole deployment and retry.

See :ref:`troubleshoot_providers` for details about testing provider configuration.

Script Failure
~~~~~~~~~~~~~~

If the script fails to complete after it has created the Digital Rebar Admin node and before it completed Admin configuration, you can retry the script by providing the ``--device-id`` instead of ``--deploy-admin``.  This will tell the script retry the Rebar Admin setup.