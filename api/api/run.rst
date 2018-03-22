
.. note:: WARNING WARNING WARNING:  This is the Digital Rebar v2 product documentation.  The v2 version is EOL as of September 2017.  Please refer to the new Digital Rebar Provision v3 documentation:  http:\/\/provision.readthedocs.io\/en\/tip\/README.html

.. index::
  pair: Run; API

.. _api_run:

Run APIs
~~~~~~~~

Run APIs allow users to inspect the state of the annealer queue.

    They are read only.

API Actions
^^^^^^^^^^^

+----------+-------------------------+---------------+------------------------------------------------+
| Verb     | URL                     | Type          | Comments                                       |
+==========+=========================+===============+================================================+
| GET      | api/v2/runs             | list of run   | List all items in queue                        |
+----------+-------------------------+---------------+------------------------------------------------+
| GET      | api/v2/runs/[node id]   | list of run   | shows list of queue items for the given node   |
+----------+-------------------------+---------------+------------------------------------------------+
| PUT      | not suppored            | n/a           |                                                |
+----------+-------------------------+---------------+------------------------------------------------+
| POST     | not supported           | n/a           |                                                |
+----------+-------------------------+---------------+------------------------------------------------+
| DELETE   | not supported           | n/a           |                                                |
+----------+-------------------------+---------------+------------------------------------------------+

