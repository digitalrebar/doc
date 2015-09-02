Sledgehammer Hooks
==================

This file documents the hooks available in the Sledgehammer image that
can be used to customize how Sledgehammer transitions through states.

The primary Sledgehammer control script (control.sh) will search for
-pre and -post hooks for every Rebar state transition it knows how to go
through. The hooks can be general (all nodes transitioning through the
state will run them) or specific to one machine. This functionality is
intended to be used to facilitate automated testing that must happen
outside of the chef-client runs. Hooks will run in the following order:

1: Machine-specific -pre hooks, 2: General -pre hooks, 3: chef-client,
4: General -post hooks, 5: Machine-specific -post hooks.

All hooks will be run in alphabetic order, and non-executable hooks will
be skipped. All hooks to be run should be staged in the /updates NFS
share on the admin node in the following directories:

-  /updates/:math:`nodename/`\ state-pre
-  /updates/$state-pre
-  /updates/$state-post
-  /updates/:math:`nodename/`\ state-post

$state = the Rebar state that Sledgehammer is transitioning through.
discovering, discovered, update, etc.

$nodename = the name of the node according to Chef.

To make writing hooks simpler, certian functions in the control.sh
script have been split into /updates/control\_lib.sh, and control.sh has
been refactored to account for these changes. If your hooks are written
in bash, they can source /updates/control\_lib.sh to pull in the
following functions:

-  get\_state get\_state will pull some information about from the
   chef-server, and store it in the local environment. Specifically, it
   will set the following environment variables: BMC\_ROUTER = the
   gateway IP address of the BMC network, if any. BMC\_ADDRESS = the IP
   address of the BMC for , if any. BMC\_NETMASK = the netmask in dotted
   quad format of the BMC network, if any. CROWBAR\_STATE = the current
   Rebar state that the node is in. HOSTNAME = the hostname of the
   system according to the Chef server. ALLOCATED = whether or not has
   been allocated

-  post\_state post\_state will attempt to transition to . If
   successful, it will then update the same environment data that

get\_state does.

-  reboot\_system This will cleanly reboot the node. You should use it
   instead of reboot to ensure that all the logs are flushed and that
   the NFS shares get umounted.

-  wait\_for\_allocated This function will spin until has been allocated
   by Rebar.

-  wait\_for\_rebar\_state If is not passed, this function will wait
   until transitions to a state other than the one it is currently at.
   If is passed, this function will wait until transitions into

-  hook\_has\_run If the current hook has already run for the current
   -pre or -post state, hook\_has\_run will return 0. Otherwise, return
   1. This function works by creating state tracking files in
   /install-logs/. To facilitate this function, control.sh exports the
   following environment variables to the hooks:
-  HOOKNAME = the name of the hook without any path components.
-  HOOKSTATE = the -pre or -post state that the hook is running in.

Hook Exit Status

All hooks must exit successfully (with a 0 return status), otherwise the
system will reboot into the debug state.
