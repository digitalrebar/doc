.. _ug_add_provider:

Add Providers
-------------

If the :ref:`rebar_cli` exists in the path in use, then the ``workloads/add-provider.sh`` 
script can be used to add providers to a running rebar system.  This method uses the :ref:`dr_info` file to
populate the provider in question. 

  ::

  	cd ~/digitalrebar/deploy
    workloads/add-provider.sh --admin-ip=[rebar ip] --provider=[google|aws|packet|debug]

Note: For AWS or Google the scripts will attempt to install their CLIs

The :ref:`providers` UI can also be used interactively.

See :ref:`configure_providers` for specific details.