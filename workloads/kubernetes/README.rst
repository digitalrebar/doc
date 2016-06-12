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

Video Examples
--------------

Rob Hirschfeld has created a `number of videos <https://www.youtube.com/playlist?list=PLXPBeIrpXjfh2lXdXkNnzAuc7_SUtYJR->`_ showing how these scripts work.

  * `Deploy on Multiple OpenStack Clouds from Same Platform (demo of Kubernetes) <https://www.youtube.com/watch?v=LIm6PD9c7NQ&index=2&list=PLXPBeIrpXjfjabMbwYyDULOX3kZmlxEXK>`_
  * `Hybrid @Kubernetesio: @OpenStack #Google #AWS <https://www.youtube.com/watch?v=C4-H1DZEQFc&index=1&list=PLXPBeIrpXjfjabMbwYyDULOX3kZmlxEXK>`_
  * `Digital Rebar Kubernetes "Easy Button" CLI - three clouds, two SDNs <https://www.youtube.com/watch?v=3qnf_OfNhHE&index=2&list=PLXPBeIrpXjfh2lXdXkNnzAuc7_SUtYJR->`_
