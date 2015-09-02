Digital Rebar Environment Simulator
===================================

  This topic uses the same infrastructure as the BDD test environment

You need a working [[devtool-build]] system.

To use the simulator
--------------------

In a new window, start erlang:

::
    'cd ~/rebar/barclamps/rebar/BDD'
    ./linux_compile.sh
    [review default.config and update if needed]

You can run the simulate interactively from 'erl' using 'dev:pop().' to create machines and 'dev:unpop().' to remove them.

You can change the nodes and other information created by the simulator by editing your copy of 'dev.config'.

Open the Digital Rebar UI under 'http://[dev system IP]:3000'
You can then explore and even run the Annealer!


