Run-In-Packet
=============

The following instructions require that you have an account at `Packet.net <https://packet.net>`_.  They could be adapted to work for other hosting providers since the Ansible script used is generic.

Additional Steps:

#. Get the Deploy code as in other instructions, :ref:`initial_install_setup`
#. Create an account at Packet.net `registration <https://app.packet.net/#/registration>`_:

  #. Note your API key
  #. Register your SSH public key (our Packet scripts do not upload a key for you!)

#. Create a :ref:`dr_info` with Packet API keys
#. ``./run_in_packet.sh <servername>``
