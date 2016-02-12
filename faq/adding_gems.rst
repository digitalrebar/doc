How do I add GEMs to my barclamps?
==============================================

Q: if I add gems to the ``rebar.yml`` under ``gems: pkgs:`` they aren't
added to my install.

A: Add them in ``rebar.yml`` under ``gems: required_pkgs:`` - those are
gems pull when Rebar is in "online" mode. Gems in ``gems: pkgs:`` will
be cached when "offline" mode is enabled (TBD).
