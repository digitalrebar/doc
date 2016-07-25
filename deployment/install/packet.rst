.. _run_in_packet:

.. index::
  pair: Packet; Run in Packet
  pair: Deployment; Run in Packet

Run-In-Packet
=============

The following instructions require an account at `Packet.net <https://packet.net>`_.  They can be adapted to work for other hosting providers, since the Ansible script used is generic.

Additional Steps:

#. Get the Deploy code as in other instructions, :ref:`initial_install_setup`.
#. Create an account at Packet.net `registration <https://app.packet.net/#/registration>`_:.

  #. Note the API key.
  #. Register the SSH public key (our Packet scripts do not automatically upload a key!).

#. Create a :ref:`dr_info` with Packet API keys.
#. ``./run_in_packet.sh <servername>``.
