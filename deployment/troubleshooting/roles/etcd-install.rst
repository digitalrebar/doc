etcd-install
============


Bootstrap-os: Remove require tty Error
--------------------------------------

:typical log message: ``Aborting, target uses selinux but python bindings (libselinux-python) aren't installed!``
:cause: Operating system optimizations running out of sequence
:solution: Rerun deployment wizard, disabling auto-commit and setting bootstrap_os to "centos" under advanced attributes menu.
