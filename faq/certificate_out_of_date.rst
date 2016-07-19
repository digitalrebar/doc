My Certificate is Out of Date
=============================

If some of your systems are reporting out of date certificates then the system cannot download files or use SSH to connect.

Typical Output
--------------

    ::
    
      curl -fgLO https://opscode-omnibus-packages.s3.amazonaws.com/el/6/i686/chef-11.18.12-1.el6.i686.rpm
      curl: (60) Peer's Certificate has expired.
      More details here: http://curl.haxx.se/docs/sslcerts.html

Likely Cause
------------

If you system clock is out of date (or has bad batteries) then it resets to an date that does not match certificate validation ranges.

Update your system clock.  You may need to replace the batteries in your system.
