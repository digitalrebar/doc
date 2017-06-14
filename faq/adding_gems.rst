.. index::
	pair: Barclamps; GEMs

.. _faq_adding_GEMs:

How are GEMs Added to Barclamps?
================================

Add gems  in ``rebar.yml`` under ``gems: required_pkgs:``.  This is where gems are pulled from when Rebar is in "online" mode. 

Gems in ``gems: pkgs:`` will
be cached when "offline" mode is enabled (TBD).

For more on barclamps, see :ref:`ui_barclamps`.
