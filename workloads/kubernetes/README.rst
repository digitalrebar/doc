.. _kubernetes_workload:

Kubernetes Workload
===================

`Kubernetes <http://kubernetes.io/>`_ is a container orchestration and management platform.

Installation
------------

FIRST, you must complete the general workloads installation in :ref:`workloads_installation`.

Next, Install the Kubernetes workload, run the workload script:

  ::

  	cd ~/digitalrebar/deploy
  	workloads/kubernetes.sh --deploy-admin=google --provider=aws --deployment-name=kubeup

Since the Kubernetes workload uses Ansible, it does not require the nodes to access an Admin node.  This allows users to run a local Admin node and provision Kubernetes to external nodes.  WARNING: A local admin requires consistent connectivity to the nodes to work - it cannot disconnect even when the script changes to waiting to anneal mode.

Video Examples
--------------

Rob Hirschfeld has created a `number of videos <https://www.youtube.com/playlist?list=PLXPBeIrpXjfh2lXdXkNnzAuc7_SUtYJR->`_ showing how these scripts work.

  * `Deploy on Multiple OpenStack Clouds from Same Platform (demo of Kubernetes) <https://www.youtube.com/watch?v=LIm6PD9c7NQ&index=2&list=PLXPBeIrpXjfjabMbwYyDULOX3kZmlxEXK>`_
  * `Hybrid @Kubernetesio: @OpenStack #Google #AWS <https://www.youtube.com/watch?v=C4-H1DZEQFc&index=1&list=PLXPBeIrpXjfjabMbwYyDULOX3kZmlxEXK>`_
  * `Digital Rebar Kubernetes "Easy Button" CLI - three clouds, two SDNs <https://www.youtube.com/watch?v=3qnf_OfNhHE&index=2&list=PLXPBeIrpXjfh2lXdXkNnzAuc7_SUtYJR->`_

Configuration Options
---------------------

We've worked hard to create safe defaults; however, if you change defaults then the downstream consumers of those values will get the correct values.

General Options
~~~~~~~~~~~~~~~

  * ``--kubernetes-master-count=<Number>`` Number of masters to start
  * ``--kubernetes-bin-dir=<String>`` Directory to store binaries ``/usr/local/bin``
  * ``--kubernetes-cluster-logging=<true|false>`` Use cluster logging
  * ``--kubernetes-cluster-monitoring=<true|false>`` Use cluster monitoring
  * ``--kubernetes-cluster-name=<String>`` Name of cluster: cluster.local
  * ``--kubernetes-local-release-dir=<String>`` Directory to download binaries: /tmp/releases
  * ``--kubernetes-log-level=<Int>``  : Kubernetes Log Level: 2
  * ``--kubernetes-test=<true|false>`` Add the test role to validate completion
  * ``--kubernetes-users=<String``   : JSON string of users with password and role

The following options are set by the script.  Override with caution!

  * ``--kubernetes-kube-service-addresses=<CIDRIP>`` Internal Service IP Addresses
  * ``--kubernetes-cloud-provider=<String>`` Is kubernetes in a cloud environment (false or type)
  * ``--kubernetes-cloud-provider-type=<String>`` Which cloud environment

Prerequisites 
~~~~~~~~~~~~~

In the future, you should be able to use an existing Etcd cluster.

  * ``--kubernetes-etcd-client-port=<Int>`` Default etcd client port: 2379
  * ``--kubernetes-etcd-peer-port=<Int>`` Default etcd peer port: 2380

Pod Configuration & UI
~~~~~~~~~~~~~~~~~~~~~~

Digital Rebar is able to perform post-install configuaration and testing.  These flags are used to configure pods on the Kubernetes cluster after is has been installed.  The sequence is handled by the Digital Rebar annealer, the script pre-loads all requests and does not hold work.

  * ``--kubernetes-dashboard=<true|false>`` Use Kubernetes-Dashboard (default UI now)
  * ``--kubernetes-dash=<true|false>`` Use Kube-Dash
  * ``--kubernetes-fabric8=<true|false>`` Use Fabric8 console
  * ``--kubernetes-guestbook=<true|false>`` Add the guestbook role to start a guestbook app
  * ``--kubernetes-ui=<true|false>``  : Use Kube-UI - deprecated but still works

Networking Options
~~~~~~~~~~~~~~~~~~

There are a lot of networking options for Kubernetes and they are constantly evolving.

There are the primary ones are generally set by users:

  * ``--kubernetes-networking=<calico|flannel|opencontrail>`` Network mode to use.  Defaults to flannel.
  * ``--kubernetes-dns=<true|false>`` Use DNS add-on. Defaults to true.
  * ``--kubernetes-network-category=<category name>`` Network category to use for underlay traffic, default: admin

DNS configuration: 

  * ``--kubernetes-dns-domain=<Domain String>`` Domain of the internal Kubernetes DNS service
  * ``--kubernetes-dns-namespace=<Kuberetenes Namespace>`` Namespace to put the DNS service in
  * ``--kubernetes-dns-replicas=<Number>`` Number of DNS replicas to run
  * ``--kubernetes-dns-upstream=<JSON ARRAY of IP>`` JSON array of DNS server IPs

Calico or Flannel:

  * ``--kubernetes-pods-subnet=<CIDRIP>`` Subnet whole calico/flannel subnet space (dotted quad)
  * ``--kubernetes-network-node-prefix=<Number>`` Subnet prefix for node calico/flannel subnet space
  * ``--kubernetes-network-prefix=<Number>`` Subnet prefix for whole calico/flannel subnet space
  * ``--kubernetes-node-count=<Number>`` Number of nodes to start

OpenContrail:

When using OpenContrail, the script will create additional nodes to handle the needed gateway services.

  * ``--kubernetes-gateway-count=<Number>`` Number of gateway nodes to start (opencontrail only)
  * ``--kubernetes-opencontrail-no-arp=<true|false>`` Should opencontrail arp or not: Google should not.  Make true for that.
  * ``--kubernetes-opencontrail-private-subnet=<CIDRIP>`` Private network space for opencontrail
  * ``--kubernetes-opencontrail-public-subnet=<CIDRIP>`` Public network space for opencontrail

