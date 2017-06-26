etcd-install
============


Bootstrap-os: Remove require tty Error
--------------------------------------

:typical log message: ``Aborting, target uses selinux but python bindings (libselinux-python) aren't installed!``
:cause: Operating system optimizations running out of sequence
:solution: Set bootstrap_os to "centos" under k8s-config service node, then retry role. Prior to future deployments, configure bootstrap_os under advanced attributes menu in install wizard.
