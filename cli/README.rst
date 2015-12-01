Digital Rebar CLI
=================

The Digital Rebar CLI provides simple access to the `REST API <../development/api>`_ for all common use cases.
The CLI provides advantages including simpler authentication and non-JSON access to many simple commands.
It is written in Golang and can be adapted as a Golang client.

The CLI is automatically created during deployment and accessible inside the Rebar_API container or from the host via `docker exec -it compose_rebar_api_1 rebar --help`

If you'd like to access the CLI *without a deployment*, the `RackN <http://rackn.com>`_ teams makes it available for download:
Select the correct architecture to retrieve the CLI:

* `Linux <https://s3-us-west-2.amazonaws.com/rebar-cli/rebar-linux-amd64>`_
* `Mac <https://s3-us-west-2.amazonaws.com/rebar-cli/rebar-darwin-amd64>`_

To use the CLI, type `rebar --help` for instructions
