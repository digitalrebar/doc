
.. note:: WARNING WARNING WARNING:  This is the Digital Rebar v2 product documentation.  That product line is EOL as of September 2017.  Please refer to the new Digital Rebar Provision v3 documentation:  http:\/\/provision.readthedocs.io\/en\/tip\/README.html

.. index::
  pair: CLI; Downloads
  pair: CLI; Setup

.. _cli_setup:

CLI Download
------------

If :ref:`rebar_cli` is available in the path, Digital Rebar can be driven from a desktop or other environment.

The Rebar client is a golang binary that can access the :ref:`digital_rebar_api` from a command line.

There are precompiled binaries that can be placed into the path or can be built from source.

Precompiled Binary
==================

To get the rebar client binary, run this:

  ::

    if [[ $(uname -s) == Darwin ]] ; then
        curl -so rebar https://s3-us-west-2.amazonaws.com/rebar-bins/master/darwin/amd64/rebar
    else
        curl -so rebar https://s3-us-west-2.amazonaws.com/rebar-bins/master/linux/amd64/rebar
    fi
    chmod +x rebar
    mv rebar /usr/local/bin


.. index::
  CLI; Running the CLI

Running the CLI
===============

To run the CLI, it is useful to specify some environment variables to reduce the options required on the actual command line.

+------------------+-------------------------+---------------------------------------------------+
| Variable         | Default                 | Comments                                          |
+==================+=========================+===================================================+
| REBAR_KEY        | rebar:rebar1            | Username and Password with a colon in between.    |
+------------------+-------------------------+---------------------------------------------------+
| REBAR_ENDPOINT   | https://127.0.0.1       | URL to access the admin from the used environment.|
+------------------+-------------------------+---------------------------------------------------+

Putting these in the environment file or shell init script can be helpful for accessing Digital Rebar.
