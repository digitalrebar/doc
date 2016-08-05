.. index::
	TODO; Troubleshooting Run-in-Google
	pair: Run-in-Google; Troubleshooting

.. _troubleshoot_google:

Troubleshooting Run-in-Google
-----------------------------

This section will cover troubleshooting tips and solutions for installing to Google. For a complete guide on installing in Google, see :ref:`run_in_google`.

FORWARDER Times Out
*******************

This section deals with the following task and subsequent timeout failure::

	TASK [FORWARDER wait until Digital Rebar service is up [1 upto 20 minutes]]

When installing to the cloud, running in FORWARDER mode is not recommended. Instead, it is recommended to run in HOST mode. This can be done by adding ``--access=HOST`` to the ``./run-in-system.sh`` command, as is done in the example code in the :ref:`run_in_google` guide. 

If the install is run in FORWARDER mode, the FORWARDER will likely timeout. Thus, if the install appears to be stuck on this step, `CTRL+C` can be used to abort the task, which can save some time. After the task fails or is aborted, add the system's internal IP address to docker0 with the command ``ip addr add [int_IP] dev docker0``, where [int_IP] is replaced with the system's internal IP. When this is done, the install can be executed again and should run without error.