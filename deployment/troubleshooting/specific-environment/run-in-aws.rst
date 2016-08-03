.. index::
	TODO; Run-in-AWS Troubleshooting
	pair: Run-in-AWS; Troubleshooting
	
.. _troubleshoot_aws:

Troubleshooting Run-in-AWS 
--------------------------

This section will cover troubleshooting tips and solutions for installing onto an AWS Server. If an issue is not covered here, please see 

General Tips
============

If the install fails, check to be sure the install command was run with sudo as follows::

	sudo ./run-in-system.sh --deploy-admin=local --access=HOST --admin-ip=$IPA

``./run-in-system`` has been known to be finicky about thi, so this may fix the issue. If it does not, see the sections below. 

