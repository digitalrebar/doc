.. _ug_add_provider:

Add Providers
-------------

If you have the :ref:`rebar_cli` in your path, then you can use the ``workloads/add-provider.sh`` 
script to add providers to a running rebar system.  This method uses the :ref:`dr_info` file to
populate the provider in question. 

  ::

  	cd ~/digitalrebar/deploy
    workloads/add-provider.sh --admin-ip=[rebar ip] --provider=[google|aws|packet|debug]

Note: For AWS or Google the scripts will attempt to install their CLIs

You can also use the :ref:`providers` UI interactively.

See :ref:`configure_providers` for specific details.