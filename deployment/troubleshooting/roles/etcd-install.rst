
.. note:: WARNING WARNING WARNING:  This is the Digital Rebar v2 product documentation.  That product line is EOL as of September 2017.  Please refer to the new Digital Rebar Provision v3 documentation:  http:\/\/provision.readthedocs.io\/en\/tip\/README.html

etcd-install
============


Bootstrap-os: Remove require tty Error
--------------------------------------

:typical log message: ``Aborting, target uses selinux but python bindings (libselinux-python) aren't installed!``
:cause: Operating system optimizations running out of sequence
:solution: Set bootstrap_os to "centos" under k8s-config service node, then retry role. Prior to future deployments, configure bootstrap_os under advanced attributes menu in install wizard.
