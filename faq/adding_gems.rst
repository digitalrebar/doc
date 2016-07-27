How are GEMs added to barclamps?
================================

Add gems  in ``rebar.yml`` under ``gems: required_pkgs:``- that is where gems are pulled from when Rebar is in "online" mode. 

Gems in ``gems: pkgs:`` will
be cached when "offline" mode is enabled (TBD).
