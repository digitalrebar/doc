BDD Object Management
^^^^^^^^^^^^^^^^^^^^^

BDD follows a pattern in which test objects are use erlang modules to
implement each model. For example, the node model is expressed in
node.erl. There are standard methods that are expected for each object
so that they can be correctly handled by =bdd\_restrat= and =bdd\_crud=
modules.

    To handle objects that have name conflicts (e.g.: group, user), BDD
    uses an alias system where a model can be registered to use an
    alias. For example, group is handled by the group\_cb model. This is
    configurated in the setup steps.

BDD CRUD
''''''''

-  create
-  read
-  update
-  delete

BDD Rest Rat
''''''''''''

