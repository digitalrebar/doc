
.. note:: WARNING WARNING WARNING:  This is the Digital Rebar v2 product documentation.  The v2 version is EOL as of September 2017.  Please refer to the new Digital Rebar Provision v3 documentation:  http:\/\/provision.readthedocs.io\/en\/tip\/README.html

.. index::
  pair: Chef; Jig
.. _chef_jig:

Chef Jig
--------


Chef Jig and Developing with Cookbooks
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The Chef Jig in the Chef Barclamp allows Digital Rebar to get data from
Chef (inbound) and create roles / set attributes into Chef (outbound)

Adding Chef Jig into a dev system
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

::

    bundle exec rake rebar:chef:inject_conn url=http://127.0.0.1:4000 name=admin key_file=/etc/chef/client.pem


Rebar and Berkshelf
~~~~~~~~~~~~~~~~~~~

For each workload (core, openstack, hardware, etc.) Rebar uses
a centralized Berkshelf file for all of the cookbooks.  The
Berksfile is in ``digitalrebar/<workload>/chef/cookbooks/Berksfile``.
Rebar ignores Berksfiles in individual cookbooks.

Berkshelf resolves cookbook dependencies by following the Berksfile
instructions for local and remote dependent cookbooks.  Dependencies are stored in the Berkshelf (path.) If using a Chef Server, Berkshelf can upload them to the Chef Server.  If using chef-solo or
chef-client -x, Berkshelf packages them on the filesystem and delivers them to
the nodes.

We encourage cloning from the `Digital Rebar github repos <https://github.com/digitalrebar>`_ and submitting
pull requests.

Developing Cookbooks
~~~~~~~~~~~~~~~~~~~~

-  As the ``rebar`` user, run all of the following.
-  Cookbook must be placed in all of the cookbooks' dependencies in
   the centralized Berksfile for them to get picked up and used by the
   Chef Jig.

   ::

       digitalrebar/<workload>/[barclamp]/chef/cookbooks/Berksfile

-  Any of the normal sources can be used to indicate the location of dependent cookbooks.
-  Put the custom and wrapper cookbooks in
   ``digitalrebar/<workload>/chef/cookbooks/<my_cookbook>``
-  The Berkshelf is located at /root/.berkshelf/ Do not edit it.  In order
   to prune it of old and unnecessary versions of cookbooks, feel
   free to use ``sudo berks shelf uninstall <cookbook> -v <version>``
   The Chef Jig should replace any missing versions of cookbooks in the
   Berkshelf next time it runs.
-  Install dependencies:

   ::

       $ cd <digitalrebar_root>/<workload>/[barclamp]/chef/cookbooks/
       $ berks install

-  Optional: If having the cookbooks that were indicated as dependents and the cookbooks that were added for reference, or for running Chef-Solo while developing.  The following example will download 
   them and place them in the correct places.

   ::

       $ cd <digitalrebar_root>/<workload>/[barclamp]/chef/cookbooks/
       $ berks install -p ./somewhere/else/to/look/at/

-  If using Chef-Solo: Package up cookbooks for delivery.  Once
   satisfied with the cookbooks, package them for Rebar to
   distribute to the nodes (even the Rebar admin node)

   ::

       $ cd <digitalrebar_root>/<workload>/[barclamp]/chef/cookbooks/
       $ berks package

-  If kicking off the annealer again for the proper role,the package.tar.gz file must be copied over to the slave nodes

Testing Cookbooks
~~~~~~~~~~~~~~~~~

TODO: Script this, possibly under 'tools'

-  create a test node (a kvm node is just fine)
-  add it to a deployment and add the node-role that the cookbook
   belongs to
-  kick off the annealer to deploy the cookbooks to a test node.

FUTURE:

-  Rebar can help integrate normal testing patterns.  We're
   considering ``test-kitchen`` integration.

