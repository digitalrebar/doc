.. index::
  pair: Kubernetes; Workloads

.. _kubernetes_workload:

Kubernetes Workload
===================

`Kubernetes <http://kubernetes.io/>`_ is a container orchestration and management platform.

Installation
------------

First, complete the general workloads installation in :ref:`workloads_installation`.

Next, to install the Kubernetes workload, run the workload script:

  ::

  	cd ~/digitalrebar/deploy
  	workloads/kubernetes.sh --deploy-admin=google --provider=aws --deployment-name=kubeup

Since the Kubernetes workload uses Ansible, it does not require the nodes to access an Admin node.  This allows users to run a local Admin node and provision Kubernetes to external nodes.  **WARNING:** A local admin requires consistent connectivity to the nodes to work! It cannot disconnect, even when the script changes to waiting to anneal mode.

Video Examples
--------------

Rob Hirschfeld has created a series of videos demonstrating how these scripts work.  A comprehensive list of these videos can be found at :ref:`kubernetes_videos`.

.. index::
  pair: Kubernetes; Workload Configuration

Configuration Options
---------------------

We've worked hard to create safe defaults. However, if defaults are changed, then the downstream consumers of those values will still get the correct values.

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

In the future, it should be possible to use an existing Etcd cluster:

  * ``--kubernetes-etcd-client-port=<Int>`` Default etcd client port: 2379
  * ``--kubernetes-etcd-peer-port=<Int>`` Default etcd peer port: 2380

Pod Configuration & UI
~~~~~~~~~~~~~~~~~~~~~~

Digital Rebar is able to perform post-install configuration and testing.  These flags are used to configure pods on the Kubernetes cluster after it has been installed.  The sequence is handled by the Digital Rebar annealer. The script pre-loads all requests and does not hold work.

  * ``--kubernetes-dashboard=<true|false>`` Use Kubernetes-Dashboard (default UI now)
  * ``--kubernetes-dash=<true|false>`` Use Kube-Dash
  * ``--kubernetes-fabric8=<true|false>`` Use Fabric8 console
  * ``--kubernetes-guestbook=<true|false>`` Add the guestbook role to start a guestbook app
  * ``--kubernetes-ui=<true|false>``  : Use Kube-UI - deprecated but still works

.. index::
  pair: Kubernetes; Network

Networking Options
~~~~~~~~~~~~~~~~~~

There are a lot of networking options for Kubernetes, and they are constantly evolving.

The primary ones are generally set by users:

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

  * ``--kubernetes-gateway-count=<Number>`` Number of gateway nodes to start (opencontrail only)
  * ``--kubernetes-opencontrail-no-arp=<true|false>`` Should opencontrail arp or not: Google should not.  Make true for that.
  * ``--kubernetes-opencontrail-private-subnet=<CIDRIP>`` Private network space for opencontrail
  * ``--kubernetes-opencontrail-public-subnet=<CIDRIP>`` Public network space for opencontrail

  **Note**: When using OpenContrail, the script will create additional nodes to handle the needed gateway services.
