
.. note:: WARNING WARNING WARNING:  This is the Digital Rebar v2 product documentation.  That product line is EOL as of September 2017.  Please refer to the new Digital Rebar Provision v3 documentation:  http:\/\/provision.readthedocs.io\/en\/tip\/README.html

.. _contrib_basic:

Contributing Basics
-------------------

These are some general guidelines for working with code in any of our repositories.
Be that ``core``, ``digitalrebar-deploy``, or ``doc``, the same git workflow should be followed.

While the following use ``core`` as an example, all the trees can be managed the same way.

Fork the Code
~~~~~~~~~~~~~

The following instructions assume a clone of ``https://github.com/digitalrebar/digitalrebar`` has already been created.

#. Create a personal fork of the ``https://github.com/digitalrebar/digitalrebar``

   #. Fork the code in order to be able to submit changes
   #. Rename the fork in Github to something like 'rebar-core' to make
      it easier to track.  We'll assume that these proceedures were followed in these
      directions
   #. Remember to update any public SSH key to github

#. Create a personal git identity (one time only)

   #. ``git config --global user.name "user.name"``
   #. ``git config --global user.email "email.address"``

#. Add a personal remote:
   ``git remote add personal https://github.com/[personal.git.name.here]/[rebar-core]\``

#. It is possible to check remotes using ``git remote -v``
#. Get the latest code from the personal repository ``git fetch personal``

To Create a Pull Request
~~~~~~~~~~~~~~~~~~~~~~~~

#. Make the change and commit it:
   ``git commit -a -m "I cut and pasted this"``
#. Get the latest code from origin: ``git fetch``
#. Sync the changed code into the trunk: ``git rebase``

   * Changes may have to be merged using ``git add [file]`` and ``git rebase --continue``

#. Push the change to the personal repository from earlier in a branch:
   ``git push personal master:[my-pull-request-branch]``
#. From the Github fork UI, create a pull request from
   my-pull-request-branch

Work On a Branch
~~~~~~~~~~~~~~~~

It's good practice to work on a branch instead of trunk.  That allows for several isolated 
changes into distinct pulls instead of co-mingling
changes.

#. Get on master using 'git checkout master'
#. Be certain to stay proficient with ``git fetch`` and ``git rebase``
#. Create a branch using ``git branch [namehere]``
#. Switch to that branch using ``git checkout [namehere]``
#. Work & commit
#. When ready to push, use
   ``git push personal [namehere]:[namehere]``

Switching between branches is possible at any time.  
Switching allows work to be done on master or for work to be done on multiple pull requests.  
This flow is especially handy if pull may take a few days to be accepted because work can still be done on
the next item while the community does the review.  It also isolates the branch 
from changes in master.  If changes from master are required, use
``git merge master`` from a branch.

