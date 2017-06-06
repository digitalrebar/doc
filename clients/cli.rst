.. index::
	pair: CLI; Client

.. _rebar_cli:

Digital Rebar CLI
=================

The Digital Rebar CLI provides simple access to the REST API (see :ref:`api_info`) for all common use cases.
The CLI provides advantages including simpler authentication and non-JSON access to many simple commands.
It is written in Golang and can be adapted as a Golang client.

The CLI is automatically created during deployment and accessible inside the Rebar_API container or from the host via ``docker exec -it compose_rebar_api_1 rebar --help``

In order to download the CLI *without* a deployment, the `RackN <http://rackn.com>`_ team has it available.
Select the correct architecture to retrieve the CLI:

* `Linux <https://s3-us-west-2.amazonaws.com/rebar-bins/master/linux/amd64/master>`_

    ::

      sudo curl -o /usr/local/sbin/rebar https://s3-us-west-2.amazonaws.com/rebar-bins/master/linux/amd64/rebar
      sudo chmod +x /usr/local/sbin/rebar
      rebar --help

* `Mac <https://s3-us-west-2.amazonaws.com/rebar-bins/master/darwin/amd64/rebar>`_

``chmod +x`` must be entered to use the CLI.  We also recommend renaming the CLI as "rebar" and placing in the execution path.

To use the CLI, type ``rebar --help`` for instructions

Ping
----

There are many commands in the CLI described in ``--help``.  The most basic is `rebar ping` which is used to make sure the CLI can connect to the server.

Parameters
----------

Parameters are used to set the server address ``-E`` and credentials ``-U`` & ``P``.  A typical instruction looks like ``rebar ping -E https://127.0.0.1 -U rebar -P rebar1``.  To avoid passing parameters into each call, we recommend setting the environment variables.


Environment Variables
---------------------

The CLI uses environment variables ``REBAR_ENDPOINT`` and ``REBAR_KEY`` if set.  The key holds both user and password using the following a "user:password" format.


Match
-----

To return a list subset, use the match instruction with json filter set.  For example: ``rebar nodes match '{"deployment_id":10}'`` will return the same JSON as ``rebar nodes list`` but only members of Deployment ID 10 will be included.
