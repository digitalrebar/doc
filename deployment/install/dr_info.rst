.. index::
  pair: DR Info File; Tools

.. _dr_info:

DR Info File (.dr_info)
=======================

For regular uses, :ref:`ui_providers` credentials can be stored in the ``~/.dr_info`` file.

There is a ``.dr_info.example`` file in the `DigitalRebar-Deployment root <https://github.com/digitalrebar/digitalrebar/blob/master/deploy/.dr_info.example>`_ that can be used as a template via ``cp ~/digitalrebar/deploy/.dr_info.example ~/.dr_info``

Sample ``.dr_info``:

  ::

    PROVIDER_PACKET_KEY=[key here]
    PROVIDER_PACKET_PROJECT_ID=[project id]
    NODENAME=rebar

    PROVIDER_AWS_ACCESS_KEY_ID=[key here]
    PROVIDER_AWS_SECRET_ACCESS_KEY=[secret here]
    PROVIDER_AWS_REGION=us-west-2

    PROVIDER_GOOGLE_PROJECT=[project_id]
    PROVIDER_GOOGLE_JSON_KEY=$(cat "$HOME/.ssh/projectname.json")

See :ref:`configure_providers` for specific details about individual providers.
