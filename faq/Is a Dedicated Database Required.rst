Is a Dedicated Database Required?
=================================

Q: do we need a dedicated database server or would that run on the same node as the digitalRebar installation?

We currently (Feb 2016) stand up our own Postgres 9.4 database to use as a backing store for Rebar and goiardi (the built-in Chef server we use).  There is nothing preventing us from using yours (if you have one handy for this sort of thing) but a bit of config work.

