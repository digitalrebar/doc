.. index::
	pair: Run-in-System; Troubleshooting

.. _troubleshoot_run_in_system:

Troubleshooting Run-In-System
-----------------------------

This section deals with the problems that arise when installing using ``./run-in-systems.sh``.

Install Will Not Start
======================
This section deals with what to do if the install will not start running.

If this occurs, be sure the install command is called with sudo as follows::

	sudo ./run-in-system.sh --deploy-admin=local --access=HOST --admin-ip=$IPA

The system may ask for the system's password at this point. Enter the password, and the install should begin to run.

Otherwise, the install will begin upon this command being given.

Permission Denied/Password Required
===================================
This section deals with the install failing due to a 'permission denied' or 'password required' error.


If an error appears, stating that a password is required or permission is denied, be sure the install command uses sudo as follows::
	
	sudo ./run-in-system.sh --deploy-admin=local --access=HOST --admin-ip=$IPA

This will fix the majority of issues regarding these failures, as it gives the install the access it needs to run properly.


Pull Compose Images Failure
===========================
This section deals with the following task::

	TASK [Pull compose images [SLOW]]

If this task fails, check the error message. If the error says "no space left on device," it is because that the device the install is being run on does not have enough memory. Free up some more room on the device, then run ``./run-in-system.sh`` again. The problem should be fixed. 

.. index::
	TODO; FOWARDER wait timeout solution

FOWARDER Wait Until Digital Rebar Service is Up
===============================================
This sections deals with the following task::

	TASK [FORWARDER wait until Digital Rebar service is up [1 upto 20 minutes]]

The install has been known to get stuck on this particular task. If this happens, the task will eventually timeout and fail. However, pressing `ctrl` and `c` simultaneously can force the task to halt. This is recommended if the step takes longer than 15 or so minutes, as it will save time.

The UX will not be accessible if this occurs. Please `contact support <https://gitter.im/digitalrebar/core?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge>`_ should this error occur.
