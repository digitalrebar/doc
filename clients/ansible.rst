
.. note:: WARNING WARNING WARNING:  This is the Digital Rebar v2 product documentation.  The v2 version is EOL as of September 2017.  Please refer to the new Digital Rebar Provision v3 documentation:  http:\/\/provision.readthedocs.io\/en\/tip\/README.html

.. index::
	pair: Ansible; Inventory

.. _clients_ansible:

Ansible Dynamic Inventory
=========================

The clients/ansible/inventory.py file can be used to generate dynamic inventory based on the api/status/inventory path.  The inventory.py file is structured to work with Ansible dyanmic inventory optimizations.

example: ``ansible -i inventory.py all -a "uname -a"``

For now, the URL and user settings must be manually changed inside the inventory.py file.
