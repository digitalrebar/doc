.. _kubernetes_workload:

Kubernetes Workload
===================

`Kubernetes <http://kubernetes.io/>`_ is a container orchestration and management platform.

This section is specific to Kubernetes, see :ref:`workloads_guide` for general install tips.

Installation
------------

Install the Kubernetes workload, run the workload script:

  ::
  
  	cd ~/digitalrebar/deploy
  	workloads/kubernetes.sh --deploy-admin=google --provider=aws --deployment-name=kubeup

