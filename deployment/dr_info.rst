Digital Rebar Info (.dr_info)
=============================

For regular uses, you can store your provider credentials in the ``~/.dr_info`` file ( `details here <./dr_info.rst>`_ )

There is a ``.dr_info.example`` file in the `DigitalRebar-Deployment root <https://github.com/rackn/digitalrebar-deploy/blob/master/.dr_info.example>`_ you can use as a template.

Sample ``.dr_info``:

  ::

    PROVIDER_PACKET_KEY=[key here]
    PROVIDER_PACKET_PROJECT_ID=[project id]
    NODENAME=rebar

    PROVIDER_AWS_ACCESS_KEY_ID=[key here]
    PROVIDER_AWS_SECRET_ACCESS_KEY=[secret here]
    PROVIDER_AWS_REGION=us-west-2

    PROVIDER_GOOGLE_PROJECT=[project]
    PROVIDER_GOOGLE_JSON_KEY=$(cat "$HOME/gce.json")



CLI Population
--------------

If you have the `rebar cli <../cli/README.rst>`_ in your path, then you can use the ``workloads/add-provider.sh`` script to add providers to a running rebar system.  

  ::

    workloads/add-provider.sh --admin-ip=[rebar ip] --provider=[google|aws|packet|debug]

Note: For AWS or Google the scripts will attempt to install their CLIs

