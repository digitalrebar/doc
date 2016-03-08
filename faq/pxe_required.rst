PXE Required?
=============

Q: A new piece of hardware arrives, I have a DC technician push into a rack and switch it on:

- does the server need a manual IPMI/IntelAMT/Drac configuration prior to that, e.g. an IP from a specific range on a backplane?
- I guess the server should be setup to boot from PXE from all available network ports?


As long as it will PXE boot to a DHCP server under our control (for now), and Rebar has been delegated an IP address to use for admin purposes, then our current node discovery workflow will handle configuring IPMI/DRAC/AMT.  Rebar was initially designed as a tool to take racks of servers from racked and cabled to running Openstack or Hadoop with minimal intervention, and configuring things like IPMI is part of that workflow that we have retained.

The Server should then be discovered, meaning it should end up in some sort of inventory that we can query that will tell us which hardware is available, Mac addresses etc.

All nodes that we manage wind up in a "system" deployment, and our API exposes that along with discovered attributes about that node.  
