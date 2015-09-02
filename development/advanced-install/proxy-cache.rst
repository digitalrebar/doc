Configuration of Proxy Cache
============================

Because Digital Rebar online access for packages, we *strongly*
recommend using a caching proxy such as Squid.

If you are behind a firewall, you should have the cache access CNTLM or
similar.

Squid Proxy (on Ubuntu)
-----------------------

1.  Configure your CNTLM proxy on :3128
2.  Install: ``sudo apt-get install squid3``
3.  Update your configuration: ``sudo vi /etc/squid3/squid.conf``
4.  make sure that you allow containers to use the proxy
5.  example https://gist.github.com/cloudedge/1b46280b7dfbffe2d763
6.  it is important to add BOTH your local subnet & the docker subnet to
    allowed
7.  include the ``always_direct allow to_localnet`` line
8.  order is very important in the configuration file
9.  Create your cache directory: ``sudo mkdir /var/cache/squid``
10. Allow Squid to write to the cache:
    ``sudo chown proxy:proxy /var/cache/squid``
11. Restart the service: ``sudo service squid3 restart``
12. Access the proxy
13. ``export http_proxy="http://127.0.0.1:8123"``
14. ``export https_proxy="http://127.0.0.1:8123"``
15. Test the proxy: ``wget google.com``

