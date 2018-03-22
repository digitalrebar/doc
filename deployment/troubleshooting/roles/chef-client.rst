
.. note:: WARNING WARNING WARNING:  This is the Digital Rebar v2 product documentation.  The v2 version is EOL as of September 2017.  Please refer to the new Digital Rebar Provision v3 documentation:  http:\/\/provision.readthedocs.io\/en\/tip\/README.html

Chef Client Role Error
======================

Cannot Download Chef Client
---------------------------

:typical log message: ``curl: (6) Could not resolve host: opscode-omnibus-packages.s3.amazonaws.com``
:cause: cannot access Chef install packages on internet
:solution: Often a retry is sufficient.  If retry fails, it may be a larger networking issue
:notes: This issue is often an indication of broader network misconfigurations because it is usually the first time that nodes are trying to connect to the internet.
