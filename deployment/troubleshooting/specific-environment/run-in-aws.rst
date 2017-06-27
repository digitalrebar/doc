.. index::
	TODO; Run-in-AWS Troubleshooting
	pair: Run-in-AWS; Troubleshooting
	
.. _troubleshoot_aws:

Troubleshooting Run-in-AWS 
--------------------------

This section will cover troubleshooting tips and solutions for installing onto an AWS Server. If an issue is not covered here, please `contact support <https://gitter.im/digitalrebar/core?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge>`_.

General Tips
============

If the install fails, check to be sure the install command was run with sudo as follows::

	sudo ./run-in-system.sh --deploy-admin=local --access=HOST --admin-ip=$IPA

``./run-in-system`` has been known to be finicky about this, so this may fix the issue. If it does not, contact support. 

