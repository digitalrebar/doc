Digital Rebar Info (.dr_info)
=============================

For regular uses, you can store your provider credentials in the ``~/.dr_info`` file ( `details here <./dr_info.rst>`_ )

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

If you have the rebar cli in your path, then you can use the `workloads/add-provider.sh` script to add providers to a running rebar system.  

  ::

    workloads/add-provider.sh --admin-ip=[rebar ip] --provider=[google|aws|packet|debug]

Note: For AWS, you also need to ``sudo pip install awscli``

