External Services Configuration
-------------------------------

| The Digital Rebar System can be configured to utilize external (not
installed or managed by Digital Rebar) services.
| These configurations are made in the following file: 
/opt/digitalrebar/core/rebar-config.sh and must be made *PRIOR* to
running production.sh to install the system. Users can configure any
combination of of these services.

DNS (Domain Name Server)
~~~~~~~~~~~~~~~~~~~~~~~~

By default Digital Rebar will utilize Bind (named) on the Admin Node
when you install Digital Rebar. All clients will be configured to use
this system when they are installed. DNS entries are automatically
updated as new nodes are configured or removed from Digital Rebar.
Digital Rebar can be configured to use an already existing DNS however
it becomes the responsability of the user to ensure that entries are
created or removed as Digital Rebar will not function correctly if the
name and IP Address are not configured with the ones assigned by Digital
Rebar (Typically MAC address of the primary interface)

-  Edit /opt/digitalrebar/core/rebar-config.sh
-  Find the line 'rebar roles bind dns-bind\_server to "$FQDN"' and
   comment it out by adding # to the front of the line.
-  Find the line '#curl -X PUT -d '{"Datacenter": "digitalrebar",
   "Node": "external", "Address": "192.168.124.11", "Service":
   {"Service": "dns-service", "Address": "192.168.124.11", "Port": 43,
   "Tags": [ "system" ]} }' http://127.0.0.1:8500/v1/catalog/register'
   uncomment it by removing the # from the front of the line and then
   change the IP address of the DNS server (192.168.124.11 in this
   example) to the IP of the system which will be serving DNS for the
   enviornment
-  Find the line '#curl -X PUT -d 'POWERDNS'
   http://127.0.0.1:8500/v1/kv/digitalrebar/private/dns/system/type?token=$CONSUL\_MACL\`
   uncomment it by removing the # from the front of the line.
-  Find the line '233 #curl -X PUT -d 'POWERDNS'
   http://127.0.0.1:8500/v1/kv/digitalrebar/private/dns/system/type?token=$CONSUL\_MACL'
   and uncomment it by removing the # from the front of the link. Change
   the POWERDNS to BIND if you aren't running POWERDNS.
-  If you are running POWERDNS, uncomment the three curl lines right
   below the previous curl command and update the -d parameters for your
   POWERDNS server.
-  Save the file and continue on with the remainder of the installation
   steps.

NTP (Network Time Protocol)
~~~~~~~~~~~~~~~~~~~~~~~~~~~

By default Digital Rebar will utilize NTP (NTPd) on the Admin node and
all clients will be configured to use this server to sync their times.
Digital Rebar can be configured not run NTP on the admin server and
configure any nodes installed so to point their clients to the IP address
specified in this file.

-  Edit /opt/digitalrebar/core/rebar-config.sh
-  Find the line 'rebar roles bind ntp-server to "$FQDN" and comment it
   out by adding # to the front of the line
-  Find the line '#curl -X PUT -d '{"Datacenter": "digitalrebar",
   "Node": "external", "Address": "192.168.124.11", "Service":
   {"Service": "ntp-service", "Address": "192.168.124.11", "Port": 123,
   "Tags": [ "system" ]} }' http://127.0.0.1:8500/v1/catalog/register'
   uncomment it by removing the # from the front of the line and then
   change the IP address of the NTP server (192.168.124.11 in this
   example) to the IP of the system which will be serving DNS for the
   enviornment.
-  Save the file and continue on with the remainder of the installation
   steps.

DHCP (Dynamic Host Configuration Protocol)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

By default Digital Rebar will configure DHCP (dhcpd) on the Admin node
and utilize it to preform boot sequences to nodes as they transition
from discovery to OS installation. Additionally it will direct a system
to use it's local drives to boot once an OS has been installed. Digital Rebar
can be configured to use an already existing DHCP Server however it
becomes the responsability of the user to ensure that nodes keep the
same IP address.

-  Edit /opt/digitalrebar/core/rebar-config.sh
-  Find the line 'rebar roles bind dhcp-database to "$FQDN"' and comment
   it out by adding # to the front of the line.
-  Save the file and continue on with the remainder of the installation
   steps.
-  On the DHCP server the user must redirect the node which is booting
   to the Digital Rebar Admin server. To do this add the following
   stanza to /etc/dhcpd/dhcpd.conf

::

    subnet 192.168.124.0 netmask 255.255.255.0 {
     option routers 192.168.124.10;
     option subnet-mask 255.255.255.0;
     option broadcast-address 192.168.124.255;
     option domain-name "neode.com";
     option domain-name-servers 192.168.124.11;
     default-lease-time 7200;
     max-lease-time 36000;
      pool {
        range 192.168.124.81 192.168.124.254;
        allow unknown-clients;
        if option arch = 00:06 {
         filename = "discovery/bootia32.efi";
      } else if option arch = 00:07 {
         filename = "discovery/bootx64.efi";
      } else {
         filename = "discovery/pxelinux.0";
      }
        next-server 192.168.124.10;
      }   
    }

-  Replace the subet, domain-name and pool information to match the
   enviornment.
-  Put the IP address of the Digital Rebar Admin Node in the next-server
   in place of 192.168.124.10.

Proxy Server
~~~~~~~~~~~~

By default, Digital Rebar will install a Proxy server on the Admin server
in order to facilitate access to packages on the internet by the target
nodes. After installation Digital Rebar will install various packages
based on the roles that are assigned to these devices. As Digital Rebar
caches the packages as they are downloaded from the internet (Note: they are only
pulled down once even if multiple systems will be accessing them). It is
possible for a user to define a different proxy server if one already
exists in the enviornment.

-  Edit /opt/digitalrebar/core/rebar-config.sh
-  Find the line 'rebar roles bind proxy-server to "$FQDN"\` and comment
   it out by adding # to the front of the line
-  Find the line 'curl -X PUT -d '{"Datacenter": "digitalrebar", "Node":
   "external", "Address": "192.168.124.9", "Service": {"Service":
   "proxy-service", "Address": "192.168.124.9", "Port": 3128, "Tags": [
   "system" ]} }' http://127.0.0.1:8500/v1/catalog/register \` uncomment
   it by removing the # from the front of the line and then change the
   IP address of the proxy server (192.168.124.9 in this example) as
   well as the port (3128 in this example) to the IP and port of the
   proxy server for the enviornment.
-  Save the file and continue on with the remainder of the installation
   steps.

AMQP Server and Service
~~~~~~~~~~~~~~~~~~~~~~~

Optionally, Digital Rebar can be configured to send events to an AMQP
server through the AMQP service. To do this, either Digital Rebar should
run its own RabbitMQ server or an AMQP service can be injected into
Digital Rebar. The system currently assumes a user of *rebar*, a
password of *rebar*, and a virtual host of */digitalrebar*.

To run a RabbitMQ service, uncomment the rabbitmq-server line in
rebar-config.sh.

To inject an AMQP service instead, uncomment the curl line for consul.
It is next to the rabbitmq-server line.

In either case, the amqp-service needs to be enabled. Uncomment the
amqp-service rebar bind command.

Once the system is operational and the services configured, you will
need to start the audit-to-event program. To do this, you will need to
run the following command as *rebar* from the
*/opt/digitalrebar/core/rails* directory: RAILS\_ENV=production bundle
exec rake audits.to\_amqp &

To see events as they happen, a sample client can be run as *rebar* from
the */opt/digitalrebar/core/rails* directory: RAILS\_ENV=production
bundle exec scripts/event\_client.rb #

The command line arguments are filters. # means all. Node.create will
return events when nodes are created. Other options are available.
