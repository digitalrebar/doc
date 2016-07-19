
.. _cli_setup:

CLI Download
------------

If :ref:`rebar_cli` is avalible in the path, Digital Rebar can be driven from a desktop or other environment.  

The rebar client is a golang binary that can access the Digital Rebar API from a command line.

There are precompiled binraries that can be placed into path or can be built from source.

Precompiled Binary
==================

To get the rebar client binary, run this:

  ::

    if [[ $(uname -s) == Darwin ]] ; then
        curl -so rebar https://s3-us-west-2.amazonaws.com/rebar-cli/rebar-darwin-amd64
    else
        curl -so rebar https://s3-us-west-2.amazonaws.com/rebar-cli/rebar-linux-amd64
    fi
    chmod +x rebar
    mv rebar /usr/local/bin


Build From Source
=================

To build from source, see the github `repo <https://github.com/digitalrebar/rebar-api>`_.

The source also allows the embedding of the Digital Rebar API into another golang program as well.


Running the CLI
===============

To run the CLI, it is useful to specify some environment variables to reduce the options required on the actual command line.

+------------------+-------------------------+----------------------------------------------------+
| Variable         | Default                 | Comments                                           |
+==================+=========================+====================================================+
| REBAR_KEY        | rebar:rebar1            | Username and Password with a colon in between.     |
+------------------+-------------------------+----------------------------------------------------+
| REBAR_ENDPOINT   | https://127.0.0.1:3000  | URL to access the admin from the used environment. |
+------------------+-------------------------+----------------------------------------------------+

Putting these in the environment file or shell init script can be helpful for accessing Digital Rebar.

