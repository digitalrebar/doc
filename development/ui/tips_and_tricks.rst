
.. note:: WARNING WARNING WARNING:  This is the Digital Rebar v2 product documentation.  The v2 version is EOL as of September 2017.  Please refer to the new Digital Rebar Provision v3 documentation:  http:\/\/provision.readthedocs.io\/en\/tip\/README.html

.. _tips_tricks:

Tips & Tricks (UI Developer)
----------------------------

Dashboard - No Polling
~~~~~~~~~~~~~~~~~~~~~~

When troubleshooting the UI or REST APIs, the Node Dashboard
(``dashboard``) polling can be challenging because it generates log traffic.
Polling can be disabled for debug by using the ``nopoll`` parameter.

For example: ``http://192.168.124.10/dashboard/89?nopoll``

Stop Rendering Navigation
~~~~~~~~~~~~~~~~~~~~~~~~~

When in developer mode, ``?nav=false`` can be passed in and
the template will not render the menu.

For example: ``http://192.168.124.10/docs?nav=false``

Force/Stop Documentation re-indexing
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

``?rebuild=[true/false]`` can be used to force the documentation
index to rebuild (also happens on web startup).  In developer mode, the
documentation will re-index every time the /doc page is hit.

-  in production mode, force re-indexing, use ``?rebuild=[anything]``
-  in developer mode, stop re-index on every load, use ``?rebuild=false``

