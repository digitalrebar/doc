.. index::
	pair: Ansible; Inventory

.. _clients_ansible:

Ansible Dynamic Inventory
=========================

The clients/ansible/inventory.py file can be used to generate dynamic inventory based on the api/status/inventory path.  The inventory.py file is structured to work with Ansible dyanmic inventory optimizations.

example: ``ansible -i inventory.py all -a "uname -a"``

For now, the URL and user settings must be manually changed inside the inventory.py file.
