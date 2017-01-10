Buiding Go Components
=====================

Many Digital Rebar components rely on GOLANG services.  These services must be build before they can be used by Digital Rebar.

To build the services, You'll need to install GOLANG 1.7 and guide.sh.  

Find the location of your Digital Rebar Go code using $GOPATH.  It should be under `$GOLANG/github.com/src/digitalrebar/digitalrebar/go` or similar.

In the `digitalrebar/go` directory, use the `build-rebar.sh` command to build the services.

Once the services have been built, you can test them into by copying them directly into the service containers.

For example:

* `docker cp ./bin/master/linux/amd64/rebar_rev_proxy compose_revproxy_1:/usr/local/bin/`
* `docker-compose restart revproxy`
