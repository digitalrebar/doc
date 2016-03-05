Running on [Packet.net](http://packet.net)
==========================================

The following instructions require that you have an account at [Packet.net](https://app.packet.net/#/registration).  They could be adapted to work for other hosting providers since the Ansible script used is generic.

Additional Steps:

#. Get the Deploy code as in other instructions
#. Create an account at Packet.net:

  #. Note your API key
  #. Register your SSH public key (our Packet scripts do not upload a key for you!)
#. Create a `~/.dr_info file <../dr_info.rst>`_ with Packet API keys
#. ``./run_in_packet.sh yourname``
