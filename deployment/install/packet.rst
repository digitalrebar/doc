# Running on [Packet.net](http://packet.net)

The following instructions require that you have an account at [Packet.net](https://app.packet.net/#/registration).  They could be adapted to work for other hosting providers since the Ansible script used is generic.

1. Get the Deploy code as in other instructions
1. Create an account at Packet.net

  1. Note your API key
  1. Register your SSH public key (our Packet scripts do not upload a key for you!)
1. Create a `~/.dr_info file <../dr_info.rst>`_ with Packet API keys
1. ``./run_in_packet.sh yourname``
