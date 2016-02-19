Digital Rebar CLI
=================

The Digital Rebar CLI provides simple access to the `REST API <../development/api>`_ for all common use cases.
The CLI provides advantages including simpler authentication and non-JSON access to many simple commands.
It is written in Golang and can be adapted as a Golang client.

The CLI is automatically created during deployment and accessible inside the Rebar_API container or from the host via `docker exec -it compose_rebar_api_1 rebar --help`

If you'd like to access the CLI *without a deployment*, the `RackN <http://rackn.com>`_ teams makes it available for download:
Select the correct architecture to retrieve the CLI:

* `Linux <https://s3-us-west-2.amazonaws.com/rebar-cli/rebar-linux-amd64>`_

    ::
    
      sudo curl -o /usr/local/sbin/rebar https://s3-us-west-2.amazonaws.com/rebar-cli/rebar-linux-amd64
      sudo chmod +x /usr/local/sbin/rebar
      rebar --help

* `Mac <https://s3-us-west-2.amazonaws.com/rebar-cli/rebar-darwin-amd64>`_

You must `chmod +x` to use the CLI.  We also recommend renaming the CLI as "rebar" and placing in your execution path.

To use the CLI, type `rebar --help` for instructions

Ping
----

There are many commands in the CLI described in --help.  The most basic is "rebar ping" which is used to make sure the CLI can connect to the server.

Parameters
----------

Parameters are used to set the server address (-E) and credentials (-U & -P).  A typical instruction looks like ``rebar ping -E https://127.0.0.1:3000 -U rebar -P rebar1``.  To avoid passing parameters into each call, we recommend setting your environment variables.


Environment Variables
---------------------

The CLI uses environment variables 'REBAR_ENDPOINT' and 'REBAR_KEY' if set.  The key holds both user and password using the following a "user:password" format.
