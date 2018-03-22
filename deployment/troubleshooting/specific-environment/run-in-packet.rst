
.. note:: WARNING WARNING WARNING:  This is the Digital Rebar v2 product documentation.  The v2 version is EOL as of September 2017.  Please refer to the new Digital Rebar Provision v3 documentation:  http:\/\/provision.readthedocs.io\/en\/tip\/README.html

.. index::
	TODO; Run-in-Packet Troubleshooting
	pair: Run-in-Packet; Troubleshooting

.. _troubleshoot_packet:

Troubleshooting Run-in-Packet
-----------------------------

This section will cover troubleshooting tips and solutions for 
installing onto a Packet Server. If an issue is not covered here, 
please `contact support <https://gitter.im/digitalrebar/core?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge>`_.

General Tips
============

If sshing to the server fails check to make sure the key is complete, 
there are sections seperated by spaces which are easily missed. 

Additionally, check to make sure to use the command provided by Packet.

After completing the ssh, installation should progress up until ''TASK[Install Prereqs[SLOW]]'' at which
point it will crash. This error has persisted and is under review by the development team. 
