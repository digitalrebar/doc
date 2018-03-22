
.. note:: WARNING WARNING WARNING:  This is the Digital Rebar v2 product documentation.  That product line is EOL as of September 2017.  Please refer to the new Digital Rebar Provision v3 documentation:  http:\/\/provision.readthedocs.io\/en\/tip\/README.html

.. index::
  Providers; Adding Providers

.. _ug_add_provider:

Add Providers
-------------

If the :ref:`rebar_cli` exists in the path in use, then the ``workloads/add-provider.sh``
script can be used to add providers to a running rebar system.  This method uses the :ref:`dr_info` file to
populate the provider in question.

  ::

  	cd ~/digitalrebar/deploy
    workloads/add-provider.sh --admin-ip=[rebar ip] --provider=[google|aws|packet|debug]

**Note**: For AWS or Google the scripts will attempt to install their CLIs

The :ref:`ux_providers` UX can also be used interactively.

See :ref:`configure_providers` for specific details.
