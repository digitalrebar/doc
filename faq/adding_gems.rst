
.. note:: WARNING WARNING WARNING:  This is the Digital Rebar v2 product documentation.  That product line is EOL as of September 2017.  Please refer to the new Digital Rebar Provision v3 documentation:  http:\/\/provision.readthedocs.io\/en\/tip\/README.html

.. index::
	pair: Barclamps; GEMs

.. _faq_adding_GEMs:

How are GEMs Added to Barclamps?
================================

Add gems  in ``rebar.yml`` under ``gems: required_pkgs:``.  This is where gems are pulled from when Rebar is in "online" mode. 

Gems in ``gems: pkgs:`` will
be cached when "offline" mode is enabled (TBD).

For more on barclamps, see :ref:`ux_barclamps`.
