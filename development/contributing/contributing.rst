.. _contrib_basic

Contributing Basics
-------------------

These are some general guidelines for working with code in any of our repositories.
Be that ``core``, ``digitalrebar-deploy``, or ``doc``, the same git workflow should be followed.

While the following use ``core`` as an example, all the trees can be managed the same way.

Fork the Code
~~~~~~~~~~~~~

We assume you already have a clone of ``https://github.com/digitalrebar/core``.

#. create a personal fork of the ``https://github.com/digitalrebar/core``

   #. Fork the code if you want to be able to submit changes
   #. rename your fork in Github to something like 'rebar-core' to make
      it easier to track. We'll assume that you did that in these
      directions
   #. remember to update your public SSH key to github

#. setup your git identity (one time only)

   #. ``git config --global user.name "user.name"``
   #. ``git config --global user.email "email.address"``

#. add a personal remote:
   ``git remote add personal`` https://github.com/[yourgitnamehere]/[rebar-core]\`
#. you can check your remotes using ``git remote -v``
#. get the latest code from your repo ``git fetch personal``

To Create a Pull Request
~~~~~~~~~~~~~~~~~~~~~~~~

#. make your change and commit it:
   ``git commit -a -m "I cut and pasted this"``
#. get the latest code from origin: ``git fetch``
#. sync your code into the trunk: ``git rebase``

   * you may have to merge changes using ``git add [file]`` and ``git rebase --continue``

#. push your change to your personal repo in a branch:
   ``git push personal master:[my-pull-request-branch]``
#. from your Github fork UI, create a pull request from
   my-pull-request-branch

Work On a Branch
~~~~~~~~~~~~~~~~

It's good practice to work on a branch instead of trunk. That allows you
to isolate several changes into distinct pulls instead of co-mingling
changes.

#. get on master using 'git checkout master'
#. make sure you are up to date using ``git fetch`` and ``git rebase``
#. create a branch using ``git branch [namehere]``
#. switch to that branch using ``git checkout [namehere]``
#. work & commit
#. when you are ready to push, use
   ``git push personal [namehere]:[namehere]``

You can switch between branches anytime! That allows you to help on
master or work on multiple pull requests. This flow is especially handy
if your pull may take a few days to be accepted because you can work on
your next item while the community does the review. It also isolates you
from changes in master. If you need to get changes from master, use
``git merge master`` from your branch.

