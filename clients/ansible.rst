Ansible Dynamic Inventory
=========================

The clients/ansible/inventory.py file can be used to generate dynamic inventory based on the api/status/inventory path.  The inventory.py file is structured to work with Ansible dyanmic inventory optimizations.

example: ``ansible -i inventory.py all -a "uname -a"``

For now, you must manually change the URL and user settings inside the inventory.py file.
