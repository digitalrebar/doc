.. index::
	Ansible; Login Issue

.. _faq_ansible_login:

Ansible Run Fails with Login Issue?
===================================

Background: Digital Rebar uses root login for control.  On some clouds (e.g. AWS), permission to use root must be added from another credential set.  This is done automatically by Digital Rebar using the existing key(s) on the system and name matches the local and remote keys.

Issue: The local privarte and remote public key do not match.

Typical Error Message

::

  fatal: [52.36.244.168] => failed to transfer file to Please login as the user "centos" rather than the user "root"./setup:
  Received message too long 1349281121

Resolution: Delete the remote key from the cloud system (typically named after the host system name).  Digital Rebar will upload a fresh public key.
